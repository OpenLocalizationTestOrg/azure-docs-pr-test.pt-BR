---
title: "excluindo contas de armazenamento do Azure, contêineres ou VHDs em uma implantação clássica de aaaTroubleshoot | Microsoft Docs"
description: "Solucionar problemas ao excluir contas de armazenamento, contêineres ou VHDs do Azure em uma implantação clássica"
services: storage
documentationcenter: 
author: genlin
manager: felixwu
editor: tysonn
tags: storage
ms.assetid: 0f7a8243-d8dc-432a-9d37-1272a0cb3a5c
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 6bbfa032e1968718c623227bb426d553e2951075
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a><span data-ttu-id="39895-103">Solucionar problemas ao excluir contas de armazenamento, contêineres ou VHDs do Azure em uma implantação clássica</span><span class="sxs-lookup"><span data-stu-id="39895-103">Troubleshoot deleting Azure storage accounts, containers, or VHDs in a classic deployment</span></span>
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

<span data-ttu-id="39895-104">Você poderá receber erros ao tentar conta de armazenamento do Azure toodelete hello, contêiner ou VHD no hello [portal do Azure](https://portal.azure.com/) ou hello [portal clássico do Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="39895-104">You might receive errors when you try toodelete hello Azure storage account, container, or VHD in hello [Azure portal](https://portal.azure.com/) or hello [Azure classic portal](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="39895-105">problemas de saudação podem ser causados por Olá circunstâncias a seguir:</span><span class="sxs-lookup"><span data-stu-id="39895-105">hello issues can be caused by hello following circumstances:</span></span>

* <span data-ttu-id="39895-106">Quando você exclui uma VM, disco hello e VHD não são automaticamente excluídos.</span><span class="sxs-lookup"><span data-stu-id="39895-106">When you delete a VM, hello disk and VHD are not automatically deleted.</span></span> <span data-ttu-id="39895-107">Que pode ser motivo Olá Falha na exclusão da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="39895-107">That might be hello reason for failure on storage account deletion.</span></span> <span data-ttu-id="39895-108">Nós não exclua o disco Olá para que você possa usar Olá disco toomount outra VM.</span><span class="sxs-lookup"><span data-stu-id="39895-108">We don't delete hello disk so that you can use hello disk toomount another VM.</span></span>
* <span data-ttu-id="39895-109">Ainda há uma concessão em um blob de disco ou hello associada com o disco de saudação.</span><span class="sxs-lookup"><span data-stu-id="39895-109">There is still a lease on a disk or hello blob that's associated with hello disk.</span></span>
* <span data-ttu-id="39895-110">Ainda há uma imagem de VM que está usando uma conta de armazenamento, contêiner ou blob.</span><span class="sxs-lookup"><span data-stu-id="39895-110">There is still a VM image that is using a blob, container, or storage account.</span></span>

<span data-ttu-id="39895-111">Se o problema do Azure não é abordado neste artigo, visite Olá fóruns do Azure em [MSDN e Olá estouro de pilha](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="39895-111">If your Azure issue is not addressed in this article, visit hello Azure forums on [MSDN and hello Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="39895-112">Você pode lançar seu problema nesses fóruns ou too@AzureSupport no Twitter.</span><span class="sxs-lookup"><span data-stu-id="39895-112">You can post your issue on these forums or too@AzureSupport on Twitter.</span></span> <span data-ttu-id="39895-113">Além disso, você pode emitir uma solicitação de suporte do Azure, selecionando **obter suporte** em Olá [suporte do Azure](https://azure.microsoft.com/support/options/) site.</span><span class="sxs-lookup"><span data-stu-id="39895-113">Also, you can file an Azure support request by selecting **Get support** on hello [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="39895-114">Sintomas</span><span class="sxs-lookup"><span data-stu-id="39895-114">Symptoms</span></span>
<span data-ttu-id="39895-115">Olá seção a seguir lista os erros comuns que podem ser exibidas ao tentar contas de armazenamento do Azure toodelete hello, contêineres ou VHDs.</span><span class="sxs-lookup"><span data-stu-id="39895-115">hello following section lists common errors that you might receive when you try toodelete hello Azure storage accounts, containers, or VHDs.</span></span>

### <a name="scenario-1-unable-toodelete-a-storage-account"></a><span data-ttu-id="39895-116">Cenário 1: Não é possível toodelete uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="39895-116">Scenario 1: Unable toodelete a storage account</span></span>
<span data-ttu-id="39895-117">Quando você navega toohello conta de armazenamento clássicas Olá [portal do Azure](https://portal.azure.com/) e selecione **excluir**, pode ser apresentada uma lista de objetos que estão impedindo a exclusão da conta de armazenamento hello:</span><span class="sxs-lookup"><span data-stu-id="39895-117">When you navigate toohello classic storage account in hello [Azure portal](https://portal.azure.com/) and select **Delete**, you may be presented with a list of objects that are preventing deletion of hello storage account:</span></span>

  ![Imagem de erro ao excluir conta de armazenamento Olá](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

<span data-ttu-id="39895-119">Quando você navega a conta de armazenamento toohello Olá [portal clássico do Azure](https://manage.windowsazure.com/) e selecione **excluir**, você poderá ver um Olá os erros a seguir:</span><span class="sxs-lookup"><span data-stu-id="39895-119">When you navigate toohello storage account in hello [Azure classic portal](https://manage.windowsazure.com/) and select **Delete**, you might see one of hello following errors:</span></span>

- <span data-ttu-id="39895-120">*A conta de armazenamento StorageAccountName contém imagens de VM. Assegure-se de que essas imagens de VM sejam removidas antes de excluir essa conta de armazenamento.*</span><span class="sxs-lookup"><span data-stu-id="39895-120">*Storage account StorageAccountName contains VM Images. Ensure these VM Images are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="39895-121">*Falha na conta de armazenamento toodelete < vm-armazenamento-account-name >. Conta de armazenamento não é possível toodelete < vm-armazenamento-account-name >: ' < vm-armazenamento-account-name > de conta de armazenamento tem algumas imagens de ativas e/ou discos. Garanta que esses discos e/ou essas imagens sejam removidos antes de excluir essa conta de armazenamento.'*.</span><span class="sxs-lookup"><span data-stu-id="39895-121">*Failed toodelete storage account <vm-storage-account-name>. Unable toodelete storage account <vm-storage-account-name>: 'Storage account <vm-storage-account-name> has some active image(s) and/or disk(s). Ensure these image(s) and/or disk(s) are removed before deleting this storage account.'.*</span></span>

- <span data-ttu-id="39895-122">*A conta de armazenamento <vm-storage-account-name> tem algumas imagens e/ou discos ativos, por exemplo, xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Garanta que esses discos e/ou essas imagens sejam removidos antes de excluir essa conta de armazenamento.*</span><span class="sxs-lookup"><span data-stu-id="39895-122">*Storage account <vm-storage-account-name> has some active image(s) and/or disk(s), e.g. xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Ensure these image(s) and/or disk(s) are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="39895-123">*A conta de armazenamento <vm-storage-account-name> tem um contêiner com artefatos de imagens e/ou discos ativos. Certifique-se de que esses artefatos são removidos do repositório de imagens de saudação antes de excluir esta conta de armazenamento*.</span><span class="sxs-lookup"><span data-stu-id="39895-123">*Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from hello image repository before deleting this storage account*.</span></span>

- <span data-ttu-id="39895-124">*A conta de armazenamento com falha no envio <vm-storage-account-name> tem um contêiner com artefatos de imagens e/ou discos ativos. Certifique-se de que esses artefatos são removidos do repositório de imagens de saudação antes de excluir esta conta de armazenamento. Quando você tentar toodelete uma conta de armazenamento e houver discos ainda estão ativos associados a ele, você verá uma mensagem indicando que há discos ativos que precisem toobe excluído*.</span><span class="sxs-lookup"><span data-stu-id="39895-124">*Submit Failed Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from hello image repository before deleting this storage account. When you attempt toodelete a storage account and there are still active disks associated with it, you will see a message telling you there are active disks that need toobe deleted*.</span></span>

### <a name="scenario-2-unable-toodelete-a-container"></a><span data-ttu-id="39895-125">Cenário 2: Não é possível toodelete um contêiner</span><span class="sxs-lookup"><span data-stu-id="39895-125">Scenario 2: Unable toodelete a container</span></span>
<span data-ttu-id="39895-126">Quando você tenta toodelete contêiner de armazenamento de saudação, você poderá ver Olá erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="39895-126">When you try toodelete hello storage container, you might see hello following error:</span></span>

<span data-ttu-id="39895-127">*Contêiner de armazenamento com falha toodelete <container name>. Erro: ' atualmente há uma concessão no contêiner de saudação e nenhuma ID de concessão foi especificada na solicitação Olá*.</span><span class="sxs-lookup"><span data-stu-id="39895-127">*Failed toodelete storage container <container name>. Error: 'There is currently a lease on hello container and no lease ID was specified in hello request*.</span></span>

<span data-ttu-id="39895-128">Ou</span><span class="sxs-lookup"><span data-stu-id="39895-128">Or</span></span>

<span data-ttu-id="39895-129">*Olá seguintes discos da máquina virtual usa blobs nesse contêiner, portanto, Olá contêiner não pode ser excluído: VirtualMachineDiskName1, VirtualMachineDiskName2,...*</span><span class="sxs-lookup"><span data-stu-id="39895-129">*hello following virtual machine disks use blobs in this container, so hello container cannot be deleted: VirtualMachineDiskName1, VirtualMachineDiskName2, ...*</span></span>

### <a name="scenario-3-unable-toodelete-a-vhd"></a><span data-ttu-id="39895-130">Cenário 3: Não é possível toodelete um VHD</span><span class="sxs-lookup"><span data-stu-id="39895-130">Scenario 3: Unable toodelete a VHD</span></span>
<span data-ttu-id="39895-131">Depois que você excluir uma máquina virtual e, em seguida, tente toodelete Olá blobs para Olá associados VHDs, você poderá receber a seguinte mensagem de saudação:</span><span class="sxs-lookup"><span data-stu-id="39895-131">After you delete a VM and then try toodelete hello blobs for hello associated VHDs, you might receive hello following message:</span></span>

<span data-ttu-id="39895-132">*Blob toodelete com falha ' caminho/XXXXXX-XXXXXX-os-1447379084699.vhd'. Erro: ' atualmente há uma concessão no blob hello e nenhuma ID de concessão foi especificada na solicitação de saudação.*</span><span class="sxs-lookup"><span data-stu-id="39895-132">*Failed toodelete blob 'path/XXXXXX-XXXXXX-os-1447379084699.vhd'. Error: 'There is currently a lease on hello blob and no lease ID was specified in hello request.*</span></span>

<span data-ttu-id="39895-133">Ou</span><span class="sxs-lookup"><span data-stu-id="39895-133">Or</span></span>

<span data-ttu-id="39895-134">*Blob 'BlobName.vhd' está em uso como disco da máquina virtual 'VirtualMachineDiskName' blob Olá não pode ser excluído.*</span><span class="sxs-lookup"><span data-stu-id="39895-134">*Blob 'BlobName.vhd' is in use as virtual machine disk 'VirtualMachineDiskName', so hello blob cannot be deleted.*</span></span>

## <a name="solution"></a><span data-ttu-id="39895-135">Solução</span><span class="sxs-lookup"><span data-stu-id="39895-135">Solution</span></span>
<span data-ttu-id="39895-136">problemas mais comuns do tooresolve hello, tente Olá método a seguir:</span><span class="sxs-lookup"><span data-stu-id="39895-136">tooresolve hello most common issues, try hello following method:</span></span>

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-hello-storage-account-container-or-vhd"></a><span data-ttu-id="39895-137">Etapa 1: Excluir todos os discos que estão impedindo a exclusão da conta de armazenamento hello, contêiner ou VHD</span><span class="sxs-lookup"><span data-stu-id="39895-137">Step 1: Delete any disks that are preventing deletion of hello storage account, container, or VHD</span></span>
1. <span data-ttu-id="39895-138">Alternar toohello [portal clássico do Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="39895-138">Switch toohello [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="39895-139">Selecione **MÁQUINA VIRTUAL** > **DISCOS**.</span><span class="sxs-lookup"><span data-stu-id="39895-139">Select **VIRTUAL MACHINE** > **DISKS**.</span></span>

    ![Imagem de discos em máquinas virtuais no portal clássico do Azure.](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. <span data-ttu-id="39895-141">Localize discos Olá associados à conta de armazenamento hello, contêiner ou VHD que você deseja toodelete.</span><span class="sxs-lookup"><span data-stu-id="39895-141">Locate hello disks that are associated with hello storage account, container, or VHD that you want toodelete.</span></span> <span data-ttu-id="39895-142">Quando você verificar o local de saudação do disco hello, você encontrará Olá associados a conta de armazenamento, contêiner ou VHD.</span><span class="sxs-lookup"><span data-stu-id="39895-142">When you check hello location of hello disk, you will find hello associated storage account, container, or VHD.</span></span>

    ![Imagem que mostra informações sobre o local para os discos no portal clássico do Azure](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. <span data-ttu-id="39895-144">Exclua discos hello usando um dos métodos a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="39895-144">Delete hello disks by using one of hello following methods:</span></span>

  - <span data-ttu-id="39895-145">Se não houver nenhuma VM listadas no hello **conectado a** campo disco hello, você pode excluir disco Olá diretamente.</span><span class="sxs-lookup"><span data-stu-id="39895-145">If  there is no VM listed on hello **Attached To** field of hello disk, you can delete hello disk directly.</span></span>

  - <span data-ttu-id="39895-146">Se o disco de saudação é um disco de dados, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="39895-146">If hello disk is a data disk, follow these steps:</span></span>

    1. <span data-ttu-id="39895-147">Verifique o nome de saudação do hello VM Olá disco está anexado ao.</span><span class="sxs-lookup"><span data-stu-id="39895-147">Check hello name of hello VM that hello disk is attached to.</span></span>
    2. <span data-ttu-id="39895-148">Vá muito**máquinas virtuais** > **instâncias**e, em seguida, localize Olá VM.</span><span class="sxs-lookup"><span data-stu-id="39895-148">Go too**Virtual Machines** > **Instances**, and then locate hello VM.</span></span>
    3. <span data-ttu-id="39895-149">Certifique-se de que nada está usando ativamente disco hello.</span><span class="sxs-lookup"><span data-stu-id="39895-149">Make sure that nothing is actively using hello disk.</span></span>
    4. <span data-ttu-id="39895-150">Selecione **desanexar disco** na parte inferior de saudação do disco de saudação do hello toodetach portal.</span><span class="sxs-lookup"><span data-stu-id="39895-150">Select **Detach Disk** at hello bottom of hello portal toodetach hello disk.</span></span>
    5. <span data-ttu-id="39895-151">Vá muito**máquinas virtuais** > **discos**e aguarde Olá **conectado a** tooturn de campo em branco.</span><span class="sxs-lookup"><span data-stu-id="39895-151">Go too**Virtual Machines** > **Disks**, and wait for hello **Attached To** field tooturn blank.</span></span> <span data-ttu-id="39895-152">Isso indica que o disco Olá foi desanexado com êxito da saudação VM.</span><span class="sxs-lookup"><span data-stu-id="39895-152">This indicates hello disk has successfully detached from hello VM.</span></span>
    6. <span data-ttu-id="39895-153">Selecione **excluir** na parte inferior de saudação do **máquinas virtuais** > **discos** toodelete disco de saudação.</span><span class="sxs-lookup"><span data-stu-id="39895-153">Select **Delete** at hello bottom of **Virtual Machines** > **Disks** toodelete hello disk.</span></span>

  - <span data-ttu-id="39895-154">Se o disco Olá é um disco do sistema operacional (Olá **contém OS** campo tem um valor como Windows) e tooa anexado VMs, siga estas etapas toodelete Olá VM.</span><span class="sxs-lookup"><span data-stu-id="39895-154">If hello disk is an OS disk (hello **Contains OS** field has a value like Windows) and attached tooa VM, follow these steps toodelete hello VM.</span></span> <span data-ttu-id="39895-155">não é possível desanexar o disco do sistema operacional Olá para que tenhamos concessão de saudação do toodelete Olá VM toorelease.</span><span class="sxs-lookup"><span data-stu-id="39895-155">hello OS disk cannot be detached, so we have toodelete hello VM toorelease hello lease.</span></span>

    1. <span data-ttu-id="39895-156">Verifique o nome da máquina Virtual de Olá Olá A que disco de dados está anexado hello.</span><span class="sxs-lookup"><span data-stu-id="39895-156">Check hello name of hello Virtual Machine hello Data Disk is attached to.</span></span>  
    2. <span data-ttu-id="39895-157">Vá muito**máquinas virtuais** > **instâncias**, e, em seguida, selecione Olá VM Olá disco está associada.</span><span class="sxs-lookup"><span data-stu-id="39895-157">Go too**Virtual Machines** > **Instances**, and then select hello VM that hello disk is attached to.</span></span>
    3. <span data-ttu-id="39895-158">Certifique-se de que nada está usando ativamente Olá de máquina virtual, e que você não precisa Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="39895-158">Make sure that nothing is actively using hello virtual machine, and that you no longer need hello virtual machine.</span></span>
    4. <span data-ttu-id="39895-159">Selecione Olá VM Olá disco está anexado, em seguida, selecione **excluir** > **Delete Olá anexou discos**.</span><span class="sxs-lookup"><span data-stu-id="39895-159">Select hello VM hello disk is attached to, then select **Delete** > **Delete hello attached disks**.</span></span>
    5. <span data-ttu-id="39895-160">Vá muito**máquinas virtuais** > **discos**e aguarde Olá toodisappear de disco.</span><span class="sxs-lookup"><span data-stu-id="39895-160">Go too**Virtual Machines** > **Disks**, and wait for hello disk toodisappear.</span></span>  <span data-ttu-id="39895-161">Pode levar alguns minutos para que essa toooccur e página de saudação toorefresh talvez seja necessário.</span><span class="sxs-lookup"><span data-stu-id="39895-161">It may take a few minutes for this toooccur, and you may need toorefresh hello page.</span></span>
    6. <span data-ttu-id="39895-162">Se o disco de saudação não desaparecem, aguarde Olá **conectado a** tooturn de campo em branco.</span><span class="sxs-lookup"><span data-stu-id="39895-162">If hello disk does not disappear, wait for hello **Attached To** field tooturn blank.</span></span> <span data-ttu-id="39895-163">Isso indica que o disco Olá totalmente soltou de saudação VM.</span><span class="sxs-lookup"><span data-stu-id="39895-163">This indicates hello disk has fully detached from hello VM.</span></span>  <span data-ttu-id="39895-164">Em seguida, selecione o disco hello e selecione **excluir** na parte inferior de saudação do disco de Olá Olá página toodelete.</span><span class="sxs-lookup"><span data-stu-id="39895-164">Then, select hello disk, and select **Delete** at hello bottom of hello page toodelete hello disk.</span></span>


   > [!NOTE]
   > <span data-ttu-id="39895-165">Se um disco estiver anexado tooa VM, não será capaz de toodelete-lo.</span><span class="sxs-lookup"><span data-stu-id="39895-165">If a disk is attached tooa VM, you will not be able toodelete it.</span></span> <span data-ttu-id="39895-166">Discos são desconectados de uma VM excluída assincronamente.</span><span class="sxs-lookup"><span data-stu-id="39895-166">Disks are detached from a deleted VM asynchronously.</span></span> <span data-ttu-id="39895-167">Pode levar alguns minutos após Olá VM seja excluído para tooclear esse campo para cima.</span><span class="sxs-lookup"><span data-stu-id="39895-167">It might take a few minutes after hello VM is deleted for this field tooclear up.</span></span>
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-hello-storage-account-or-container"></a><span data-ttu-id="39895-168">Etapa 2: Excluir as imagens de VM que estão impedindo a exclusão da conta de armazenamento hello ou do contêiner</span><span class="sxs-lookup"><span data-stu-id="39895-168">Step 2: Delete any VM Images that are preventing deletion of hello storage account or container</span></span>
1. <span data-ttu-id="39895-169">Alternar toohello [portal clássico do Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="39895-169">Switch toohello [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="39895-170">Selecione **máquina VIRTUAL** > **imagens**e, em seguida, excluir imagens Olá associados à conta de armazenamento hello, contêiner ou VHD.</span><span class="sxs-lookup"><span data-stu-id="39895-170">Select **VIRTUAL MACHINE** > **IMAGES**, and then delete hello images that are associated with hello storage account, container, or VHD.</span></span>

    <span data-ttu-id="39895-171">Depois disso, tente conta de armazenamento toodelete hello, contêiner ou VHD novamente.</span><span class="sxs-lookup"><span data-stu-id="39895-171">After that, try toodelete hello storage account, container, or VHD again.</span></span>

> [!WARNING]
> <span data-ttu-id="39895-172">Ser tooback-se de que qualquer valor que você deseja toosave antes de excluir a conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="39895-172">Be sure tooback up anything you want toosave before you delete hello account.</span></span> <span data-ttu-id="39895-173">Quando você exclui um VHD, blob, tabela, fila ou arquivo, ele é permanentemente excluído.</span><span class="sxs-lookup"><span data-stu-id="39895-173">Once you delete a VHD, blob, table, queue, or file, it is permanently deleted.</span></span> <span data-ttu-id="39895-174">Certifique-se de que o recurso de saudação não está em uso.</span><span class="sxs-lookup"><span data-stu-id="39895-174">Ensure that hello resource is not in use.</span></span>
>
>

## <a name="about-hello-stopped-deallocated-status"></a><span data-ttu-id="39895-175">Sobre Olá status parado (desalocado)</span><span class="sxs-lookup"><span data-stu-id="39895-175">About hello Stopped (deallocated) status</span></span>
<span data-ttu-id="39895-176">Máquinas virtuais que foram criados no modelo de implantação clássico hello e que foram retidos terá Olá **parado (desalocado)** status em qualquer Olá [portal do Azure](https://portal.azure.com/) ou [portal clássico do Azure ](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="39895-176">VMs that were created in hello classic deployment model and that have been retained will have hello **Stopped (deallocated)** status on either hello [Azure portal](https://portal.azure.com/) or [Azure classic portal](https://manage.windowsazure.com/).</span></span>

<span data-ttu-id="39895-177">**Portal Clássico do Azure**:</span><span class="sxs-lookup"><span data-stu-id="39895-177">**Azure classic portal**:</span></span>

![Status Parado (Desalocado) para VMs no portal do Azure.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

<span data-ttu-id="39895-179">**Portal do Azure**:</span><span class="sxs-lookup"><span data-stu-id="39895-179">**Azure portal**:</span></span>

![Status Parado (desalocado) para VMs no portal clássico do Azure.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

<span data-ttu-id="39895-181">Um status "Parada (desalocada)" libera recursos do computador hello, como saudação da CPU, memória e rede.</span><span class="sxs-lookup"><span data-stu-id="39895-181">A "Stopped (deallocated)" status releases hello computer resources, such as hello CPU, memory, and network.</span></span> <span data-ttu-id="39895-182">No entanto, discos Hello, ainda são mantidos para que você pode rapidamente recriar Olá VM se necessário.</span><span class="sxs-lookup"><span data-stu-id="39895-182">hello disks, however, are still retained so that you can quickly re-create hello VM if necessary.</span></span> <span data-ttu-id="39895-183">Esses discos são criados sobre os VHDs cujos backups são feitos pelo armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="39895-183">These disks are created on top of VHDs, which are backed by Azure storage.</span></span> <span data-ttu-id="39895-184">conta de armazenamento Olá tem esses VHDs e discos de saudação têm concessões nesses VHDs.</span><span class="sxs-lookup"><span data-stu-id="39895-184">hello storage account has these VHDs, and hello disks have leases on those VHDs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39895-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="39895-185">Next steps</span></span>
* [<span data-ttu-id="39895-186">Excluir uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="39895-186">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
