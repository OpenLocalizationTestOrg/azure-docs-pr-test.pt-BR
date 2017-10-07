---
title: aaaCreate VM de um disco especializado no Azure | Microsoft Docs
description: "Crie uma nova VM anexando um disco especializado não gerenciado, no modelo de implantação do Gerenciador de recursos de saudação."
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: c88f213b6629a6c1d6ff5845e76c2f7719672714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a><span data-ttu-id="45550-103">Criar uma VM a partir de um VHD especializado em uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="45550-103">Create a VM from a specialized VHD in a storage account</span></span>

<span data-ttu-id="45550-104">Crie uma nova VM anexando um disco especializado de não gerenciado, como o disco do sistema operacional hello usando o Powershell.</span><span class="sxs-lookup"><span data-stu-id="45550-104">Create a new VM by attaching a specialized unmanaged disk as hello OS disk using Powershell.</span></span> <span data-ttu-id="45550-105">Um disco especializado é uma cópia do VHD de uma VM existente que mantém as contas de usuário hello, aplicativos e outros dados de estado da VM original.</span><span class="sxs-lookup"><span data-stu-id="45550-105">A specialized disk is a copy of VHD from an existing VM that maintains hello user accounts, applications and other state data from your original VM.</span></span> 

<span data-ttu-id="45550-106">Você tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="45550-106">You have two options:</span></span>
* [<span data-ttu-id="45550-107">Carregar um VHD</span><span class="sxs-lookup"><span data-stu-id="45550-107">Upload a VHD</span></span>](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="45550-108">Copiar Olá VHD de uma VM existente do Azure</span><span class="sxs-lookup"><span data-stu-id="45550-108">Copy hello VHD of an existing Azure VM</span></span>](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a><span data-ttu-id="45550-109">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="45550-109">Before you begin</span></span>
<span data-ttu-id="45550-110">Se você usar o PowerShell, certifique-se de que você tem a versão mais recente Olá de saudação módulo AzureRM.Compute PowerShell.</span><span class="sxs-lookup"><span data-stu-id="45550-110">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="45550-111">Executar Olá tooinstall de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="45550-111">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute 
```
<span data-ttu-id="45550-112">Para saber mais, confira [Azure PowerShell Versioning](/powershell/azure/overview) (Controle de versão do Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="45550-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="45550-113">Opção 1: Carregar um VHD especializado</span><span class="sxs-lookup"><span data-stu-id="45550-113">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="45550-114">Você pode carregar Olá que VHD de uma VM especializada criado com uma ferramenta de virtualização local, como o Hyper-V, ou em uma VM exportada de outra nuvem.</span><span class="sxs-lookup"><span data-stu-id="45550-114">You can upload hello VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-hello-vm"></a><span data-ttu-id="45550-115">Preparar Olá VM</span><span class="sxs-lookup"><span data-stu-id="45550-115">Prepare hello VM</span></span>
<span data-ttu-id="45550-116">Você pode carregar um VHD especializado que foi criado usando uma VM local ou um VHD exportado de outra nuvem.</span><span class="sxs-lookup"><span data-stu-id="45550-116">You can upload a specialized VHD that was created using an on-premises VM or a VHD exported from another cloud.</span></span> <span data-ttu-id="45550-117">Um VHD especializado mantém as contas de usuário hello, aplicativos e outros dados de estado da VM original.</span><span class="sxs-lookup"><span data-stu-id="45550-117">A specialized VHD maintains hello user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="45550-118">Se você pretende toouse Olá VHD como-é toocreate uma nova VM, certifique-se de saudação etapas forem concluída.</span><span class="sxs-lookup"><span data-stu-id="45550-118">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span> 
  
  * <span data-ttu-id="45550-119">[Preparar um tooAzure tooupload de VHD do Windows](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="45550-119">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="45550-120">**Não** generalizar Olá VM usando o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="45550-120">**Do not** generalize hello VM using Sysprep.</span></span>
  * <span data-ttu-id="45550-121">Remova quaisquer ferramentas de virtualização de convidado e os agentes instalados em Olá VM (ou seja, as ferramentas do VMware).</span><span class="sxs-lookup"><span data-stu-id="45550-121">Remove any guest virtualization tools and agents that are installed on hello VM (i.e. VMware tools).</span></span>
  * <span data-ttu-id="45550-122">Certifique-se de saudação VM é configurada toopull seu endereço IP e as configurações de DNS por meio de DHCP.</span><span class="sxs-lookup"><span data-stu-id="45550-122">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="45550-123">Isso garante que o servidor Olá obtém um endereço IP em redes de saudação quando ele é iniciado.</span><span class="sxs-lookup"><span data-stu-id="45550-123">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span> 


### <a name="get-hello-storage-account"></a><span data-ttu-id="45550-124">Obter a conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="45550-124">Get hello storage account</span></span>
<span data-ttu-id="45550-125">Você precisa de uma conta de armazenamento na imagem VM do Azure toostore Olá carregado.</span><span class="sxs-lookup"><span data-stu-id="45550-125">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="45550-126">Você pode usar uma conta de armazenamento existente ou criar uma nova.</span><span class="sxs-lookup"><span data-stu-id="45550-126">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="45550-127">as contas de armazenamento disponível Olá tooshow, digite:</span><span class="sxs-lookup"><span data-stu-id="45550-127">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="45550-128">Se você quiser toouse uma conta de armazenamento existente, vá toohello [carregar imagem VM Olá](#upload-the-vm-vhd-to-your-storage-account) seção.</span><span class="sxs-lookup"><span data-stu-id="45550-128">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="45550-129">Se você precisar toocreate uma conta de armazenamento, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="45550-129">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="45550-130">Você precisará nome Olá Olá do grupo de recursos onde a conta de armazenamento Olá deve ser criada.</span><span class="sxs-lookup"><span data-stu-id="45550-130">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="45550-131">toofind todos os grupos de recursos Olá que estão em sua assinatura, o tipo:</span><span class="sxs-lookup"><span data-stu-id="45550-131">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="45550-132">toocreate um grupo de recursos denominado **myResourceGroup** em Olá **Oeste dos EUA** região, digite:</span><span class="sxs-lookup"><span data-stu-id="45550-132">toocreate a resource group named **myResourceGroup** in hello **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="45550-133">Criar uma conta de armazenamento denominada **mystorageaccount** neste grupo de recursos usando Olá [AzureRmStorageAccount novo](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="45550-133">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
### <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="45550-134">Carregar conta de armazenamento Olá VHD tooyour</span><span class="sxs-lookup"><span data-stu-id="45550-134">Upload hello VHD tooyour storage account</span></span>
<span data-ttu-id="45550-135">Saudação de uso [AzureRmVhd adicionar](/powershell/module/azurerm.compute/add-azurermvhd) contêiner do cmdlet tooupload Olá imagem tooa na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="45550-135">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello image tooa container in your storage account.</span></span> <span data-ttu-id="45550-136">Este exemplo hello de carregamentos de arquivo **myVHD.vhd** de `"C:\Users\Public\Documents\Virtual hard disks\"` tooa conta de armazenamento denominada **mystorageaccount** em Olá **myResourceGroup** grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="45550-136">This example uploads hello file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named **mystorageaccount** in hello **myResourceGroup** resource group.</span></span> <span data-ttu-id="45550-137">arquivo Hello será colocado no contêiner Olá denominado **mycontainer** e o novo nome de arquivo hello serão **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="45550-137">hello file will be placed into hello container named **mycontainer** and hello new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="45550-138">Se for bem-sucedido, você receberá uma resposta que parece semelhante toothis:</span><span class="sxs-lookup"><span data-stu-id="45550-138">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="45550-139">Dependendo de sua conexão de rede e o tamanho de saudação do arquivo VHD, este comando pode demorar um pouco toocomplete.</span><span class="sxs-lookup"><span data-stu-id="45550-139">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete.</span></span>


## <a name="option-2-copy-hello-vhd-from-an-existing-azure-vm"></a><span data-ttu-id="45550-140">Opção 2: Copiar Olá VHD de uma VM existente do Azure</span><span class="sxs-lookup"><span data-stu-id="45550-140">Option 2: Copy hello VHD from an existing Azure VM</span></span>

<span data-ttu-id="45550-141">Você pode copiar um toouse de conta de armazenamento do VHD tooanother ao criar uma VM de novo, duplicada.</span><span class="sxs-lookup"><span data-stu-id="45550-141">You can copy a VHD tooanother storage account toouse when creating a new, duplicate VM.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="45550-142">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="45550-142">Before you begin</span></span>
<span data-ttu-id="45550-143">Lembre-se de:</span><span class="sxs-lookup"><span data-stu-id="45550-143">Make sure that you:</span></span>

* <span data-ttu-id="45550-144">Obter informações sobre a saudação **contas de armazenamento de origem e destino**.</span><span class="sxs-lookup"><span data-stu-id="45550-144">Have information about hello **source and destination storage accounts**.</span></span> <span data-ttu-id="45550-145">Para saudação de VM de origem, você precisa de nomes de conta e o contêiner de armazenamento de saudação do toohave.</span><span class="sxs-lookup"><span data-stu-id="45550-145">For hello source VM, you need toohave hello storage account and container names.</span></span> <span data-ttu-id="45550-146">Normalmente, o nome de contêiner de Olá será **vhds**.</span><span class="sxs-lookup"><span data-stu-id="45550-146">Usually, hello container name will be **vhds**.</span></span> <span data-ttu-id="45550-147">Você também precisa toohave uma conta de armazenamento de destino.</span><span class="sxs-lookup"><span data-stu-id="45550-147">You also need toohave a destination storage account.</span></span> <span data-ttu-id="45550-148">Se você ainda não tiver um, você pode criar um usando o portal de saudação (**mais serviços** > contas de armazenamento > Adicionar) ou usando Olá [AzureRmStorageAccount novo](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="45550-148">If you don't already have one, you can create one using either hello portal (**More Services** > Storage accounts > Add) or using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet.</span></span> 
* <span data-ttu-id="45550-149">Baixar e instalar Olá [ferramenta AzCopy](../../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="45550-149">Have downloaded and installed hello [AzCopy tool](../../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="deallocate-hello-vm"></a><span data-ttu-id="45550-150">Desalocar Olá VM</span><span class="sxs-lookup"><span data-stu-id="45550-150">Deallocate hello VM</span></span>
<span data-ttu-id="45550-151">Desaloque Olá VM, o que libera Olá VHD toobe copiado.</span><span class="sxs-lookup"><span data-stu-id="45550-151">Deallocate hello VM, which frees up hello VHD toobe copied.</span></span> 

* <span data-ttu-id="45550-152">**Portal**: clique em **Máquinas virtuais** > **myVM** > Parar</span><span class="sxs-lookup"><span data-stu-id="45550-152">**Portal**: Click **Virtual machines** > **myVM** > Stop</span></span>
* <span data-ttu-id="45550-153">**PowerShell**: Use [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (desalocar) Olá VM denominada **myVM** no grupo de recursos **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="45550-153">**Powershell**: Use [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (deallocate) hello VM named **myVM** in resource group **myResourceGroup**.</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="45550-154">Olá **Status** para Olá VM em hello Azure portal muda de **parado** muito**parado (desalocado)**.</span><span class="sxs-lookup"><span data-stu-id="45550-154">hello **Status** for hello VM in hello Azure portal changes from **Stopped** too**Stopped (deallocated)**.</span></span>

### <a name="get-hello-storage-account-urls"></a><span data-ttu-id="45550-155">Obter Olá URLs de conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="45550-155">Get hello storage account URLs</span></span>
<span data-ttu-id="45550-156">Você precisa de URLs Olá Olá origem e destino de contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="45550-156">You need hello URLs of hello source and destination storage accounts.</span></span> <span data-ttu-id="45550-157">Olá URLs se parecer com: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span><span class="sxs-lookup"><span data-stu-id="45550-157">hello URLs look like: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span></span> <span data-ttu-id="45550-158">Se você já souber o nome da conta e o contêiner de armazenamento hello, pode apenas substituir Olá informações entre Olá colchetes toocreate sua URL.</span><span class="sxs-lookup"><span data-stu-id="45550-158">If you already know hello storage account and container name, you can just replace hello information between hello brackets toocreate your URL.</span></span> 

<span data-ttu-id="45550-159">Você pode usar o hello portal do Azure ou Azure Powershell tooget Olá URL:</span><span class="sxs-lookup"><span data-stu-id="45550-159">You can use hello Azure portal or Azure Powershell tooget hello URL:</span></span>

* <span data-ttu-id="45550-160">**Portal**: clique em Olá  **>**  para **mais serviços** > **contas de armazenamento**  >   *conta de armazenamento* > **Blobs** e seu arquivo VHD de origem provavelmente está em Olá **vhds** contêiner.</span><span class="sxs-lookup"><span data-stu-id="45550-160">**Portal**: Click hello **>** for **More services** > **Storage accounts** > *storage account* > **Blobs** and your source VHD file is probably in hello **vhds** container.</span></span> <span data-ttu-id="45550-161">Clique em **propriedades** para contêiner hello e copiar texto de saudação rotulada **URL**.</span><span class="sxs-lookup"><span data-stu-id="45550-161">Click **Properties** for hello container, and copy hello text labeled **URL**.</span></span> <span data-ttu-id="45550-162">Você precisará Olá URLs de ambos os contêineres de origem e destino hello.</span><span class="sxs-lookup"><span data-stu-id="45550-162">You'll need hello URLs of both hello source and destination containers.</span></span> 
* <span data-ttu-id="45550-163">**PowerShell**: Use [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget informações Olá VM denominada **myVM** no grupo de recursos de saudação **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="45550-163">**Powershell**: Use [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget hello information for VM named **myVM** in hello resource group **myResourceGroup**.</span></span> <span data-ttu-id="45550-164">Nos resultados de hello, examinar Olá **perfil de armazenamento** seção para Olá **Uri do Vhd**.</span><span class="sxs-lookup"><span data-stu-id="45550-164">In hello results, look in hello **Storage profile** section for hello **Vhd Uri**.</span></span> <span data-ttu-id="45550-165">primeira parte Olá Olá Uri é contêiner de toohello URL hello e Olá última parte é Olá nome do VHD do sistema operacional para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="45550-165">hello first part of hello Uri is hello URL toohello container and hello last part is hello OS VHD name for hello VM.</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-hello-storage-access-keys"></a><span data-ttu-id="45550-166">Obter chaves de acesso de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="45550-166">Get hello storage access keys</span></span>
<span data-ttu-id="45550-167">Localize chaves de acesso de saudação para Olá contas de armazenamento de origem e de destino.</span><span class="sxs-lookup"><span data-stu-id="45550-167">Find hello access keys for hello source and destination storage accounts.</span></span> <span data-ttu-id="45550-168">Para obter mais informações sobre as chaves de acesso, consulte [Sobre as contas de armazenamento do Azure](../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="45550-168">For more information about access keys, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span></span>

* <span data-ttu-id="45550-169">**Portal**: Clique em **Mais serviços** > **Contas de armazenamento** > *conta de armazenamento* > **Chaves de acesso**.</span><span class="sxs-lookup"><span data-stu-id="45550-169">**Portal**: Click **More services** > **Storage accounts** > *storage account* > **Access keys**.</span></span> <span data-ttu-id="45550-170">Copiar a chave de saudação rotulado como **key1**.</span><span class="sxs-lookup"><span data-stu-id="45550-170">Copy hello key labeled as **key1**.</span></span>
* <span data-ttu-id="45550-171">**PowerShell**: Use [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget Olá armazenamento chave Olá conta de armazenamento **mystorageaccount** no grupo de recursos de saudação  **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="45550-171">**Powershell**: Use [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello storage key for hello storage account **mystorageaccount** in hello resource group **myResourceGroup**.</span></span> <span data-ttu-id="45550-172">Copiar chave de saudação rotulada **key1**.</span><span class="sxs-lookup"><span data-stu-id="45550-172">Copy hello key labeled **key1**.</span></span>

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-hello-vhd"></a><span data-ttu-id="45550-173">Copiar Olá VHD</span><span class="sxs-lookup"><span data-stu-id="45550-173">Copy hello VHD</span></span>
<span data-ttu-id="45550-174">Você pode copiar arquivos entre as contas de armazenamento usando o AzCopy.</span><span class="sxs-lookup"><span data-stu-id="45550-174">You can copy files between storage accounts using AzCopy.</span></span> <span data-ttu-id="45550-175">Para o contêiner de destino hello, se o contêiner de saudação especificado não existir, ele será criado para você.</span><span class="sxs-lookup"><span data-stu-id="45550-175">For hello destination container, if hello specified container doesn't exist, it will be created for you.</span></span> 

<span data-ttu-id="45550-176">toouse AzCopy, abra um prompt de comando no computador local e navegue pasta toohello onde AzCopy é instalado.</span><span class="sxs-lookup"><span data-stu-id="45550-176">toouse AzCopy, open a command prompt on your local machine and navigate toohello folder where AzCopy is installed.</span></span> <span data-ttu-id="45550-177">Ele será semelhante a muito*C:\Program Files (x86) \Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="45550-177">It will be similar too*C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy*.</span></span> 

<span data-ttu-id="45550-178">toocopy todos Olá arquivos dentro de um contêiner, que você usar o hello **/S** alternar.</span><span class="sxs-lookup"><span data-stu-id="45550-178">toocopy all of hello files within a container, you use hello **/S** switch.</span></span> <span data-ttu-id="45550-179">Isso pode ser usado toocopy Olá VHD do sistema operacional e todos os discos de dados Olá se eles estiverem em Olá mesmo contêiner.</span><span class="sxs-lookup"><span data-stu-id="45550-179">This can be used toocopy hello OS VHD and all of hello data disks if they are in hello same container.</span></span> <span data-ttu-id="45550-180">Este exemplo mostra como toocopy todos Olá arquivos no contêiner Olá **mysourcecontainer** na conta de armazenamento **mysourcestorageaccount** toohello contêiner **mydestinationcontainer**  em Olá **mydestinationstorageaccount** conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="45550-180">This example shows how toocopy all of hello files in hello container **mysourcecontainer** in storage account **mysourcestorageaccount** toohello container **mydestinationcontainer** in hello **mydestinationstorageaccount** storage account.</span></span> <span data-ttu-id="45550-181">Substitua os nomes de saudação de contas de armazenamento hello e contêineres com seus próprios.</span><span class="sxs-lookup"><span data-stu-id="45550-181">Replace hello names of hello storage accounts and containers with your own.</span></span> <span data-ttu-id="45550-182">Substitua `<sourceStorageAccountKey1>` e `<destinationStorageAccountKey1>` pelas suas próprias chaves.</span><span class="sxs-lookup"><span data-stu-id="45550-182">Replace `<sourceStorageAccountKey1>` and `<destinationStorageAccountKey1>` with your own keys.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

<span data-ttu-id="45550-183">Se você desejar somente toocopy um VHD específico em um contêiner com vários arquivos, você também pode especificar nome do arquivo hello usando Olá /Pattern comutador.</span><span class="sxs-lookup"><span data-stu-id="45550-183">If you only want toocopy a specific VHD in a container with multiple files, you can also specify hello file name using hello /Pattern switch.</span></span> <span data-ttu-id="45550-184">Neste exemplo, Olá somente o arquivo chamado **myFileName.vhd** serão copiados.</span><span class="sxs-lookup"><span data-stu-id="45550-184">In this example, only hello file named **myFileName.vhd** will be copied.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


<span data-ttu-id="45550-185">Quando ele for concluído, você receberá uma mensagem como a seguinte:</span><span class="sxs-lookup"><span data-stu-id="45550-185">When it is finished, you will get a message that looks something like:</span></span>

```
Finished 2 of total 2 file(s).
[2016/10/07 17:37:41] Transfer summary:
-----------------
Total files transferred: 2
Transfer successfully:   2
Transfer skipped:        0
Transfer failed:         0
Elapsed time:            00.00:13:07
```

### <a name="troubleshooting"></a><span data-ttu-id="45550-186">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="45550-186">Troubleshooting</span></span>
* <span data-ttu-id="45550-187">Quando você usa AZCopy, se você vir o erro hello "Servidor falha na solicitação de saudação tooauthenticate", certifique-se de valor de saudação do cabeçalho de autorização hello está formado corretamente e inclui assinatura hello.</span><span class="sxs-lookup"><span data-stu-id="45550-187">When you use AZCopy, if you see hello error "Server failed tooauthenticate hello request", make sure hello value of hello Authorization header is formed correctly including hello signature.</span></span> <span data-ttu-id="45550-188">Se você estiver usando a chave 2 ou a chave de armazenamento secundário hello, tente usar chave de armazenamento principal ou 1º hello.</span><span class="sxs-lookup"><span data-stu-id="45550-188">If you are using Key 2 or hello secondary storage key, try using hello primary or 1st storage key.</span></span>

## <a name="create-hello-new-vm"></a><span data-ttu-id="45550-189">Criar hello nova VM</span><span class="sxs-lookup"><span data-stu-id="45550-189">Create hello new VM</span></span> 

<span data-ttu-id="45550-190">Você precisa de rede toocreate e outros toobe de recursos VM usada pelo Olá nova VM.</span><span class="sxs-lookup"><span data-stu-id="45550-190">You need toocreate networking and other VM resources toobe used by hello new VM.</span></span>

### <a name="create-hello-subnet-and-vnet"></a><span data-ttu-id="45550-191">Criar rede virtual e a sub-rede de saudação</span><span class="sxs-lookup"><span data-stu-id="45550-191">Create hello subNet and vNet</span></span>

<span data-ttu-id="45550-192">Criar rede virtual de saudação e a sub-rede de saudação [rede virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="45550-192">Create hello vNet and subNet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="45550-193">Crie uma sub-rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="45550-193">Create hello subNet.</span></span> <span data-ttu-id="45550-194">Este exemplo cria uma sub-rede denominada **mySubNet**, no grupo de recursos de saudação **myResourceGroup**, e define Olá prefixo de endereço de sub-rede muito**10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="45550-194">This example creates a subnet named **mySubNet**, in hello resource group **myResourceGroup**, and sets hello subnet address prefix too**10.0.0.0/24**.</span></span>
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="45550-195">Crie rede virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="45550-195">Create hello vNet.</span></span> <span data-ttu-id="45550-196">Este exemplo define Olá toobe de nome de rede virtual **myVnetName**, Olá local muito**Oeste dos EUA**, e Olá prefixo de endereço de rede virtual Olá muito**10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="45550-196">This example sets hello virtual network name toobe **myVnetName**, hello location too**West US**, and hello address prefix for hello virtual network too**10.0.0.0/16**.</span></span> 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="45550-197">Criar um endereço IP público e uma NIC</span><span class="sxs-lookup"><span data-stu-id="45550-197">Create a public IP address and NIC</span></span>
<span data-ttu-id="45550-198">comunicação tooenable com máquina virtual de saudação na rede virtual Olá, é necessário um [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e uma interface de rede.</span><span class="sxs-lookup"><span data-stu-id="45550-198">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="45550-199">Crie o IP público hello.</span><span class="sxs-lookup"><span data-stu-id="45550-199">Create hello public IP.</span></span> <span data-ttu-id="45550-200">Neste exemplo, nome do endereço IP público hello está definido muito**myIP**.</span><span class="sxs-lookup"><span data-stu-id="45550-200">In this example, hello public IP address name is set too**myIP**.</span></span>
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="45550-201">Criar NIC hello.</span><span class="sxs-lookup"><span data-stu-id="45550-201">Create hello NIC.</span></span> <span data-ttu-id="45550-202">Neste exemplo, o nome NIC do hello está definido muito**myNicName**.</span><span class="sxs-lookup"><span data-stu-id="45550-202">In this example, hello NIC name is set too**myNicName**.</span></span>
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="45550-203">Criar um grupo de segurança de rede hello e uma regra RDP</span><span class="sxs-lookup"><span data-stu-id="45550-203">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="45550-204">toolog capaz de toobe em tooyour VM usando o RDP, você precisa toohave uma regra de segurança que permita o acesso RDP na porta 3389.</span><span class="sxs-lookup"><span data-stu-id="45550-204">toobe able toolog in tooyour VM using RDP, you need toohave an security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="45550-205">Porque hello VHD para Olá que nova VM foi criada a partir de um existente especializado VM, depois Olá VM for criado, você pode usar uma conta existente na máquina de virtual de origem Olá que tiveram permissão toolog sobre como usar o RDP.</span><span class="sxs-lookup"><span data-stu-id="45550-205">Because hello VHD for hello new VM was created from an existing specialized VM, after hello VM is created you can use an existing account from hello source virtual machine that had permission toolog on using RDP.</span></span>
<span data-ttu-id="45550-206">Este exemplo define Olá nome NSG muito**myNsg** e Olá RDP nome da regra muito**myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="45550-206">This example sets hello NSG name too**myNsg** and hello RDP rule name too**myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="45550-207">Para obter mais informações sobre pontos de extremidade e regras NSG, consulte [a abertura de portas tooa VM no Azure usando o PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="45550-207">For more information about endpoints and NSG rules, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="set-hello-vm-name-and-size"></a><span data-ttu-id="45550-208">Definir nome VM hello e tamanho</span><span class="sxs-lookup"><span data-stu-id="45550-208">Set hello VM name and size</span></span>

<span data-ttu-id="45550-209">Este exemplo define Olá nome da VM muito "myVM" e Olá VM tamanho muito "Standard_A2".</span><span class="sxs-lookup"><span data-stu-id="45550-209">This example sets hello VM name too"myVM" and hello VM size too"Standard_A2".</span></span>
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a><span data-ttu-id="45550-210">Adicionar Olá NIC</span><span class="sxs-lookup"><span data-stu-id="45550-210">Add hello NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-hello-os-disk"></a><span data-ttu-id="45550-211">Configurar o disco Olá SO</span><span class="sxs-lookup"><span data-stu-id="45550-211">Configure hello OS disk</span></span>

1. <span data-ttu-id="45550-212">Defina hello URI para Olá VHD carregado ou copiado.</span><span class="sxs-lookup"><span data-stu-id="45550-212">Set hello URI for hello VHD that you uploaded or copied.</span></span> <span data-ttu-id="45550-213">Neste exemplo, Olá arquivo do VHD chamado **myOsDisk.vhd** é mantido em uma conta de armazenamento denominada **myStorageAccount** em um contêiner chamado **myContainer**.</span><span class="sxs-lookup"><span data-stu-id="45550-213">In this example, hello VHD file named **myOsDisk.vhd** is kept in a storage account named **myStorageAccount** in a container named **myContainer**.</span></span>

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. <span data-ttu-id="45550-214">Adicione disco Olá sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="45550-214">Add hello OS disk.</span></span> <span data-ttu-id="45550-215">Neste exemplo, quando Olá disco do sistema operacional é criado, Olá termo "osDisk" é appened toohello VM nome toocreate Olá SO nome do disco.</span><span class="sxs-lookup"><span data-stu-id="45550-215">In this example, when hello OS disk is created, hello term "osDisk" is appened toohello VM name toocreate hello OS disk name.</span></span> <span data-ttu-id="45550-216">Este exemplo também especifica que este VHD com base em Windows deve ser anexado toohello VM como disco Olá sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="45550-216">This example also specifies that this Windows-based VHD should be attached toohello VM as hello OS disk.</span></span>
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

<span data-ttu-id="45550-217">Opcional: Se você tiver os discos de dados que toobe necessidade anexado toohello VM, adicione discos de dados hello usando URLs de saudação de dados VHDs e Olá número de unidade lógica (Lun) apropriado.</span><span class="sxs-lookup"><span data-stu-id="45550-217">Optional: If you have data disks that need toobe attached toohello VM, add hello data disks by using hello URLs of data VHDs and hello appropriate Logical Unit Number (Lun).</span></span>

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

<span data-ttu-id="45550-218">Ao usar uma conta de armazenamento, URLs de disco do sistema operacional e dados de saudação algo parecido com isto: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span><span class="sxs-lookup"><span data-stu-id="45550-218">When using a storage account, hello data and operating system disk URLs look something like this: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span></span> <span data-ttu-id="45550-219">Você pode encontrar isso no portal de saudação navegando toohello contêiner de armazenamento de destino, clicando em sistema operacional de saudação ou dados VHD que foi copiada e, em seguida, copiar o conteúdo de saudação da URL de saudação.</span><span class="sxs-lookup"><span data-stu-id="45550-219">You can find this on hello portal by browsing toohello target storage container, clicking hello operating system or data VHD that was copied, and then copying hello contents of hello URL.</span></span>


### <a name="complete-hello-vm"></a><span data-ttu-id="45550-220">Concluir Olá VM</span><span class="sxs-lookup"><span data-stu-id="45550-220">Complete hello VM</span></span> 

<span data-ttu-id="45550-221">Criar hello VM usando as configurações de saudação que acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="45550-221">Create hello VM using hello configurations that we just created.</span></span>

```powershell
#Create hello new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

<span data-ttu-id="45550-222">Se o comando for bem-sucedido, você verá uma saída como esta:</span><span class="sxs-lookup"><span data-stu-id="45550-222">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="45550-223">Verifique se esse Olá que VM foi criada</span><span class="sxs-lookup"><span data-stu-id="45550-223">Verify that hello VM was created</span></span>
<span data-ttu-id="45550-224">Você deve ver Olá recém-criado VM em Olá [portal do Azure](https://portal.azure.com), em **procurar** > **máquinas virtuais**, ou por meio de saudação do PowerShell a seguir comandos:</span><span class="sxs-lookup"><span data-stu-id="45550-224">You should see hello newly created VM either in hello [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="45550-225">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="45550-225">Next steps</span></span>
<span data-ttu-id="45550-226">toosign em tooyour nova máquina virtual toohello procurar VM em Olá [portal](https://portal.azure.com), clique em **conectar**e abra Olá o RDP.</span><span class="sxs-lookup"><span data-stu-id="45550-226">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="45550-227">Use credenciais de conta de saudação do seu toosign de máquina virtual original na nova máquina de virtual tooyour.</span><span class="sxs-lookup"><span data-stu-id="45550-227">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="45550-228">Para obter mais informações, consulte [como tooconnect e logon tooan virtuais do Azure do computador que executa o Windows](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="45550-228">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md).</span></span>

