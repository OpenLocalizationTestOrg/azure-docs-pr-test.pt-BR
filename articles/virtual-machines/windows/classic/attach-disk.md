---
title: "Anexar disco a uma VM clássica do Azure | Microsoft Docs"
description: "Anexe um disco de dados a uma máquina virtual do Windows criada com o modelo de implantação clássica e inicialize-a."
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
ms.openlocfilehash: 087d5cda354f6e1780bddd3725859444177abd16
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="attach-a-data-disk-to-a-windows-virtual-machine-created-with-the-classic-deployment-model"></a><span data-ttu-id="2e758-103">Anexe um disco de dados a uma máquina virtual do Windows criada com o modelo de implantação clássico</span><span class="sxs-lookup"><span data-stu-id="2e758-103">Attach a data disk to a Windows virtual machine created with the classic deployment model</span></span>
<!--
Refernce article:
    If you want to use the new portal, see [How to attach a data disk to a Windows VM in the Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

<span data-ttu-id="2e758-104">Este artigo mostra como anexar discos novos e existentes criados com o modelo de implantação Clássico a uma máquina virtual Windows usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2e758-104">This article shows you how to attach new and existing disks created with the Classic deployment model to a Windows virtual machine using the Azure portal.</span></span>

<span data-ttu-id="2e758-105">Você também pode [anexar um disco de dados a uma VM Linux no portal do Azure](../../linux/attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2e758-105">You can also [attach a data disk to a Linux VM in the Azure portal](../../linux/attach-disk-portal.md).</span></span>

<span data-ttu-id="2e758-106">Antes de anexar um disco, leia estas dicas:</span><span class="sxs-lookup"><span data-stu-id="2e758-106">Before you attach a disk, review these tips:</span></span>

* <span data-ttu-id="2e758-107">O tamanho da máquina virtual controla quantos discos de dados você pode anexar a ela.</span><span class="sxs-lookup"><span data-stu-id="2e758-107">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="2e758-108">Para obter detalhes, consulte [Tamanhos das máquinas virtuais](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e758-108">For details, see [Sizes for virtual machines](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="2e758-109">Para usar o Armazenamento Premium, você precisa de uma máquina virtual da série DS ou GS.</span><span class="sxs-lookup"><span data-stu-id="2e758-109">To use Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="2e758-110">Você pode usar discos de contas de armazenamento Premium e Standard com essas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="2e758-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="2e758-111">O armazenamento Premium está disponível em determinadas regiões.</span><span class="sxs-lookup"><span data-stu-id="2e758-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="2e758-112">Para obter detalhes, confira [Armazenamento Premium: armazenamento de alto desempenho para as cargas de trabalho das máquinas virtuais do Azure](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e758-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="2e758-113">Para um novo disco, você não precisa criá-lo primeiro porque o Azure cria quando você anexa o mesmo.</span><span class="sxs-lookup"><span data-stu-id="2e758-113">For a new disk, you don't need to create it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="2e758-114">Você também pode [anexar um disco de dados usando o Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2e758-114">You can also [attach a data disk using Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e758-115">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2e758-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>

## <a name="find-the-virtual-machine"></a><span data-ttu-id="2e758-116">Localizar a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2e758-116">Find the virtual machine</span></span>
1. <span data-ttu-id="2e758-117">Entre no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2e758-117">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2e758-118">Escolha a máquina virtual nos recursos listados no painel.</span><span class="sxs-lookup"><span data-stu-id="2e758-118">Select the virtual machine from the resource listed on the dashboard.</span></span>
3. <span data-ttu-id="2e758-119">No painel esquerdo, em **Configurações**, clique em **Discos**.</span><span class="sxs-lookup"><span data-stu-id="2e758-119">In the left pane under **Settings**, click **Disks**.</span></span>

    ![Abrir configurações de disco](./media/attach-disk/virtualmachinedisks.png)

<span data-ttu-id="2e758-121">Continue seguindo as instruções para anexar um [novo disco](#option-1-attach-a-new-disk) ou um [disco existente](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="2e758-121">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="2e758-122">Opção 1: Anexar e inicializar um novo disco</span><span class="sxs-lookup"><span data-stu-id="2e758-122">Option 1: Attach and initialize a new disk</span></span>

1. <span data-ttu-id="2e758-123">Na folha **Discos**, clique em **Anexar novo**.</span><span class="sxs-lookup"><span data-stu-id="2e758-123">On the **Disks** blade, click **Attach new**.</span></span>
2. <span data-ttu-id="2e758-124">Examine as configurações padrão, atualize conforme necessário e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="2e758-124">Review the default settings, update as necessary, and then click **OK**.</span></span>

   ![Analisar configurações de disco](./media/attach-disk/attach-new.png)

3. <span data-ttu-id="2e758-126">Depois que o Azure cria o disco e o anexa à máquina virtual, o novo disco é listado nas configurações de disco da máquina virtual em **Discos de Dados**.</span><span class="sxs-lookup"><span data-stu-id="2e758-126">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="2e758-127">Inicializar um novo disco de dados</span><span class="sxs-lookup"><span data-stu-id="2e758-127">Initialize a new data disk</span></span>

1. <span data-ttu-id="2e758-128">Conectar-se à máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2e758-128">Connect to the virtual machine.</span></span> <span data-ttu-id="2e758-129">Para obter instruções, consulte [Como se conectar e fazer logon em uma máquina virtual do Azure executando o Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e758-129">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="2e758-130">Depois de entrar na máquina virtual, abra o **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="2e758-130">After you log on to the virtual machine, open **Server Manager**.</span></span> <span data-ttu-id="2e758-131">No painel esquerdo, selecione **Arquivos e serviços de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="2e758-131">In the left pane, select **File and Storage Services**.</span></span>

    ![Abra o gerenciador de servidor.](../media/attach-disk-portal/fileandstorageservices.png)

3. <span data-ttu-id="2e758-133">Escolha **Discos**.</span><span class="sxs-lookup"><span data-stu-id="2e758-133">Select **Disks**.</span></span>
4. <span data-ttu-id="2e758-134">A seção **Discos** lista os discos.</span><span class="sxs-lookup"><span data-stu-id="2e758-134">The **Disks** section lists the disks.</span></span> <span data-ttu-id="2e758-135">Na maioria das vezes, uma máquina virtual tem disco 0, disco 1 e disco 2.</span><span class="sxs-lookup"><span data-stu-id="2e758-135">Most often, a virtual machine has disk 0, disk 1, and disk 2.</span></span> <span data-ttu-id="2e758-136">Disco 0 é o disco do sistema operacional, disco 1 é o disco temporário e disco 2 é o disco de dados que você acabou de conectar à máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2e758-136">Disk 0 is the operating system disk, disk 1 is the temporary disk, and disk 2 is the data disk newly attached to the virtual machine.</span></span> <span data-ttu-id="2e758-137">O disco de dados lista a Partição como **Desconhecido**.</span><span class="sxs-lookup"><span data-stu-id="2e758-137">The data disk lists the Partition as **Unknown**.</span></span>

 <span data-ttu-id="2e758-138">Clique com o botão direito do mouse no disco e selecione **Inicializar**.</span><span class="sxs-lookup"><span data-stu-id="2e758-138">Right-click the disk and select **Initialize**.</span></span>

5. <span data-ttu-id="2e758-139">Você é notificado de que todos os dados serão apagados quando o disco for inicializado.</span><span class="sxs-lookup"><span data-stu-id="2e758-139">You're notified that all data will be erased when the disk is initialized.</span></span> <span data-ttu-id="2e758-140">Clique em **Sim** para confirmar o aviso e inicializar o disco.</span><span class="sxs-lookup"><span data-stu-id="2e758-140">Click **Yes** to acknowledge the warning and initialize the disk.</span></span> <span data-ttu-id="2e758-141">Depois de concluir, a partição será listada como **GPT**.</span><span class="sxs-lookup"><span data-stu-id="2e758-141">Once complete, the partition will be listed as **GPT**.</span></span> <span data-ttu-id="2e758-142">Clique com o botão direito do mouse no disco novamente e selecione **Novo Volume**.</span><span class="sxs-lookup"><span data-stu-id="2e758-142">Right-click the disk again and select **New Volume**.</span></span>

6. <span data-ttu-id="2e758-143">Conclua o assistente usando os valores padrão.</span><span class="sxs-lookup"><span data-stu-id="2e758-143">Complete the wizard using the default values.</span></span> <span data-ttu-id="2e758-144">Quando o assistente for concluído, a seção **Volumes** listará o novo volume.</span><span class="sxs-lookup"><span data-stu-id="2e758-144">When the wizard is done, the **Volumes** section lists the new volume.</span></span> <span data-ttu-id="2e758-145">Agora, o disco está online e pronto para armazenar dados.</span><span class="sxs-lookup"><span data-stu-id="2e758-145">The disk is now online and ready to store data.</span></span>

    ![Volume inicializado com êxito](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="2e758-147">Opção 2: Anexar um disco existente</span><span class="sxs-lookup"><span data-stu-id="2e758-147">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="2e758-148">Na folha **Discos**, clique em **Anexar existente**.</span><span class="sxs-lookup"><span data-stu-id="2e758-148">On the **Disks** blade, click **Attach existing**.</span></span>
2. <span data-ttu-id="2e758-149">Em **Anexar disco existente**, clique em **Local**.</span><span class="sxs-lookup"><span data-stu-id="2e758-149">Under **Attach existing disk**, click **Location**.</span></span>

   ![Anexar disco existente](./media/attach-disk/attachexistingdisksettings.png)
3. <span data-ttu-id="2e758-151">Em **Contas de armazenamento**, selecione a conta e o contêiner que mantém o arquivo .vhd.</span><span class="sxs-lookup"><span data-stu-id="2e758-151">Under **Storage accounts**, select the account and container that holds the .vhd file.</span></span>

   ![Localização do VHD](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. <span data-ttu-id="2e758-153">Selecionar o arquivo .vhd</span><span class="sxs-lookup"><span data-stu-id="2e758-153">Select the .vhd file.</span></span>
5. <span data-ttu-id="2e758-154">Em **Anexar disco existente**, o arquivo que você selecionou é listado em **Arquivo VHD**.</span><span class="sxs-lookup"><span data-stu-id="2e758-154">Under **Attach existing disk**, the file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="2e758-155">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="2e758-155">Click **OK**.</span></span>
6. <span data-ttu-id="2e758-156">Depois que o Azure anexa o disco à máquina virtual, ele é listado nas configurações de disco da máquina virtual em **Discos de Dados**.</span><span class="sxs-lookup"><span data-stu-id="2e758-156">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="2e758-157">Usar TRIM com o armazenamento padrão</span><span class="sxs-lookup"><span data-stu-id="2e758-157">Use TRIM with standard storage</span></span>

<span data-ttu-id="2e758-158">Se você usar o armazenamento padrão (HDD), será necessário habilitar o TRIM.</span><span class="sxs-lookup"><span data-stu-id="2e758-158">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="2e758-159">O TRIM descarta os blocos não usados do disco para que você seja cobrado apenas pelo armazenamento que está efetivamente sendo usado.</span><span class="sxs-lookup"><span data-stu-id="2e758-159">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="2e758-160">Usar o TRIM pode poupar dinheiro, incluindo blocos não utilizados que resultam da exclusão de arquivos grandes.</span><span class="sxs-lookup"><span data-stu-id="2e758-160">Using TRIM can save costs, including unused blocks that result from deleting large files.</span></span>

<span data-ttu-id="2e758-161">Você pode executar esse comando para verificar a configuração de TRIM.</span><span class="sxs-lookup"><span data-stu-id="2e758-161">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="2e758-162">Abra um prompt de comando na sua VM do Windows e digite:</span><span class="sxs-lookup"><span data-stu-id="2e758-162">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="2e758-163">Se o comando retornar 0, o TRIM estará habilitado corretamente.</span><span class="sxs-lookup"><span data-stu-id="2e758-163">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="2e758-164">Se ele retornar 1, execute o seguinte comando para habilitar o TRIM:</span><span class="sxs-lookup"><span data-stu-id="2e758-164">If it returns 1, run the following command to enable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a><span data-ttu-id="2e758-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2e758-165">Next steps</span></span>
<span data-ttu-id="2e758-166">Caso seu aplicativo precise usar a unidade D: para armazenar dados, é possível [alterar a letra da unidade do disco temporário do Windows](../../virtual-machines-windows-change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="2e758-166">If your application needs to use the D: drive to store data, you can [change the drive letter of the Windows temporary disk](../../virtual-machines-windows-change-drive-letter.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2e758-167">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="2e758-167">Additional resources</span></span>
[<span data-ttu-id="2e758-168">Sobre discos e VHDs para máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="2e758-168">About disks and VHDs for virtual machines</span></span>](../../virtual-machines-linux-about-disks-vhds.md)
