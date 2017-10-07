---
title: "erros de aaaTroubleshoot quando você excluir contas de armazenamento do Azure, contêineres ou VHDs | Microsoft Docs"
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
ms.openlocfilehash: 33261562a2dd2614b35bc1118924513f8c624d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a><span data-ttu-id="40c0b-103">Solucione erros ao excluir contas de Armazenamento do Azure, contêineres ou VHDs</span><span class="sxs-lookup"><span data-stu-id="40c0b-103">Troubleshoot errors when you delete Azure storage accounts, containers, or VHDs</span></span>

<span data-ttu-id="40c0b-104">Você poderá receber erros ao tentar toodelete uma conta de armazenamento do Azure, um contêiner ou um disco rígido virtual (VHD) no hello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="40c0b-104">You might receive errors when you try toodelete an Azure storage account, container, or virtual hard disk (VHD) in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="40c0b-105">Este artigo fornece uma solução orientação toohelp resolver Olá problema em uma implantação do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="40c0b-105">This article provides troubleshooting guidance toohelp resolve hello problem in an Azure Resource Manager deployment.</span></span>

<span data-ttu-id="40c0b-106">Se este artigo não resolver o problema do Azure, visite Olá fóruns do Azure em [MSDN e o estouro de pilha](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="40c0b-106">If this article doesn't address your Azure problem, visit hello Azure forums on [MSDN and Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="40c0b-107">Você pode lançar seu problema nesses fóruns ou too@AzureSupport no Twitter.</span><span class="sxs-lookup"><span data-stu-id="40c0b-107">You can post your problem on these forums or too@AzureSupport on Twitter.</span></span> <span data-ttu-id="40c0b-108">Além disso, você pode emitir uma solicitação de suporte do Azure, selecionando **obter suporte** em Olá [suporte do Azure](https://azure.microsoft.com/support/options/) site.</span><span class="sxs-lookup"><span data-stu-id="40c0b-108">Also, you can file an Azure support request by selecting **Get support** on hello [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="40c0b-109">Sintomas</span><span class="sxs-lookup"><span data-stu-id="40c0b-109">Symptoms</span></span>
### <a name="scenario-1"></a><span data-ttu-id="40c0b-110">Cenário 1</span><span class="sxs-lookup"><span data-stu-id="40c0b-110">Scenario 1</span></span>
<span data-ttu-id="40c0b-111">Quando você tenta toodelete um VHD em uma conta de armazenamento em uma implantação do Gerenciador de recursos, você receberá Olá a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="40c0b-111">When you try toodelete a VHD in a storage account in a Resource Manager deployment, you receive hello following error message:</span></span>

<span data-ttu-id="40c0b-112">**Falha ao blob toodelete 'vhds/BlobName.vhd'. Erro: Há uma concessão no blob hello e nenhuma ID de concessão foi especificada na solicitação de saudação.**</span><span class="sxs-lookup"><span data-stu-id="40c0b-112">**Failed toodelete blob 'vhds/BlobName.vhd'. Error: There is currently a lease on hello blob and no lease ID was specified in hello request.**</span></span>

<span data-ttu-id="40c0b-113">Esse problema pode ocorrer porque uma máquina virtual (VM) tem uma concessão no VHD que você está tentando toodelete de saudação.</span><span class="sxs-lookup"><span data-stu-id="40c0b-113">This problem can occur because a virtual machine (VM) has a lease on hello VHD that you are trying toodelete.</span></span>

### <a name="scenario-2"></a><span data-ttu-id="40c0b-114">Cenário 2</span><span class="sxs-lookup"><span data-stu-id="40c0b-114">Scenario 2</span></span>
<span data-ttu-id="40c0b-115">Quando você tenta toodelete um contêiner em uma conta de armazenamento em uma implantação do Gerenciador de recursos, você receberá Olá a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="40c0b-115">When you try toodelete a container in a storage account in a Resource Manager deployment, you receive hello following error message:</span></span>

<span data-ttu-id="40c0b-116">**Falha no contêiner de armazenamento de toodelete 'vhds'. Erro: Há uma concessão no contêiner hello e nenhuma ID de concessão foi especificada na solicitação de saudação.**</span><span class="sxs-lookup"><span data-stu-id="40c0b-116">**Failed toodelete storage container 'vhds'. Error: There is currently a lease on hello container and no lease ID was specified in hello request.**</span></span>

<span data-ttu-id="40c0b-117">Esse problema pode ocorrer porque o contêiner de saudação tem um VHD que está bloqueado no estado de concessão de saudação.</span><span class="sxs-lookup"><span data-stu-id="40c0b-117">This problem can occur because hello container has a VHD that is locked in hello lease state.</span></span>

### <a name="scenario-3"></a><span data-ttu-id="40c0b-118">Cenário 3</span><span class="sxs-lookup"><span data-stu-id="40c0b-118">Scenario 3</span></span>
<span data-ttu-id="40c0b-119">Quando você tenta toodelete uma conta de armazenamento em uma implantação do Gerenciador de recursos, você receberá Olá a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="40c0b-119">When you try toodelete a storage account in a Resource Manager deployment, you receive hello following error message:</span></span>

<span data-ttu-id="40c0b-120">**Falha na conta de armazenamento toodelete 'StorageAccountName'. Erro: a conta de armazenamento Olá não pode ser excluída devido tooits artefatos estão em uso.**</span><span class="sxs-lookup"><span data-stu-id="40c0b-120">**Failed toodelete storage account 'StorageAccountName'. Error: hello storage account cannot be deleted due tooits artifacts being in use.**</span></span>

<span data-ttu-id="40c0b-121">Esse problema pode ocorrer porque a conta de armazenamento Olá contém um VHD que está em estado de concessão de saudação.</span><span class="sxs-lookup"><span data-stu-id="40c0b-121">This problem can occur because hello storage account contains a VHD that is in hello lease state.</span></span>

## <a name="solution"></a><span data-ttu-id="40c0b-122">Solução</span><span class="sxs-lookup"><span data-stu-id="40c0b-122">Solution</span></span> 
<span data-ttu-id="40c0b-123">tooresolve esses problemas, você deve identificar Olá VHD que está causando o erro hello e Olá associados a VM.</span><span class="sxs-lookup"><span data-stu-id="40c0b-123">tooresolve these problems, you must identify hello VHD that is causing hello error and hello associated VM.</span></span> <span data-ttu-id="40c0b-124">Em seguida, desanexar Olá VHD da VM da saudação (para discos de dados) ou excluir Olá VM que está usando Olá VHD (para discos do sistema operacional).</span><span class="sxs-lookup"><span data-stu-id="40c0b-124">Then, detach hello VHD from hello VM (for data disks) or delete hello VM that is using hello VHD (for OS disks).</span></span> <span data-ttu-id="40c0b-125">Isso remove a concessão Olá Olá VHD e permite que ele toobe excluído.</span><span class="sxs-lookup"><span data-stu-id="40c0b-125">This removes hello lease from hello VHD and allows it toobe deleted.</span></span> 

<span data-ttu-id="40c0b-126">toodo isso, usar um dos métodos a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="40c0b-126">toodo this, use one of hello following methods:</span></span>

### <a name="method-1---use-azure-storage-explorer"></a><span data-ttu-id="40c0b-127">Método 1 – Usar o Gerenciador de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="40c0b-127">Method 1 - Use Azure storage explorer</span></span>

### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a><span data-ttu-id="40c0b-128">Etapa 1 identificar Olá VHD que impedem a exclusão da conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="40c0b-128">Step 1 Identify hello VHD that prevent deletion of hello storage account</span></span>

1. <span data-ttu-id="40c0b-129">Quando você exclui a conta de armazenamento hello, será exibida uma caixa de diálogo de mensagem, como a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="40c0b-129">When you delete hello storage account, you will receive a message dialog such as hello following:</span></span> 

    ![mensagem ao excluir a conta de armazenamento Olá](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="40c0b-131">Verificar Olá **disco URL** conta de armazenamento tooidentify hello e hello VHD que impede que você excluir a conta de armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="40c0b-131">Check hello **Disk URL** tooidentify hello storage account and hello VHD that prevents you delete hello storage account.</span></span> <span data-ttu-id="40c0b-132">Em Olá exemplo a seguir, Olá cadeia de caracteres antes de ". n e t" é o nome de conta de armazenamento hello e "SCCM2012-2015-08-28.vhd" é o nome do VHD de saudação.</span><span class="sxs-lookup"><span data-stu-id="40c0b-132">In hello following example, hello string before “.blob.core.windows.net “ is hello storage account name, and "SCCM2012-2015-08-28.vhd" is hello VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-hello-vhd-by-using-azure-storage-explorer"></a><span data-ttu-id="40c0b-133">Saudação de exclusão de etapa 2 VHD usando o Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="40c0b-133">Step 2 Delete hello VHD by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="40c0b-134">Download e instalação Olá última versão do [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="40c0b-134">Download and Install hello latest version of [Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="40c0b-135">Essa ferramenta é um aplicativo autônomo da Microsoft que permite que você tooeasily o trabalho com dados de armazenamento do Azure no Windows e Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="40c0b-135">This tool is a standalone app from Microsoft that allows you tooeasily work with Azure Storage data on Windows, macOS and Linux.</span></span>
2. <span data-ttu-id="40c0b-136">Abra o Gerenciador de Armazenamento do Azure e selecione</span><span class="sxs-lookup"><span data-stu-id="40c0b-136">Open Azure Storage Explorer, select</span></span> ![o ícone de conta](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) <span data-ttu-id="40c0b-138">na barra de saudação à esquerda, selecione seu ambiente do Azure e entrar.</span><span class="sxs-lookup"><span data-stu-id="40c0b-138">on hello left bar, select your Azure environment, and then sign in.</span></span>

3. <span data-ttu-id="40c0b-139">Selecione todas as assinaturas ou assinatura Olá que contém a conta de armazenamento Olá que deseja toodelete.</span><span class="sxs-lookup"><span data-stu-id="40c0b-139">Select all subscriptions or hello subscription that contains hello storage account you want toodelete.</span></span>

    ![adicionar assinatura](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. <span data-ttu-id="40c0b-141">Vá toohello conta de armazenamento que são obtidos Olá disco URL anterior, selecione Olá **contêineres de Blob** > **vhds** e procure Olá VHD que impede que você excluir conta de armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="40c0b-141">Go toohello storage account that we obtained from hello disk URL earlier, select hello **Blob Containers** > **vhds** and search for hello VHD that prevents you delete hello storage account.</span></span>
5. <span data-ttu-id="40c0b-142">Se Olá VHD for encontrado, verifique Olá **nome da VM** Olá toofind de coluna VM que está usando este VHD.</span><span class="sxs-lookup"><span data-stu-id="40c0b-142">If hello VHD is found,  check hello **VM Name** column toofind hello VM that is using this VHD.</span></span>

    ![Verifique a VM](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. <span data-ttu-id="40c0b-144">Remova concessão Olá Olá VHD usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="40c0b-144">Remove hello lease from hello VHD by using Azure portal.</span></span> <span data-ttu-id="40c0b-145">Para obter mais informações, consulte [remover concessão de saudação do hello VHD](#remove-the-lease-from-the-vhd).</span><span class="sxs-lookup"><span data-stu-id="40c0b-145">For more information, see [Remove hello lease from hello VHD](#remove-the-lease-from-the-vhd).</span></span> 

7. <span data-ttu-id="40c0b-146">Vá toohello Azure Storage Explorer, clique com botão direito Olá VHD e, em seguida, selecione Excluir.</span><span class="sxs-lookup"><span data-stu-id="40c0b-146">Go toohello Azure Storage Explorer, right-click hello VHD and then select delete.</span></span>

8. <span data-ttu-id="40c0b-147">Exclua a conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="40c0b-147">Delete hello storage account.</span></span>

### <a name="method-2---use-azure-portal"></a><span data-ttu-id="40c0b-148">Método 2 – Usar o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="40c0b-148">Method 2 - Use Azure portal</span></span> 

#### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a><span data-ttu-id="40c0b-149">Etapa 1: Identificar Olá VHD que impedem a exclusão da conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="40c0b-149">Step 1: Identify hello VHD that prevent deletion of hello storage account</span></span>

1. <span data-ttu-id="40c0b-150">Quando você exclui a conta de armazenamento hello, será exibida uma caixa de diálogo de mensagem, como a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="40c0b-150">When you delete hello storage account, you will receive a message dialog such as hello following:</span></span> 

    ![mensagem ao excluir a conta de armazenamento Olá](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="40c0b-152">Verificar Olá **disco URL** conta de armazenamento tooidentify hello e hello VHD que impede que você excluir a conta de armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="40c0b-152">Check hello **Disk URL** tooidentify hello storage account and hello VHD that prevents you delete hello storage account.</span></span> <span data-ttu-id="40c0b-153">Em Olá exemplo a seguir, Olá cadeia de caracteres antes de ". n e t" é o nome de conta de armazenamento hello e "SCCM2012-2015-08-28.vhd" é o nome do VHD de saudação.</span><span class="sxs-lookup"><span data-stu-id="40c0b-153">In hello following example, hello string before “.blob.core.windows.net “ is hello storage account name, and "SCCM2012-2015-08-28.vhd" is hello VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. <span data-ttu-id="40c0b-154">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="40c0b-154">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
3. <span data-ttu-id="40c0b-155">No menu de Hub hello, selecione **todos os recursos**.</span><span class="sxs-lookup"><span data-stu-id="40c0b-155">On hello Hub menu, select **All resources**.</span></span> <span data-ttu-id="40c0b-156">Vá toohello conta de armazenamento e, em seguida, selecione **Blobs** > **vhds**.</span><span class="sxs-lookup"><span data-stu-id="40c0b-156">Go toohello storage account, and then select **Blobs** > **vhds**.</span></span>

    ![Captura de tela de portal hello, com conta de armazenamento hello e contêiner de "vhds" hello realçado](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. <span data-ttu-id="40c0b-158">Localize Olá VHD que são obtidos da URL de disco Olá anteriormente.</span><span class="sxs-lookup"><span data-stu-id="40c0b-158">Locate hello VHD that we obtained from hello disk URL earlier.</span></span> <span data-ttu-id="40c0b-159">Em seguida, determinar quais usando a VM Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="40c0b-159">Then, determine which VM is using hello VHD.</span></span> <span data-ttu-id="40c0b-160">Normalmente, você pode determinar qual VM contém Olá VHD verificando o nome da saudação VHD:</span><span class="sxs-lookup"><span data-stu-id="40c0b-160">Usually, you can determine which VM holds hello VHD by checking name of hello VHD:</span></span>

<span data-ttu-id="40c0b-161">VM no modelo de desenvolvimento do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="40c0b-161">VM in Resource Manager development  model</span></span>

   * <span data-ttu-id="40c0b-162">Discos de sistema operacional geralmente seguem esta convenção de nomenclatura: NomeDaVM-AAAA-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="40c0b-162">OS disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="40c0b-163">Discos de dados geralmente seguem esta convenção de nomenclatura: NomeDaVM-AAAA-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="40c0b-163">Data disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

<span data-ttu-id="40c0b-164">VM no modelo de desenvolvimento clássico</span><span class="sxs-lookup"><span data-stu-id="40c0b-164">VM in Classic development model</span></span>

   * <span data-ttu-id="40c0b-165">Discos de sistema operacional geralmente seguem esta convenção de nomenclatura: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="40c0b-165">OS disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="40c0b-166">Discos de dados geralmente seguem esta convenção de nomenclatura: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="40c0b-166">Data disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

#### <a name="step-2-remove-hello-lease-from-hello-vhd"></a><span data-ttu-id="40c0b-167">Etapa 2: Remover a concessão de saudação do hello VHD</span><span class="sxs-lookup"><span data-stu-id="40c0b-167">Step 2: Remove hello lease from hello VHD</span></span>

<span data-ttu-id="40c0b-168">[Remova a concessão Olá Olá VHD](#remove-the-lease-from-the-vhd)e, em seguida, excluir a conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="40c0b-168">[Remove hello lease from hello VHD](#remove-the-lease-from-the-vhd), and then delete hello storage account.</span></span>

## <a name="what-is-a-lease"></a><span data-ttu-id="40c0b-169">O que é uma concessão?</span><span class="sxs-lookup"><span data-stu-id="40c0b-169">What is a lease?</span></span>
<span data-ttu-id="40c0b-170">Uma concessão é um bloqueio que pode ser usado toocontrol acesso tooa blob (por exemplo, um VHD).</span><span class="sxs-lookup"><span data-stu-id="40c0b-170">A lease is a lock that can be used toocontrol access tooa blob (for example, a VHD).</span></span> <span data-ttu-id="40c0b-171">Quando um blob é concedido, somente os proprietários de saudação de concessão de saudação podem acessar o blob de saudação.</span><span class="sxs-lookup"><span data-stu-id="40c0b-171">When a blob is leased, only hello owners of hello lease can access hello blob.</span></span> <span data-ttu-id="40c0b-172">Uma concessão é importante para Olá motivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="40c0b-172">A lease is important for hello following reasons:</span></span>

* <span data-ttu-id="40c0b-173">Isso impede a corrupção de dados se vários proprietários tente toowrite toohello mesma parte do blob de saudação no hello simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="40c0b-173">It prevents data corruption if multiple owners try toowrite toohello same portion of hello blob at hello same time.</span></span>
* <span data-ttu-id="40c0b-174">Ela impede que o blob hello está sendo excluído se algo estiver usando ativamente (por exemplo, uma máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="40c0b-174">It prevents hello blob from being deleted if something is actively using it (for example, a VM).</span></span>
* <span data-ttu-id="40c0b-175">Isso impedirá a conta de armazenamento Olá sejam excluídas se algo estiver usando ativamente (por exemplo, uma máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="40c0b-175">It prevents hello storage account from being deleted if something is actively using it (for example, a VM).</span></span>

### <a name="remove-hello-lease-from-hello-vhd"></a><span data-ttu-id="40c0b-176">Remova a concessão Olá Olá VHD</span><span class="sxs-lookup"><span data-stu-id="40c0b-176">Remove hello lease from hello VHD</span></span>
<span data-ttu-id="40c0b-177">Se Olá VHD é um disco do sistema operacional, você deve excluir a concessão de Olá Olá VM tooremove:</span><span class="sxs-lookup"><span data-stu-id="40c0b-177">If hello VHD is an OS disk, you must delete hello VM tooremove hello lease:</span></span>

1. <span data-ttu-id="40c0b-178">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="40c0b-178">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="40c0b-179">Em Olá **Hub** menu, selecione **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="40c0b-179">On hello **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="40c0b-180">Selecione Olá VM que contém uma concessão no VHD de saudação.</span><span class="sxs-lookup"><span data-stu-id="40c0b-180">Select hello VM that holds a lease on hello VHD.</span></span>
4. <span data-ttu-id="40c0b-181">Certifique-se de que nada está usando ativamente Olá de máquina virtual, e que você não precisa Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="40c0b-181">Make sure that nothing is actively using hello virtual machine, and that you no longer need hello virtual machine.</span></span>
5. <span data-ttu-id="40c0b-182">Na parte superior de saudação do hello **VM detalhes** folha, selecione **excluir**e, em seguida, clique em **Sim** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="40c0b-182">At hello top of hello **VM details** blade, select **Delete**, and then click **Yes** tooconfirm.</span></span>
6. <span data-ttu-id="40c0b-183">Olá VM deve ser excluído, mas Olá VHD pode ser mantido.</span><span class="sxs-lookup"><span data-stu-id="40c0b-183">hello VM should be deleted, but hello VHD can be retained.</span></span> <span data-ttu-id="40c0b-184">No entanto, Olá VHD não deve ter uma concessão nele.</span><span class="sxs-lookup"><span data-stu-id="40c0b-184">However, hello VHD should no longer have a lease on it.</span></span> <span data-ttu-id="40c0b-185">Ele pode levar alguns minutos para Olá toobe de concessão liberada.</span><span class="sxs-lookup"><span data-stu-id="40c0b-185">It may take a few minutes for hello lease toobe released.</span></span> <span data-ttu-id="40c0b-186">tooverify que Olá concessão for liberada, vá muito**todos os recursos** > **nome da conta de armazenamento** > **Blobs**  >  **vhds**.</span><span class="sxs-lookup"><span data-stu-id="40c0b-186">tooverify that hello lease is released, go too**All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="40c0b-187">Em Olá **propriedades de Blob** painel, Olá **Status de concessão** o valor deve ser **desbloqueado**.</span><span class="sxs-lookup"><span data-stu-id="40c0b-187">In hello **Blob properties** pane, hello **Lease Status** value should be **Unlocked**.</span></span>

<span data-ttu-id="40c0b-188">Se Olá VHD é um disco de dados, desanexe Olá VHD de concessão de Olá Olá VM tooremove:</span><span class="sxs-lookup"><span data-stu-id="40c0b-188">If hello VHD is a data disk, detach hello VHD from hello VM tooremove hello lease:</span></span>

1. <span data-ttu-id="40c0b-189">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="40c0b-189">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="40c0b-190">Em Olá **Hub** menu, selecione **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="40c0b-190">On hello **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="40c0b-191">Selecione Olá VM que contém uma concessão no VHD de saudação.</span><span class="sxs-lookup"><span data-stu-id="40c0b-191">Select hello VM that holds a lease on hello VHD.</span></span>
4. <span data-ttu-id="40c0b-192">Selecione **discos** em Olá **VM detalhes** folha.</span><span class="sxs-lookup"><span data-stu-id="40c0b-192">Select **Disks** on hello **VM details** blade.</span></span>
5. <span data-ttu-id="40c0b-193">Selecione Olá disco de dados que contém uma concessão no VHD de saudação.</span><span class="sxs-lookup"><span data-stu-id="40c0b-193">Select hello data disk that holds a lease on hello VHD.</span></span> <span data-ttu-id="40c0b-194">Você pode determinar que o VHD está anexado no disco Olá verificando URL Olá Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="40c0b-194">You can determine which VHD is attached in hello disk by checking hello URL of hello VHD.</span></span>
6. <span data-ttu-id="40c0b-195">Determine com certeza que nada está usando ativamente o disco de dados hello.</span><span class="sxs-lookup"><span data-stu-id="40c0b-195">Determine with certainty that nothing is actively using hello data disk.</span></span>
7. <span data-ttu-id="40c0b-196">Clique em **desanexar** em Olá **disco detalhes** folha.</span><span class="sxs-lookup"><span data-stu-id="40c0b-196">Click **Detach** on hello **Disk details** blade.</span></span>
8. <span data-ttu-id="40c0b-197">disco Olá agora deve ser desanexado de saudação VM e Olá VHD não deve ter uma concessão nele.</span><span class="sxs-lookup"><span data-stu-id="40c0b-197">hello disk should now be detached from hello VM, and hello VHD should no longer have a lease on it.</span></span> <span data-ttu-id="40c0b-198">Ele pode levar alguns minutos para Olá toobe de concessão liberada.</span><span class="sxs-lookup"><span data-stu-id="40c0b-198">It may take a few minutes for hello lease toobe released.</span></span> <span data-ttu-id="40c0b-199">tooverify que Olá concessão foi liberado, vá muito**todos os recursos** > **nome da conta de armazenamento** > **Blobs**  >  **vhds**.</span><span class="sxs-lookup"><span data-stu-id="40c0b-199">tooverify that hello lease has been released, go too**All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="40c0b-200">Em Olá **propriedades de Blob** painel, Olá **Status de concessão** o valor deve ser **desbloqueado**.</span><span class="sxs-lookup"><span data-stu-id="40c0b-200">In hello **Blob properties** pane, hello **Lease Status** value should be **Unlocked**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40c0b-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="40c0b-201">Next steps</span></span>
* [<span data-ttu-id="40c0b-202">Excluir uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="40c0b-202">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
* [<span data-ttu-id="40c0b-203">Como toobreak Olá bloqueado concessão de armazenamento de blob no Microsoft Azure (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="40c0b-203">How toobreak hello locked lease of blob storage in Microsoft Azure (PowerShell)</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
