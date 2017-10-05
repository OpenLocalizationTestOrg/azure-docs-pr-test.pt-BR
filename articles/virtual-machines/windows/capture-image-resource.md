---
title: Como criar uma imagem gerenciada no Azure | Microsoft Docs
description: "Crie uma imagem gerenciada de uma VM ou um VHD generalizado no Azure. Imagens podem ser usadas para criar várias VMs que usam discos gerenciados."
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
ms.openlocfilehash: f64b81489ab426b50ec89af369e1581ac71848be
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a><span data-ttu-id="c9da2-104">Criar uma imagem gerenciada de uma VM generalizada no Azure</span><span class="sxs-lookup"><span data-stu-id="c9da2-104">Create a managed image of a generalized VM in Azure</span></span>

<span data-ttu-id="c9da2-105">Um recurso de imagem gerenciada pode ser criado com base em uma VM generalizada que é armazenada como um disco gerenciado ou um disco não gerenciado em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c9da2-105">A managed image resource can be created from a generalized VM that is stored as either a managed disk or an unmanaged disk in a storage account.</span></span> <span data-ttu-id="c9da2-106">Em seguida, a imagem pode ser usada para criar várias VMs.</span><span class="sxs-lookup"><span data-stu-id="c9da2-106">The image can then be used to create multiple VMs.</span></span> 


## <a name="generalize-the-windows-vm-using-sysprep"></a><span data-ttu-id="c9da2-107">Generalizar a VM Windows usando Sysprep</span><span class="sxs-lookup"><span data-stu-id="c9da2-107">Generalize the Windows VM using Sysprep</span></span>

<span data-ttu-id="c9da2-108">O Sysprep remove todas as informações pessoais da conta, entre outros itens, e prepara o computador para ser utilizado como uma imagem.</span><span class="sxs-lookup"><span data-stu-id="c9da2-108">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="c9da2-109">Para obter detalhes sobre o Sysprep, consulte [Como usar o Sysprep: uma introdução](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="c9da2-109">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="c9da2-110">Verifique se as funções de servidor em execução no computador são suportadas pelo Sysprep.</span><span class="sxs-lookup"><span data-stu-id="c9da2-110">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="c9da2-111">Para obter mais informações, consulte [Suporte do Sysprep para funções de servidor](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="c9da2-111">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c9da2-112">Se você estiver executando o Sysprep antes de carregar o VHD para o Azure pela primeira vez, verifique se você [preparou sua VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de executar o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="c9da2-112">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="c9da2-113">Entre na máquina virtual Windows.</span><span class="sxs-lookup"><span data-stu-id="c9da2-113">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="c9da2-114">Abra uma janela de prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="c9da2-114">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="c9da2-115">Altere o diretório para **%windir%\system32\sysprep** e, a seguir, execute`sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="c9da2-115">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="c9da2-116">Na caixa de diálogo **Ferramenta de Preparação do Sistema**, selecione **Entrar na Configuração Inicial pelo Usuário do Sistema (OOBE)** e verifique se a caixa de seleção **Generalizar** está marcada.</span><span class="sxs-lookup"><span data-stu-id="c9da2-116">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="c9da2-117">Em **Opções de Desligamento**, selecione **Desligar**.</span><span class="sxs-lookup"><span data-stu-id="c9da2-117">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="c9da2-118">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c9da2-118">Click **OK**.</span></span>
   
    ![Inicie o Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="c9da2-120">Quando o Sysprep for concluído, desligará a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c9da2-120">When Sysprep completes, it shuts down the virtual machine.</span></span> <span data-ttu-id="c9da2-121">Não reinicie a VM.</span><span class="sxs-lookup"><span data-stu-id="c9da2-121">Do not restart the VM.</span></span>


## <a name="create-a-managed-image-in-the-portal"></a><span data-ttu-id="c9da2-122">Criação de uma imagem gerenciada no portal</span><span class="sxs-lookup"><span data-stu-id="c9da2-122">Create a managed image in the portal</span></span> 

1. <span data-ttu-id="c9da2-123">Abra o [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c9da2-123">Open the [portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c9da2-124">Clique no sinal de mais para criar um recurso novo.</span><span class="sxs-lookup"><span data-stu-id="c9da2-124">Click the plus sign to create a new resource.</span></span>
3. <span data-ttu-id="c9da2-125">No filtro da pesquisa, digite **Imagem**.</span><span class="sxs-lookup"><span data-stu-id="c9da2-125">In the filter search, type **Image**.</span></span>
4. <span data-ttu-id="c9da2-126">Selecione a **Imagem** dos resultados.</span><span class="sxs-lookup"><span data-stu-id="c9da2-126">Select **Image** from the results.</span></span>
5. <span data-ttu-id="c9da2-127">Na folha **Imagem**, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c9da2-127">In the **Image** blade, click **Create**.</span></span>
6. <span data-ttu-id="c9da2-128">No **Nome**, digite um nome para a imagem.</span><span class="sxs-lookup"><span data-stu-id="c9da2-128">In **Name**, type a name for the image.</span></span>
7. <span data-ttu-id="c9da2-129">Se você tiver mais de uma assinatura, selecione a correta na lista suspensa **Assinatura**.</span><span class="sxs-lookup"><span data-stu-id="c9da2-129">If you have more than one subscription, select the correct one from the **Subscription** drop-down.</span></span>
7. <span data-ttu-id="c9da2-130">Em **Grupo de Recursos**, escolha **Criar novo** e digite um nome ou escolha **Existente** e escolha na lista suspensa um grupo de recursos a ser usado.</span><span class="sxs-lookup"><span data-stu-id="c9da2-130">In **Resource Group** either select **Create new** and type in a name, or select **From existing** and select a resource group to use from the drop-down list.</span></span>
8. <span data-ttu-id="c9da2-131">Em **Local**, escolha o local de seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c9da2-131">In **Location**, choose the location of your resource group.</span></span>
9. <span data-ttu-id="c9da2-132">Em **Tipo de sistema operacional** selecione o tipo de sistema operacional: Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="c9da2-132">In **OS type** select the type of operating system, either Windows or Linux.</span></span>
11. <span data-ttu-id="c9da2-133">Em **Armazenamento de blobs**, clique em **Procurar** para procurar o VHD no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9da2-133">In **Storage blob**, click **Browse** to look for the VHD in your Azure storage.</span></span>
12. <span data-ttu-id="c9da2-134">Em **Tipo de conta** escolha entre Standard_LRS ou Premium_LRS.</span><span class="sxs-lookup"><span data-stu-id="c9da2-134">In **Account type** choose Standard_LRS or Premium_LRS.</span></span> <span data-ttu-id="c9da2-135">O Standard usa unidades de disco rígido e premium usa unidades de estado sólido.</span><span class="sxs-lookup"><span data-stu-id="c9da2-135">Standard uses hard-disk drives and Premium uses solid-state drives.</span></span> <span data-ttu-id="c9da2-136">Ambos usam o armazenamento redundante localmente.</span><span class="sxs-lookup"><span data-stu-id="c9da2-136">Both use locally-redundant storage.</span></span>
13. <span data-ttu-id="c9da2-137">Em **cache de disco** selecione a opção de cache de disco apropriada.</span><span class="sxs-lookup"><span data-stu-id="c9da2-137">In **Disk caching** select the appropriate disk caching option.</span></span> <span data-ttu-id="c9da2-138">As opções são **nenhum**, **somente leitura** e **leitura\gravação**.</span><span class="sxs-lookup"><span data-stu-id="c9da2-138">The options are **None**, **Read-only** and **Read\write**.</span></span>
14. <span data-ttu-id="c9da2-139">Opcional: você também pode adicionar um disco de dados existente à imagem clicando em **+ Adicionar disco de dados**.</span><span class="sxs-lookup"><span data-stu-id="c9da2-139">Optional: You can also add an existing data disk to the image by clicking **+ Add data disk**.</span></span>  
15. <span data-ttu-id="c9da2-140">Quando terminar as seleções, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c9da2-140">When you are done making your selections, click **Create**.</span></span>
16. <span data-ttu-id="c9da2-141">Depois que a imagem for criada, você verá como um recurso de **imagem** na lista de recursos no grupo de recursos que você escolheu.</span><span class="sxs-lookup"><span data-stu-id="c9da2-141">After the image is created, you will see it as an **Image** resource in the list of resources in the resource group you chose.</span></span>



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a><span data-ttu-id="c9da2-142">Criação de uma imagem gerenciada de uma VM usando o Powershell</span><span class="sxs-lookup"><span data-stu-id="c9da2-142">Create a managed image of a VM using Powershell</span></span>

<span data-ttu-id="c9da2-143">Criar uma imagem diretamente da VM garante que a imagem inclui todos os discos associados à VM, incluindo o disco do sistema operacional e os discos de dados.</span><span class="sxs-lookup"><span data-stu-id="c9da2-143">Creating an image directly from the VM ensures that the image includes all of the disks associated with the VM, including the OS Disk and any data disks.</span></span>


<span data-ttu-id="c9da2-144">Antes de iniciar, confira se você tem a versão mais recente do módulo AzureRM.Compute do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c9da2-144">Before you begin, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="c9da2-145">Execute o comando a seguir para instalá-lo.</span><span class="sxs-lookup"><span data-stu-id="c9da2-145">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="c9da2-146">Para saber mais, confira [Azure PowerShell Versioning](/powershell/azure/overview) (Controle de versão do Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="c9da2-146">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


1. <span data-ttu-id="c9da2-147">Defina algumas variáveis.</span><span class="sxs-lookup"><span data-stu-id="c9da2-147">Create some variables.</span></span>

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. <span data-ttu-id="c9da2-148">Verifique se a VM foi desalocada.</span><span class="sxs-lookup"><span data-stu-id="c9da2-148">Make sure the VM has been deallocated.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="c9da2-149">Defina o status da máquina virtual como **Generalizado**.</span><span class="sxs-lookup"><span data-stu-id="c9da2-149">Set the status of the virtual machine to **Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. <span data-ttu-id="c9da2-150">Obtenha a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c9da2-150">Get the virtual machine.</span></span> 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. <span data-ttu-id="c9da2-151">Crie a configuração de imagem.</span><span class="sxs-lookup"><span data-stu-id="c9da2-151">Create the image configuration.</span></span>

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. <span data-ttu-id="c9da2-152">Crie a imagem.</span><span class="sxs-lookup"><span data-stu-id="c9da2-152">Create the image.</span></span>

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a><span data-ttu-id="c9da2-153">Crie uma imagem gerenciada de um VHD no PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9da2-153">Create a managed image of a VHD in PowerShell</span></span>

<span data-ttu-id="c9da2-154">Crie uma imagem gerenciada usando o VHD do sistema operacional generalizado.</span><span class="sxs-lookup"><span data-stu-id="c9da2-154">Create a managed image using your generalized OS VHD.</span></span>


1.  <span data-ttu-id="c9da2-155">Primeiro, defina os parâmetros comuns:</span><span class="sxs-lookup"><span data-stu-id="c9da2-155">First, set the common parameters:</span></span>

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. <span data-ttu-id="c9da2-156">Pare/desaloque a VM.</span><span class="sxs-lookup"><span data-stu-id="c9da2-156">Step\deallocate the VM.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="c9da2-157">Marque a VM como generalizada.</span><span class="sxs-lookup"><span data-stu-id="c9da2-157">Mark the VM as generalized.</span></span>

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  <span data-ttu-id="c9da2-158">Crie a imagem usando o VHD do sistema operacional generalizado.</span><span class="sxs-lookup"><span data-stu-id="c9da2-158">Create the image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a><span data-ttu-id="c9da2-159">Crie uma imagem gerenciada de um instantâneo usando o Powershell</span><span class="sxs-lookup"><span data-stu-id="c9da2-159">Create a managed image from a snapshot using Powershell</span></span>

<span data-ttu-id="c9da2-160">Você também pode criar uma imagem gerenciada de um instantâneo do VHD de uma VM generalizada.</span><span class="sxs-lookup"><span data-stu-id="c9da2-160">You can also create a managed image from a snapshot of the VHD from a generalized VM.</span></span>

    
1. <span data-ttu-id="c9da2-161">Defina algumas variáveis.</span><span class="sxs-lookup"><span data-stu-id="c9da2-161">Create some variables.</span></span> 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. <span data-ttu-id="c9da2-162">Crie o instantâneo.</span><span class="sxs-lookup"><span data-stu-id="c9da2-162">Get the snapshot.</span></span>

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. <span data-ttu-id="c9da2-163">Crie a configuração de imagem.</span><span class="sxs-lookup"><span data-stu-id="c9da2-163">Create the image configuration.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. <span data-ttu-id="c9da2-164">Crie a imagem.</span><span class="sxs-lookup"><span data-stu-id="c9da2-164">Create the image.</span></span>

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a><span data-ttu-id="c9da2-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c9da2-165">Next steps</span></span>
- <span data-ttu-id="c9da2-166">Agora você pode [criar uma VM a partir de uma imagem gerenciada generalizada](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c9da2-166">Now you can [create a VM from the generalized managed image](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>  

