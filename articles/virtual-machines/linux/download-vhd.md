---
title: aaaDownload um VHD do Linux do Azure | Microsoft Docs
description: "Baixar um VHD do Linux usando Olá CLI do Azure e Olá portal do Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: 7e08e985a64a6be581b8f5eedcce60fbd314eaf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-linux-vhd-from-azure"></a><span data-ttu-id="b2c9b-103">Baixar um VHD do Linux por meio do Azure</span><span class="sxs-lookup"><span data-stu-id="b2c9b-103">Download a Linux VHD from Azure</span></span>

<span data-ttu-id="b2c9b-104">Neste artigo, você aprenderá como toodownload uma [Linux virtual VHD (disco rígido)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Olá arquivo do Azure usando a CLI do Azure e o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-104">In this article, you learn how toodownload a [Linux virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) file from Azure using hello Azure CLI and Azure portal.</span></span> 

<span data-ttu-id="b2c9b-105">Máquinas virtuais (VMs) em uso do Azure [discos](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) como toostore um local de um sistema operacional, aplicativos e dados.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-105">Virtual machines (VMs) in Azure use [disks](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="b2c9b-106">Todas as VMs do Azure têm, pelo menos, dois discos – um disco do sistema operacional Windows e um disco temporário.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="b2c9b-107">disco do sistema operacional Olá é inicialmente criado de uma imagem e disco do sistema operacional hello e imagem Olá são VHDs armazenados em uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-107">hello operating system disk is initially created from an image, and both hello operating system disk and hello image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="b2c9b-108">Máquinas virtuais também podem ter um ou mais discos de dados que também são armazenados em VHDs.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

<span data-ttu-id="b2c9b-109">Se você ainda não fez isso, instale a [CLI 2.0 do Azure](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="b2c9b-109">If you haven't already done so, install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>

## <a name="stop-hello-vm"></a><span data-ttu-id="b2c9b-110">Parar Olá VM</span><span class="sxs-lookup"><span data-stu-id="b2c9b-110">Stop hello VM</span></span>

<span data-ttu-id="b2c9b-111">Não é possível baixar um VHD do Azure, se ele estiver anexado tooa executando VM.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-111">A VHD can’t be downloaded from Azure if it's attached tooa running VM.</span></span> <span data-ttu-id="b2c9b-112">É necessário toodownload VM da saudação toostop um VHD.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-112">You need toostop hello VM toodownload a VHD.</span></span> <span data-ttu-id="b2c9b-113">Se você quiser toouse um VHD como um [imagem](tutorial-custom-images.md) toocreate outras VMs com novos discos, você precisa toodeprovision e generalizar sistema de operacional Olá contido em Olá de arquivo e parar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-113">If you want toouse a VHD as an [image](tutorial-custom-images.md) toocreate other VMs with new disks, you need toodeprovision and generalize hello operating system contained in hello file and stop hello VM.</span></span> <span data-ttu-id="b2c9b-114">Olá toouse VHD como um disco para uma nova instância de uma VM existente ou um disco de dados, você só precisa toostop e desalocar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-114">toouse hello VHD as a disk for a new instance of an existing VM or data disk, you only need toostop and deallocate hello VM.</span></span>

<span data-ttu-id="b2c9b-115">toouse Olá VHD como uma imagem toocreate outras VMs, conclua estas etapas:</span><span class="sxs-lookup"><span data-stu-id="b2c9b-115">toouse hello VHD as an image toocreate other VMs, complete these steps:</span></span>

1. <span data-ttu-id="b2c9b-116">Use SSH, nome da conta hello e endereço IP público de saudação do hello VM tooconnect tooit e seu provisionamento.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-116">Use SSH, hello account name, and hello public IP address of hello VM tooconnect tooit and deprovision it.</span></span> <span data-ttu-id="b2c9b-117">Olá + usuário parâmetro também remove a última conta de usuário provisionado hello.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-117">hello +user parameter also removes hello last provisioned user account.</span></span> <span data-ttu-id="b2c9b-118">Se você é trazer credenciais de conta no toohello VM, deixe este + parâmetro de usuário.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-118">If you are baking account credentials in toohello VM, leave out this +user parameter.</span></span> <span data-ttu-id="b2c9b-119">Olá, exemplo a seguir remove última conta de usuário provisionado hello:</span><span class="sxs-lookup"><span data-stu-id="b2c9b-119">hello following example removes hello last provisioned user account:</span></span>

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. <span data-ttu-id="b2c9b-120">Entrar tooyour conta do Azure com [logon az](https://docs.microsoft.com/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="b2c9b-120">Sign in tooyour Azure account with [az login](https://docs.microsoft.com/cli/azure/#login).</span></span>
3. <span data-ttu-id="b2c9b-121">Parar e desalocar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-121">Stop and deallocate hello VM.</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="b2c9b-122">Generalize Olá VM.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-122">Generalize hello VM.</span></span> 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

<span data-ttu-id="b2c9b-123">Olá toouse VHD como um disco para uma nova instância de uma VM existente ou um disco de dados, execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="b2c9b-123">toouse hello VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="b2c9b-124">Entrar toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b2c9b-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="b2c9b-125">No menu de Hub hello, clique em **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-125">On hello Hub menu, click **Virtual Machines**.</span></span>
3.  <span data-ttu-id="b2c9b-126">Selecione Olá VM na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-126">Select hello VM from hello list.</span></span>
4.  <span data-ttu-id="b2c9b-127">Na folha de saudação para Olá VM, clique em **parar**.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-127">On hello blade for hello VM, click **Stop**.</span></span>

    ![Parar a VM](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="b2c9b-129">Gerar a URL de SAS</span><span class="sxs-lookup"><span data-stu-id="b2c9b-129">Generate SAS URL</span></span>

<span data-ttu-id="b2c9b-130">arquivo VHD Olá toodownload, você precisa toogenerate um [assinatura de acesso compartilhado (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-130">toodownload hello VHD file, you need toogenerate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="b2c9b-131">Quando Olá URL é gerado, um tempo de expiração é atribuído toohello URL.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-131">When hello URL is generated, an expiration time is assigned toohello URL.</span></span>

1.  <span data-ttu-id="b2c9b-132">No menu de saudação da folha de saudação para Olá VM, clique em **discos**.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-132">On hello menu of hello blade for hello VM, click **Disks**.</span></span>
2.  <span data-ttu-id="b2c9b-133">Selecione o disco do sistema operacional Olá para Olá VM e, em seguida, clique em **exportar**.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-133">Select hello operating system disk for hello VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="b2c9b-134">Clique em **Gerar URL**.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-134">Click **Generate URL**.</span></span>

    ![Gerar a URL](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a><span data-ttu-id="b2c9b-136">Baixar o VHD</span><span class="sxs-lookup"><span data-stu-id="b2c9b-136">Download VHD</span></span>

1.  <span data-ttu-id="b2c9b-137">Olá URL que foi gerado, clique em arquivo VHD de saudação do Download.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-137">Under hello URL that was generated, click Download hello VHD file.</span></span>

    ![Baixar o VHD](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="b2c9b-139">Talvez seja necessário tooclick **salvar** no download de Olá Olá navegador toostart.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-139">You may need tooclick **Save** in hello browser toostart hello download.</span></span> <span data-ttu-id="b2c9b-140">saudação padrão nome para o arquivo VHD Olá é *abcd*.</span><span class="sxs-lookup"><span data-stu-id="b2c9b-140">hello default name for hello VHD file is *abcd*.</span></span>

    ![Clique em Salvar no navegador Olá](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="b2c9b-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b2c9b-142">Next steps</span></span>

- <span data-ttu-id="b2c9b-143">Saiba como muito[carregar e criar uma VM do Linux do disco personalizado com hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b2c9b-143">Learn how too[upload and create a Linux VM from custom disk with hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
- <span data-ttu-id="b2c9b-144">[Gerenciar discos do Azure Olá CLI do Azure](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b2c9b-144">[Manage Azure disks hello Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

