---
title: "Anexar um disco de dados gerenciado a uma VM Windows – Azure | Microsoft Docs"
description: "Como anexar um novo disco de dados gerenciado a uma VM Windows no portal do Azure usando o modelo de implantação do Resource Manager."
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
ms.openlocfilehash: f0cf88a06c5470ef173b22e7213419a6c8760723
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-attach-a-managed-data-disk-to-a-windows-vm-in-the-azure-portal"></a><span data-ttu-id="30de6-103">Como anexar um disco de dados gerenciado a uma VM Windows no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="30de6-103">How to attach a managed data disk to a Windows VM in the Azure portal</span></span>

<span data-ttu-id="30de6-104">Este artigo mostra como anexar um novo disco de dados gerenciado a máquinas virtuais Windows por meio do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="30de6-104">This article shows you how to attach a new managed data disk to Windows virtual machines through the Azure portal.</span></span> <span data-ttu-id="30de6-105">Antes de fazer isso, revise estas dicas:</span><span class="sxs-lookup"><span data-stu-id="30de6-105">Before you do this, review these tips:</span></span>

* <span data-ttu-id="30de6-106">O tamanho da máquina virtual controla quantos discos de dados você pode anexar a ela.</span><span class="sxs-lookup"><span data-stu-id="30de6-106">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="30de6-107">Para obter detalhes, consulte [Tamanhos das máquinas virtuais](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="30de6-107">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="30de6-108">Para um novo disco, você não precisa criá-lo primeiro porque o Azure cria quando você anexa o mesmo.</span><span class="sxs-lookup"><span data-stu-id="30de6-108">For a new disk, you don't need to create it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="30de6-109">Você também pode [anexar um disco de dados usando o Powershell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="30de6-109">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>



## <a name="add-a-data-disk"></a><span data-ttu-id="30de6-110">Adicionar um disco de dados</span><span class="sxs-lookup"><span data-stu-id="30de6-110">Add a data disk</span></span>
1. <span data-ttu-id="30de6-111">No menu à esquerda, clique em **Máquinas Virtuais**.</span><span class="sxs-lookup"><span data-stu-id="30de6-111">In the menu on the left, click **Virtual Machines**.</span></span>
2. <span data-ttu-id="30de6-112">Selecione a máquina virtual na lista.</span><span class="sxs-lookup"><span data-stu-id="30de6-112">Select the virtual machine from the list.</span></span>
3. <span data-ttu-id="30de6-113">Na folha da máquina virtual, clique em **Discos**.</span><span class="sxs-lookup"><span data-stu-id="30de6-113">On the virtual machine blade, click **Disks**.</span></span>
   4. <span data-ttu-id="30de6-114">Na folha **Discos**, clique em **+ Adicionar disco de dados**.</span><span class="sxs-lookup"><span data-stu-id="30de6-114">On the **Disks** blade, click **+ Add data disk**.</span></span>
5. <span data-ttu-id="30de6-115">No menu suspenso do novo disco, selecione **Criar vazio**.</span><span class="sxs-lookup"><span data-stu-id="30de6-115">In the drop-down for the new disk, select **Create empty**.</span></span>
6. <span data-ttu-id="30de6-116">Na folha **Criar disco gerenciado**, digite um nome para o disco e ajuste as outras configurações, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="30de6-116">In the **Create managed disk** blade, type in a name for the disk and adjust the other settings as necessary.</span></span> <span data-ttu-id="30de6-117">Quando terminar, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="30de6-117">When you are done, click **Create**.</span></span>
7. <span data-ttu-id="30de6-118">Na folha **Discos**, clique em Salvar para salvar a nova configuração de disco da VM.</span><span class="sxs-lookup"><span data-stu-id="30de6-118">In the **Disks** blade, click save to save the new disk configuration for the VM.</span></span>
6. <span data-ttu-id="30de6-119">Depois que o Azure cria o disco e o anexa à máquina virtual, o novo disco é listado nas configurações de disco da máquina virtual em **Discos de Dados**.</span><span class="sxs-lookup"><span data-stu-id="30de6-119">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="initialize-a-new-data-disk"></a><span data-ttu-id="30de6-120">Inicializar um novo disco de dados</span><span class="sxs-lookup"><span data-stu-id="30de6-120">Initialize a new data disk</span></span>

1. <span data-ttu-id="30de6-121">Conecte-se à VM.</span><span class="sxs-lookup"><span data-stu-id="30de6-121">Connect to the VM.</span></span>
1. <span data-ttu-id="30de6-122">Clique no menu Iniciar dentro da VM, digite **diskmgmt.msc** e clique em **Enter**.</span><span class="sxs-lookup"><span data-stu-id="30de6-122">Click the start menu inside the VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="30de6-123">Isso iniciará o snap-in Gerenciamento de Disco.</span><span class="sxs-lookup"><span data-stu-id="30de6-123">This will start the Disk Management snap-in.</span></span>
2. <span data-ttu-id="30de6-124">O Gerenciamento de Disco reconhecerá que você tem um disco novo não inicializado e a janela Inicializar Disco será exibida.</span><span class="sxs-lookup"><span data-stu-id="30de6-124">Disk Management will recognize that you have a new, un-initialized disk and the Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="30de6-125">Verifique se o novo disco está selecionado e clique em **OK** para inicializá-lo.</span><span class="sxs-lookup"><span data-stu-id="30de6-125">Make sure the new disk is selected and click **OK** to initialize it.</span></span>
4. <span data-ttu-id="30de6-126">O novo disco agora será exibido como **não alocado**.</span><span class="sxs-lookup"><span data-stu-id="30de6-126">The new disk will now appear as **unallocated**.</span></span> <span data-ttu-id="30de6-127">Clique com o botão direito do mouse em qualquer lugar do disco e selecione **Novo volume simples**.</span><span class="sxs-lookup"><span data-stu-id="30de6-127">Right-click anywhere on the disk and select **New simple volume**.</span></span> <span data-ttu-id="30de6-128">O **Assistente para Novo Volume Simples** será iniciado.</span><span class="sxs-lookup"><span data-stu-id="30de6-128">The **New Simple Volume Wizard** will start.</span></span>
5. <span data-ttu-id="30de6-129">Percorra as etapas do assistente mantendo todos os padrões. Quando terminar, selecione **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="30de6-129">Go through the wizard, keeping all of the defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="30de6-130">Feche Gerenciamento de Disco.</span><span class="sxs-lookup"><span data-stu-id="30de6-130">Close Disk Management.</span></span>
7. <span data-ttu-id="30de6-131">Você receberá um pop-up que é necessário para formatar o novo disco antes que você possa usá-lo.</span><span class="sxs-lookup"><span data-stu-id="30de6-131">You will get a pop-up that you need to format the new disk before you can use it.</span></span> <span data-ttu-id="30de6-132">Clique em **Formatar disco**.</span><span class="sxs-lookup"><span data-stu-id="30de6-132">Click **Format disk**.</span></span>
8. <span data-ttu-id="30de6-133">Na caixa de diálogo **Formatar novo disco**, verifique as configurações e, em seguida, clique em **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="30de6-133">In the **Format new disk** dialog, check the settings and then click **Start**.</span></span>
9. <span data-ttu-id="30de6-134">Você receberá um aviso informando que a formatação dos discos apagará todos os dados; clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="30de6-134">You will get a warning that formatting the disks will erase all of the data, click **OK**.</span></span>
10. <span data-ttu-id="30de6-135">Quando a formatação for concluída, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="30de6-135">When the format is complete, click **OK**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="30de6-136">Usar TRIM com o armazenamento padrão</span><span class="sxs-lookup"><span data-stu-id="30de6-136">Use TRIM with standard storage</span></span>

<span data-ttu-id="30de6-137">Se você usar o armazenamento padrão (HDD), será necessário habilitar o TRIM.</span><span class="sxs-lookup"><span data-stu-id="30de6-137">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="30de6-138">O TRIM descarta os blocos não usados do disco para que você seja cobrado apenas pelo armazenamento que está efetivamente sendo usado.</span><span class="sxs-lookup"><span data-stu-id="30de6-138">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="30de6-139">Isso poderá representar uma economia dos custos se você criar arquivos grandes e, em seguida, excluí-los.</span><span class="sxs-lookup"><span data-stu-id="30de6-139">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="30de6-140">Você pode executar esse comando para verificar a configuração de TRIM.</span><span class="sxs-lookup"><span data-stu-id="30de6-140">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="30de6-141">Abra um prompt de comando na sua VM do Windows e digite:</span><span class="sxs-lookup"><span data-stu-id="30de6-141">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="30de6-142">Se o comando retornar 0, o TRIM estará habilitado corretamente.</span><span class="sxs-lookup"><span data-stu-id="30de6-142">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="30de6-143">Se ele retornar 1, execute o seguinte comando para habilitar o TRIM:</span><span class="sxs-lookup"><span data-stu-id="30de6-143">If it returns 1, run the following command to enable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="30de6-144">Após a exclusão de dados do disco, você pode garantir a liberação de operações TRIM corretamente executando a desfragmentação com TRIM:</span><span class="sxs-lookup"><span data-stu-id="30de6-144">After deleting data from your disk, you can ensure the TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="30de6-145">Você também pode garantir que o volume inteiro seja reduzido formatando-o.</span><span class="sxs-lookup"><span data-stu-id="30de6-145">You can also ensure the entire volume is trimmed by formatting the volume.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30de6-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="30de6-146">Next steps</span></span>
<span data-ttu-id="30de6-147">Caso seu aplicativo precise usar a unidade D: para armazenar dados, é possível [alterar a letra da unidade do disco temporário do Windows](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="30de6-147">If you application needs to use the D: drive to store data, you can [change the drive letter of the Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
