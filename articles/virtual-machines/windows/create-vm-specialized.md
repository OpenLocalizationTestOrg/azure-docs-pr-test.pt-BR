---
title: aaaCreate uma VM do Windows em um VHD especializado no Azure | Microsoft Docs
description: "Crie uma nova VM do Windows, anexando um disco gerenciado especializado como disco do sistema operacional hello usando o modelo de implantação do Gerenciador de recursos de saudação."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cynthn
ms.openlocfilehash: c72c6f4fb650e2664e87cf38ec9be62f0b2209fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a><span data-ttu-id="b7d2b-103">Criar uma VM do Windos a partir de um disco especializado</span><span class="sxs-lookup"><span data-stu-id="b7d2b-103">Create a Windows VM from a specialized disk</span></span>

<span data-ttu-id="b7d2b-104">Crie uma nova VM, anexando um disco gerenciado especializado como disco do sistema operacional hello usando o Powershell.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-104">Create a new VM by attaching a specialized managed disk as hello OS disk using Powershell.</span></span> <span data-ttu-id="b7d2b-105">Um disco especializado é uma cópia do disco rígido virtual (VHD) de uma VM existente que mantém as contas de usuário hello, aplicativos e outros dados de estado da VM original.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-105">A specialized disk is a copy of virtual hard disk (VHD) from an existing VM that maintains hello user accounts, applications, and other state data from your original VM.</span></span> 

<span data-ttu-id="b7d2b-106">Quando você usa um toocreate especializada do VHD uma nova VM, Olá nova VM retém o nome do computador de saudação do hello VM original.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-106">When you use a specialized VHD toocreate a new VM, hello new VM retains hello computer name of hello original VM.</span></span> <span data-ttu-id="b7d2b-107">Outras informações específicas do computador também são mantidas e, em alguns casos, essas informações duplicadas podem causar problemas.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-107">Other computer-specific information is also be kept and, in some cases, this duplicate information could cause issues.</span></span> <span data-ttu-id="b7d2b-108">Lembre-se de que tipos de informações específicas do computador seus aplicativos dependem ao copiar uma VM.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-108">Be aware of what types of computer-specific information your applications rely on when copying a VM.</span></span>

<span data-ttu-id="b7d2b-109">Você tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="b7d2b-109">You have two options:</span></span>
* [<span data-ttu-id="b7d2b-110">Carregar um VHD</span><span class="sxs-lookup"><span data-stu-id="b7d2b-110">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="b7d2b-111">Copiar uma VM existente do Azure</span><span class="sxs-lookup"><span data-stu-id="b7d2b-111">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

<span data-ttu-id="b7d2b-112">Este tópico mostra como toouse gerenciada discos.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-112">This topic shows you how toouse managed disks.</span></span> <span data-ttu-id="b7d2b-113">Se você tiver uma implantação herdada que requer o uso de uma conta de armazenamento, consulte [Criar uma VM em um VHD especializado em uma conta de armazenamento](sa-create-vm-specialized.md)</span><span class="sxs-lookup"><span data-stu-id="b7d2b-113">If you have a legacy deployment that requires using a storage account, see [Create a VM from a specialized VHD in a storage account](sa-create-vm-specialized.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b7d2b-114">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="b7d2b-114">Before you begin</span></span>
<span data-ttu-id="b7d2b-115">Se você usar o PowerShell, certifique-se de que você tem a versão mais recente Olá de saudação módulo AzureRM.Compute PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-115">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="b7d2b-116">Para saber mais, confira [Azure PowerShell Versioning](/powershell/azure/overview) (Controle de versão do Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="b7d2b-116">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="b7d2b-117">Opção 1: Carregar um VHD especializado</span><span class="sxs-lookup"><span data-stu-id="b7d2b-117">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="b7d2b-118">Você pode carregar Olá que VHD de uma VM especializada criado com uma ferramenta de virtualização local, como o Hyper-V, ou em uma VM exportada de outra nuvem.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-118">You can upload hello VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-hello-vm"></a><span data-ttu-id="b7d2b-119">Preparar Olá VM</span><span class="sxs-lookup"><span data-stu-id="b7d2b-119">Prepare hello VM</span></span>
<span data-ttu-id="b7d2b-120">Se você pretende toouse Olá VHD como-é toocreate uma nova VM, certifique-se de saudação etapas forem concluída.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-120">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span> 
  
  * <span data-ttu-id="b7d2b-121">[Preparar um tooAzure tooupload de VHD do Windows](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b7d2b-121">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="b7d2b-122">**Não** generalizar Olá VM usando o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-122">**Do not** generalize hello VM using Sysprep.</span></span>
  * <span data-ttu-id="b7d2b-123">Remova quaisquer ferramentas de virtualização de convidado e os agentes que estão instalados na VM da saudação (como as ferramentas do VMware).</span><span class="sxs-lookup"><span data-stu-id="b7d2b-123">Remove any guest virtualization tools and agents that are installed on hello VM (like VMware tools).</span></span>
  * <span data-ttu-id="b7d2b-124">Certifique-se de saudação VM é configurada toopull seu endereço IP e as configurações de DNS por meio de DHCP.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-124">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="b7d2b-125">Isso garante que o servidor Olá obtém um endereço IP em redes de saudação quando ele é iniciado.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-125">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span> 


### <a name="get-hello-storage-account"></a><span data-ttu-id="b7d2b-126">Obter a conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="b7d2b-126">Get hello storage account</span></span>
<span data-ttu-id="b7d2b-127">Você precisa de um armazenamento de conta no Azure toostore Olá carregar o VHD.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-127">You need a storage account in Azure toostore hello uploaded VHD.</span></span> <span data-ttu-id="b7d2b-128">Você pode usar uma conta de armazenamento existente ou criar uma nova.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-128">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="b7d2b-129">as contas de armazenamento disponível Olá tooshow, digite:</span><span class="sxs-lookup"><span data-stu-id="b7d2b-129">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="b7d2b-130">Se você quiser toouse uma conta de armazenamento existente, vá toohello [carregamento Olá VHD](#upload-the-vhd-to-your-storage-account) seção.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-130">If you want toouse an existing storage account, proceed toohello [Upload hello VHD](#upload-the-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="b7d2b-131">Se você precisar toocreate uma conta de armazenamento, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="b7d2b-131">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="b7d2b-132">Você precisará nome Olá Olá do grupo de recursos onde a conta de armazenamento Olá deve ser criada.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-132">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="b7d2b-133">toofind todos os grupos de recursos Olá que estão em sua assinatura, o tipo:</span><span class="sxs-lookup"><span data-stu-id="b7d2b-133">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="b7d2b-134">toocreate um grupo de recursos denominado *myResourceGroup* em Olá *Oeste dos EUA* região, digite:</span><span class="sxs-lookup"><span data-stu-id="b7d2b-134">toocreate a resource group named *myResourceGroup* in hello *West US* region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="b7d2b-135">Criar uma conta de armazenamento denominada *mystorageaccount* neste grupo de recursos usando Olá [AzureRmStorageAccount novo](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b7d2b-135">Create a storage account named *mystorageaccount* in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="b7d2b-136">Carregar conta de armazenamento Olá VHD tooyour</span><span class="sxs-lookup"><span data-stu-id="b7d2b-136">Upload hello VHD tooyour storage account</span></span> 
<span data-ttu-id="b7d2b-137">Saudação de uso [AzureRmVhd adicionar](/powershell/module/azurerm.compute/add-azurermvhd) contêiner de tooa do VHD do cmdlet tooupload Olá em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-137">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello VHD tooa container in your storage account.</span></span> <span data-ttu-id="b7d2b-138">Este exemplo hello de carregamentos de arquivo *myVHD.vhd* de `"C:\Users\Public\Documents\Virtual hard disks\"` tooa conta de armazenamento denominada *mystorageaccount* em Olá *myResourceGroup* grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-138">This example uploads hello file *myVHD.vhd* from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named *mystorageaccount* in hello *myResourceGroup* resource group.</span></span> <span data-ttu-id="b7d2b-139">Olá arquivo é armazenado no contêiner Olá denominado *mycontainer* e o novo nome de arquivo hello serão *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-139">hello file is stored in hello container named *mycontainer* and hello new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="b7d2b-140">Se for bem-sucedido, você receberá uma resposta que parece semelhante toothis:</span><span class="sxs-lookup"><span data-stu-id="b7d2b-140">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="b7d2b-141">Dependendo de sua conexão de rede e o tamanho de saudação do arquivo VHD, este comando pode demorar um pouco toocomplete</span><span class="sxs-lookup"><span data-stu-id="b7d2b-141">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete</span></span>

### <a name="create-a-managed-disk-from-hello-vhd"></a><span data-ttu-id="b7d2b-142">Criar um disco gerenciado de saudação VHD</span><span class="sxs-lookup"><span data-stu-id="b7d2b-142">Create a managed disk from hello VHD</span></span>

<span data-ttu-id="b7d2b-143">Criar um disco gerenciado de saudação especializado VHD em sua conta de armazenamento usando [AzureRMDisk novo](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="b7d2b-143">Create a managed disk from hello specialized VHD in your storage account using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="b7d2b-144">Este exemplo usa **myOSDisk1** para o nome do disco hello, coloca Olá disco em *StandardLRS* armazenamento e usa *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* como hello URI para o VHD de origem hello.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-144">This example uses **myOSDisk1** for hello disk name, puts hello disk in *StandardLRS* storage, and uses *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* as hello URI for hello source VHD.</span></span>

<span data-ttu-id="b7d2b-145">Criar um novo grupo de recursos para Olá nova VM.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-145">Create a new resource group for hello new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="b7d2b-146">Criar novo disco de SO Olá da saudação carregar o VHD.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-146">Create hello new OS disk from hello uploaded VHD.</span></span> 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a><span data-ttu-id="b7d2b-147">Opção 2: Copiar uma VM existente do Azure</span><span class="sxs-lookup"><span data-stu-id="b7d2b-147">Option 2: Copy an existing Azure VM</span></span>

<span data-ttu-id="b7d2b-148">Você pode criar uma cópia de uma VM que usa discos gerenciado por tirar um instantâneo de VM de saudação, em seguida, usando esse Instantâneo toocreate gerenciado um novo disco e uma nova VM.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-148">You can create a copy of a VM that uses managed disks by taking a snapshot of hello VM, then using that snapshot toocreate a new managed disk and a new VM.</span></span>


### <a name="take-a-snapshot-of-hello-os-disk"></a><span data-ttu-id="b7d2b-149">Tirar um instantâneo do disco do sistema operacional Olá</span><span class="sxs-lookup"><span data-stu-id="b7d2b-149">Take a snapshot of hello OS disk</span></span>

<span data-ttu-id="b7d2b-150">Você pode tirar um instantâneo de toda a VM (incluindo todos os discos) ou apenas um único disco.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-150">You can take a snapshot of and entire VM (including all disks) or of just a single disk.</span></span> <span data-ttu-id="b7d2b-151">Olá etapas a seguir mostram como tootake um instantâneo do disco de saudação SO apenas do VM usando Olá [AzureRmSnapshot novo](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-151">hello following steps show you how tootake a snapshot of just hello OS disk of your VM using hello [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span></span> 

<span data-ttu-id="b7d2b-152">Defina alguns parâmetros.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-152">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

<span data-ttu-id="b7d2b-153">Obtenha o objeto da VM de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-153">Get hello VM object.</span></span>

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
<span data-ttu-id="b7d2b-154">Obter o nome do disco Olá sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-154">Get hello OS disk name.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

<span data-ttu-id="b7d2b-155">Crie configuração de saudação de instantâneo.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-155">Create hello snapshot configuration.</span></span> 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

<span data-ttu-id="b7d2b-156">Tire instantâneo hello.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-156">Take hello snapshot.</span></span>

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


<span data-ttu-id="b7d2b-157">Se você planejar toouse Olá instantâneo toocreate uma VM que precisa toobe alto desempenho, use o parâmetro hello `-AccountType Premium_LRS` com o comando Olá AzureRmSnapshot de novo.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-157">If you plan toouse hello snapshot toocreate a VM that needs toobe high performing, use hello parameter `-AccountType Premium_LRS` with hello New-AzureRmSnapshot command.</span></span> <span data-ttu-id="b7d2b-158">parâmetro Hello cria o instantâneo de saudação para que ela é armazenada como um disco de gerenciado para Premium.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-158">hello parameter creates hello snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="b7d2b-159">Os Discos Gerenciados Premium são mais caros que os Standard.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-159">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="b7d2b-160">Portanto certifique-se de que você realmente precisa Premium antes de usar o parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-160">So be sure you really need Premium before using hello parameter.</span></span>

### <a name="create-a-new-disk-from-hello-snapshot"></a><span data-ttu-id="b7d2b-161">Criar um novo disco de instantâneo Olá</span><span class="sxs-lookup"><span data-stu-id="b7d2b-161">Create a new disk from hello snapshot</span></span>

<span data-ttu-id="b7d2b-162">Criar um disco gerenciado de saudação instantâneo usando [AzureRMDisk novo](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="b7d2b-162">Create a managed disk from hello snapshot using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="b7d2b-163">Este exemplo usa *myOSDisk* para o nome do disco hello.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-163">This example uses *myOSDisk* for hello disk name.</span></span>

<span data-ttu-id="b7d2b-164">Criar um novo grupo de recursos para Olá nova VM.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-164">Create a new resource group for hello new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="b7d2b-165">Definir nome de disco Olá sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-165">Set hello OS disk name.</span></span> 

```powershell
$osDiskName = 'myOsDisk'
```

<span data-ttu-id="b7d2b-166">Crie disco de saudação gerenciado.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-166">Create hello managed disk.</span></span>

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-hello-new-vm"></a><span data-ttu-id="b7d2b-167">Criar hello nova VM</span><span class="sxs-lookup"><span data-stu-id="b7d2b-167">Create hello new VM</span></span> 

<span data-ttu-id="b7d2b-168">Criar rede e outros toobe de recursos VM usada pelo Olá nova VM.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-168">Create networking and other VM resources toobe used by hello new VM.</span></span>

### <a name="create-hello-subnet-and-vnet"></a><span data-ttu-id="b7d2b-169">Criar rede virtual e a sub-rede de saudação</span><span class="sxs-lookup"><span data-stu-id="b7d2b-169">Create hello subNet and vNet</span></span>

<span data-ttu-id="b7d2b-170">Criar rede virtual de saudação e a sub-rede de saudação [rede virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b7d2b-170">Create hello vNet and subNet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="b7d2b-171">Crie uma sub-rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-171">Create hello subNet.</span></span> <span data-ttu-id="b7d2b-172">Este exemplo cria uma sub-rede denominada **mySubNet**, no grupo de recursos de saudação **myDestinationResourceGroup**, e define Olá prefixo de endereço de sub-rede muito**10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-172">This example creates a subnet named **mySubNet**, in hello resource group **myDestinationResourceGroup**, and sets hello subnet address prefix too**10.0.0.0/24**.</span></span>
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="b7d2b-173">Crie rede virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-173">Create hello vNet.</span></span> <span data-ttu-id="b7d2b-174">Este exemplo define Olá toobe de nome de rede virtual **myVnetName**, Olá local muito**Oeste dos EUA**, e Olá prefixo de endereço de rede virtual Olá muito**10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-174">This example sets hello virtual network name toobe **myVnetName**, hello location too**West US**, and hello address prefix for hello virtual network too**10.0.0.0/16**.</span></span> 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="b7d2b-175">Criar um grupo de segurança de rede hello e uma regra RDP</span><span class="sxs-lookup"><span data-stu-id="b7d2b-175">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="b7d2b-176">toolog capaz de toobe em tooyour VM usando o RDP, você precisa toohave uma regra de segurança que permita o acesso RDP na porta 3389.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-176">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="b7d2b-177">Porque hello VHD para Olá nova VM foi criada a partir de uma VM especializada existente, você pode usar uma conta da máquina de virtual de origem Olá para RDP.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-177">Because hello VHD for hello new VM was created from an existing specialized VM, you can use an account from hello source virtual machine for RDP.</span></span>

<span data-ttu-id="b7d2b-178">Este exemplo define Olá nome NSG muito**myNsg** e Olá RDP nome da regra muito**myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-178">This example sets hello NSG name too**myNsg** and hello RDP rule name too**myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="b7d2b-179">Para obter mais informações sobre pontos de extremidade e regras NSG, consulte [a abertura de portas tooa VM no Azure usando o PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b7d2b-179">For more information about endpoints and NSG rules, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="b7d2b-180">Criar um endereço IP público e uma NIC</span><span class="sxs-lookup"><span data-stu-id="b7d2b-180">Create a public IP address and NIC</span></span>
<span data-ttu-id="b7d2b-181">comunicação tooenable com máquina virtual de saudação na rede virtual Olá, é necessário um [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e uma interface de rede.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-181">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

<span data-ttu-id="b7d2b-182">Crie o IP público hello.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-182">Create hello public IP.</span></span> <span data-ttu-id="b7d2b-183">Neste exemplo, nome do endereço IP público hello está definido muito**myIP**.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-183">In this example, hello public IP address name is set too**myIP**.</span></span>
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

<span data-ttu-id="b7d2b-184">Criar NIC hello.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-184">Create hello NIC.</span></span> <span data-ttu-id="b7d2b-185">Neste exemplo, o nome NIC do hello está definido muito**myNicName**.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-185">In this example, hello NIC name is set too**myNicName**.</span></span>
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-hello-vm-name-and-size"></a><span data-ttu-id="b7d2b-186">Definir nome VM hello e tamanho</span><span class="sxs-lookup"><span data-stu-id="b7d2b-186">Set hello VM name and size</span></span>

<span data-ttu-id="b7d2b-187">Este exemplo define Olá nome da VM muito*myVM* e Olá VM muito o tamanho*Standard_A2*.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-187">This example sets hello VM name too*myVM* and hello VM size too*Standard_A2*.</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a><span data-ttu-id="b7d2b-188">Adicionar Olá NIC</span><span class="sxs-lookup"><span data-stu-id="b7d2b-188">Add hello NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-hello-os-disk"></a><span data-ttu-id="b7d2b-189">Adicionar disco Olá SO</span><span class="sxs-lookup"><span data-stu-id="b7d2b-189">Add hello OS disk</span></span> 

<span data-ttu-id="b7d2b-190">Adicionar configuração usando o hello OS disco toohello [AzureRmVMOSDisk conjunto](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="b7d2b-190">Add hello OS disk toohello configuration using [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span> <span data-ttu-id="b7d2b-191">Este exemplo define o tamanho de saudação do disco de saudação muito*128 GB* e anexa o disco Olá gerenciado como um *Windows* disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-191">This example sets hello size of hello disk too*128 GB* and attaches hello managed disk as a *Windows* OS disk.</span></span>
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-hello-vm"></a><span data-ttu-id="b7d2b-192">Concluir Olá VM</span><span class="sxs-lookup"><span data-stu-id="b7d2b-192">Complete hello VM</span></span> 

<span data-ttu-id="b7d2b-193">Criar hello VM usando [AzureRMVM novo](/powershell/module/azurerm.compute/new-azurermvm)Olá configurações que acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-193">Create hello VM using [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)hello configurations that we just created.</span></span>

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

<span data-ttu-id="b7d2b-194">Se o comando for bem-sucedido, você verá uma saída como esta:</span><span class="sxs-lookup"><span data-stu-id="b7d2b-194">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="b7d2b-195">Verifique se esse Olá que VM foi criada</span><span class="sxs-lookup"><span data-stu-id="b7d2b-195">Verify that hello VM was created</span></span>
<span data-ttu-id="b7d2b-196">Você deve ver Olá recém-criado VM em Olá [portal do Azure](https://portal.azure.com), em **procurar** > **máquinas virtuais**, ou por meio de saudação do PowerShell a seguir comandos:</span><span class="sxs-lookup"><span data-stu-id="b7d2b-196">You should see hello newly created VM either in hello [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="b7d2b-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b7d2b-197">Next steps</span></span>
<span data-ttu-id="b7d2b-198">toosign em tooyour nova máquina virtual toohello procurar VM em Olá [portal](https://portal.azure.com), clique em **conectar**e abra Olá o RDP.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-198">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="b7d2b-199">Use credenciais de conta de saudação do seu toosign de máquina virtual original na nova máquina de virtual tooyour.</span><span class="sxs-lookup"><span data-stu-id="b7d2b-199">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="b7d2b-200">Para obter mais informações, consulte [como tooconnect e logon tooan virtuais do Azure do computador que executa o Windows](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="b7d2b-200">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md).</span></span>

