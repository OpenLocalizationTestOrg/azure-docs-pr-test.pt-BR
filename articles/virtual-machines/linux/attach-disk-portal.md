---
title: aaaAttach um disco de dados tooa VM do Linux | Microsoft Docs
description: "Como tooa de disco de dados novos ou existentes tooattach VM do Linux no hello usando o portal do Azure Olá modelo de implantação do Gerenciador de recursos."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5e1c6212-976c-4962-a297-177942f90907
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: cynthn
ms.openlocfilehash: 069c3c6f5e71a8c495342e6d0c6f3d92c4ed5053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-vm-in-hello-azure-portal"></a><span data-ttu-id="a107f-103">Como tooattach dados de um disco tooa VM do Linux no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a107f-103">How tooattach a data disk tooa Linux VM in hello Azure portal</span></span>
<span data-ttu-id="a107f-104">Este artigo mostra como tooattach novo e existente discos tooa máquina de virtual do Linux por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a107f-104">This article shows you how tooattach both new and existing disks tooa Linux virtual machine through hello Azure portal.</span></span> <span data-ttu-id="a107f-105">Você também pode [anexar tooa um disco de dados VM do Windows no portal do Azure de saudação](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a107f-105">You can also [attach a data disk tooa Windows VM in hello Azure portal](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="a107f-106">Você pode escolher toouse qualquer um dos discos do Azure gerenciados ou não gerenciados discos.</span><span class="sxs-lookup"><span data-stu-id="a107f-106">You can choose toouse either Azure Managed Disks or unmanaged disks.</span></span> <span data-ttu-id="a107f-107">Discos gerenciados são tratados pelo Olá plataforma Windows Azure e não exigem qualquer etapa de preparação ou local toostore-los.</span><span class="sxs-lookup"><span data-stu-id="a107f-107">Managed disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="a107f-108">Discos não gerenciados exigem uma conta de armazenamento e têm algumas [cotas e limites que se aplicam](../../azure-subscription-service-limits.md#storage-limits).</span><span class="sxs-lookup"><span data-stu-id="a107f-108">Unmanaged disks require a storage account and have some [quotas and limits that apply](../../azure-subscription-service-limits.md#storage-limits).</span></span> <span data-ttu-id="a107f-109">Para saber mais sobre Azure Managed Disks, veja [Visão geral dos Azure Managed Disks](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a107f-109">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="a107f-110">Antes de anexar discos tooyour VM, examine essas dicas:</span><span class="sxs-lookup"><span data-stu-id="a107f-110">Before you attach disks tooyour VM, review these tips:</span></span>

* <span data-ttu-id="a107f-111">tamanho de saudação da máquina virtual de saudação controla quantos discos de dados, você pode anexar.</span><span class="sxs-lookup"><span data-stu-id="a107f-111">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="a107f-112">Para obter detalhes, consulte [Tamanhos das máquinas virtuais](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a107f-112">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="a107f-113">toouse armazenamento Premium, você precisa de uma máquina virtual da série DS ou série GS.</span><span class="sxs-lookup"><span data-stu-id="a107f-113">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="a107f-114">Você pode usar discos Premium e Standard com essas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="a107f-114">You can use both Premium and Standard disks with these virtual machines.</span></span> <span data-ttu-id="a107f-115">O armazenamento Premium está disponível em determinadas regiões.</span><span class="sxs-lookup"><span data-stu-id="a107f-115">Premium storage is available in certain regions.</span></span> <span data-ttu-id="a107f-116">Para obter detalhes, confira [Armazenamento Premium: armazenamento de alto desempenho para as cargas de trabalho das máquinas virtuais do Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a107f-116">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="a107f-117">Discos anexados toovirtual máquinas são, na verdade, os arquivos. vhd armazenados no Azure.</span><span class="sxs-lookup"><span data-stu-id="a107f-117">Disks attached toovirtual machines are actually .vhd files stored in Azure.</span></span> <span data-ttu-id="a107f-118">Para obter detalhes, confira [Sobre discos e VHDs para máquinas virtuais](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a107f-118">For details, see [About disks and VHDs for virtual machines](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="find-hello-virtual-machine"></a><span data-ttu-id="a107f-119">Localizar a máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="a107f-119">Find hello virtual machine</span></span>
1. <span data-ttu-id="a107f-120">Entrar toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a107f-120">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a107f-121">No menu de Hub hello, clique em **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="a107f-121">On hello Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="a107f-122">Selecione máquina virtual de Olá Olá lista.</span><span class="sxs-lookup"><span data-stu-id="a107f-122">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="a107f-123">toohello Virtual máquinas folha, **Essentials**, clique em **discos**.</span><span class="sxs-lookup"><span data-stu-id="a107f-123">toohello Virtual machines blade, in **Essentials**, click **Disks**.</span></span>
   
    ![Abrir configurações de disco](./media/attach-disk-portal/find-disk-settings.png)

<span data-ttu-id="a107f-125">Continue seguindo as instruções para anexar um [disco gerenciado](#use-azure-managed-disks) ou um [disco não gerenciado](#use-unmanaged-disks).</span><span class="sxs-lookup"><span data-stu-id="a107f-125">Continue by following instructions for attaching either a [managed disk](#use-azure-managed-disks) or [unmanaged disk](#use-unmanaged-disks).</span></span>

## <a name="use-azure-managed-disks"></a><span data-ttu-id="a107f-126">Usar o Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="a107f-126">Use Azure Managed Disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="a107f-127">Anexar um novo disco</span><span class="sxs-lookup"><span data-stu-id="a107f-127">Attach a new disk</span></span>

1. <span data-ttu-id="a107f-128">Em Olá **discos** folha, clique em **+ adicionar disco de dados**.</span><span class="sxs-lookup"><span data-stu-id="a107f-128">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="a107f-129">Clique o menu suspenso de saudação para **nome** e selecione **criar disco**:</span><span class="sxs-lookup"><span data-stu-id="a107f-129">Click hello drop-down menu for **Name** and select **Create disk**:</span></span>

    ![Criar disco gerenciado do Azure](./media/attach-disk-portal/create-new-md.png)

3. <span data-ttu-id="a107f-131">Insira um nome para o disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="a107f-131">Enter a name for your managed disk.</span></span> <span data-ttu-id="a107f-132">Examine as configurações padrão de saudação, atualizar conforme necessário e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="a107f-132">Review hello default settings, update as necessary, and then click **Create**.</span></span>
   
   ![Analisar configurações de disco](./media/attach-disk-portal/create-new-md-settings.png)

4. <span data-ttu-id="a107f-134">Clique em **salvar** toocreate Olá gerenciados em disco e a atualização de configuração da VM hello:</span><span class="sxs-lookup"><span data-stu-id="a107f-134">Click **Save** toocreate hello managed disk and update hello VM configuration:</span></span>

   ![Salvar novo Azure Managed Disk](./media/attach-disk-portal/confirm-create-new-md.png)

5. <span data-ttu-id="a107f-136">Depois do Azure cria o disco hello e anexa toohello virtual machine, novo disco de saudação é listado em configurações de disco da máquina de virtual Olá em **discos de dados**.</span><span class="sxs-lookup"><span data-stu-id="a107f-136">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span> <span data-ttu-id="a107f-137">Como discos gerenciados são um recurso de nível superior, o disco de saudação aparece na raiz de Olá Olá do grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="a107f-137">As managed disks are a top-level resource, hello disk appears at hello root of hello resource group:</span></span>

   ![Azure Managed Disk no grupo de recursos](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a><span data-ttu-id="a107f-139">Anexar um disco existente</span><span class="sxs-lookup"><span data-stu-id="a107f-139">Attach an existing disk</span></span>
1. <span data-ttu-id="a107f-140">Em Olá **discos** folha, clique em **+ adicionar disco de dados**.</span><span class="sxs-lookup"><span data-stu-id="a107f-140">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="a107f-141">Clique o menu suspenso de saudação para **nome** tooview uma lista de existentes gerenciadas discos acessíveis tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="a107f-141">Click hello drop-down menu for **Name** tooview a list of existing managed disks accessible tooyour Azure subscription.</span></span> <span data-ttu-id="a107f-142">Selecione Olá gerenciado tooattach de disco:</span><span class="sxs-lookup"><span data-stu-id="a107f-142">Select hello managed disk tooattach:</span></span>

   ![Anexar um Azure Managed Disk existente](./media/attach-disk-portal/select-existing-md.png)

3. <span data-ttu-id="a107f-144">Clique em **salvar** tooattach Olá existente gerenciados em disco e a atualização de configuração da VM hello:</span><span class="sxs-lookup"><span data-stu-id="a107f-144">Click **Save** tooattach hello existing managed disk and update hello VM configuration:</span></span>
   
   ![Salvar atualizações do Azure Managed Disk](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. <span data-ttu-id="a107f-146">Após anexa Azure hello disco toohello VM, ela é listada em configurações de disco da máquina de virtual Olá em **discos de dados**.</span><span class="sxs-lookup"><span data-stu-id="a107f-146">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-unmanaged-disks"></a><span data-ttu-id="a107f-147">Usar discos não gerenciados</span><span class="sxs-lookup"><span data-stu-id="a107f-147">Use unmanaged disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="a107f-148">Anexar um novo disco</span><span class="sxs-lookup"><span data-stu-id="a107f-148">Attach a new disk</span></span>

1. <span data-ttu-id="a107f-149">Em Olá **discos** folha, clique em **+ adicionar disco de dados**.</span><span class="sxs-lookup"><span data-stu-id="a107f-149">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="a107f-150">Examine as configurações padrão de saudação, atualizar conforme necessário e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="a107f-150">Review hello default settings, update as necessary, and then click **OK**.</span></span>
   
   ![Analisar configurações de disco](./media/attach-disk-portal/attach-new.png)
3. <span data-ttu-id="a107f-152">Depois do Azure cria o disco hello e anexa toohello virtual machine, novo disco de saudação é listado em configurações de disco da máquina de virtual Olá em **discos de dados**.</span><span class="sxs-lookup"><span data-stu-id="a107f-152">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="attach-an-existing-disk"></a><span data-ttu-id="a107f-153">Anexar um disco existente</span><span class="sxs-lookup"><span data-stu-id="a107f-153">Attach an existing disk</span></span>
1. <span data-ttu-id="a107f-154">Em Olá **discos** folha, clique em **+ adicionar disco de dados**.</span><span class="sxs-lookup"><span data-stu-id="a107f-154">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="a107f-155">Em **Anexar disco existente**, clique em **Arquivo VHD**.</span><span class="sxs-lookup"><span data-stu-id="a107f-155">Under **Attach existing disk**, click **VHD File**.</span></span>
   
   ![Anexar disco existente](./media/attach-disk-portal/attach-existing.png)
3. <span data-ttu-id="a107f-157">Em **contas de armazenamento**, selecione conta hello e contêiner que contém o arquivo. vhd de saudação.</span><span class="sxs-lookup"><span data-stu-id="a107f-157">Under **Storage accounts**, select hello account and container that holds hello .vhd file.</span></span>
   
   ![Localização do VHD](./media/attach-disk-portal/find-storage-container.png)
4. <span data-ttu-id="a107f-159">Selecione o arquivo. vhd de saudação.</span><span class="sxs-lookup"><span data-stu-id="a107f-159">Select hello .vhd file.</span></span>
5. <span data-ttu-id="a107f-160">Em **anexar o disco existente**, arquivo hello você selecionou é listado em **arquivo VHD**.</span><span class="sxs-lookup"><span data-stu-id="a107f-160">Under **Attach existing disk**, hello file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="a107f-161">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a107f-161">Click **OK**.</span></span>
6. <span data-ttu-id="a107f-162">Após anexa Azure hello disco toohello VM, ela é listada em configurações de disco da máquina de virtual Olá em **discos de dados**.</span><span class="sxs-lookup"><span data-stu-id="a107f-162">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a107f-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a107f-163">Next steps</span></span>
<span data-ttu-id="a107f-164">Depois de saudação disco for adicionado, será necessário tooprepare-lo para uso.</span><span class="sxs-lookup"><span data-stu-id="a107f-164">After hello disk is added, you need tooprepare it for use.</span></span> <span data-ttu-id="a107f-165">Para obter mais informações, veja [Como: inicializar um novo disco de dados no Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="a107f-165">For more information, see [How to: Initialize a new data disk in Linux](add-disk.md).</span></span>
