---
title: "Verifique Olá unidade d: de uma VM de um disco de dados | Microsoft Docs"
description: "Descreve como toochange letras das unidades para uma VM do Windows para que você pode usar a unidade d: de saudação como uma unidade de dados."
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
ms.openlocfilehash: 43939da1a890ac4049266487951e3889aa0ed9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-d-drive-as-a-data-drive-on-a-windows-vm"></a><span data-ttu-id="a4a08-103">Use a unidade d: de saudação como uma unidade de dados em uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="a4a08-103">Use hello D: drive as a data drive on a Windows VM</span></span>
<span data-ttu-id="a4a08-104">Se seu aplicativo precisa toouse Olá dados toostore unidade, siga essas instruções toouse outra letra de unidade de disco temporário hello.</span><span class="sxs-lookup"><span data-stu-id="a4a08-104">If your application needs toouse hello D drive toostore data, follow these instructions toouse a different drive letter for hello temporary disk.</span></span> <span data-ttu-id="a4a08-105">Nunca use Olá disco temporário toostore os dados que você precisa tookeep.</span><span class="sxs-lookup"><span data-stu-id="a4a08-105">Never use hello temporary disk toostore data that you need tookeep.</span></span>

<span data-ttu-id="a4a08-106">Se você redimensionar ou **parar (desalocar)** uma máquina virtual, isso pode disparar o posicionamento de máquina virtual de saudação tooa hipervisor novo.</span><span class="sxs-lookup"><span data-stu-id="a4a08-106">If you resize or **Stop (Deallocate)** a virtual machine, this may trigger placement of hello virtual machine tooa new hypervisor.</span></span> <span data-ttu-id="a4a08-107">Um evento de manutenção planejada ou não planejada também pode disparar esse posicionamento.</span><span class="sxs-lookup"><span data-stu-id="a4a08-107">A planned or unplanned maintenance event may also trigger this placement.</span></span> <span data-ttu-id="a4a08-108">Nesse cenário, o disco temporário Olá será toohello reatribuídos a primeira letra de unidade disponível.</span><span class="sxs-lookup"><span data-stu-id="a4a08-108">In this scenario, hello temporary disk will be reassigned toohello first available drive letter.</span></span> <span data-ttu-id="a4a08-109">Se você tiver um aplicativo que requer especificamente d:. hello, você precisa toofollow essas etapas tootemporarily mover Olá pagefile.sys, anexar um novo disco de dados e atribuir-lhe Olá letra D e, em seguida, mover Olá pagefile.sys unidade temporária toohello de volta.</span><span class="sxs-lookup"><span data-stu-id="a4a08-109">If you have an application that specifically requires hello D: drive, you need toofollow these steps tootemporarily move hello pagefile.sys, attach a new data disk and assign it hello letter D and then move hello pagefile.sys back toohello temporary drive.</span></span> <span data-ttu-id="a4a08-110">Uma vez concluído, Azure não terão volta Olá d: se Olá VM move hipervisor diferentes tooa.</span><span class="sxs-lookup"><span data-stu-id="a4a08-110">Once complete, Azure will not take back hello D: if hello VM moves tooa different hypervisor.</span></span>

<span data-ttu-id="a4a08-111">Para obter mais informações sobre como o Azure usa o disco temporário hello, consulte [Noções básicas sobre unidades temporárias de saudação em máquinas virtuais do Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="a4a08-111">For more information about how Azure uses hello temporary disk, see [Understanding hello temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>

## <a name="attach-hello-data-disk"></a><span data-ttu-id="a4a08-112">Anexar disco de dados Olá</span><span class="sxs-lookup"><span data-stu-id="a4a08-112">Attach hello data disk</span></span>
<span data-ttu-id="a4a08-113">Primeiro, você precisará tooattach Olá dados disco toohello VM.</span><span class="sxs-lookup"><span data-stu-id="a4a08-113">First, you'll need tooattach hello data disk toohello virtual machine.</span></span> <span data-ttu-id="a4a08-114">toodo este usando o portal de hello, consulte [como tooattach um dados gerenciados de disco no portal do Azure de saudação](attach-managed-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a4a08-114">toodo this using hello portal, see [How tooattach a managed data disk in hello Azure portal](attach-managed-disk-portal.md).</span></span>

## <a name="temporarily-move-pagefilesys-tooc-drive"></a><span data-ttu-id="a4a08-115">Mover temporariamente pagefile.sys tooC unidade</span><span class="sxs-lookup"><span data-stu-id="a4a08-115">Temporarily move pagefile.sys tooC drive</span></span>
1. <span data-ttu-id="a4a08-116">Conecte-se a máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="a4a08-116">Connect toohello virtual machine.</span></span> 
2. <span data-ttu-id="a4a08-117">Saudação de atalho **iniciar** menu e selecione **sistema**.</span><span class="sxs-lookup"><span data-stu-id="a4a08-117">Right-click hello **Start** menu and select **System**.</span></span>
3. <span data-ttu-id="a4a08-118">No menu à esquerda do hello, selecione **configurações avançadas do sistema**.</span><span class="sxs-lookup"><span data-stu-id="a4a08-118">In hello left-hand menu, select **Advanced system settings**.</span></span>
4. <span data-ttu-id="a4a08-119">Em Olá **desempenho** seção, selecione **configurações**.</span><span class="sxs-lookup"><span data-stu-id="a4a08-119">In hello **Performance** section, select **Settings**.</span></span>
5. <span data-ttu-id="a4a08-120">Selecione Olá **avançado** guia.</span><span class="sxs-lookup"><span data-stu-id="a4a08-120">Select hello **Advanced** tab.</span></span>
6. <span data-ttu-id="a4a08-121">Em Olá **Memória Virtual** seção, selecione **alteração**.</span><span class="sxs-lookup"><span data-stu-id="a4a08-121">In hello **Virtual memory** section, select **Change**.</span></span>
7. <span data-ttu-id="a4a08-122">Selecione Olá **C** unidade e, em seguida, clique em **Tamanho gerenciado pelo sistema** e, em seguida, clique em **definir**.</span><span class="sxs-lookup"><span data-stu-id="a4a08-122">Select hello **C** drive and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="a4a08-123">Selecione Olá **D** unidade e, em seguida, clique em **nenhum arquivo de paginação** e, em seguida, clique em **definir**.</span><span class="sxs-lookup"><span data-stu-id="a4a08-123">Select hello **D** drive and then click **No paging file** and then click **Set**.</span></span>
9. <span data-ttu-id="a4a08-124">Clique em Aplicar.</span><span class="sxs-lookup"><span data-stu-id="a4a08-124">Click Apply.</span></span> <span data-ttu-id="a4a08-125">Você receberá um aviso que computador Olá precisa toobe reiniciado para Olá alterações tootake efeito.</span><span class="sxs-lookup"><span data-stu-id="a4a08-125">You will get a warning that hello computer needs toobe restarted for hello changes tootake affect.</span></span>
10. <span data-ttu-id="a4a08-126">Reinicie a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4a08-126">Restart hello virtual machine.</span></span>

## <a name="change-hello-drive-letters"></a><span data-ttu-id="a4a08-127">Alterar Olá letras de unidade</span><span class="sxs-lookup"><span data-stu-id="a4a08-127">Change hello drive letters</span></span>
1. <span data-ttu-id="a4a08-128">Uma vez Olá VM reiniciar, faça logon novamente toohello VM.</span><span class="sxs-lookup"><span data-stu-id="a4a08-128">Once hello VM restarts, log back on toohello VM.</span></span>
2. <span data-ttu-id="a4a08-129">Clique em Olá **iniciar** menu e tipo **diskmgmt.msc** e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="a4a08-129">Click hello **Start** menu and type **diskmgmt.msc** and hit Enter.</span></span> <span data-ttu-id="a4a08-130">O Gerenciamento de Disco será iniciado.</span><span class="sxs-lookup"><span data-stu-id="a4a08-130">Disk Management will start.</span></span>
3. <span data-ttu-id="a4a08-131">Clique duas vezes em **D**, Olá unidade de armazenamento temporário e selecione **alterar a letra da unidade e caminhos**.</span><span class="sxs-lookup"><span data-stu-id="a4a08-131">Right-click on **D**, hello Temporary Storage drive, and select **Change Drive Letter and Paths**.</span></span>
4. <span data-ttu-id="a4a08-132">Na Letra da unidade, selecione uma nova unidade como, por exemplo, **T** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a4a08-132">Under Drive letter, select a new drive such as **T** and then click **OK**.</span></span> 
5. <span data-ttu-id="a4a08-133">Clique com botão direito no disco de dados hello e selecione **alterar a letra da unidade e caminhos**.</span><span class="sxs-lookup"><span data-stu-id="a4a08-133">Right-click on hello data disk, and select **Change Drive Letter and Paths**.</span></span>
6. <span data-ttu-id="a4a08-134">Na Letra da unidade, selecione a unidade **D** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a4a08-134">Under Drive letter, select drive **D** and then click **OK**.</span></span> 

## <a name="move-pagefilesys-back-toohello-temporary-storage-drive"></a><span data-ttu-id="a4a08-135">Mova pagefile.sys unidade de armazenamento temporário de toohello back</span><span class="sxs-lookup"><span data-stu-id="a4a08-135">Move pagefile.sys back toohello temporary storage drive</span></span>
1. <span data-ttu-id="a4a08-136">Saudação de atalho **iniciar** menu e selecione **sistema**</span><span class="sxs-lookup"><span data-stu-id="a4a08-136">Right-click hello **Start** menu and select **System**</span></span>
2. <span data-ttu-id="a4a08-137">No menu à esquerda do hello, selecione **configurações avançadas do sistema**.</span><span class="sxs-lookup"><span data-stu-id="a4a08-137">In hello left-hand menu, select **Advanced system settings**.</span></span>
3. <span data-ttu-id="a4a08-138">Em Olá **desempenho** seção, selecione **configurações**.</span><span class="sxs-lookup"><span data-stu-id="a4a08-138">In hello **Performance** section, select **Settings**.</span></span>
4. <span data-ttu-id="a4a08-139">Selecione Olá **avançado** guia.</span><span class="sxs-lookup"><span data-stu-id="a4a08-139">Select hello **Advanced** tab.</span></span>
5. <span data-ttu-id="a4a08-140">Em Olá **Memória Virtual** seção, selecione **alteração**.</span><span class="sxs-lookup"><span data-stu-id="a4a08-140">In hello **Virtual memory** section, select **Change**.</span></span>
6. <span data-ttu-id="a4a08-141">Selecione unidade Olá SO **C** e clique em **nenhum arquivo de paginação** e, em seguida, clique em **definir**.</span><span class="sxs-lookup"><span data-stu-id="a4a08-141">Select hello OS drive **C** and click **No paging file** and then click **Set**.</span></span>
7. <span data-ttu-id="a4a08-142">Selecione a unidade de armazenamento temporário de saudação **T** e, em seguida, clique em **Tamanho gerenciado pelo sistema** e, em seguida, clique em **definir**.</span><span class="sxs-lookup"><span data-stu-id="a4a08-142">Select hello temporary storage drive **T** and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="a4a08-143">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="a4a08-143">Click **Apply**.</span></span> <span data-ttu-id="a4a08-144">Você receberá um aviso que computador Olá precisa toobe reiniciado para Olá alterações tootake efeito.</span><span class="sxs-lookup"><span data-stu-id="a4a08-144">You will get a warning that hello computer needs toobe restarted for hello changes tootake affect.</span></span>
9. <span data-ttu-id="a4a08-145">Reinicie a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4a08-145">Restart hello virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4a08-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a4a08-146">Next steps</span></span>
* <span data-ttu-id="a4a08-147">Você pode aumentar Olá armazenamento disponível tooyour máquina virtual [anexar um disco de dados adicionais](attach-managed-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a4a08-147">You can increase hello storage available tooyour virtual machine by [attaching a additional data disk](attach-managed-disk-portal.md).</span></span>

