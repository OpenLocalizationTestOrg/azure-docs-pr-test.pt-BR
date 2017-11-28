---
title: aaaCreate uma VM do Azure gerenciados de um VHD local generalizado | Microsoft Docs
description: "Carregar um tooAzure VHD generalizado e usá-lo toocreate novas VMs, no modelo de implantação do Gerenciador de recursos de saudação."
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
ms.date: 05/19/2017
ms.author: cynthn
ms.openlocfilehash: 2fd0c0eec922e6ca8af4e712c1bceb1f9466105c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-toocreate-new-vms-in-azure"></a><span data-ttu-id="d1b38-103">Carregar um VHD generalizado e usá-lo toocreate novas VMs no Azure</span><span class="sxs-lookup"><span data-stu-id="d1b38-103">Upload a generalized VHD and use it toocreate new VMs in Azure</span></span>

<span data-ttu-id="d1b38-104">Este tópico orienta você a usar PowerShell tooupload um VHD de um tooAzure VM generalizado, criar uma imagem de saudação VHD e criar uma nova VM da imagem.</span><span class="sxs-lookup"><span data-stu-id="d1b38-104">This topic walks you through using PowerShell tooupload a VHD of a generalized VM tooAzure, create an image from hello VHD and create a new VM from that image.</span></span> <span data-ttu-id="d1b38-105">Você pode carregar um VHD exportado de uma ferramenta de virtualização local ou de outra nuvem.</span><span class="sxs-lookup"><span data-stu-id="d1b38-105">You can upload a VHD exported from an on-premises virtualization tool or from another cloud.</span></span> <span data-ttu-id="d1b38-106">Usando [discos gerenciados](managed-disks-overview.md) para Olá nova VM simplifica o gerenciamento de VM hello e fornece maior disponibilidade quando Olá VM é colocada em um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="d1b38-106">Using [Managed Disks](managed-disks-overview.md) for hello new VM simplifies hello VM managment and provides better availability when hello VM is placed in an availability set.</span></span> 

<span data-ttu-id="d1b38-107">Se você quiser toouse um exemplo de script, consulte [tooupload script tooAzure um VHD de exemplo e criar uma nova VM](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span><span class="sxs-lookup"><span data-stu-id="d1b38-107">If you want toouse a sample script, see [Sample script tooupload a VHD tooAzure and create a new VM](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d1b38-108">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="d1b38-108">Before you begin</span></span>

- <span data-ttu-id="d1b38-109">Antes de carregar qualquer tooAzure VHD, você deve seguir [preparar um tooAzure de tooupload Windows VHD ou VHDX](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="d1b38-109">Before uploading any VHD tooAzure, you should follow [Prepare a Windows VHD or VHDX tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
- <span data-ttu-id="d1b38-110">Revisão [planejar a migração de saudação do discos tooManaged](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) antes de iniciar a migração muito[discos gerenciados](managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d1b38-110">Review [Plan for hello migration tooManaged Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) before starting your migration too[Managed Disks](managed-disks-overview.md).</span></span>
- <span data-ttu-id="d1b38-111">Certifique-se de que você tem a versão mais recente Olá de saudação módulo AzureRM.Compute PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1b38-111">Make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="d1b38-112">Executar Olá tooinstall de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="d1b38-112">Run hello following command tooinstall it.</span></span>

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    <span data-ttu-id="d1b38-113">Para saber mais, confira [Azure PowerShell Versioning](/powershell/azure/overview) (Controle de versão do Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="d1b38-113">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="d1b38-114">Generalize Olá VM do Windows usando Sysprep</span><span class="sxs-lookup"><span data-stu-id="d1b38-114">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="d1b38-115">O Sysprep remove todas as suas informações de conta pessoal, entre outras coisas e prepara Olá máquina toobe usado como uma imagem.</span><span class="sxs-lookup"><span data-stu-id="d1b38-115">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="d1b38-116">Para obter detalhes sobre o Sysprep, consulte [como tooUse Sysprep: uma introdução](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="d1b38-116">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="d1b38-117">Certifique-se de funções de servidor de saudação em execução na máquina Olá Sysprep oferece suporte.</span><span class="sxs-lookup"><span data-stu-id="d1b38-117">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="d1b38-118">Para obter mais informações, consulte [Suporte do Sysprep para funções de servidor](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="d1b38-118">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1b38-119">Se você estiver executando o Sysprep antes de carregar seu tooAzure VHD para Olá primeira vez, verifique se você tem [preparado sua VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de executar o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="d1b38-119">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="d1b38-120">Entrar toohello máquina virtual do Windows.</span><span class="sxs-lookup"><span data-stu-id="d1b38-120">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="d1b38-121">Abra a janela de Prompt de comando hello como administrador.</span><span class="sxs-lookup"><span data-stu-id="d1b38-121">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="d1b38-122">Altere o diretório de saudação muito**%windir%\system32\sysprep**e, em seguida, execute `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="d1b38-122">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="d1b38-123">Em Olá **ferramenta de preparação do sistema** caixa de diálogo, selecione **Enter System Out-of-Box Experience (OOBE)**e certifique-se de que Olá **generalizar** caixa de seleção é marcada.</span><span class="sxs-lookup"><span data-stu-id="d1b38-123">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="d1b38-124">Em **Opções de Desligamento**, selecione **Desligar**.</span><span class="sxs-lookup"><span data-stu-id="d1b38-124">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="d1b38-125">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d1b38-125">Click **OK**.</span></span>
   
    ![Inicie o Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="d1b38-127">Quando o Sysprep for concluído, desligar máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1b38-127">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="d1b38-128">Não reinicie Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d1b38-128">Do not restart hello VM.</span></span>



## <a name="log-in-tooazure"></a><span data-ttu-id="d1b38-129">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="d1b38-129">Log in tooAzure</span></span>
<span data-ttu-id="d1b38-130">Se você ainda não tiver o PowerShell versão 1.4 ou superior instalado, leia [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d1b38-130">If you don't already have PowerShell version 1.4 or above installed, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="d1b38-131">Abra o PowerShell do Azure e entrar tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1b38-131">Open Azure PowerShell and sign in tooyour Azure account.</span></span> <span data-ttu-id="d1b38-132">Uma janela pop-up é aberto para você tooenter suas credenciais de conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1b38-132">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="d1b38-133">Obter IDs de assinatura Olá para suas assinaturas disponíveis.</span><span class="sxs-lookup"><span data-stu-id="d1b38-133">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="d1b38-134">Definir Olá assinatura correto usando a ID de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1b38-134">Set hello correct subscription using hello subscription ID.</span></span> <span data-ttu-id="d1b38-135">Substituir  *<subscriptionID>*  com ID Olá Olá corrigir a assinatura.</span><span class="sxs-lookup"><span data-stu-id="d1b38-135">Replace *<subscriptionID>* with hello ID of hello correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-hello-storage-account"></a><span data-ttu-id="d1b38-136">Obter a conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="d1b38-136">Get hello storage account</span></span>
<span data-ttu-id="d1b38-137">Você precisa de uma conta de armazenamento na imagem VM do Azure toostore Olá carregado.</span><span class="sxs-lookup"><span data-stu-id="d1b38-137">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="d1b38-138">Você pode usar uma conta de armazenamento existente ou criar uma nova.</span><span class="sxs-lookup"><span data-stu-id="d1b38-138">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="d1b38-139">Se usar o hello VHD toocreate um disco gerenciado para uma VM, local de conta de armazenamento Olá deve ser mesmo local Olá onde você estará criando Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d1b38-139">If you will be using hello VHD toocreate a managed disk for a VM, hello storage account location must be same hello location where you will be creating hello VM.</span></span>

<span data-ttu-id="d1b38-140">as contas de armazenamento disponível Olá tooshow, digite:</span><span class="sxs-lookup"><span data-stu-id="d1b38-140">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="d1b38-141">Se você quiser toouse uma conta de armazenamento existente, vá toohello [carregar imagem VM Olá](#upload-the-vm-vhd-to-your-storage-account) seção.</span><span class="sxs-lookup"><span data-stu-id="d1b38-141">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="d1b38-142">Se você precisar toocreate uma conta de armazenamento, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="d1b38-142">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="d1b38-143">Você precisará nome Olá Olá do grupo de recursos onde a conta de armazenamento Olá deve ser criada.</span><span class="sxs-lookup"><span data-stu-id="d1b38-143">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="d1b38-144">toofind todos os grupos de recursos Olá que estão em sua assinatura, o tipo:</span><span class="sxs-lookup"><span data-stu-id="d1b38-144">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="d1b38-145">toocreate um grupo de recursos denominado **myResourceGroup** em Olá **Leste dos EUA** região, digite:</span><span class="sxs-lookup"><span data-stu-id="d1b38-145">toocreate a resource group named **myResourceGroup** in hello **East US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. <span data-ttu-id="d1b38-146">Criar uma conta de armazenamento denominada **mystorageaccount** neste grupo de recursos usando Olá [AzureRmStorageAccount novo](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d1b38-146">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    <span data-ttu-id="d1b38-147">Os valores válidos para -SkuName são:</span><span class="sxs-lookup"><span data-stu-id="d1b38-147">Valid values for -SkuName are:</span></span>
   
   * <span data-ttu-id="d1b38-148">**Standard_LRS** – Armazenamento com redundância local.</span><span class="sxs-lookup"><span data-stu-id="d1b38-148">**Standard_LRS** - Locally redundant storage.</span></span> 
   * <span data-ttu-id="d1b38-149">**Standard_ZRS** – Armazenamento com redundância de zona.</span><span class="sxs-lookup"><span data-stu-id="d1b38-149">**Standard_ZRS** - Zone redundant storage.</span></span>
   * <span data-ttu-id="d1b38-150">**Standard_GRS** – Armazenamento com redundância geográfica.</span><span class="sxs-lookup"><span data-stu-id="d1b38-150">**Standard_GRS** - Geo redundant storage.</span></span> 
   * <span data-ttu-id="d1b38-151">**Standard_RAGRS** – Armazenamento com redundância geográfica com acesso de leitura.</span><span class="sxs-lookup"><span data-stu-id="d1b38-151">**Standard_RAGRS** - Read access geo redundant storage.</span></span> 
   * <span data-ttu-id="d1b38-152">**Premium_LRS** – Armazenamento com redundância local Premium.</span><span class="sxs-lookup"><span data-stu-id="d1b38-152">**Premium_LRS** - Premium locally redundant storage.</span></span> 

## <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="d1b38-153">Carregar conta de armazenamento Olá VHD tooyour</span><span class="sxs-lookup"><span data-stu-id="d1b38-153">Upload hello VHD tooyour storage account</span></span>

<span data-ttu-id="d1b38-154">Saudação de uso [AzureRmVhd adicionar](https://msdn.microsoft.com/library/mt603554.aspx) contêiner de tooa do VHD do cmdlet tooupload Olá em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d1b38-154">Use hello [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet tooupload hello VHD tooa container in your storage account.</span></span> <span data-ttu-id="d1b38-155">Este exemplo hello de carregamentos de arquivo *myVHD.vhd* de *"discos de rígidos C:\Users\Public\Documents\Virtual\"*  tooa conta de armazenamento denominada *mystorageaccount*em Olá *myResourceGroup* grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d1b38-155">This example uploads hello file *myVHD.vhd* from *"C:\Users\Public\Documents\Virtual hard disks\"* tooa storage account named *mystorageaccount* in hello *myResourceGroup* resource group.</span></span> <span data-ttu-id="d1b38-156">arquivo Hello será colocado no contêiner Olá denominado *mycontainer* e o novo nome de arquivo hello serão *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="d1b38-156">hello file will be placed into hello container named *mycontainer* and hello new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="d1b38-157">Se for bem-sucedido, você receberá uma resposta que parece semelhante toothis:</span><span class="sxs-lookup"><span data-stu-id="d1b38-157">If successful, you get a response that looks similar toothis:</span></span>

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="d1b38-158">Dependendo de sua conexão de rede e o tamanho de saudação do arquivo VHD, este comando pode demorar um pouco toocomplete</span><span class="sxs-lookup"><span data-stu-id="d1b38-158">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete</span></span>

<span data-ttu-id="d1b38-159">Salvar Olá **URI de destino** toouse caminho mais tarde, se você vai toocreate um disco gerenciado ou uma nova VM usando Olá carregar o VHD.</span><span class="sxs-lookup"><span data-stu-id="d1b38-159">Save hello **Destination URI** path toouse later if you are going toocreate a managed disk or a new VM using hello uploaded VHD.</span></span>

### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="d1b38-160">Outras opções para carregar um VHD</span><span class="sxs-lookup"><span data-stu-id="d1b38-160">Other options for uploading a VHD</span></span>
 
 
<span data-ttu-id="d1b38-161">Você também pode carregar uma conta de armazenamento de tooyour VHD usando um dos seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="d1b38-161">You can also upload a VHD tooyour storage account using one of hello following:</span></span>

- [<span data-ttu-id="d1b38-162">AzCopy</span><span class="sxs-lookup"><span data-stu-id="d1b38-162">AzCopy</span></span>](http://aka.ms/downloadazcopy)
- [<span data-ttu-id="d1b38-163">API do Blob da Cópia de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="d1b38-163">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [<span data-ttu-id="d1b38-164">Carregamento de Blobs do Gerenciador de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="d1b38-164">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
- [<span data-ttu-id="d1b38-165">Referência de API REST do Serviço de Importação/Exportação do Armazenamento</span><span class="sxs-lookup"><span data-stu-id="d1b38-165">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)
-   <span data-ttu-id="d1b38-166">É recomendável usar o Serviço de Importação/Exportação se o tempo de carregamento estimado é de mais de sete dias.</span><span class="sxs-lookup"><span data-stu-id="d1b38-166">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="d1b38-167">Você pode usar [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate tempo de saudação da unidade de tamanho e a transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="d1b38-167">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello time from data size and transfer unit.</span></span> 
    <span data-ttu-id="d1b38-168">Importação/exportação pode ser usado a conta de armazenamento padrão de tooa toocopy.</span><span class="sxs-lookup"><span data-stu-id="d1b38-168">Import/Export can be used toocopy tooa standard storage account.</span></span> <span data-ttu-id="d1b38-169">Você precisará toocopy da conta de armazenamento toopremium de armazenamento padrão usando uma ferramenta como AzCopy.</span><span class="sxs-lookup"><span data-stu-id="d1b38-169">You will need toocopy from standard storage toopremium storage account using a tool like AzCopy.</span></span>


## <a name="create-a-managed-image-from-hello-uploaded-vhd"></a><span data-ttu-id="d1b38-170">Criar um gerenciado imagem de saudação carregar o VHD</span><span class="sxs-lookup"><span data-stu-id="d1b38-170">Create a managed image from hello uploaded VHD</span></span> 

<span data-ttu-id="d1b38-171">Crie uma imagem gerenciada usando o VHD do sistema operacional generalizado.</span><span class="sxs-lookup"><span data-stu-id="d1b38-171">Create a managed image using your generalized OS VHD.</span></span> <span data-ttu-id="d1b38-172">Substitua valores hello com suas próprias informações.</span><span class="sxs-lookup"><span data-stu-id="d1b38-172">Replace hello values with your own information.</span></span>


1.  <span data-ttu-id="d1b38-173">Primeiro, defina os parâmetros comuns de saudação:</span><span class="sxs-lookup"><span data-stu-id="d1b38-173">First, set hello common parameters:</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  <span data-ttu-id="d1b38-174">Crie imagem de saudação usando o VHD do sistema operacional generalizado.</span><span class="sxs-lookup"><span data-stu-id="d1b38-174">Create hello image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a><span data-ttu-id="d1b38-175">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="d1b38-175">Create a virtual network</span></span>
<span data-ttu-id="d1b38-176">Criar rede virtual de saudação e a sub-rede de saudação [rede virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d1b38-176">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="d1b38-177">Crie uma sub-rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1b38-177">Create hello subnet.</span></span> <span data-ttu-id="d1b38-178">Este exemplo cria uma sub-rede denominada *mySubnet* com prefixo de endereço de saudação *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="d1b38-178">This example creates a subnet named *mySubnet* with hello address prefix of *10.0.0.0/24*.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="d1b38-179">Crie rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="d1b38-179">Create hello virtual network.</span></span> <span data-ttu-id="d1b38-180">Este exemplo cria uma rede virtual denominada *myVnet* com prefixo de endereço de saudação *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="d1b38-180">This example creates a virtual network named *myVnet* with hello address prefix of *10.0.0.0/16*.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="d1b38-181">Criar um endereço IP público e um adaptador de rede</span><span class="sxs-lookup"><span data-stu-id="d1b38-181">Create a public IP address and network interface</span></span>

<span data-ttu-id="d1b38-182">comunicação tooenable com máquina virtual de saudação na rede virtual Olá, é necessário um [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e uma interface de rede.</span><span class="sxs-lookup"><span data-stu-id="d1b38-182">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="d1b38-183">Criar um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="d1b38-183">Create a public IP address.</span></span> <span data-ttu-id="d1b38-184">Este exemplo cria um endereço IP público chamado *myPip*.</span><span class="sxs-lookup"><span data-stu-id="d1b38-184">This example creates a public IP address named *myPip*.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="d1b38-185">Criar NIC hello.</span><span class="sxs-lookup"><span data-stu-id="d1b38-185">Create hello NIC.</span></span> <span data-ttu-id="d1b38-186">Este exemplo cria uma NIC chamada **myNic**.</span><span class="sxs-lookup"><span data-stu-id="d1b38-186">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="d1b38-187">Criar um grupo de segurança de rede hello e uma regra RDP</span><span class="sxs-lookup"><span data-stu-id="d1b38-187">Create hello network security group and an RDP rule</span></span>

<span data-ttu-id="d1b38-188">toolog capaz de toobe em tooyour VM usando o RDP, você precisa toohave uma regra de segurança de rede (NSG) que permite o acesso RDP na porta 3389.</span><span class="sxs-lookup"><span data-stu-id="d1b38-188">toobe able toolog in tooyour VM using RDP, you need toohave a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="d1b38-189">Este exemplo cria um NSG chamado *myNsg* que contém uma regra chamada *myRdpRule* que permite tráfego RDP pela porta 3389.</span><span class="sxs-lookup"><span data-stu-id="d1b38-189">This example creates an NSG named *myNsg* that contains a rule called *myRdpRule* that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="d1b38-190">Para obter mais informações sobre os NSGs, consulte [a abertura de portas tooa VM no Azure usando o PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d1b38-190">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="d1b38-191">Criar uma variável para a rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="d1b38-191">Create a variable for hello virtual network</span></span>

<span data-ttu-id="d1b38-192">Crie uma variável para a rede virtual Olá concluída.</span><span class="sxs-lookup"><span data-stu-id="d1b38-192">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a><span data-ttu-id="d1b38-193">Obter credenciais Olá Olá VM</span><span class="sxs-lookup"><span data-stu-id="d1b38-193">Get hello credentials for hello VM</span></span>

<span data-ttu-id="d1b38-194">Olá seguinte cmdlet abrirá uma janela onde você inserirá um novo toouse de nome e senha de usuário como conta de administrador local Olá para acessar remotamente Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d1b38-194">hello following cmdlet will open a window where you will enter a new user name and password toouse as hello local administrator account for remotely accessing hello VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="add-hello-vm-name-and-size-toohello-vm-configuration"></a><span data-ttu-id="d1b38-195">Adicione hello nome da VM e a configuração da VM toohello tamanho.</span><span class="sxs-lookup"><span data-stu-id="d1b38-195">Add hello VM name and size toohello VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a><span data-ttu-id="d1b38-196">Imagem VM do conjunto hello como imagem de origem para Olá nova VM</span><span class="sxs-lookup"><span data-stu-id="d1b38-196">Set hello VM image as source image for hello new VM</span></span>

<span data-ttu-id="d1b38-197">Definir a imagem de origem de hello usando uma ID de Olá Olá gerenciado da imagem da VM.</span><span class="sxs-lookup"><span data-stu-id="d1b38-197">Set hello source image using hello ID of hello managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a><span data-ttu-id="d1b38-198">Definir configuração de SO hello e adicionar NIC hello.</span><span class="sxs-lookup"><span data-stu-id="d1b38-198">Set hello OS configuration and add hello NIC.</span></span>

<span data-ttu-id="d1b38-199">Insira o tipo de armazenamento da saudação (PremiumLRS ou StandardLRS) e o tamanho de saudação do disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="d1b38-199">Enter hello storage type (PremiumLRS or StandardLRS) and hello size of hello OS disk.</span></span> <span data-ttu-id="d1b38-200">Este exemplo define o tipo de conta Olá muito*PremiumLRS*, Olá muito o tamanho do disco*128 GB* e cache de disco muito*ReadWrite*.</span><span class="sxs-lookup"><span data-stu-id="d1b38-200">This example sets hello account type too*PremiumLRS*, hello disk size too*128 GB* and disk caching too*ReadWrite*.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a><span data-ttu-id="d1b38-201">Criar hello VM</span><span class="sxs-lookup"><span data-stu-id="d1b38-201">Create hello VM</span></span>

<span data-ttu-id="d1b38-202">Criar hello nova VM usando a configuração de saudação armazenado em Olá **$vm** variável.</span><span class="sxs-lookup"><span data-stu-id="d1b38-202">Create hello new VM using hello configuration stored in hello **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="d1b38-203">Verifique se esse Olá que VM foi criada</span><span class="sxs-lookup"><span data-stu-id="d1b38-203">Verify that hello VM was created</span></span>
<span data-ttu-id="d1b38-204">Ao concluir, você deverá ver Olá recém-criado VM em Olá [portal do Azure](https://portal.azure.com) em **procurar** > **máquinas virtuais**, ou usando o seguinte Olá Comandos do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d1b38-204">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="d1b38-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d1b38-205">Next steps</span></span>

<span data-ttu-id="d1b38-206">toosign em tooyour nova máquina virtual toohello procurar VM em Olá [portal](https://portal.azure.com), clique em **conectar**e abra Olá o RDP.</span><span class="sxs-lookup"><span data-stu-id="d1b38-206">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="d1b38-207">Use credenciais de conta de saudação do seu toosign de máquina virtual original na nova máquina de virtual tooyour.</span><span class="sxs-lookup"><span data-stu-id="d1b38-207">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="d1b38-208">Para obter mais informações, consulte [como tooconnect e logon tooan virtuais do Azure do computador que executa o Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d1b38-208">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

