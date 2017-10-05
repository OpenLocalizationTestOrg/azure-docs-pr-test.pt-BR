---
title: 'Tornar a unidade D: de uma VM um disco de dados | Microsoft Docs'
description: "Descreve como alterar letras de unidade de uma VM do Windows para que seja possível usar a unidade D: como uma unidade de dados."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 0867a931-0055-4e31-8403-9b38a3eeb904
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: cynthn
ms.openlocfilehash: 7667175c01be2421bfc3badd83b1d8aaeb29bfde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-d-drive-as-a-data-drive-on-a-windows-vm"></a><span data-ttu-id="0943f-103">Usar a unidade D: como uma unidade de dados em uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="0943f-103">Use the D: drive as a data drive on a Windows VM</span></span>
<span data-ttu-id="0943f-104">Se seu aplicativo precisar usar a unidade D para armazenar dados, siga estas instruções para usar uma letra da unidade diferente para o disco temporário.</span><span class="sxs-lookup"><span data-stu-id="0943f-104">If your application needs to use the D drive to store data, follow these instructions to use a different drive letter for the temporary disk.</span></span> <span data-ttu-id="0943f-105">Nunca use o disco temporário para armazenar os dados que você precisa manter.</span><span class="sxs-lookup"><span data-stu-id="0943f-105">Never use the temporary disk to store data that you need to keep.</span></span>

<span data-ttu-id="0943f-106">Caso você redimensione ou use a opção **Parar (Desalocar)** para uma máquina virtual, isso poderá disparar o posicionamento da máquina virtual para um novo hipervisor.</span><span class="sxs-lookup"><span data-stu-id="0943f-106">If you resize or **Stop (Deallocate)** a virtual machine, this may trigger placement of the virtual machine to a new hypervisor.</span></span> <span data-ttu-id="0943f-107">Um evento de manutenção planejada ou não planejada também pode disparar esse posicionamento.</span><span class="sxs-lookup"><span data-stu-id="0943f-107">A planned or unplanned maintenance event may also trigger this placement.</span></span> <span data-ttu-id="0943f-108">Nesse cenário, o disco temporário será reatribuído à primeira letra da unidade disponível.</span><span class="sxs-lookup"><span data-stu-id="0943f-108">In this scenario, the temporary disk will be reassigned to the first available drive letter.</span></span> <span data-ttu-id="0943f-109">Caso você tenha um aplicativo que exija especificamente a unidade D:, é necessário seguir estas etapas para mover temporariamente o pagefile.sys, anexar um novo disco de dados e atribuí-lo à letra D, bem como mover o pagefile.sys de volta à unidade temporária.</span><span class="sxs-lookup"><span data-stu-id="0943f-109">If you have an application that specifically requires the D: drive, you need to follow these steps to temporarily move the pagefile.sys, attach a new data disk and assign it the letter D and then move the pagefile.sys back to the temporary drive.</span></span> <span data-ttu-id="0943f-110">Depois de concluído, o Azure não usará novamente a unidade D: se a VM for movida para um hipervisor diferente.</span><span class="sxs-lookup"><span data-stu-id="0943f-110">Once complete, Azure will not take back the D: if the VM moves to a different hypervisor.</span></span>

<span data-ttu-id="0943f-111">Para obter mais informações sobre como o Azure usa o disco temporário, veja [Noções básicas sobre a unidade temporária nas Máquinas Virtuais do Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="0943f-111">For more information about how Azure uses the temporary disk, see [Understanding the temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>

## <a name="attach-the-data-disk"></a><span data-ttu-id="0943f-112">Anexar o disco de dados</span><span class="sxs-lookup"><span data-stu-id="0943f-112">Attach the data disk</span></span>
<span data-ttu-id="0943f-113">Primeiro, você precisará anexar o disco de dados à máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0943f-113">First, you'll need to attach the data disk to the virtual machine.</span></span> <span data-ttu-id="0943f-114">Para fazer isso usando o portal, veja [Como anexar um disco de dados gerenciado no Portal do Azure](attach-managed-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0943f-114">To do this using the portal, see [How to attach a managed data disk in the Azure portal](attach-managed-disk-portal.md).</span></span>

## <a name="temporarily-move-pagefilesys-to-c-drive"></a><span data-ttu-id="0943f-115">Mover temporariamente o pagefile.sys para a unidade C</span><span class="sxs-lookup"><span data-stu-id="0943f-115">Temporarily move pagefile.sys to C drive</span></span>
1. <span data-ttu-id="0943f-116">Conectar-se à máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0943f-116">Connect to the virtual machine.</span></span> 
2. <span data-ttu-id="0943f-117">Clique com o botão direito do mouse no menu **Iniciar** e selecione **Sistema**.</span><span class="sxs-lookup"><span data-stu-id="0943f-117">Right-click the **Start** menu and select **System**.</span></span>
3. <span data-ttu-id="0943f-118">No menu à esquerda, selecione **Configurações avançadas do sistema**.</span><span class="sxs-lookup"><span data-stu-id="0943f-118">In the left-hand menu, select **Advanced system settings**.</span></span>
4. <span data-ttu-id="0943f-119">Na seção **Desempenho**, selecione **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="0943f-119">In the **Performance** section, select **Settings**.</span></span>
5. <span data-ttu-id="0943f-120">Selecione a guia **Avançado** .</span><span class="sxs-lookup"><span data-stu-id="0943f-120">Select the **Advanced** tab.</span></span>
6. <span data-ttu-id="0943f-121">Na seção **Memória virtual**, selecione **Alterar**.</span><span class="sxs-lookup"><span data-stu-id="0943f-121">In the **Virtual memory** section, select **Change**.</span></span>
7. <span data-ttu-id="0943f-122">Selecione a unidade **C**, em seguida, clique em **Tamanho gerenciado pelo sistema** e clique em **Definir**.</span><span class="sxs-lookup"><span data-stu-id="0943f-122">Select the **C** drive and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="0943f-123">Selecione a unidade **C**, em seguida, clique em **Nenhum arquivo de paginação** e clique em **Definir**.</span><span class="sxs-lookup"><span data-stu-id="0943f-123">Select the **D** drive and then click **No paging file** and then click **Set**.</span></span>
9. <span data-ttu-id="0943f-124">Clique em Aplicar.</span><span class="sxs-lookup"><span data-stu-id="0943f-124">Click Apply.</span></span> <span data-ttu-id="0943f-125">Você receberá um aviso de que o computador precisa ser reiniciado para que as alterações entrem em vigor.</span><span class="sxs-lookup"><span data-stu-id="0943f-125">You will get a warning that the computer needs to be restarted for the changes to take affect.</span></span>
10. <span data-ttu-id="0943f-126">Reinicie a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0943f-126">Restart the virtual machine.</span></span>

## <a name="change-the-drive-letters"></a><span data-ttu-id="0943f-127">Alterar a letra da unidade</span><span class="sxs-lookup"><span data-stu-id="0943f-127">Change the drive letters</span></span>
1. <span data-ttu-id="0943f-128">Depois que a VM for reiniciada, faça logon novamente na VM.</span><span class="sxs-lookup"><span data-stu-id="0943f-128">Once the VM restarts, log back on to the VM.</span></span>
2. <span data-ttu-id="0943f-129">Clique no menu **Iniciar**, digite **diskmgmt.msc** e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="0943f-129">Click the **Start** menu and type **diskmgmt.msc** and hit Enter.</span></span> <span data-ttu-id="0943f-130">O Gerenciamento de Disco será iniciado.</span><span class="sxs-lookup"><span data-stu-id="0943f-130">Disk Management will start.</span></span>
3. <span data-ttu-id="0943f-131">Clique com o botão direito do mouse em **D**, a unidade de Armazenamento Temporário e selecione **Alterar Letra da Unidade e Caminhos**.</span><span class="sxs-lookup"><span data-stu-id="0943f-131">Right-click on **D**, the Temporary Storage drive, and select **Change Drive Letter and Paths**.</span></span>
4. <span data-ttu-id="0943f-132">Na Letra da unidade, selecione uma nova unidade como, por exemplo, **T** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="0943f-132">Under Drive letter, select a new drive such as **T** and then click **OK**.</span></span> 
5. <span data-ttu-id="0943f-133">Clique com o botão direito do mouse no disco de dados e selecione **Alterar Letra da Unidade e Caminhos**.</span><span class="sxs-lookup"><span data-stu-id="0943f-133">Right-click on the data disk, and select **Change Drive Letter and Paths**.</span></span>
6. <span data-ttu-id="0943f-134">Na Letra da unidade, selecione a unidade **D** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="0943f-134">Under Drive letter, select drive **D** and then click **OK**.</span></span> 

## <a name="move-pagefilesys-back-to-the-temporary-storage-drive"></a><span data-ttu-id="0943f-135">Mova o pagefile.sys de volta para a unidade de armazenamento temporário</span><span class="sxs-lookup"><span data-stu-id="0943f-135">Move pagefile.sys back to the temporary storage drive</span></span>
1. <span data-ttu-id="0943f-136">Clique com o botão direito do mouse no menu **Iniciar** e selecione **Sistema**</span><span class="sxs-lookup"><span data-stu-id="0943f-136">Right-click the **Start** menu and select **System**</span></span>
2. <span data-ttu-id="0943f-137">No menu à esquerda, selecione **Configurações avançadas do sistema**.</span><span class="sxs-lookup"><span data-stu-id="0943f-137">In the left-hand menu, select **Advanced system settings**.</span></span>
3. <span data-ttu-id="0943f-138">Na seção **Desempenho**, selecione **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="0943f-138">In the **Performance** section, select **Settings**.</span></span>
4. <span data-ttu-id="0943f-139">Selecione a guia **Avançado** .</span><span class="sxs-lookup"><span data-stu-id="0943f-139">Select the **Advanced** tab.</span></span>
5. <span data-ttu-id="0943f-140">Na seção **Memória virtual**, selecione **Alterar**.</span><span class="sxs-lookup"><span data-stu-id="0943f-140">In the **Virtual memory** section, select **Change**.</span></span>
6. <span data-ttu-id="0943f-141">Selecione a unidade **C** do SO, em seguida, clique em **Nenhum arquivo de paginação** e clique em **Definir**.</span><span class="sxs-lookup"><span data-stu-id="0943f-141">Select the OS drive **C** and click **No paging file** and then click **Set**.</span></span>
7. <span data-ttu-id="0943f-142">Selecione a unidade **T** de armazenamento temporário, em seguida, clique em **Tamanho gerenciado pelo sistema** e clique em **Definir**.</span><span class="sxs-lookup"><span data-stu-id="0943f-142">Select the temporary storage drive **T** and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="0943f-143">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="0943f-143">Click **Apply**.</span></span> <span data-ttu-id="0943f-144">Você receberá um aviso de que o computador precisa ser reiniciado para que as alterações entrem em vigor.</span><span class="sxs-lookup"><span data-stu-id="0943f-144">You will get a warning that the computer needs to be restarted for the changes to take affect.</span></span>
9. <span data-ttu-id="0943f-145">Reinicie a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0943f-145">Restart the virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0943f-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0943f-146">Next steps</span></span>
* <span data-ttu-id="0943f-147">É possível aumentar o armazenamento disponível para sua máquina virtual [anexando um disco de dados adicional](attach-managed-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0943f-147">You can increase the storage available to your virtual machine by [attaching a additional data disk](attach-managed-disk-portal.md).</span></span>

