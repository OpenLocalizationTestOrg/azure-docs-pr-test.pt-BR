---
title: aaaCreate uma imagem gerenciada no Azure | Microsoft Docs
description: "Crie uma imagem gerenciada de uma VM ou um VHD generalizado no Azure. Imagens pode ser usado toocreate várias VMs que usam discos gerenciados."
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
ms.date: 02/27/2017
ms.author: cynthn
ms.openlocfilehash: d8cd6c2ce8c5d704de2c845abced85139944d682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a><span data-ttu-id="993dd-104">Criar uma imagem gerenciada de uma VM generalizada no Azure</span><span class="sxs-lookup"><span data-stu-id="993dd-104">Create a managed image of a generalized VM in Azure</span></span>

<span data-ttu-id="993dd-105">Um recurso de imagem gerenciada pode ser criado com base em uma VM generalizada que é armazenada como um disco gerenciado ou um disco não gerenciado em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="993dd-105">A managed image resource can be created from a generalized VM that is stored as either a managed disk or an unmanaged disk in a storage account.</span></span> <span data-ttu-id="993dd-106">Olá imagem pode então ser usado toocreate várias VMs.</span><span class="sxs-lookup"><span data-stu-id="993dd-106">hello image can then be used toocreate multiple VMs.</span></span> 


## <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="993dd-107">Generalize Olá VM do Windows usando Sysprep</span><span class="sxs-lookup"><span data-stu-id="993dd-107">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="993dd-108">O Sysprep remove todas as suas informações de conta pessoal, entre outras coisas e prepara Olá máquina toobe usado como uma imagem.</span><span class="sxs-lookup"><span data-stu-id="993dd-108">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="993dd-109">Para obter detalhes sobre o Sysprep, consulte [como tooUse Sysprep: uma introdução](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="993dd-109">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="993dd-110">Certifique-se de funções de servidor de saudação em execução na máquina Olá Sysprep oferece suporte.</span><span class="sxs-lookup"><span data-stu-id="993dd-110">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="993dd-111">Para obter mais informações, consulte [Suporte do Sysprep para funções de servidor](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="993dd-111">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="993dd-112">Se você estiver executando o Sysprep antes de carregar seu tooAzure VHD para Olá primeira vez, verifique se você tem [preparado sua VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de executar o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="993dd-112">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="993dd-113">Entrar toohello máquina virtual do Windows.</span><span class="sxs-lookup"><span data-stu-id="993dd-113">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="993dd-114">Abra a janela de Prompt de comando hello como administrador.</span><span class="sxs-lookup"><span data-stu-id="993dd-114">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="993dd-115">Altere o diretório de saudação muito**%windir%\system32\sysprep**e, em seguida, execute `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="993dd-115">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="993dd-116">Em Olá **ferramenta de preparação do sistema** caixa de diálogo, selecione **Enter System Out-of-Box Experience (OOBE)**e certifique-se de que Olá **generalizar** caixa de seleção é marcada.</span><span class="sxs-lookup"><span data-stu-id="993dd-116">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="993dd-117">Em **Opções de Desligamento**, selecione **Desligar**.</span><span class="sxs-lookup"><span data-stu-id="993dd-117">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="993dd-118">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="993dd-118">Click **OK**.</span></span>
   
    ![Inicie o Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="993dd-120">Quando o Sysprep for concluído, desligar máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="993dd-120">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="993dd-121">Não reinicie Olá VM.</span><span class="sxs-lookup"><span data-stu-id="993dd-121">Do not restart hello VM.</span></span>


## <a name="create-a-managed-image-in-hello-portal"></a><span data-ttu-id="993dd-122">Criar uma imagem gerenciada no portal de saudação</span><span class="sxs-lookup"><span data-stu-id="993dd-122">Create a managed image in hello portal</span></span> 

1. <span data-ttu-id="993dd-123">Olá abrir [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="993dd-123">Open hello [portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="993dd-124">Clique em Olá toocreate de sinal de adição de um novo recurso.</span><span class="sxs-lookup"><span data-stu-id="993dd-124">Click hello plus sign toocreate a new resource.</span></span>
3. <span data-ttu-id="993dd-125">Na pesquisa do filtro hello, digite **imagem**.</span><span class="sxs-lookup"><span data-stu-id="993dd-125">In hello filter search, type **Image**.</span></span>
4. <span data-ttu-id="993dd-126">Selecione **imagem** dos resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="993dd-126">Select **Image** from hello results.</span></span>
5. <span data-ttu-id="993dd-127">Em Olá **imagem** folha, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="993dd-127">In hello **Image** blade, click **Create**.</span></span>
6. <span data-ttu-id="993dd-128">Em **nome**, digite um nome para a imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="993dd-128">In **Name**, type a name for hello image.</span></span>
7. <span data-ttu-id="993dd-129">Se você tiver mais de uma assinatura, selecione Olá um correto do hello **assinatura** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="993dd-129">If you have more than one subscription, select hello correct one from hello **Subscription** drop-down.</span></span>
7. <span data-ttu-id="993dd-130">Em **grupo de recursos** selecione **criar novo** e digite um nome ou selecione **de existente** e selecione um toouse do grupo de recursos na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="993dd-130">In **Resource Group** either select **Create new** and type in a name, or select **From existing** and select a resource group toouse from hello drop-down list.</span></span>
8. <span data-ttu-id="993dd-131">Em **local**, escolha o local de saudação do seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="993dd-131">In **Location**, choose hello location of your resource group.</span></span>
9. <span data-ttu-id="993dd-132">Em **tipo de SO** Selecionar tipo de saudação do sistema operacional Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="993dd-132">In **OS type** select hello type of operating system, either Windows or Linux.</span></span>
11. <span data-ttu-id="993dd-133">Em **blob de armazenamento**, clique em **procurar** toolook para Olá VHD no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="993dd-133">In **Storage blob**, click **Browse** toolook for hello VHD in your Azure storage.</span></span>
12. <span data-ttu-id="993dd-134">Em **Tipo de conta** escolha entre Standard_LRS ou Premium_LRS.</span><span class="sxs-lookup"><span data-stu-id="993dd-134">In **Account type** choose Standard_LRS or Premium_LRS.</span></span> <span data-ttu-id="993dd-135">O Standard usa unidades de disco rígido e premium usa unidades de estado sólido.</span><span class="sxs-lookup"><span data-stu-id="993dd-135">Standard uses hard-disk drives and Premium uses solid-state drives.</span></span> <span data-ttu-id="993dd-136">Ambos usam o armazenamento redundante localmente.</span><span class="sxs-lookup"><span data-stu-id="993dd-136">Both use locally-redundant storage.</span></span>
13. <span data-ttu-id="993dd-137">Em **cache de disco** Olá selecione a opção de cache de disco adequado.</span><span class="sxs-lookup"><span data-stu-id="993dd-137">In **Disk caching** select hello appropriate disk caching option.</span></span> <span data-ttu-id="993dd-138">Opções de saudação são **nenhum**, **somente leitura** e **leitura \ gravação**.</span><span class="sxs-lookup"><span data-stu-id="993dd-138">hello options are **None**, **Read-only** and **Read\write**.</span></span>
14. <span data-ttu-id="993dd-139">Opcional: Você também pode adicionar uma imagem de toohello de disco de dados existente, clicando em **+ adicionar disco de dados**.</span><span class="sxs-lookup"><span data-stu-id="993dd-139">Optional: You can also add an existing data disk toohello image by clicking **+ Add data disk**.</span></span>  
15. <span data-ttu-id="993dd-140">Quando terminar as seleções, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="993dd-140">When you are done making your selections, click **Create**.</span></span>
16. <span data-ttu-id="993dd-141">Após a criação de imagem hello, você verá como um **imagem** recurso na lista de saudação de recursos no grupo de recursos de saudação escolhido.</span><span class="sxs-lookup"><span data-stu-id="993dd-141">After hello image is created, you will see it as an **Image** resource in hello list of resources in hello resource group you chose.</span></span>



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a><span data-ttu-id="993dd-142">Criação de uma imagem gerenciada de uma VM usando o Powershell</span><span class="sxs-lookup"><span data-stu-id="993dd-142">Create a managed image of a VM using Powershell</span></span>

<span data-ttu-id="993dd-143">Criar uma imagem diretamente de saudação que VM garante essa imagem Olá inclui todos os discos de saudação associados à saudação VM, incluindo hello disco do sistema operacional e eventuais discos de dados.</span><span class="sxs-lookup"><span data-stu-id="993dd-143">Creating an image directly from hello VM ensures that hello image includes all of hello disks associated with hello VM, including hello OS Disk and any data disks.</span></span>


<span data-ttu-id="993dd-144">Antes de começar, certifique-se de que você tem a versão mais recente Olá de saudação módulo AzureRM.Compute PowerShell.</span><span class="sxs-lookup"><span data-stu-id="993dd-144">Before you begin, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="993dd-145">Executar Olá tooinstall de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="993dd-145">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="993dd-146">Para saber mais, confira [Azure PowerShell Versioning](/powershell/azure/overview) (Controle de versão do Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="993dd-146">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


1. <span data-ttu-id="993dd-147">Defina algumas variáveis.</span><span class="sxs-lookup"><span data-stu-id="993dd-147">Create some variables.</span></span>

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. <span data-ttu-id="993dd-148">Verifique se Olá que VM ser desalocada.</span><span class="sxs-lookup"><span data-stu-id="993dd-148">Make sure hello VM has been deallocated.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="993dd-149">Definir status da saudação da máquina virtual de saudação muito**generalizado**.</span><span class="sxs-lookup"><span data-stu-id="993dd-149">Set hello status of hello virtual machine too**Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. <span data-ttu-id="993dd-150">Obtenha a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="993dd-150">Get hello virtual machine.</span></span> 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. <span data-ttu-id="993dd-151">Crie a configuração de imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="993dd-151">Create hello image configuration.</span></span>

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. <span data-ttu-id="993dd-152">Crie imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="993dd-152">Create hello image.</span></span>

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a><span data-ttu-id="993dd-153">Crie uma imagem gerenciada de um VHD no PowerShell</span><span class="sxs-lookup"><span data-stu-id="993dd-153">Create a managed image of a VHD in PowerShell</span></span>

<span data-ttu-id="993dd-154">Crie uma imagem gerenciada usando o VHD do sistema operacional generalizado.</span><span class="sxs-lookup"><span data-stu-id="993dd-154">Create a managed image using your generalized OS VHD.</span></span>


1.  <span data-ttu-id="993dd-155">Primeiro, defina os parâmetros comuns de saudação:</span><span class="sxs-lookup"><span data-stu-id="993dd-155">First, set hello common parameters:</span></span>

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. <span data-ttu-id="993dd-156">Olá Step\deallocate VM.</span><span class="sxs-lookup"><span data-stu-id="993dd-156">Step\deallocate hello VM.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="993dd-157">Marca Olá VM como generalizado.</span><span class="sxs-lookup"><span data-stu-id="993dd-157">Mark hello VM as generalized.</span></span>

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  <span data-ttu-id="993dd-158">Crie imagem de saudação usando o VHD do sistema operacional generalizado.</span><span class="sxs-lookup"><span data-stu-id="993dd-158">Create hello image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a><span data-ttu-id="993dd-159">Crie uma imagem gerenciada de um instantâneo usando o Powershell</span><span class="sxs-lookup"><span data-stu-id="993dd-159">Create a managed image from a snapshot using Powershell</span></span>

<span data-ttu-id="993dd-160">Você também pode criar uma imagem gerenciada de um instantâneo de saudação VHD de uma VM generalizada.</span><span class="sxs-lookup"><span data-stu-id="993dd-160">You can also create a managed image from a snapshot of hello VHD from a generalized VM.</span></span>

    
1. <span data-ttu-id="993dd-161">Defina algumas variáveis.</span><span class="sxs-lookup"><span data-stu-id="993dd-161">Create some variables.</span></span> 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. <span data-ttu-id="993dd-162">Obter instantâneo de saudação.</span><span class="sxs-lookup"><span data-stu-id="993dd-162">Get hello snapshot.</span></span>

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. <span data-ttu-id="993dd-163">Crie a configuração de imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="993dd-163">Create hello image configuration.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. <span data-ttu-id="993dd-164">Crie imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="993dd-164">Create hello image.</span></span>

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a><span data-ttu-id="993dd-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="993dd-165">Next steps</span></span>
- <span data-ttu-id="993dd-166">Agora você pode [criar uma máquina virtual de imagem gerenciada Olá generalizado](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="993dd-166">Now you can [create a VM from hello generalized managed image](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>    

