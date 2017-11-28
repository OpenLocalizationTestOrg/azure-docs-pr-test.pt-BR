---
title: "aaaAttach um tooa de disco de dados não gerenciados Windows VM - Azure | Microsoft Docs"
description: "Como tooattach não gerenciada de dados novo ou existente disco tooa VM do Windows no hello usando o portal do Azure Olá modelo de implantação do Gerenciador de recursos."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3790fc59-7264-41df-b7a3-8d1226799885
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: 923a6663974143bf359970f9b0eb0d36cabcba9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-an-unmanaged-data-disk-tooa-windows-vm-in-hello-azure-portal"></a><span data-ttu-id="d899a-103">Como tooattach um dados não gerenciados disco tooa VM do Windows no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d899a-103">How tooattach an unmanaged data disk tooa Windows VM in hello Azure portal</span></span>

<span data-ttu-id="d899a-104">Este artigo mostra como tooattach novo e existente não gerenciado discos tooWindows máquinas de virtuais por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d899a-104">This article shows you how tooattach both new and existing unmanaged disks tooWindows virtual machines through hello Azure portal.</span></span> <span data-ttu-id="d899a-105">Você também pode [anexar um disco de dados usando o PowerShell](./attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d899a-105">You can also [attach a data disk using PowerShell](./attach-disk-ps.md).</span></span> <span data-ttu-id="d899a-106">Antes de fazer isso, revise estas dicas:</span><span class="sxs-lookup"><span data-stu-id="d899a-106">Before you do this, review these tips:</span></span>

* <span data-ttu-id="d899a-107">tamanho de saudação da máquina virtual de saudação controla quantos discos de dados, você pode anexar.</span><span class="sxs-lookup"><span data-stu-id="d899a-107">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="d899a-108">Para obter detalhes, consulte [Tamanhos das máquinas virtuais](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="d899a-108">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="d899a-109">toouse armazenamento Premium, você precisa de uma máquina virtual da série DS ou série GS.</span><span class="sxs-lookup"><span data-stu-id="d899a-109">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="d899a-110">Você pode usar discos de contas de armazenamento Premium e Standard com essas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="d899a-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="d899a-111">O armazenamento Premium está disponível em determinadas regiões.</span><span class="sxs-lookup"><span data-stu-id="d899a-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="d899a-112">Para obter detalhes, confira [Armazenamento Premium: armazenamento de alto desempenho para as cargas de trabalho das máquinas virtuais do Azure](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d899a-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="d899a-113">Para um novo disco, você não precisa toocreate-lo primeiro porque o Azure cria quando anexá-lo.</span><span class="sxs-lookup"><span data-stu-id="d899a-113">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>


<span data-ttu-id="d899a-114">Você também pode [anexar um disco de dados usando o Powershell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d899a-114">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>


## <a name="find-hello-virtual-machine"></a><span data-ttu-id="d899a-115">Localizar a máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="d899a-115">Find hello virtual machine</span></span>
1. <span data-ttu-id="d899a-116">Entrar toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d899a-116">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d899a-117">No menu Olá Olá esquerda, clique em **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="d899a-117">In hello menu on hello left, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="d899a-118">Selecione máquina virtual de Olá Olá lista.</span><span class="sxs-lookup"><span data-stu-id="d899a-118">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="d899a-119">Na folha de máquinas virtuais de saudação, clique em **discos**.</span><span class="sxs-lookup"><span data-stu-id="d899a-119">In hello Virtual machines blade, click **Disks**.</span></span>
   
<span data-ttu-id="d899a-120">Continue seguindo as instruções para anexar um [novo disco](#option-1-attach-a-new-disk) ou um [disco existente](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="d899a-120">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="d899a-121">Opção 1: Anexar e inicializar um novo disco</span><span class="sxs-lookup"><span data-stu-id="d899a-121">Option 1: Attach and initialize a new disk</span></span>
1. <span data-ttu-id="d899a-122">Em Olá **discos** folha, clique em **+ adicionar disco de dados**.</span><span class="sxs-lookup"><span data-stu-id="d899a-122">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="d899a-123">Em Olá **anexar disco gerenciado** folha, digite um nome para o disco de saudação em **nome** e, em seguida, selecione **New (disco vazio)** na **tipo de fonte**.</span><span class="sxs-lookup"><span data-stu-id="d899a-123">In hello **Attach managed disk** blade, type a name for hello disk in **Name** and then select **New (empty disk)** in **Source type**.</span></span>
3. <span data-ttu-id="d899a-124">Em **contêiner de armazenamento**, clique em Olá **procurar** botão e procurar toohello conta de armazenamento e contêiner qual seria Olá novo VHD toobe armazenado e, em seguida, clique em **selecione**.</span><span class="sxs-lookup"><span data-stu-id="d899a-124">Under **Storage container**, click hello **Browse** button and browse toohello storage account and container where you would like hello new VHD toobe stored and then click **Select**.</span></span> 
  
   ![Analisar configurações de disco](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. <span data-ttu-id="d899a-126">Quando tiver terminado com as configurações de saudação de disco de dados hello, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="d899a-126">When you are done with hello settings for hello data disk, click **OK**.</span></span>
4. <span data-ttu-id="d899a-127">Em Olá **discos** folha, clique em **salvar** configuração da VM toohello tooadd Olá disco.</span><span class="sxs-lookup"><span data-stu-id="d899a-127">Back in hello **Disks** blade, click **Save** tooadd hello disk toohello VM configuration.</span></span>


### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="d899a-128">Inicializar um novo disco de dados</span><span class="sxs-lookup"><span data-stu-id="d899a-128">Initialize a new data disk</span></span>

1. <span data-ttu-id="d899a-129">Conecte-se a máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="d899a-129">Connect toohello virtual machine.</span></span> <span data-ttu-id="d899a-130">Para obter instruções, consulte [como tooconnect e logon tooan virtuais do Azure do computador que executa o Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d899a-130">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
1. <span data-ttu-id="d899a-131">Clique em Olá **iniciar** menu dentro Olá VM e digite **diskmgmt.msc** e clique em **Enter**.</span><span class="sxs-lookup"><span data-stu-id="d899a-131">Click hello **Start** menu inside hello VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="d899a-132">Isso inicia o snap-in de gerenciamento de disco de saudação.</span><span class="sxs-lookup"><span data-stu-id="d899a-132">This starts hello Disk Management snap-in.</span></span>
2. <span data-ttu-id="d899a-133">Gerenciamento de disco reconhece que você tenha um disco novo e não inicializado e Olá inicializar disco janela será exibida.</span><span class="sxs-lookup"><span data-stu-id="d899a-133">Disk Management recognizes that you have a new, uninitialized disk and hello Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="d899a-134">Verifique se o novo disco de saudação é selecionado e clique em **Okey** tooinitialize-lo.</span><span class="sxs-lookup"><span data-stu-id="d899a-134">Make sure hello new disk is selected and click **OK** tooinitialize it.</span></span>
4. <span data-ttu-id="d899a-135">Olá novo disco agora aparece como **não alocado**.</span><span class="sxs-lookup"><span data-stu-id="d899a-135">hello new disk now appears as **unallocated**.</span></span> <span data-ttu-id="d899a-136">Clique em qualquer lugar no disco hello e selecione **novo volume simples**.</span><span class="sxs-lookup"><span data-stu-id="d899a-136">Right-click anywhere on hello disk and select **New simple volume**.</span></span> <span data-ttu-id="d899a-137">Olá **Assistente de novo Volume simples** inicia.</span><span class="sxs-lookup"><span data-stu-id="d899a-137">hello **New Simple Volume Wizard** starts.</span></span>
5. <span data-ttu-id="d899a-138">Vá pelo assistente hello, mantendo todos os padrões de hello quando você terminar de selecionar **concluir**.</span><span class="sxs-lookup"><span data-stu-id="d899a-138">Go through hello wizard, keeping all of hello defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="d899a-139">Feche Gerenciamento de Disco.</span><span class="sxs-lookup"><span data-stu-id="d899a-139">Close Disk Management.</span></span>
7. <span data-ttu-id="d899a-140">Você receberá um pop-up que você precisa novo disco de saudação tooformat antes de você pode usá-lo.</span><span class="sxs-lookup"><span data-stu-id="d899a-140">You get a pop-up that you need tooformat hello new disk before you can use it.</span></span> <span data-ttu-id="d899a-141">Clique em **Formatar disco**.</span><span class="sxs-lookup"><span data-stu-id="d899a-141">Click **Format disk**.</span></span>
8. <span data-ttu-id="d899a-142">Em Olá **disco no novo formato** caixa de diálogo, verifique as configurações de saudação e depois clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="d899a-142">In hello **Format new disk** dialog, check hello settings and then click **Start**.</span></span>
9. <span data-ttu-id="d899a-143">Você receberá um aviso de que a formatação de discos Olá apaga todos os dados de saudação, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="d899a-143">You get a warning that formatting hello disks erases all of hello data, click **OK**.</span></span>
10. <span data-ttu-id="d899a-144">Quando o formato de saudação for concluído, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="d899a-144">When hello format is complete, click **OK**.</span></span>


## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="d899a-145">Opção 2: Anexar um disco existente</span><span class="sxs-lookup"><span data-stu-id="d899a-145">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="d899a-146">Em Olá **discos** folha, clique em **+ adicionar disco de dados**.</span><span class="sxs-lookup"><span data-stu-id="d899a-146">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="d899a-147">Em Olá **anexar o disco não gerenciado** folha, na **tipo de fonte** selecione **blob existente**.</span><span class="sxs-lookup"><span data-stu-id="d899a-147">On hello **Attach unmanaged disk** blade, in **Source type** select **Existing blob**.</span></span>

    ![Analisar configurações de disco](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. <span data-ttu-id="d899a-149">Clique em **procurar** toonavigate toohello conta de armazenamento e o contêiner onde hello VHD existente está localizado.</span><span class="sxs-lookup"><span data-stu-id="d899a-149">Click **Browse** toonavigate toohello storage account and container where hello existing VHD is located.</span></span> <span data-ttu-id="d899a-150">Clique em e Olá VHD e, em seguida, clique em **selecione**.</span><span class="sxs-lookup"><span data-stu-id="d899a-150">Click and hello VHD and then click **Select**.</span></span>
4. <span data-ttu-id="d899a-151">Clique em **Okey** em Olá **anexar o disco não gerenciado** folha.</span><span class="sxs-lookup"><span data-stu-id="d899a-151">Click **OK** in hello **Attach unmanaged disk** blade.</span></span>
5. <span data-ttu-id="d899a-152">Em Olá **discos** folha, clique em **salvar** tooadd Olá toohello da configuração de disco Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d899a-152">In hello **Disks** blade, click **Save** tooadd hello disk toohello configuration for hello VM.</span></span>
   


## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="d899a-153">Usar TRIM com o armazenamento padrão</span><span class="sxs-lookup"><span data-stu-id="d899a-153">Use TRIM with standard storage</span></span>

<span data-ttu-id="d899a-154">Se você usar o armazenamento padrão (HDD), será necessário habilitar o TRIM.</span><span class="sxs-lookup"><span data-stu-id="d899a-154">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="d899a-155">TRIM descarta blocos não usados no disco Olá para que você é cobrado somente para o armazenamento que você está usando.</span><span class="sxs-lookup"><span data-stu-id="d899a-155">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="d899a-156">Isso poderá representar uma economia dos custos se você criar arquivos grandes e, em seguida, excluí-los.</span><span class="sxs-lookup"><span data-stu-id="d899a-156">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="d899a-157">Você pode executar essa configuração de CORTE de saudação do comando toocheck.</span><span class="sxs-lookup"><span data-stu-id="d899a-157">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="d899a-158">Abra um prompt de comando na sua VM do Windows e digite:</span><span class="sxs-lookup"><span data-stu-id="d899a-158">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="d899a-159">Se o comando Olá retorna 0, TRIM está habilitada corretamente.</span><span class="sxs-lookup"><span data-stu-id="d899a-159">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="d899a-160">Se ele retorna 1, execute Olá comando tooenable TRIM a seguir:</span><span class="sxs-lookup"><span data-stu-id="d899a-160">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="d899a-161">Depois de excluir dados do disco, você pode garantir operações de CORTE de saudação liberação corretamente executando desfragmentação com TRIM:</span><span class="sxs-lookup"><span data-stu-id="d899a-161">After deleting data from your disk, you can ensure hello TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="d899a-162">Você também pode garantir a todo o volume Olá é cortado ao formatar o volume de saudação.</span><span class="sxs-lookup"><span data-stu-id="d899a-162">You can also ensure hello entire volume is trimmed by formatting hello volume.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d899a-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d899a-163">Next steps</span></span>
<span data-ttu-id="d899a-164">Se seu aplicativo precisa de dados de toostore toouse saudação d: unidade, você pode [alterar Olá letra da unidade de disco temporário do Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d899a-164">If you application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

