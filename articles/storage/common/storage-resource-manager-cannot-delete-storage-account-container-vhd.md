---
title: "Solucione erros ao excluir contas de Armazenamento do Azure, contêineres ou VHDs | Microsoft Docs"
description: "Solucione erros ao excluir contas de Armazenamento do Azure, contêineres ou VHDs"
services: storage
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: storage
ms.assetid: 17403aa1-fe8d-45ec-bc33-2c0b61126286
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 11944dd38b1cc30106c0b76a108480c018ca39d4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a><span data-ttu-id="5f556-103">Solucione erros ao excluir contas de Armazenamento do Azure, contêineres ou VHDs</span><span class="sxs-lookup"><span data-stu-id="5f556-103">Troubleshoot errors when you delete Azure storage accounts, containers, or VHDs</span></span>

<span data-ttu-id="5f556-104">Você pode receber erros ao tentar excluir a conta de armazenamento do Azure, o contêiner ou o VHD (disco rígido virtual) no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5f556-104">You might receive errors when you try to delete an Azure storage account, container, or virtual hard disk (VHD) in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5f556-105">Este artigo fornece orientação a fim de ajudar a resolver o problema em uma implantação do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5f556-105">This article provides troubleshooting guidance to help resolve the problem in an Azure Resource Manager deployment.</span></span>

<span data-ttu-id="5f556-106">Se este artigo não solucionar o problema do Azure, visite os fóruns do Azure na [MSDN e Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="5f556-106">If this article doesn't address your Azure problem, visit the Azure forums on [MSDN and Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="5f556-107">Você pode postar seu problema nesses fóruns ou usando @AzureSupport no Twitter.</span><span class="sxs-lookup"><span data-stu-id="5f556-107">You can post your problem on these forums or to @AzureSupport on Twitter.</span></span> <span data-ttu-id="5f556-108">Além disso, você pode registrar uma solicitação de suporte do Azure selecionando **Obter suporte** no site de [suporte do Azure](https://azure.microsoft.com/support/options/) .</span><span class="sxs-lookup"><span data-stu-id="5f556-108">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="5f556-109">Sintomas</span><span class="sxs-lookup"><span data-stu-id="5f556-109">Symptoms</span></span>
### <a name="scenario-1"></a><span data-ttu-id="5f556-110">Cenário 1</span><span class="sxs-lookup"><span data-stu-id="5f556-110">Scenario 1</span></span>
<span data-ttu-id="5f556-111">Quando você tenta excluir um VHD em uma conta de armazenamento de uma implantação do Resource Manager, a seguinte mensagem de erro é exibida:</span><span class="sxs-lookup"><span data-stu-id="5f556-111">When you try to delete a VHD in a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="5f556-112">**Falha ao excluir o blob 'vhds/BlobName.vhd'. Erro: Atualmente, há uma concessão no blob e nenhuma ID de concessão foi especificada na solicitação**</span><span class="sxs-lookup"><span data-stu-id="5f556-112">**Failed to delete blob 'vhds/BlobName.vhd'. Error: There is currently a lease on the blob and no lease ID was specified in the request.**</span></span>

<span data-ttu-id="5f556-113">Esse problema pode ocorrer porque uma VM (máquina virtual) tem uma concessão no VHD que você está tentando excluir.</span><span class="sxs-lookup"><span data-stu-id="5f556-113">This problem can occur because a virtual machine (VM) has a lease on the VHD that you are trying to delete.</span></span>

### <a name="scenario-2"></a><span data-ttu-id="5f556-114">Cenário 2</span><span class="sxs-lookup"><span data-stu-id="5f556-114">Scenario 2</span></span>
<span data-ttu-id="5f556-115">Quando você tenta excluir um contêiner em uma conta de armazenamento de uma implantação do Resource Manager, a seguinte mensagem de erro é exibida:</span><span class="sxs-lookup"><span data-stu-id="5f556-115">When you try to delete a container in a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="5f556-116">**Falha ao excluir o contêiner de armazenamento 'vhds'. Erro: Atualmente, há uma concessão no contêiner e nenhuma ID de concessão foi especificada na solicitação.**</span><span class="sxs-lookup"><span data-stu-id="5f556-116">**Failed to delete storage container 'vhds'. Error: There is currently a lease on the container and no lease ID was specified in the request.**</span></span>

<span data-ttu-id="5f556-117">Esse problema pode ocorrer porque o contêiner tem um VHD que está bloqueado no estado de concessão.</span><span class="sxs-lookup"><span data-stu-id="5f556-117">This problem can occur because the container has a VHD that is locked in the lease state.</span></span>

### <a name="scenario-3"></a><span data-ttu-id="5f556-118">Cenário 3</span><span class="sxs-lookup"><span data-stu-id="5f556-118">Scenario 3</span></span>
<span data-ttu-id="5f556-119">Quando você tenta excluir uma conta de armazenamento em uma conta de armazenamento em uma implantação do Resource Manager, a seguinte mensagem de erro é exibida:</span><span class="sxs-lookup"><span data-stu-id="5f556-119">When you try to delete a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="5f556-120">**Falha ao excluir a conta de armazenamento 'StorageAccountName'. Erro: A conta de armazenamento não pode ser excluída, pois seus artefatos estão em uso.**</span><span class="sxs-lookup"><span data-stu-id="5f556-120">**Failed to delete storage account 'StorageAccountName'. Error: The storage account cannot be deleted due to its artifacts being in use.**</span></span>

<span data-ttu-id="5f556-121">Esse problema pode ocorrer porque a conta de armazenamento tem um VHD que está em estado de concessão.</span><span class="sxs-lookup"><span data-stu-id="5f556-121">This problem can occur because the storage account contains a VHD that is in the lease state.</span></span>

## <a name="solution"></a><span data-ttu-id="5f556-122">Solução</span><span class="sxs-lookup"><span data-stu-id="5f556-122">Solution</span></span> 
<span data-ttu-id="5f556-123">Para resolver esses problemas, você deve identificar o VHD que está causando o erro e a VM associada.</span><span class="sxs-lookup"><span data-stu-id="5f556-123">To resolve these problems, you must identify the VHD that is causing the error and the associated VM.</span></span> <span data-ttu-id="5f556-124">Em seguida, desanexe o VHD da VM (para discos de dados) ou exclua a VM que está usando o VHD (para discos do sistema operacional).</span><span class="sxs-lookup"><span data-stu-id="5f556-124">Then, detach the VHD from the VM (for data disks) or delete the VM that is using the VHD (for OS disks).</span></span> <span data-ttu-id="5f556-125">Isso remove a concessão do VHD e permite que ele seja excluído.</span><span class="sxs-lookup"><span data-stu-id="5f556-125">This removes the lease from the VHD and allows it to be deleted.</span></span> 

<span data-ttu-id="5f556-126">Para tal, use um dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="5f556-126">To do this, use one of the following methods:</span></span>

### <a name="method-1---use-azure-storage-explorer"></a><span data-ttu-id="5f556-127">Método 1 – Usar o Gerenciador de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="5f556-127">Method 1 - Use Azure storage explorer</span></span>

### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a><span data-ttu-id="5f556-128">Etapa 1 Identificar o VHD que impede a exclusão da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="5f556-128">Step 1 Identify the VHD that prevent deletion of the storage account</span></span>

1. <span data-ttu-id="5f556-129">Quando você excluir a conta de armazenamento, será exibida uma caixa de diálogo de mensagem como a seguinte:</span><span class="sxs-lookup"><span data-stu-id="5f556-129">When you delete the storage account, you will receive a message dialog such as the following:</span></span> 

    ![mensagem ao excluir a conta de armazenamento](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="5f556-131">Verifique a **URL do Disco** para identificar a conta de armazenamento e o VHD que impede a exclusão da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5f556-131">Check the **Disk URL** to identify the storage account and the VHD that prevents you delete the storage account.</span></span> <span data-ttu-id="5f556-132">No exemplo a seguir, a cadeia de caracteres antes de “.blob.core.windows.net “ é o nome da conta de armazenamento e “SCCM2012-2015-08-28.vhd” é o nome do VHD.</span><span class="sxs-lookup"><span data-stu-id="5f556-132">In the following example, the string before “.blob.core.windows.net “ is the storage account name, and "SCCM2012-2015-08-28.vhd" is the VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-the-vhd-by-using-azure-storage-explorer"></a><span data-ttu-id="5f556-133">Etapa 2 Excluir o VHD usando o Gerenciador de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="5f556-133">Step 2 Delete the VHD by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="5f556-134">Baixe e instale a versão mais recente do [Gerenciador de Armazenamento do Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="5f556-134">Download and Install the latest version of [Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="5f556-135">Essa ferramenta é um aplicativo independente da Microsoft que permite trabalhar com os dados do Armazenamento do Azure no Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="5f556-135">This tool is a standalone app from Microsoft that allows you to easily work with Azure Storage data on Windows, macOS and Linux.</span></span>
2. <span data-ttu-id="5f556-136">Abra o Gerenciador de Armazenamento do Azure e selecione</span><span class="sxs-lookup"><span data-stu-id="5f556-136">Open Azure Storage Explorer, select</span></span> ![o ícone de conta](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) <span data-ttu-id="5f556-138">na barra de ferramentas à esquerda, selecione seu ambiente do Azure e entre na conta.</span><span class="sxs-lookup"><span data-stu-id="5f556-138">on the left bar, select your Azure environment, and then sign in.</span></span>

3. <span data-ttu-id="5f556-139">Selecione todas as assinaturas ou a assinatura que contém a conta de armazenamento que você deseja excluir.</span><span class="sxs-lookup"><span data-stu-id="5f556-139">Select all subscriptions or the subscription that contains the storage account you want to delete.</span></span>

    ![adicionar assinatura](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. <span data-ttu-id="5f556-141">Acesse a conta de armazenamento obtida da URL do disco anteriormente, selecione os **Contêineres de Blob** > **vhds** e pesquise o VHD que impede a exclusão da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5f556-141">Go to the storage account that we obtained from the disk URL earlier, select the **Blob Containers** > **vhds** and search for the VHD that prevents you delete the storage account.</span></span>
5. <span data-ttu-id="5f556-142">Se o VHD for encontrado, verifique a coluna **Nome da VM** para encontrar a máquina virtual que está usando esse VHD.</span><span class="sxs-lookup"><span data-stu-id="5f556-142">If the VHD is found,  check the **VM Name** column to find the VM that is using this VHD.</span></span>

    ![Verifique a VM](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. <span data-ttu-id="5f556-144">Remova a concessão do VHD usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f556-144">Remove the lease from the VHD by using Azure portal.</span></span> <span data-ttu-id="5f556-145">Para obter mais informações, consulte [Remover a concessão do VHD](#remove-the-lease-from-the-vhd).</span><span class="sxs-lookup"><span data-stu-id="5f556-145">For more information, see [Remove the lease from the VHD](#remove-the-lease-from-the-vhd).</span></span> 

7. <span data-ttu-id="5f556-146">Acesse o Gerenciador de Armazenamento do Azure, clique com o botão direito no VHD e selecione Excluir.</span><span class="sxs-lookup"><span data-stu-id="5f556-146">Go to the Azure Storage Explorer, right-click the VHD and then select delete.</span></span>

8. <span data-ttu-id="5f556-147">Excluir a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5f556-147">Delete the storage account.</span></span>

### <a name="method-2---use-azure-portal"></a><span data-ttu-id="5f556-148">Método 2 – Usar o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5f556-148">Method 2 - Use Azure portal</span></span> 

#### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a><span data-ttu-id="5f556-149">Etapa 1 Identificar o VHD que impede a exclusão da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="5f556-149">Step 1: Identify the VHD that prevent deletion of the storage account</span></span>

1. <span data-ttu-id="5f556-150">Quando você excluir a conta de armazenamento, será exibida uma caixa de diálogo de mensagem como a seguinte:</span><span class="sxs-lookup"><span data-stu-id="5f556-150">When you delete the storage account, you will receive a message dialog such as the following:</span></span> 

    ![mensagem ao excluir a conta de armazenamento](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="5f556-152">Verifique a **URL do Disco** para identificar a conta de armazenamento e o VHD que impede a exclusão da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5f556-152">Check the **Disk URL** to identify the storage account and the VHD that prevents you delete the storage account.</span></span> <span data-ttu-id="5f556-153">No exemplo a seguir, a cadeia de caracteres antes de “.blob.core.windows.net “ é o nome da conta de armazenamento e “SCCM2012-2015-08-28.vhd” é o nome do VHD.</span><span class="sxs-lookup"><span data-stu-id="5f556-153">In the following example, the string before “.blob.core.windows.net “ is the storage account name, and "SCCM2012-2015-08-28.vhd" is the VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. <span data-ttu-id="5f556-154">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5f556-154">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
3. <span data-ttu-id="5f556-155">No menu Hub, selecione **Todos os recursos**.</span><span class="sxs-lookup"><span data-stu-id="5f556-155">On the Hub menu, select **All resources**.</span></span> <span data-ttu-id="5f556-156">Vá para a conta de armazenamento e selecione **Blobs** > **vhds**.</span><span class="sxs-lookup"><span data-stu-id="5f556-156">Go to the storage account, and then select **Blobs** > **vhds**.</span></span>

    ![Captura de tela do portal, com a conta de armazenamento e o contêiner "vhds" realçados](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. <span data-ttu-id="5f556-158">Localize o VHD obtido da URL de disco anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5f556-158">Locate the VHD that we obtained from the disk URL earlier.</span></span> <span data-ttu-id="5f556-159">Em seguida, determine qual VM está usando o VHD.</span><span class="sxs-lookup"><span data-stu-id="5f556-159">Then, determine which VM is using the VHD.</span></span> <span data-ttu-id="5f556-160">Normalmente, você pode determinar qual VM armazena o VHD verificando o nome do VHD:</span><span class="sxs-lookup"><span data-stu-id="5f556-160">Usually, you can determine which VM holds the VHD by checking name of the VHD:</span></span>

<span data-ttu-id="5f556-161">VM no modelo de desenvolvimento do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5f556-161">VM in Resource Manager development  model</span></span>

   * <span data-ttu-id="5f556-162">Discos de sistema operacional geralmente seguem esta convenção de nomenclatura: NomeDaVM-AAAA-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="5f556-162">OS disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="5f556-163">Discos de dados geralmente seguem esta convenção de nomenclatura: NomeDaVM-AAAA-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="5f556-163">Data disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

<span data-ttu-id="5f556-164">VM no modelo de desenvolvimento clássico</span><span class="sxs-lookup"><span data-stu-id="5f556-164">VM in Classic development model</span></span>

   * <span data-ttu-id="5f556-165">Discos de sistema operacional geralmente seguem esta convenção de nomenclatura: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="5f556-165">OS disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="5f556-166">Discos de dados geralmente seguem esta convenção de nomenclatura: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="5f556-166">Data disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

#### <a name="step-2-remove-the-lease-from-the-vhd"></a><span data-ttu-id="5f556-167">Etapa 2: Remover a concessão do VHD</span><span class="sxs-lookup"><span data-stu-id="5f556-167">Step 2: Remove the lease from the VHD</span></span>

<span data-ttu-id="5f556-168">[Remova a concessão do VHD](#remove-the-lease-from-the-vhd) e exclua a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5f556-168">[Remove the lease from the VHD](#remove-the-lease-from-the-vhd), and then delete the storage account.</span></span>

## <a name="what-is-a-lease"></a><span data-ttu-id="5f556-169">O que é uma concessão?</span><span class="sxs-lookup"><span data-stu-id="5f556-169">What is a lease?</span></span>
<span data-ttu-id="5f556-170">Uma concessão é um bloqueio que pode ser usado para controlar o acesso a um blob (por exemplo, um VHD).</span><span class="sxs-lookup"><span data-stu-id="5f556-170">A lease is a lock that can be used to control access to a blob (for example, a VHD).</span></span> <span data-ttu-id="5f556-171">Quando um blob é concedido, somente os proprietários da concessão podem acessar o blob.</span><span class="sxs-lookup"><span data-stu-id="5f556-171">When a blob is leased, only the owners of the lease can access the blob.</span></span> <span data-ttu-id="5f556-172">Uma concessão é importante pelos seguintes motivos:</span><span class="sxs-lookup"><span data-stu-id="5f556-172">A lease is important for the following reasons:</span></span>

* <span data-ttu-id="5f556-173">Ele impede a corrupção de dados se vários proprietários tentarem gravar na mesma parte do blob ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="5f556-173">It prevents data corruption if multiple owners try to write to the same portion of the blob at the same time.</span></span>
* <span data-ttu-id="5f556-174">Ela impede a exclusão do blob se algo o estiver usando ativamente (por exemplo, uma VM).</span><span class="sxs-lookup"><span data-stu-id="5f556-174">It prevents the blob from being deleted if something is actively using it (for example, a VM).</span></span>
* <span data-ttu-id="5f556-175">Ela impede a exclusão da conta de armazenamento se algo a estiver usando ativamente (por exemplo, uma VM).</span><span class="sxs-lookup"><span data-stu-id="5f556-175">It prevents the storage account from being deleted if something is actively using it (for example, a VM).</span></span>

### <a name="remove-the-lease-from-the-vhd"></a><span data-ttu-id="5f556-176">Remover a concessão do VHD</span><span class="sxs-lookup"><span data-stu-id="5f556-176">Remove the lease from the VHD</span></span>
<span data-ttu-id="5f556-177">Se o VHD for um disco do sistema operacional, você deverá excluir a VM para remover a concessão:</span><span class="sxs-lookup"><span data-stu-id="5f556-177">If the VHD is an OS disk, you must delete the VM to remove the lease:</span></span>

1. <span data-ttu-id="5f556-178">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5f556-178">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5f556-179">No menu do **Hub**, selecione **Máquinas Virtuais**.</span><span class="sxs-lookup"><span data-stu-id="5f556-179">On the **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="5f556-180">Selecione a VM que contém uma concessão no VHD.</span><span class="sxs-lookup"><span data-stu-id="5f556-180">Select the VM that holds a lease on the VHD.</span></span>
4. <span data-ttu-id="5f556-181">Certifique-se de que nada esteja usando ativamente a máquina virtual, e que você não precise mais da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5f556-181">Make sure that nothing is actively using the virtual machine, and that you no longer need the virtual machine.</span></span>
5. <span data-ttu-id="5f556-182">Na parte superior da folha **Detalhes da VM**, selecione **Excluir** e clique em **Sim** para confirmar.</span><span class="sxs-lookup"><span data-stu-id="5f556-182">At the top of the **VM details** blade, select **Delete**, and then click **Yes** to confirm.</span></span>
6. <span data-ttu-id="5f556-183">A VM deve ser excluída, mas o VHD pode ser mantido.</span><span class="sxs-lookup"><span data-stu-id="5f556-183">The VM should be deleted, but the VHD can be retained.</span></span> <span data-ttu-id="5f556-184">No entanto, o VHD não deve ter mais uma concessão.</span><span class="sxs-lookup"><span data-stu-id="5f556-184">However, the VHD should no longer have a lease on it.</span></span> <span data-ttu-id="5f556-185">Talvez demore alguns minutos para o serviço ser liberado.</span><span class="sxs-lookup"><span data-stu-id="5f556-185">It may take a few minutes for the lease to be released.</span></span> <span data-ttu-id="5f556-186">Para verificar se a concessão foi liberada, acesse **Todos os recursos** > **Nome da Conta de Armazenamento** > **Blobs** > **vhds**.</span><span class="sxs-lookup"><span data-stu-id="5f556-186">To verify that the lease is released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="5f556-187">No painel **Propriedades de blob**, o valor do **Status de Concessão** deve ser **Desbloqueado**.</span><span class="sxs-lookup"><span data-stu-id="5f556-187">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span></span>

<span data-ttu-id="5f556-188">Se o VHD for um disco de dados, desanexe o VHD da VM para remover a concessão:</span><span class="sxs-lookup"><span data-stu-id="5f556-188">If the VHD is a data disk, detach the VHD from the VM to remove the lease:</span></span>

1. <span data-ttu-id="5f556-189">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5f556-189">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5f556-190">No menu do **Hub**, selecione **Máquinas Virtuais**.</span><span class="sxs-lookup"><span data-stu-id="5f556-190">On the **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="5f556-191">Selecione a VM que contém uma concessão no VHD.</span><span class="sxs-lookup"><span data-stu-id="5f556-191">Select the VM that holds a lease on the VHD.</span></span>
4. <span data-ttu-id="5f556-192">Selecione **Discos** na folha **Detalhes da VM**.</span><span class="sxs-lookup"><span data-stu-id="5f556-192">Select **Disks** on the **VM details** blade.</span></span>
5. <span data-ttu-id="5f556-193">Selecione o disco de dados que contém uma concessão no VHD.</span><span class="sxs-lookup"><span data-stu-id="5f556-193">Select the data disk that holds a lease on the VHD.</span></span> <span data-ttu-id="5f556-194">Você pode determinar qual VHD está anexado ao disco verificando a URL do VHD.</span><span class="sxs-lookup"><span data-stu-id="5f556-194">You can determine which VHD is attached in the disk by checking the URL of the VHD.</span></span>
6. <span data-ttu-id="5f556-195">Determine com certeza que nada está usando ativamente o disco de dados.</span><span class="sxs-lookup"><span data-stu-id="5f556-195">Determine with certainty that nothing is actively using the data disk.</span></span>
7. <span data-ttu-id="5f556-196">Clique em **Desanexar** na folha **Detalhes do disco**.</span><span class="sxs-lookup"><span data-stu-id="5f556-196">Click **Detach** on the **Disk details** blade.</span></span>
8. <span data-ttu-id="5f556-197">Agora, o disco deve ser desanexado da VM, e o VHD não deve ter mais uma concessão.</span><span class="sxs-lookup"><span data-stu-id="5f556-197">The disk should now be detached from the VM, and the VHD should no longer have a lease on it.</span></span> <span data-ttu-id="5f556-198">Talvez demore alguns minutos para o serviço ser liberado.</span><span class="sxs-lookup"><span data-stu-id="5f556-198">It may take a few minutes for the lease to be released.</span></span> <span data-ttu-id="5f556-199">Para verificar se a concessão foi liberada, acesse **Todos os recursos** > **Nome da Conta de Armazenamento** > **Blobs** > **vhds**.</span><span class="sxs-lookup"><span data-stu-id="5f556-199">To verify that the lease has been released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="5f556-200">No painel **Propriedades de blob**, o valor do **Status de Concessão** deve ser **Desbloqueado**.</span><span class="sxs-lookup"><span data-stu-id="5f556-200">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f556-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5f556-201">Next steps</span></span>
* [<span data-ttu-id="5f556-202">Excluir uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="5f556-202">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
* [<span data-ttu-id="5f556-203">How to break the locked lease of blob storage in Microsoft Azure (PowerShell) (Como interromper a liberação de bloqueio do armazenamento de blobs no Microsoft Azure (PowerShell))</span><span class="sxs-lookup"><span data-stu-id="5f556-203">How to break the locked lease of blob storage in Microsoft Azure (PowerShell)</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
