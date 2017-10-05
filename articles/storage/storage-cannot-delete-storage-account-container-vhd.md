---
title: "Solucionar problemas ao excluir contas de armazenamento, contêineres ou VHDs do Azure em uma implantação clássica | Microsoft Docs"
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
ms.openlocfilehash: 9f3e824414ad6c1a0aba98a3d549ee63ddc7272f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a><span data-ttu-id="f984d-103">Solucionar problemas ao excluir contas de armazenamento, contêineres ou VHDs do Azure em uma implantação clássica</span><span class="sxs-lookup"><span data-stu-id="f984d-103">Troubleshoot deleting Azure storage accounts, containers, or VHDs in a classic deployment</span></span>
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

<span data-ttu-id="f984d-104">Você pode receber erros ao tentar excluir a conta de armazenamento, o contêiner ou o VHD do Azure no [portal do Azure](https://portal.azure.com/) ou no [portal clássico do Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="f984d-104">You might receive errors when you try to delete the Azure storage account, container, or VHD in the [Azure portal](https://portal.azure.com/) or the [Azure classic portal](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="f984d-105">Os problemas podem ser causados pelas seguintes circunstâncias:</span><span class="sxs-lookup"><span data-stu-id="f984d-105">The issues can be caused by the following circumstances:</span></span>

* <span data-ttu-id="f984d-106">Ao excluir uma VM, o disco e o VHD não são automaticamente excluídos.</span><span class="sxs-lookup"><span data-stu-id="f984d-106">When you delete a VM, the disk and VHD are not automatically deleted.</span></span> <span data-ttu-id="f984d-107">Esse pode ser o motivo da falha na exclusão da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f984d-107">That might be the reason for failure on storage account deletion.</span></span> <span data-ttu-id="f984d-108">Não excluímos o disco para que você possa usá-lo para montar outra VM.</span><span class="sxs-lookup"><span data-stu-id="f984d-108">We don't delete the disk so that you can use the disk to mount another VM.</span></span>
* <span data-ttu-id="f984d-109">Ainda há uma concessão em um disco ou o blob que está associado ao disco.</span><span class="sxs-lookup"><span data-stu-id="f984d-109">There is still a lease on a disk or the blob that's associated with the disk.</span></span>
* <span data-ttu-id="f984d-110">Ainda há uma imagem de VM que está usando uma conta de armazenamento, contêiner ou blob.</span><span class="sxs-lookup"><span data-stu-id="f984d-110">There is still a VM image that is using a blob, container, or storage account.</span></span>

<span data-ttu-id="f984d-111">Se o problema do Azure não for resolvido neste artigo, visite os fóruns do Azure no [MSDN e Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="f984d-111">If your Azure issue is not addressed in this article, visit the Azure forums on [MSDN and the Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="f984d-112">Você pode postar seu problema nesses fóruns ou usando @AzureSupport no Twitter.</span><span class="sxs-lookup"><span data-stu-id="f984d-112">You can post your issue on these forums or to @AzureSupport on Twitter.</span></span> <span data-ttu-id="f984d-113">Além disso, você pode registrar uma solicitação de suporte do Azure selecionando **Obter suporte** no site de [suporte do Azure](https://azure.microsoft.com/support/options/) .</span><span class="sxs-lookup"><span data-stu-id="f984d-113">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="f984d-114">Sintomas</span><span class="sxs-lookup"><span data-stu-id="f984d-114">Symptoms</span></span>
<span data-ttu-id="f984d-115">A seção a seguir lista erros comuns que você pode receber ao tentar excluir contas de armazenamento, contêineres ou VHDs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f984d-115">The following section lists common errors that you might receive when you try to delete the Azure storage accounts, containers, or VHDs.</span></span>

### <a name="scenario-1-unable-to-delete-a-storage-account"></a><span data-ttu-id="f984d-116">Cenário 1: Não é possível excluir uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f984d-116">Scenario 1: Unable to delete a storage account</span></span>
<span data-ttu-id="f984d-117">Quando você navega para a conta de armazenamento clássica no [Portal do Azure](https://portal.azure.com/) e seleciona **Excluir**, pode ser que seja exibida uma lista de objetos que estão impedindo a exclusão da conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="f984d-117">When you navigate to the classic storage account in the [Azure portal](https://portal.azure.com/) and select **Delete**, you may be presented with a list of objects that are preventing deletion of the storage account:</span></span>

  ![Imagem do erro ao excluir a conta de armazenamento](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

<span data-ttu-id="f984d-119">Ao navegar para a conta de armazenamento no [Portal Clássico do Azure](https://manage.windowsazure.com/) e selecionar **Excluir**, você pode ver um dos seguintes erros:</span><span class="sxs-lookup"><span data-stu-id="f984d-119">When you navigate to the storage account in the [Azure classic portal](https://manage.windowsazure.com/) and select **Delete**, you might see one of the following errors:</span></span>

- <span data-ttu-id="f984d-120">*A conta de armazenamento StorageAccountName contém imagens de VM. Assegure-se de que essas imagens de VM sejam removidas antes de excluir essa conta de armazenamento.*</span><span class="sxs-lookup"><span data-stu-id="f984d-120">*Storage account StorageAccountName contains VM Images. Ensure these VM Images are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="f984d-121">*Falha ao excluir a conta de armazenamento <vm-storage-account-name>. Não é possível excluir a conta de armazenamento <vm-storage-account-name>: a conta de armazenamento <vm-storage-account-name> tem algumas imagens e/ou discos ativos. Garanta que esses discos e/ou essas imagens sejam removidos antes de excluir essa conta de armazenamento.'*.</span><span class="sxs-lookup"><span data-stu-id="f984d-121">*Failed to delete storage account <vm-storage-account-name>. Unable to delete storage account <vm-storage-account-name>: 'Storage account <vm-storage-account-name> has some active image(s) and/or disk(s). Ensure these image(s) and/or disk(s) are removed before deleting this storage account.'.*</span></span>

- <span data-ttu-id="f984d-122">*A conta de armazenamento <vm-storage-account-name> tem algumas imagens e/ou discos ativos, por exemplo, xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Garanta que esses discos e/ou essas imagens sejam removidos antes de excluir essa conta de armazenamento.*</span><span class="sxs-lookup"><span data-stu-id="f984d-122">*Storage account <vm-storage-account-name> has some active image(s) and/or disk(s), e.g. xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Ensure these image(s) and/or disk(s) are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="f984d-123">*A conta de armazenamento <vm-storage-account-name> tem um contêiner com artefatos de imagens e/ou discos ativos. Garanta que esses artefatos sejam removidos do repositório de imagens antes de excluir essa conta de armazenamento*.</span><span class="sxs-lookup"><span data-stu-id="f984d-123">*Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from the image repository before deleting this storage account*.</span></span>

- <span data-ttu-id="f984d-124">*A conta de armazenamento com falha no envio <vm-storage-account-name> tem um contêiner com artefatos de imagens e/ou discos ativos. Garanta que esses artefatos sejam removidos do repositório de imagens antes de excluir essa conta de armazenamento. Quando você tentar excluir uma conta de armazenamento e ainda houver discos ativos associados a ela, uma mensagem informando que há discos ativos que precisam ser excluídos será exibida*.</span><span class="sxs-lookup"><span data-stu-id="f984d-124">*Submit Failed Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from the image repository before deleting this storage account. When you attempt to delete a storage account and there are still active disks associated with it, you will see a message telling you there are active disks that need to be deleted*.</span></span>

### <a name="scenario-2-unable-to-delete-a-container"></a><span data-ttu-id="f984d-125">Cenário 2: Não é possível excluir um contêiner</span><span class="sxs-lookup"><span data-stu-id="f984d-125">Scenario 2: Unable to delete a container</span></span>
<span data-ttu-id="f984d-126">Ao tentar excluir o contêiner de armazenamento, o seguinte erro poderá ser exibido:</span><span class="sxs-lookup"><span data-stu-id="f984d-126">When you try to delete the storage container, you might see the following error:</span></span>

<span data-ttu-id="f984d-127">*Falha ao excluir o contêiner de armazenamento <container name>. Erro: 'Atualmente, há uma concessão no contêiner e nenhuma ID de concessão foi especificada na solicitação*.</span><span class="sxs-lookup"><span data-stu-id="f984d-127">*Failed to delete storage container <container name>. Error: 'There is currently a lease on the container and no lease ID was specified in the request*.</span></span>

<span data-ttu-id="f984d-128">ou o</span><span class="sxs-lookup"><span data-stu-id="f984d-128">Or</span></span>

<span data-ttu-id="f984d-129">*Os seguintes discos da máquina virtual usam blobs nesse contêiner, portanto o contêiner não pode ser excluído: VirtualMachineDiskName1, VirtualMachineDiskName2, ...*</span><span class="sxs-lookup"><span data-stu-id="f984d-129">*The following virtual machine disks use blobs in this container, so the container cannot be deleted: VirtualMachineDiskName1, VirtualMachineDiskName2, ...*</span></span>

### <a name="scenario-3-unable-to-delete-a-vhd"></a><span data-ttu-id="f984d-130">Cenário 3: Não é possível excluir um VHD</span><span class="sxs-lookup"><span data-stu-id="f984d-130">Scenario 3: Unable to delete a VHD</span></span>
<span data-ttu-id="f984d-131">Depois de excluir uma VM e então tentar excluir os blobs para os VHDs associados, você pode receber a seguinte mensagem:</span><span class="sxs-lookup"><span data-stu-id="f984d-131">After you delete a VM and then try to delete the blobs for the associated VHDs, you might receive the following message:</span></span>

<span data-ttu-id="f984d-132">*Falha ao excluir o blob 'path/XXXXXX-XXXXXX-os-1447379084699.vhd'. Erro: 'Atualmente, há uma concessão no blob e nenhuma ID de concessão foi especificada na solicitação*.</span><span class="sxs-lookup"><span data-stu-id="f984d-132">*Failed to delete blob 'path/XXXXXX-XXXXXX-os-1447379084699.vhd'. Error: 'There is currently a lease on the blob and no lease ID was specified in the request.*</span></span>

<span data-ttu-id="f984d-133">Ou</span><span class="sxs-lookup"><span data-stu-id="f984d-133">Or</span></span>

<span data-ttu-id="f984d-134">*O blob 'BlobName.vhd' está em uso como o disco de máquina virtual 'VirtualMachineDiskName', portanto não é possível excluir o blob.*</span><span class="sxs-lookup"><span data-stu-id="f984d-134">*Blob 'BlobName.vhd' is in use as virtual machine disk 'VirtualMachineDiskName', so the blob cannot be deleted.*</span></span>

## <a name="solution"></a><span data-ttu-id="f984d-135">Solução</span><span class="sxs-lookup"><span data-stu-id="f984d-135">Solution</span></span>
<span data-ttu-id="f984d-136">Para resolver os problemas mais comuns, tente o seguinte método:</span><span class="sxs-lookup"><span data-stu-id="f984d-136">To resolve the most common issues, try the following method:</span></span>

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-the-storage-account-container-or-vhd"></a><span data-ttu-id="f984d-137">Etapa 1: Excluir os discos que estão impedindo a exclusão da conta de armazenamento, do contêiner ou do VHD</span><span class="sxs-lookup"><span data-stu-id="f984d-137">Step 1: Delete any disks that are preventing deletion of the storage account, container, or VHD</span></span>
1. <span data-ttu-id="f984d-138">Alterne para o [portal clássico do Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="f984d-138">Switch to the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="f984d-139">Selecione **MÁQUINA VIRTUAL** > **DISCOS**.</span><span class="sxs-lookup"><span data-stu-id="f984d-139">Select **VIRTUAL MACHINE** > **DISKS**.</span></span>

    ![Imagem de discos em máquinas virtuais no portal clássico do Azure.](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. <span data-ttu-id="f984d-141">Localize os discos associados à conta de armazenamento, ao contêiner ou ao VHD que você quer excluir.</span><span class="sxs-lookup"><span data-stu-id="f984d-141">Locate the disks that are associated with the storage account, container, or VHD that you want to delete.</span></span> <span data-ttu-id="f984d-142">Ao verificar o local do disco, você encontrará a conta de armazenamento, o contêiner ou o VHD associado.</span><span class="sxs-lookup"><span data-stu-id="f984d-142">When you check the location of the disk, you will find the associated storage account, container, or VHD.</span></span>

    ![Imagem que mostra informações sobre o local para os discos no portal clássico do Azure](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. <span data-ttu-id="f984d-144">Exclua os discos usando um dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="f984d-144">Delete the disks by using one of the following methods:</span></span>

  - <span data-ttu-id="f984d-145">Se não houver nenhuma VM listada no campo **Conectado a** do disco, você poderá excluir os discos diretamente.</span><span class="sxs-lookup"><span data-stu-id="f984d-145">If  there is no VM listed on the **Attached To** field of the disk, you can delete the disk directly.</span></span>

  - <span data-ttu-id="f984d-146">Se o disco for um disco de dados, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="f984d-146">If the disk is a data disk, follow these steps:</span></span>

    1. <span data-ttu-id="f984d-147">Verifique o nome da VM à qual o disco está anexado.</span><span class="sxs-lookup"><span data-stu-id="f984d-147">Check the name of the VM that the disk is attached to.</span></span>
    2. <span data-ttu-id="f984d-148">Acesse **Máquinas Virtuais** > **Instâncias** e localize a VM.</span><span class="sxs-lookup"><span data-stu-id="f984d-148">Go to **Virtual Machines** > **Instances**, and then locate the VM.</span></span>
    3. <span data-ttu-id="f984d-149">Verifique se o disco não está sendo usado ativamente.</span><span class="sxs-lookup"><span data-stu-id="f984d-149">Make sure that nothing is actively using the disk.</span></span>
    4. <span data-ttu-id="f984d-150">Selecione **Desanexar Disco** na parte inferior do portal para desanexar o disco.</span><span class="sxs-lookup"><span data-stu-id="f984d-150">Select **Detach Disk** at the bottom of the portal to detach the disk.</span></span>
    5. <span data-ttu-id="f984d-151">Acesse **Máquinas Virtuais** > **Discos** e aguarde o campo **Conectado a** ficar em branco.</span><span class="sxs-lookup"><span data-stu-id="f984d-151">Go to **Virtual Machines** > **Disks**, and wait for the **Attached To** field to turn blank.</span></span> <span data-ttu-id="f984d-152">Isso indica que o disco foi desanexado com êxito da VM.</span><span class="sxs-lookup"><span data-stu-id="f984d-152">This indicates the disk has successfully detached from the VM.</span></span>
    6. <span data-ttu-id="f984d-153">Selecione **Excluir** na parte inferior de **Máquinas Virtuais** > **Discos** para excluir o disco.</span><span class="sxs-lookup"><span data-stu-id="f984d-153">Select **Delete** at the bottom of **Virtual Machines** > **Disks** to delete the disk.</span></span>

  - <span data-ttu-id="f984d-154">Se o disco for um disco de sistema operacional (o campo **Contém sistema operacional** terá um valor como Windows) e estiver anexado a uma VM, siga estas etapas para excluir a VM.</span><span class="sxs-lookup"><span data-stu-id="f984d-154">If the disk is an OS disk (the **Contains OS** field has a value like Windows) and attached to a VM, follow these steps to delete the VM.</span></span> <span data-ttu-id="f984d-155">O disco de sistema operacional não pode ser desanexado, portanto é preciso excluir a VM para liberar a concessão.</span><span class="sxs-lookup"><span data-stu-id="f984d-155">The OS disk cannot be detached, so we have to delete the VM to release the lease.</span></span>

    1. <span data-ttu-id="f984d-156">Verifique o nome da máquina virtual à qual o disco de dados está anexado.</span><span class="sxs-lookup"><span data-stu-id="f984d-156">Check the name of the Virtual Machine the Data Disk is attached to.</span></span>  
    2. <span data-ttu-id="f984d-157">Acesse **Máquinas Virtuais** > **Instâncias** e selecione a VM à qual o disco está anexado.</span><span class="sxs-lookup"><span data-stu-id="f984d-157">Go to **Virtual Machines** > **Instances**, and then select the VM that the disk is attached to.</span></span>
    3. <span data-ttu-id="f984d-158">Certifique-se de que nada esteja usando ativamente a máquina virtual, e que você não precise mais da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f984d-158">Make sure that nothing is actively using the virtual machine, and that you no longer need the virtual machine.</span></span>
    4. <span data-ttu-id="f984d-159">Selecione a VM à qual o disco está anexado e selecione **Excluir** > **Excluir os discos conectados**.</span><span class="sxs-lookup"><span data-stu-id="f984d-159">Select the VM the disk is attached to, then select **Delete** > **Delete the attached disks**.</span></span>
    5. <span data-ttu-id="f984d-160">Acesse **Máquinas Virtuais** > **Discos** e aguarde o disco desaparecer.</span><span class="sxs-lookup"><span data-stu-id="f984d-160">Go to **Virtual Machines** > **Disks**, and wait for the disk to disappear.</span></span>  <span data-ttu-id="f984d-161">Pode levar alguns minutos para que isso ocorra e talvez seja necessário atualizar a página.</span><span class="sxs-lookup"><span data-stu-id="f984d-161">It may take a few minutes for this to occur, and you may need to refresh the page.</span></span>
    6. <span data-ttu-id="f984d-162">Se o disco não desaparecer, aguarde o campo **Conectado a** ficar em branco.</span><span class="sxs-lookup"><span data-stu-id="f984d-162">If the disk does not disappear, wait for the **Attached To** field to turn blank.</span></span> <span data-ttu-id="f984d-163">Isso indica que o disco foi totalmente desanexado da VM.</span><span class="sxs-lookup"><span data-stu-id="f984d-163">This indicates the disk has fully detached from the VM.</span></span>  <span data-ttu-id="f984d-164">Em seguida, selecione o disco e selecione **Excluir** na parte inferior da página para excluir o disco.</span><span class="sxs-lookup"><span data-stu-id="f984d-164">Then, select the disk, and select **Delete** at the bottom of the page to delete the disk.</span></span>


   > [!NOTE]
   > <span data-ttu-id="f984d-165">Se um disco estiver conectado a uma VM, você não poderá excluí-lo.</span><span class="sxs-lookup"><span data-stu-id="f984d-165">If a disk is attached to a VM, you will not be able to delete it.</span></span> <span data-ttu-id="f984d-166">Discos são desconectados de uma VM excluída assincronamente.</span><span class="sxs-lookup"><span data-stu-id="f984d-166">Disks are detached from a deleted VM asynchronously.</span></span> <span data-ttu-id="f984d-167">A limpeza desse campo pode levar alguns minutos depois da exclusão de uma VM.</span><span class="sxs-lookup"><span data-stu-id="f984d-167">It might take a few minutes after the VM is deleted for this field to clear up.</span></span>
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-the-storage-account-or-container"></a><span data-ttu-id="f984d-168">Etapa 2: Excluir todas as imagens de VM que estão impedindo a exclusão da conta de armazenamento ou do contêiner</span><span class="sxs-lookup"><span data-stu-id="f984d-168">Step 2: Delete any VM Images that are preventing deletion of the storage account or container</span></span>
1. <span data-ttu-id="f984d-169">Alterne para o [portal clássico do Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="f984d-169">Switch to the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="f984d-170">Escolha **MÁQUINA VIRTUAL** > **IMAGENS** e exclua as imagens associadas à conta de armazenamento, ao contêiner ou ao VHD.</span><span class="sxs-lookup"><span data-stu-id="f984d-170">Select **VIRTUAL MACHINE** > **IMAGES**, and then delete the images that are associated with the storage account, container, or VHD.</span></span>

    <span data-ttu-id="f984d-171">Depois disso, tente excluir a conta de armazenamento, o contêiner ou o VHD novamente.</span><span class="sxs-lookup"><span data-stu-id="f984d-171">After that, try to delete the storage account, container, or VHD again.</span></span>

> [!WARNING]
> <span data-ttu-id="f984d-172">Não se esqueça de fazer backup de todas as informações que você deseja salvar antes de excluir a conta.</span><span class="sxs-lookup"><span data-stu-id="f984d-172">Be sure to back up anything you want to save before you delete the account.</span></span> <span data-ttu-id="f984d-173">Quando você exclui um VHD, blob, tabela, fila ou arquivo, ele é permanentemente excluído.</span><span class="sxs-lookup"><span data-stu-id="f984d-173">Once you delete a VHD, blob, table, queue, or file, it is permanently deleted.</span></span> <span data-ttu-id="f984d-174">Assegure-se de que o recurso não esteja em uso.</span><span class="sxs-lookup"><span data-stu-id="f984d-174">Ensure that the resource is not in use.</span></span>
>
>

## <a name="about-the-stopped-deallocated-status"></a><span data-ttu-id="f984d-175">Sobre o status Parado (desalocado)</span><span class="sxs-lookup"><span data-stu-id="f984d-175">About the Stopped (deallocated) status</span></span>
<span data-ttu-id="f984d-176">As VMs que foram criadas no modelo de implantação clássico e retidas terão o status **Parado (desalocado)** no [portal do Azure](https://portal.azure.com/) ou no [portal clássico do Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="f984d-176">VMs that were created in the classic deployment model and that have been retained will have the **Stopped (deallocated)** status on either the [Azure portal](https://portal.azure.com/) or [Azure classic portal](https://manage.windowsazure.com/).</span></span>

<span data-ttu-id="f984d-177">**Portal Clássico do Azure**:</span><span class="sxs-lookup"><span data-stu-id="f984d-177">**Azure classic portal**:</span></span>

![Status Parado (Desalocado) para VMs no portal do Azure.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

<span data-ttu-id="f984d-179">**Portal do Azure**:</span><span class="sxs-lookup"><span data-stu-id="f984d-179">**Azure portal**:</span></span>

![Status Parado (desalocado) para VMs no portal clássico do Azure.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

<span data-ttu-id="f984d-181">Um status "Parado (desalocado)" libera recursos do computador, como CPU, memória e rede.</span><span class="sxs-lookup"><span data-stu-id="f984d-181">A "Stopped (deallocated)" status releases the computer resources, such as the CPU, memory, and network.</span></span> <span data-ttu-id="f984d-182">No entanto, os discos ainda são mantidos para que você possa recriar rapidamente a VM, se necessário.</span><span class="sxs-lookup"><span data-stu-id="f984d-182">The disks, however, are still retained so that you can quickly re-create the VM if necessary.</span></span> <span data-ttu-id="f984d-183">Esses discos são criados sobre os VHDs cujos backups são feitos pelo armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f984d-183">These disks are created on top of VHDs, which are backed by Azure storage.</span></span> <span data-ttu-id="f984d-184">A conta de armazenamento tem esses VHDs e os discos têm concessões nesses VHDs.</span><span class="sxs-lookup"><span data-stu-id="f984d-184">The storage account has these VHDs, and the disks have leases on those VHDs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f984d-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f984d-185">Next steps</span></span>
* [<span data-ttu-id="f984d-186">Excluir uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f984d-186">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
