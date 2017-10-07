---
title: aaaDownload um VHD do Windows do Azure | Microsoft Docs
description: "Baixe um VHD do Windows usando Olá portal do Azure."
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
ms.openlocfilehash: d0ca8842db98f22751f01648c0ba4e5cde090043
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-windows-vhd-from-azure"></a><span data-ttu-id="2e331-103">Baixar um VHD do Windows Azure</span><span class="sxs-lookup"><span data-stu-id="2e331-103">Download a Windows VHD from Azure</span></span>

<span data-ttu-id="2e331-104">Neste artigo, você aprenderá como toodownload uma [disco rígido virtual do Windows (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Olá de arquivo do Azure usando portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e331-104">In this article, you learn how toodownload a [Windows virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) file from Azure using hello Azure portal.</span></span> 

<span data-ttu-id="2e331-105">Máquinas virtuais (VMs) em uso do Azure [discos](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) como toostore um local de um sistema operacional, aplicativos e dados.</span><span class="sxs-lookup"><span data-stu-id="2e331-105">Virtual machines (VMs) in Azure use [disks](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="2e331-106">Todas as VMs do Azure têm, pelo menos, dois discos – um disco do sistema operacional Windows e um disco temporário.</span><span class="sxs-lookup"><span data-stu-id="2e331-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="2e331-107">disco do sistema operacional Olá é inicialmente criado de uma imagem e disco do sistema operacional hello e imagem Olá são VHDs armazenados em uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e331-107">hello operating system disk is initially created from an image, and both hello operating system disk and hello image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="2e331-108">Máquinas virtuais também podem ter um ou mais discos de dados que também são armazenados em VHDs.</span><span class="sxs-lookup"><span data-stu-id="2e331-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

## <a name="stop-hello-vm"></a><span data-ttu-id="2e331-109">Parar Olá VM</span><span class="sxs-lookup"><span data-stu-id="2e331-109">Stop hello VM</span></span>

<span data-ttu-id="2e331-110">Não é possível baixar um VHD do Azure, se ele estiver anexado tooa executando VM.</span><span class="sxs-lookup"><span data-stu-id="2e331-110">A VHD can’t be downloaded from Azure if it's attached tooa running VM.</span></span> <span data-ttu-id="2e331-111">É necessário toodownload VM da saudação toostop um VHD.</span><span class="sxs-lookup"><span data-stu-id="2e331-111">You need toostop hello VM toodownload a VHD.</span></span> <span data-ttu-id="2e331-112">Se você quiser toouse um VHD como um [imagem](tutorial-custom-images.md) toocreate outras VMs com novos discos, use [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize Olá sistema operacional contido no arquivo hello e, em seguida, parar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="2e331-112">If you want toouse a VHD as an [image](tutorial-custom-images.md) toocreate other VMs with new disks, you use [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello operating system contained in hello file and then stop hello VM.</span></span> <span data-ttu-id="2e331-113">Olá toouse VHD como um disco para uma nova instância de uma VM existente ou um disco de dados, você só precisa toostop e desalocar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="2e331-113">toouse hello VHD as a disk for a new instance of an existing VM or data disk, you only need toostop and deallocate hello VM.</span></span>

<span data-ttu-id="2e331-114">toouse Olá VHD como uma imagem toocreate outras VMs, conclua estas etapas:</span><span class="sxs-lookup"><span data-stu-id="2e331-114">toouse hello VHD as an image toocreate other VMs, complete these steps:</span></span>

1.  <span data-ttu-id="2e331-115">Se você ainda não fez isso, entre no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2e331-115">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="2e331-116">[Conecte-se a VM de toohello](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e331-116">[Connect toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
3.  <span data-ttu-id="2e331-117">No hello VM, abra a janela de Prompt de comando hello como um administrador.</span><span class="sxs-lookup"><span data-stu-id="2e331-117">On hello VM, open hello Command Prompt window as an administrator.</span></span>
4.  <span data-ttu-id="2e331-118">Altere o diretório de saudação muito*%windir%\system32\sysprep* e execute sysprep.exe.</span><span class="sxs-lookup"><span data-stu-id="2e331-118">Change hello directory too*%windir%\system32\sysprep* and run sysprep.exe.</span></span>
5.  <span data-ttu-id="2e331-119">Na caixa de diálogo Ferramenta de preparação do sistema hello, selecione **Enter System Out-of-Box Experience (OOBE)**e certifique-se de que **generalizar** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="2e331-119">In hello System Preparation Tool dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that **Generalize** is selected.</span></span>
6.  <span data-ttu-id="2e331-120">Em Opções de Desligamento, selecione **Desligar** e **OK**.</span><span class="sxs-lookup"><span data-stu-id="2e331-120">In Shutdown Options, select **Shutdown**, and then click **OK**.</span></span> 

<span data-ttu-id="2e331-121">Olá toouse VHD como um disco para uma nova instância de uma VM existente ou um disco de dados, execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="2e331-121">toouse hello VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="2e331-122">No menu de Hub de saudação do hello portal do Azure, clique em **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="2e331-122">On hello Hub menu in hello Azure portal, click **Virtual Machines**.</span></span>
2.  <span data-ttu-id="2e331-123">Selecione Olá VM na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="2e331-123">Select hello VM from hello list.</span></span>
3.  <span data-ttu-id="2e331-124">Na folha de saudação para Olá VM, clique em **parar**.</span><span class="sxs-lookup"><span data-stu-id="2e331-124">On hello blade for hello VM, click **Stop**.</span></span>

    ![Parar a VM](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="2e331-126">Gerar a URL de SAS</span><span class="sxs-lookup"><span data-stu-id="2e331-126">Generate SAS URL</span></span>

<span data-ttu-id="2e331-127">arquivo VHD Olá toodownload, você precisa toogenerate um [assinatura de acesso compartilhado (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span><span class="sxs-lookup"><span data-stu-id="2e331-127">toodownload hello VHD file, you need toogenerate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="2e331-128">Quando Olá URL é gerado, um tempo de expiração é atribuído toohello URL.</span><span class="sxs-lookup"><span data-stu-id="2e331-128">When hello URL is generated, an expiration time is assigned toohello URL.</span></span>

1.  <span data-ttu-id="2e331-129">No menu de saudação da folha de saudação para Olá VM, clique em **discos**.</span><span class="sxs-lookup"><span data-stu-id="2e331-129">On hello menu of hello blade for hello VM, click **Disks**.</span></span>
2.  <span data-ttu-id="2e331-130">Selecione o disco do sistema operacional Olá para Olá VM e, em seguida, clique em **exportar**.</span><span class="sxs-lookup"><span data-stu-id="2e331-130">Select hello operating system disk for hello VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="2e331-131">Definir o tempo de expiração de saudação da saudação URL muito*36000*.</span><span class="sxs-lookup"><span data-stu-id="2e331-131">Set hello expiration time of hello URL too*36000*.</span></span>
4.  <span data-ttu-id="2e331-132">Clique em **Gerar URL**.</span><span class="sxs-lookup"><span data-stu-id="2e331-132">Click **Generate URL**.</span></span>

    ![Gerar a URL](./media/download-vhd/export-generate.png)

> [!NOTE]
> <span data-ttu-id="2e331-134">tempo de expiração de saudação é aumentado de saudação padrão tooprovide tempo suficiente toodownload Olá arquivo VHD grande para um sistema operacional Windows Server.</span><span class="sxs-lookup"><span data-stu-id="2e331-134">hello expiration time is increased from hello default tooprovide enough time toodownload hello large VHD file for a Windows Server operating system.</span></span> <span data-ttu-id="2e331-135">Você pode esperar um arquivo VHD que contém tootake de sistema operacional Windows Server Olá toodownload de várias horas dependendo de sua conexão.</span><span class="sxs-lookup"><span data-stu-id="2e331-135">You can expect a VHD file that contains hello Windows Server operating system tootake several hours toodownload depending on your connection.</span></span> <span data-ttu-id="2e331-136">Se você estiver baixando um VHD para um disco de dados, o tempo padrão de saudação é suficiente.</span><span class="sxs-lookup"><span data-stu-id="2e331-136">If you are downloading a VHD for a data disk, hello default time is sufficient.</span></span> 
> 
> 

## <a name="download-vhd"></a><span data-ttu-id="2e331-137">Baixar o VHD</span><span class="sxs-lookup"><span data-stu-id="2e331-137">Download VHD</span></span>

1.  <span data-ttu-id="2e331-138">Olá URL que foi gerado, clique em arquivo VHD de saudação do Download.</span><span class="sxs-lookup"><span data-stu-id="2e331-138">Under hello URL that was generated, click Download hello VHD file.</span></span>

    ![Baixar o VHD](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="2e331-140">Talvez seja necessário tooclick **salvar** no download de Olá Olá navegador toostart.</span><span class="sxs-lookup"><span data-stu-id="2e331-140">You may need tooclick **Save** in hello browser toostart hello download.</span></span> <span data-ttu-id="2e331-141">saudação padrão nome para o arquivo VHD Olá é *abcd*.</span><span class="sxs-lookup"><span data-stu-id="2e331-141">hello default name for hello VHD file is *abcd*.</span></span>

    ![Clique em Salvar no navegador Olá](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="2e331-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2e331-143">Next steps</span></span>

- <span data-ttu-id="2e331-144">Saiba como muito[carregar um tooAzure do arquivo VHD](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e331-144">Learn how too[upload a VHD file tooAzure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
- <span data-ttu-id="2e331-145">[Criar discos gerenciados de discos não gerenciados em uma conta de armazenamento](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e331-145">[Create managed disks from unmanaged disks in a storage account](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
- <span data-ttu-id="2e331-146">[Gerenciar discos do Azure com o PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e331-146">[Manage Azure disks with PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

