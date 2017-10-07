---
title: "aaaAttach tooa um disco clássico VM do Azure | Microsoft Docs"
description: "Anexar dados disco tooa máquina virtual do Windows criada com o modelo de implantação clássico hello e inicializá-lo."
services: virtual-machines-windows, storage
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: be4e3e74-05bc-4527-969f-84f10a1d66a7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: cynthn
ms.openlocfilehash: bfe1b0fa066277d28d3862a18da4b1023cb4452d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-virtual-machine-created-with-hello-classic-deployment-model"></a><span data-ttu-id="9906e-103">Anexar dados disco tooa máquina virtual do Windows criada com o modelo de implantação clássico Olá</span><span class="sxs-lookup"><span data-stu-id="9906e-103">Attach a data disk tooa Windows virtual machine created with hello classic deployment model</span></span>
<!--
Refernce article:
    If you want toouse hello new portal, see [How tooattach a data disk tooa Windows VM in hello Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

<span data-ttu-id="9906e-104">Este artigo mostra como discos de tooattach novos e existentes criados com hello clássico implantação modelo tooa máquina virtual do Windows usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9906e-104">This article shows you how tooattach new and existing disks created with hello Classic deployment model tooa Windows virtual machine using hello Azure portal.</span></span>

<span data-ttu-id="9906e-105">Você também pode [anexar tooa um disco de dados VM do Linux no portal do Azure de saudação](../../linux/attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9906e-105">You can also [attach a data disk tooa Linux VM in hello Azure portal](../../linux/attach-disk-portal.md).</span></span>

<span data-ttu-id="9906e-106">Antes de anexar um disco, leia estas dicas:</span><span class="sxs-lookup"><span data-stu-id="9906e-106">Before you attach a disk, review these tips:</span></span>

* <span data-ttu-id="9906e-107">tamanho de saudação da máquina virtual de saudação controla quantos discos de dados, você pode anexar.</span><span class="sxs-lookup"><span data-stu-id="9906e-107">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="9906e-108">Para obter detalhes, consulte [Tamanhos das máquinas virtuais](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9906e-108">For details, see [Sizes for virtual machines](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="9906e-109">toouse armazenamento Premium, você precisa de uma máquina virtual da série DS ou série GS.</span><span class="sxs-lookup"><span data-stu-id="9906e-109">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="9906e-110">Você pode usar discos de contas de armazenamento Premium e Standard com essas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="9906e-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="9906e-111">O armazenamento Premium está disponível em determinadas regiões.</span><span class="sxs-lookup"><span data-stu-id="9906e-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="9906e-112">Para obter detalhes, confira [Armazenamento Premium: armazenamento de alto desempenho para as cargas de trabalho das máquinas virtuais do Azure](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9906e-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="9906e-113">Para um novo disco, você não precisa toocreate-lo primeiro porque o Azure cria quando anexá-lo.</span><span class="sxs-lookup"><span data-stu-id="9906e-113">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="9906e-114">Você também pode [anexar um disco de dados usando o Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9906e-114">You can also [attach a data disk using Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9906e-115">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9906e-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>

## <a name="find-hello-virtual-machine"></a><span data-ttu-id="9906e-116">Localizar a máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="9906e-116">Find hello virtual machine</span></span>
1. <span data-ttu-id="9906e-117">Entrar toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9906e-117">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9906e-118">Olá selecione máquina de virtual do recurso Olá listado no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="9906e-118">Select hello virtual machine from hello resource listed on hello dashboard.</span></span>
3. <span data-ttu-id="9906e-119">No painel esquerdo, Olá em **configurações**, clique em **discos**.</span><span class="sxs-lookup"><span data-stu-id="9906e-119">In hello left pane under **Settings**, click **Disks**.</span></span>

    ![Abrir configurações de disco](./media/attach-disk/virtualmachinedisks.png)

<span data-ttu-id="9906e-121">Continue seguindo as instruções para anexar um [novo disco](#option-1-attach-a-new-disk) ou um [disco existente](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="9906e-121">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="9906e-122">Opção 1: Anexar e inicializar um novo disco</span><span class="sxs-lookup"><span data-stu-id="9906e-122">Option 1: Attach and initialize a new disk</span></span>

1. <span data-ttu-id="9906e-123">Em Olá **discos** folha, clique em **anexar novos**.</span><span class="sxs-lookup"><span data-stu-id="9906e-123">On hello **Disks** blade, click **Attach new**.</span></span>
2. <span data-ttu-id="9906e-124">Examine as configurações padrão de saudação, atualizar conforme necessário e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="9906e-124">Review hello default settings, update as necessary, and then click **OK**.</span></span>

   ![Analisar configurações de disco](./media/attach-disk/attach-new.png)

3. <span data-ttu-id="9906e-126">Depois do Azure cria o disco hello e anexa toohello virtual machine, novo disco de saudação é listado em configurações de disco da máquina de virtual Olá em **discos de dados**.</span><span class="sxs-lookup"><span data-stu-id="9906e-126">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="9906e-127">Inicializar um novo disco de dados</span><span class="sxs-lookup"><span data-stu-id="9906e-127">Initialize a new data disk</span></span>

1. <span data-ttu-id="9906e-128">Conecte-se a máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="9906e-128">Connect toohello virtual machine.</span></span> <span data-ttu-id="9906e-129">Para obter instruções, consulte [como tooconnect e logon tooan virtuais do Azure do computador que executa o Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9906e-129">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="9906e-130">Após fazer logon na máquina virtual de toohello, abra **Gerenciador do servidor**.</span><span class="sxs-lookup"><span data-stu-id="9906e-130">After you log on toohello virtual machine, open **Server Manager**.</span></span> <span data-ttu-id="9906e-131">No painel esquerdo do hello, selecione **serviços de arquivo e armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="9906e-131">In hello left pane, select **File and Storage Services**.</span></span>

    ![Abra o gerenciador de servidor.](../media/attach-disk-portal/fileandstorageservices.png)

3. <span data-ttu-id="9906e-133">Escolha **Discos**.</span><span class="sxs-lookup"><span data-stu-id="9906e-133">Select **Disks**.</span></span>
4. <span data-ttu-id="9906e-134">Olá **discos** seção lista os discos de saudação.</span><span class="sxs-lookup"><span data-stu-id="9906e-134">hello **Disks** section lists hello disks.</span></span> <span data-ttu-id="9906e-135">Na maioria das vezes, uma máquina virtual tem disco 0, disco 1 e disco 2.</span><span class="sxs-lookup"><span data-stu-id="9906e-135">Most often, a virtual machine has disk 0, disk 1, and disk 2.</span></span> <span data-ttu-id="9906e-136">Disco 0 é o disco do sistema operacional hello, disco 1 é Olá temporário e o disco 2 é o disco de dados Olá recentemente anexado toohello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="9906e-136">Disk 0 is hello operating system disk, disk 1 is hello temporary disk, and disk 2 is hello data disk newly attached toohello virtual machine.</span></span> <span data-ttu-id="9906e-137">listas de disco de dados Olá Olá partição como **desconhecido**.</span><span class="sxs-lookup"><span data-stu-id="9906e-137">hello data disk lists hello Partition as **Unknown**.</span></span>

 <span data-ttu-id="9906e-138">Disco hello e selecione **inicializar**.</span><span class="sxs-lookup"><span data-stu-id="9906e-138">Right-click hello disk and select **Initialize**.</span></span>

5. <span data-ttu-id="9906e-139">Você é notificado de que todos os dados serão apagados quando Olá disco é inicializado.</span><span class="sxs-lookup"><span data-stu-id="9906e-139">You're notified that all data will be erased when hello disk is initialized.</span></span> <span data-ttu-id="9906e-140">Clique em **Sim** tooacknowledge Olá aviso e inicializar Olá em disco.</span><span class="sxs-lookup"><span data-stu-id="9906e-140">Click **Yes** tooacknowledge hello warning and initialize hello disk.</span></span> <span data-ttu-id="9906e-141">Uma vez concluído, partição hello será listada como **GPT**.</span><span class="sxs-lookup"><span data-stu-id="9906e-141">Once complete, hello partition will be listed as **GPT**.</span></span> <span data-ttu-id="9906e-142">Disco Olá novamente e selecione **Novo Volume**.</span><span class="sxs-lookup"><span data-stu-id="9906e-142">Right-click hello disk again and select **New Volume**.</span></span>

6. <span data-ttu-id="9906e-143">Conclua o Assistente de saudação usando valores padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="9906e-143">Complete hello wizard using hello default values.</span></span> <span data-ttu-id="9906e-144">Quando termina de assistente hello, Olá **Volumes** seção lista novo volume de saudação.</span><span class="sxs-lookup"><span data-stu-id="9906e-144">When hello wizard is done, hello **Volumes** section lists hello new volume.</span></span> <span data-ttu-id="9906e-145">disco de saudação agora está online e pronto toostore dados.</span><span class="sxs-lookup"><span data-stu-id="9906e-145">hello disk is now online and ready toostore data.</span></span>

    ![Volume inicializado com êxito](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="9906e-147">Opção 2: Anexar um disco existente</span><span class="sxs-lookup"><span data-stu-id="9906e-147">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="9906e-148">Em Olá **discos** folha, clique em **anexar existente**.</span><span class="sxs-lookup"><span data-stu-id="9906e-148">On hello **Disks** blade, click **Attach existing**.</span></span>
2. <span data-ttu-id="9906e-149">Em **Anexar disco existente**, clique em **Local**.</span><span class="sxs-lookup"><span data-stu-id="9906e-149">Under **Attach existing disk**, click **Location**.</span></span>

   ![Anexar disco existente](./media/attach-disk/attachexistingdisksettings.png)
3. <span data-ttu-id="9906e-151">Em **contas de armazenamento**, selecione conta hello e contêiner que contém o arquivo. vhd de saudação.</span><span class="sxs-lookup"><span data-stu-id="9906e-151">Under **Storage accounts**, select hello account and container that holds hello .vhd file.</span></span>

   ![Localização do VHD](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. <span data-ttu-id="9906e-153">Selecione o arquivo. vhd de saudação.</span><span class="sxs-lookup"><span data-stu-id="9906e-153">Select hello .vhd file.</span></span>
5. <span data-ttu-id="9906e-154">Em **anexar o disco existente**, arquivo hello você selecionou é listado em **arquivo VHD**.</span><span class="sxs-lookup"><span data-stu-id="9906e-154">Under **Attach existing disk**, hello file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="9906e-155">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9906e-155">Click **OK**.</span></span>
6. <span data-ttu-id="9906e-156">Após anexa Azure hello disco toohello VM, ela é listada em configurações de disco da máquina de virtual Olá em **discos de dados**.</span><span class="sxs-lookup"><span data-stu-id="9906e-156">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="9906e-157">Usar TRIM com o armazenamento padrão</span><span class="sxs-lookup"><span data-stu-id="9906e-157">Use TRIM with standard storage</span></span>

<span data-ttu-id="9906e-158">Se você usar o armazenamento padrão (HDD), será necessário habilitar o TRIM.</span><span class="sxs-lookup"><span data-stu-id="9906e-158">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="9906e-159">TRIM descarta blocos não usados no disco Olá para que você é cobrado somente para o armazenamento que você está usando.</span><span class="sxs-lookup"><span data-stu-id="9906e-159">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="9906e-160">Usar o TRIM pode poupar dinheiro, incluindo blocos não utilizados que resultam da exclusão de arquivos grandes.</span><span class="sxs-lookup"><span data-stu-id="9906e-160">Using TRIM can save costs, including unused blocks that result from deleting large files.</span></span>

<span data-ttu-id="9906e-161">Você pode executar essa configuração de CORTE de saudação do comando toocheck.</span><span class="sxs-lookup"><span data-stu-id="9906e-161">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="9906e-162">Abra um prompt de comando na sua VM do Windows e digite:</span><span class="sxs-lookup"><span data-stu-id="9906e-162">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="9906e-163">Se o comando Olá retorna 0, TRIM está habilitada corretamente.</span><span class="sxs-lookup"><span data-stu-id="9906e-163">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="9906e-164">Se ele retorna 1, execute Olá comando tooenable TRIM a seguir:</span><span class="sxs-lookup"><span data-stu-id="9906e-164">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a><span data-ttu-id="9906e-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9906e-165">Next steps</span></span>
<span data-ttu-id="9906e-166">Se seu aplicativo precisa de dados de toostore toouse saudação d: unidade, você pode [alterar Olá letra da unidade de disco temporário do Windows hello](../../virtual-machines-windows-change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="9906e-166">If your application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](../../virtual-machines-windows-change-drive-letter.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9906e-167">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9906e-167">Additional resources</span></span>
[<span data-ttu-id="9906e-168">Sobre discos e VHDs para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="9906e-168">About disks and VHDs for virtual machines</span></span>](../../virtual-machines-linux-about-disks-vhds.md)
