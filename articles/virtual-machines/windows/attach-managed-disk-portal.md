---
title: aaaAttach um tooa de disco de dados gerenciados VM do Windows - Azure | Microsoft Docs
description: "Como tooattach novo gerenciados tooa de disco de dados em hello usando o portal do Azure VM do Windows hello modelo de implantação do Gerenciador de recursos."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: bacc0589ad2d93e4d3d055c8f837f8db27291ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-managed-data-disk-tooa-windows-vm-in-hello-azure-portal"></a><span data-ttu-id="463b7-103">Como tooattach um dados gerenciados disco tooa VM do Windows no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="463b7-103">How tooattach a managed data disk tooa Windows VM in hello Azure portal</span></span>

<span data-ttu-id="463b7-104">Este artigo mostra como tooattach novos dados gerenciados disco tooWindows máquinas de virtuais por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="463b7-104">This article shows you how tooattach a new managed data disk tooWindows virtual machines through hello Azure portal.</span></span> <span data-ttu-id="463b7-105">Antes de fazer isso, revise estas dicas:</span><span class="sxs-lookup"><span data-stu-id="463b7-105">Before you do this, review these tips:</span></span>

* <span data-ttu-id="463b7-106">tamanho de saudação da máquina virtual de saudação controla quantos discos de dados, você pode anexar.</span><span class="sxs-lookup"><span data-stu-id="463b7-106">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="463b7-107">Para obter detalhes, consulte [Tamanhos das máquinas virtuais](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="463b7-107">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="463b7-108">Para um novo disco, você não precisa toocreate-lo primeiro porque o Azure cria quando anexá-lo.</span><span class="sxs-lookup"><span data-stu-id="463b7-108">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="463b7-109">Você também pode [anexar um disco de dados usando o Powershell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="463b7-109">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>



## <a name="add-a-data-disk"></a><span data-ttu-id="463b7-110">Adicionar um disco de dados</span><span class="sxs-lookup"><span data-stu-id="463b7-110">Add a data disk</span></span>
1. <span data-ttu-id="463b7-111">No menu Olá Olá esquerda, clique em **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="463b7-111">In hello menu on hello left, click **Virtual Machines**.</span></span>
2. <span data-ttu-id="463b7-112">Selecione máquina virtual de Olá Olá lista.</span><span class="sxs-lookup"><span data-stu-id="463b7-112">Select hello virtual machine from hello list.</span></span>
3. <span data-ttu-id="463b7-113">Na folha de máquina virtual de saudação, clique em **discos**.</span><span class="sxs-lookup"><span data-stu-id="463b7-113">On hello virtual machine blade, click **Disks**.</span></span>
   4. <span data-ttu-id="463b7-114">Em Olá **discos** folha, clique em **+ adicionar disco de dados**.</span><span class="sxs-lookup"><span data-stu-id="463b7-114">On hello **Disks** blade, click **+ Add data disk**.</span></span>
5. <span data-ttu-id="463b7-115">No hello suspenso para um novo disco de saudação, selecione **criar vazio**.</span><span class="sxs-lookup"><span data-stu-id="463b7-115">In hello drop-down for hello new disk, select **Create empty**.</span></span>
6. <span data-ttu-id="463b7-116">Em Olá **disco gerenciado criar** folha, digite um nome para o disco hello e ajuste Olá outras configurações conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="463b7-116">In hello **Create managed disk** blade, type in a name for hello disk and adjust hello other settings as necessary.</span></span> <span data-ttu-id="463b7-117">Quando terminar, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="463b7-117">When you are done, click **Create**.</span></span>
7. <span data-ttu-id="463b7-118">Em Olá **discos** folha, clique em Salvar toosave Olá nova configuração de disco Olá VM.</span><span class="sxs-lookup"><span data-stu-id="463b7-118">In hello **Disks** blade, click save toosave hello new disk configuration for hello VM.</span></span>
6. <span data-ttu-id="463b7-119">Depois do Azure cria o disco hello e anexa toohello virtual machine, novo disco de saudação é listado em configurações de disco da máquina de virtual Olá em **discos de dados**.</span><span class="sxs-lookup"><span data-stu-id="463b7-119">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="initialize-a-new-data-disk"></a><span data-ttu-id="463b7-120">Inicializar um novo disco de dados</span><span class="sxs-lookup"><span data-stu-id="463b7-120">Initialize a new data disk</span></span>

1. <span data-ttu-id="463b7-121">Conecte-se toohello VM.</span><span class="sxs-lookup"><span data-stu-id="463b7-121">Connect toohello VM.</span></span>
1. <span data-ttu-id="463b7-122">Clique em menu de início hello dentro Olá VM e o tipo **diskmgmt.msc** e clique em **Enter**.</span><span class="sxs-lookup"><span data-stu-id="463b7-122">Click hello start menu inside hello VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="463b7-123">Isso iniciará Olá snap-in Gerenciamento de disco.</span><span class="sxs-lookup"><span data-stu-id="463b7-123">This will start hello Disk Management snap-in.</span></span>
2. <span data-ttu-id="463b7-124">Gerenciamento de disco reconhecerá que você tenha um novo disco não inicializado e Olá inicializar disco janela será exibida.</span><span class="sxs-lookup"><span data-stu-id="463b7-124">Disk Management will recognize that you have a new, un-initialized disk and hello Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="463b7-125">Verifique se o novo disco de saudação é selecionado e clique em **Okey** tooinitialize-lo.</span><span class="sxs-lookup"><span data-stu-id="463b7-125">Make sure hello new disk is selected and click **OK** tooinitialize it.</span></span>
4. <span data-ttu-id="463b7-126">novo disco de saudação aparecerão como **não alocado**.</span><span class="sxs-lookup"><span data-stu-id="463b7-126">hello new disk will now appear as **unallocated**.</span></span> <span data-ttu-id="463b7-127">Clique em qualquer lugar no disco hello e selecione **novo volume simples**.</span><span class="sxs-lookup"><span data-stu-id="463b7-127">Right-click anywhere on hello disk and select **New simple volume**.</span></span> <span data-ttu-id="463b7-128">Olá **Assistente de novo Volume simples** será iniciado.</span><span class="sxs-lookup"><span data-stu-id="463b7-128">hello **New Simple Volume Wizard** will start.</span></span>
5. <span data-ttu-id="463b7-129">Vá pelo assistente hello, mantendo todos os padrões de hello quando você terminar de selecionar **concluir**.</span><span class="sxs-lookup"><span data-stu-id="463b7-129">Go through hello wizard, keeping all of hello defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="463b7-130">Feche Gerenciamento de Disco.</span><span class="sxs-lookup"><span data-stu-id="463b7-130">Close Disk Management.</span></span>
7. <span data-ttu-id="463b7-131">Você receberá um pop-up que você precisa novo disco de saudação tooformat antes de você pode usá-lo.</span><span class="sxs-lookup"><span data-stu-id="463b7-131">You will get a pop-up that you need tooformat hello new disk before you can use it.</span></span> <span data-ttu-id="463b7-132">Clique em **Formatar disco**.</span><span class="sxs-lookup"><span data-stu-id="463b7-132">Click **Format disk**.</span></span>
8. <span data-ttu-id="463b7-133">Em Olá **disco no novo formato** caixa de diálogo, verifique as configurações de saudação e depois clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="463b7-133">In hello **Format new disk** dialog, check hello settings and then click **Start**.</span></span>
9. <span data-ttu-id="463b7-134">Você receberá um aviso que formatar discos Olá irá apagar todos os dados de saudação, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="463b7-134">You will get a warning that formatting hello disks will erase all of hello data, click **OK**.</span></span>
10. <span data-ttu-id="463b7-135">Quando o formato de saudação for concluído, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="463b7-135">When hello format is complete, click **OK**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="463b7-136">Usar TRIM com o armazenamento padrão</span><span class="sxs-lookup"><span data-stu-id="463b7-136">Use TRIM with standard storage</span></span>

<span data-ttu-id="463b7-137">Se você usar o armazenamento padrão (HDD), será necessário habilitar o TRIM.</span><span class="sxs-lookup"><span data-stu-id="463b7-137">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="463b7-138">TRIM descarta blocos não usados no disco Olá para que você é cobrado somente para o armazenamento que você está usando.</span><span class="sxs-lookup"><span data-stu-id="463b7-138">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="463b7-139">Isso poderá representar uma economia dos custos se você criar arquivos grandes e, em seguida, excluí-los.</span><span class="sxs-lookup"><span data-stu-id="463b7-139">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="463b7-140">Você pode executar essa configuração de CORTE de saudação do comando toocheck.</span><span class="sxs-lookup"><span data-stu-id="463b7-140">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="463b7-141">Abra um prompt de comando na sua VM do Windows e digite:</span><span class="sxs-lookup"><span data-stu-id="463b7-141">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="463b7-142">Se o comando Olá retorna 0, TRIM está habilitada corretamente.</span><span class="sxs-lookup"><span data-stu-id="463b7-142">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="463b7-143">Se ele retorna 1, execute Olá comando tooenable TRIM a seguir:</span><span class="sxs-lookup"><span data-stu-id="463b7-143">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="463b7-144">Depois de excluir dados do disco, você pode garantir operações de CORTE de saudação liberação corretamente executando desfragmentação com TRIM:</span><span class="sxs-lookup"><span data-stu-id="463b7-144">After deleting data from your disk, you can ensure hello TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="463b7-145">Você também pode garantir a todo o volume Olá é cortado ao formatar o volume de saudação.</span><span class="sxs-lookup"><span data-stu-id="463b7-145">You can also ensure hello entire volume is trimmed by formatting hello volume.</span></span>

## <a name="next-steps"></a><span data-ttu-id="463b7-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="463b7-146">Next steps</span></span>
<span data-ttu-id="463b7-147">Se seu aplicativo precisa de dados de toostore toouse saudação d: unidade, você pode [alterar Olá letra da unidade de disco temporário do Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="463b7-147">If you application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
