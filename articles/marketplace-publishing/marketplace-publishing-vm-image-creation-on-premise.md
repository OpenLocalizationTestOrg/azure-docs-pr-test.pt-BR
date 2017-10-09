---
title: "aaaCreating uma imagem de máquina virtual local para hello Azure Marketplace | Microsoft Docs"
description: "Compreender e executar Olá etapas toocreate uma imagem VM no local e implantar toohello Azure Marketplace para outros toopurchase."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 26dfbd5a-8685-4b19-987e-c20ca60540ec
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c7a265330f1e494db8d0e981a38ee00d85746bb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-hello-azure-marketplace"></a><span data-ttu-id="23549-103">Desenvolver uma imagem de máquina virtual local para hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="23549-103">Develop an on-premises virtual machine image for hello Azure Marketplace</span></span>
<span data-ttu-id="23549-104">É altamente recomendável que você desenvolver Azure discos rígidos virtuais (VHDs) diretamente na nuvem hello usando o protocolo de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="23549-104">We strongly recommend that you develop Azure virtual hard disks (VHDs) directly in hello cloud by using Remote Desktop Protocol.</span></span> <span data-ttu-id="23549-105">No entanto, se for necessário, é possível toodownload um VHD e desenvolvê-lo usando a infraestrutura local.</span><span class="sxs-lookup"><span data-stu-id="23549-105">However, if you must, it is possible toodownload a VHD and develop it by using on-premises infrastructure.</span></span>  

<span data-ttu-id="23549-106">Para o desenvolvimento local, você deve baixar o VHD de saudação criada do sistema operacional do hello VM.</span><span class="sxs-lookup"><span data-stu-id="23549-106">For on-premises development, you must download hello operating system VHD of hello created VM.</span></span> <span data-ttu-id="23549-107">Essas etapas podem ocorrer como parte da etapa 3.3 acima.</span><span class="sxs-lookup"><span data-stu-id="23549-107">These steps would take place as part of step 3.3, above.</span></span>  

## <a name="download-a-vhd-image"></a><span data-ttu-id="23549-108">Baixar uma imagem VHD</span><span class="sxs-lookup"><span data-stu-id="23549-108">Download a VHD image</span></span>
### <a name="locate-a-blob-url"></a><span data-ttu-id="23549-109">Localize uma URL para Blobs</span><span class="sxs-lookup"><span data-stu-id="23549-109">Locate a blob URL</span></span>
<span data-ttu-id="23549-110">Em Olá VHD do toodownload ordem, primeiro localize Olá URL do blob de disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="23549-110">In order toodownload hello VHD, first locate hello blob URL for hello operating system disk.</span></span>

<span data-ttu-id="23549-111">Localizar a URL de blob de saudação da saudação novo [portal do Microsoft Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="23549-111">Locate hello blob URL from hello new [Microsoft Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="23549-112">Vá muito**procurar** > **VMs**, e, em seguida, selecione Olá implantado VM.</span><span class="sxs-lookup"><span data-stu-id="23549-112">Go too**Browse** > **VMs**, and then select hello deployed VM.</span></span>
2. <span data-ttu-id="23549-113">Em **configurar**, selecione Olá **discos** lado a lado, que abre a folha de discos de saudação.</span><span class="sxs-lookup"><span data-stu-id="23549-113">Under **Configure**, select hello **Disks** tile, which opens hello Disks blade.</span></span>
   
   ![desenho](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. <span data-ttu-id="23549-115">Selecione Olá **disco do sistema operacional**, que abre outra folha que exibe as propriedades do disco, incluindo o local do VHD hello.</span><span class="sxs-lookup"><span data-stu-id="23549-115">Select hello **OS Disk**, which opens another blade that displays disk properties, including hello VHD location.</span></span>
4. <span data-ttu-id="23549-116">Copie a URL do blob.</span><span class="sxs-lookup"><span data-stu-id="23549-116">Copy this blob URL.</span></span>
   
   ![desenho](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. <span data-ttu-id="23549-118">Agora, excluir Olá implantado VM sem excluir os discos de backup hello.</span><span class="sxs-lookup"><span data-stu-id="23549-118">Now, delete hello deployed VM without deleting hello backing disks.</span></span> <span data-ttu-id="23549-119">Você também pode interromper Olá VM em vez de excluí-lo.</span><span class="sxs-lookup"><span data-stu-id="23549-119">You can also stop hello VM instead of deleting it.</span></span> <span data-ttu-id="23549-120">Não baixe o VHD do sistema operacional hello quando Olá VM está em execução.</span><span class="sxs-lookup"><span data-stu-id="23549-120">Do not download hello operating system VHD when hello VM is running.</span></span>
   
   ![desenho](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a><span data-ttu-id="23549-122">Baixe um VHD</span><span class="sxs-lookup"><span data-stu-id="23549-122">Download a VHD</span></span>
<span data-ttu-id="23549-123">Depois que você souber a URL do blob Olá, você pode baixar Olá VHD usando Olá [portal do Azure](http://manage.windowsazure.com/) ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23549-123">After you know hello blob URL, you can download hello VHD by using hello [Azure portal](http://manage.windowsazure.com/) or PowerShell.</span></span>  

> [!NOTE]
> <span data-ttu-id="23549-124">Em tempo de saudação da criação deste guia, toodownload de funcionalidade Olá um VHD ainda não está presente no novo portal do Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="23549-124">At hello time of this guide’s creation, hello functionality toodownload a VHD is not yet present in hello new Microsoft Azure portal.</span></span>  
> 
> 

<span data-ttu-id="23549-125">**Baixar Olá VHD do sistema operacional por meio de saudação atual [portal do Azure](http://manage.windowsazure.com/)**</span><span class="sxs-lookup"><span data-stu-id="23549-125">**Download hello operating system VHD via hello current [Azure portal](http://manage.windowsazure.com/)**</span></span>

1. <span data-ttu-id="23549-126">Entrar no portal do Azure de toohello se você ainda não fez isso.</span><span class="sxs-lookup"><span data-stu-id="23549-126">Sign in toohello Azure portal if you have not done so already.</span></span>
2. <span data-ttu-id="23549-127">Clique em Olá **armazenamento** guia.</span><span class="sxs-lookup"><span data-stu-id="23549-127">Click hello **Storage** tab.</span></span>
3. <span data-ttu-id="23549-128">Selecione a conta de armazenamento de saudação em qual Olá VHD é armazenado.</span><span class="sxs-lookup"><span data-stu-id="23549-128">Select hello storage account within which hello VHD is stored.</span></span>
   
   ![desenho](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. <span data-ttu-id="23549-130">Isso exibe as propriedades da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="23549-130">This displays storage account properties.</span></span> <span data-ttu-id="23549-131">Selecione Olá **contêineres** guia.</span><span class="sxs-lookup"><span data-stu-id="23549-131">Select hello **Containers** tab.</span></span>
   
   ![desenho](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. <span data-ttu-id="23549-133">Selecione Olá contêiner no qual Olá VHD é armazenado.</span><span class="sxs-lookup"><span data-stu-id="23549-133">Select hello container in which hello VHD is stored.</span></span> <span data-ttu-id="23549-134">Por padrão, quando criadas no portal de saudação Olá VHD é armazenado em um contêiner de vhds.</span><span class="sxs-lookup"><span data-stu-id="23549-134">By default, when created from hello portal, hello VHD is stored in a vhds container.</span></span>
   
   ![desenho](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. <span data-ttu-id="23549-136">Selecione Olá correto VHD do sistema operacional, comparando Olá URL toohello um que é salvo.</span><span class="sxs-lookup"><span data-stu-id="23549-136">Select hello correct operating system VHD by comparing hello URL toohello one you saved.</span></span>
7. <span data-ttu-id="23549-137">Clique em **Download**.</span><span class="sxs-lookup"><span data-stu-id="23549-137">Click **Download**.</span></span>
   
   ![desenho](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a><span data-ttu-id="23549-139">Baixar um VHD usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="23549-139">Download a VHD by using PowerShell</span></span>
<span data-ttu-id="23549-140">Além disso toousing Olá portal do Azure, você pode usar o hello [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet toodownload Olá VHD do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="23549-140">In addition toousing hello Azure portal, you can use hello [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet toodownload hello operating system VHD.</span></span>

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
<span data-ttu-id="23549-141">Por exemplo, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span><span class="sxs-lookup"><span data-stu-id="23549-141">For example, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span></span>

> [!NOTE]
> <span data-ttu-id="23549-142">**Save-AzureVhd** também tem um **NumberOfThreads** opção que pode ser usado tooincrease paralelismo toomake Olá melhor uso de largura de banda disponível para download de saudação.</span><span class="sxs-lookup"><span data-stu-id="23549-142">**Save-AzureVhd** also has a **NumberOfThreads** option that can be used tooincrease parallelism toomake hello best use of available bandwidth for hello download.</span></span>
> 
> 

## <a name="upload-vhds-tooan-azure-storage-account"></a><span data-ttu-id="23549-143">Carregar VHDs tooan conta de armazenamento Azure</span><span class="sxs-lookup"><span data-stu-id="23549-143">Upload VHDs tooan Azure storage account</span></span>
<span data-ttu-id="23549-144">Se você preparou seus VHDs locais, você precisa tooupload-los em um armazenamento de conta no Azure.</span><span class="sxs-lookup"><span data-stu-id="23549-144">If you prepared your VHDs on-premises, you need tooupload them into a storage account in Azure.</span></span> <span data-ttu-id="23549-145">Esta etapa ocorre depois de criar o VHD local, mas antes de obter a certificação para a imagem da VM.</span><span class="sxs-lookup"><span data-stu-id="23549-145">This step takes place after creating your VHD on-premises but before obtaining certification for your VM image.</span></span>

### <a name="create-a-storage-account-and-container"></a><span data-ttu-id="23549-146">Criar uma conta e um contêiner de armazenamento</span><span class="sxs-lookup"><span data-stu-id="23549-146">Create a storage account and container</span></span>
<span data-ttu-id="23549-147">É recomendável que os VHDs ser carregado em uma conta de armazenamento em uma região de saudação dos Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="23549-147">We recommend that VHDs be uploaded into a storage account in a region in hello United States.</span></span> <span data-ttu-id="23549-148">Todos os VHDs para uma única SKU devem ser colocados em um único contêiner dentro de uma única conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="23549-148">All VHDs for a single SKU should be placed in a single container within a single storage account.</span></span>

<span data-ttu-id="23549-149">toocreate uma conta de armazenamento, você pode usar o hello [portal do Microsoft Azure](https://portal.azure.com/), PowerShell ou ferramenta de linha de comando do Linux hello.</span><span class="sxs-lookup"><span data-stu-id="23549-149">toocreate a storage account, you can use hello [Microsoft Azure portal](https://portal.azure.com/), PowerShell, or hello Linux command-line tool.</span></span>  

<span data-ttu-id="23549-150">**Criar uma conta de armazenamento do portal do Microsoft Azure Olá**</span><span class="sxs-lookup"><span data-stu-id="23549-150">**Create a storage account from hello Microsoft Azure portal**</span></span>

1. <span data-ttu-id="23549-151">Clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="23549-151">Click **New**.</span></span>
2. <span data-ttu-id="23549-152">Selecione **Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="23549-152">Select **Storage**.</span></span>
3. <span data-ttu-id="23549-153">Preencha o nome de conta de armazenamento hello e, em seguida, selecione um local.</span><span class="sxs-lookup"><span data-stu-id="23549-153">Fill in hello storage account name, and then select a location.</span></span>
   
   ![desenho](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. <span data-ttu-id="23549-155">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="23549-155">Click **Create**.</span></span>
5. <span data-ttu-id="23549-156">folha de saudação para Olá criado a conta de armazenamento deve estar aberta.</span><span class="sxs-lookup"><span data-stu-id="23549-156">hello blade for hello created storage account should be open.</span></span> <span data-ttu-id="23549-157">Caso contrário, selecione **Procurar** > **Contas de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="23549-157">If not, select **Browse** > **Storage Accounts**.</span></span> <span data-ttu-id="23549-158">Olá armazenamento conta folha, selecione a conta de armazenamento Olá criada.</span><span class="sxs-lookup"><span data-stu-id="23549-158">On hello Storage account blade, select hello storage account created.</span></span>
6. <span data-ttu-id="23549-159">Selecione **Contêineres**.</span><span class="sxs-lookup"><span data-stu-id="23549-159">Select **Containers**.</span></span>
   
   ![desenho](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. <span data-ttu-id="23549-161">Na folha de contêineres hello, selecione **adicionar**e, em seguida, insira um permissões de contêiner de nome e a saudação do contêiner.</span><span class="sxs-lookup"><span data-stu-id="23549-161">On hello Containers blade, select **Add**, and then enter a container name and hello container permissions.</span></span> <span data-ttu-id="23549-162">Selecione **Particular** nas permissões do contêiner.</span><span class="sxs-lookup"><span data-stu-id="23549-162">Select **Private** for container permissions.</span></span>

> [!TIP]
> <span data-ttu-id="23549-163">É recomendável que você crie um contêiner de por que você está planejando toopublish SKU.</span><span class="sxs-lookup"><span data-stu-id="23549-163">We recommend that you create one container per SKU that you are planning toopublish.</span></span>
> 
> 

  ![desenho](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a><span data-ttu-id="23549-165">Criar uma conta de armazenamento usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="23549-165">Create a storage account by using PowerShell</span></span>
<span data-ttu-id="23549-166">Usando o PowerShell, crie uma conta de armazenamento usando Olá [AzureStorageAccount novo](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="23549-166">Using PowerShell, create a storage account by using hello [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span></span>

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

<span data-ttu-id="23549-167">Em seguida, você pode criar um contêiner dentro dessa conta de armazenamento usando Olá [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="23549-167">Then you can create a container within that storage account by using hello [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span></span>

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> <span data-ttu-id="23549-168">Esses comandos pressupõem que contexto de conta de armazenamento atual da saudação já foi definido no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23549-168">Those commands assume that hello current storage account context has already been set in PowerShell.</span></span>   <span data-ttu-id="23549-169">Consulte também[Configurando o Azure PowerShell](marketplace-publishing-powershell-setup.md) para obter mais detalhes sobre a instalação do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23549-169">Refer too[Setting up Azure PowerShell](marketplace-publishing-powershell-setup.md) for more details on PowerShell setup.</span></span>  
> 
> ### <a name="create-a-storage-account-by-using-hello-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="23549-170">Criar uma conta de armazenamento usando a ferramenta de linha de comando Olá para Mac e Linux</span><span class="sxs-lookup"><span data-stu-id="23549-170">Create a storage account by using hello command-line tool for Mac and Linux</span></span>
> <span data-ttu-id="23549-171">A partir da [ferramenta de linha de comando do Linux](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), crie uma conta de armazenamento da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="23549-171">From [Linux command-line tool](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), create a storage account as follows.</span></span>
> 
> 

        azure storage account create mystorageaccount --location "West US"

<span data-ttu-id="23549-172">Crie um contêiner da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="23549-172">Create a container as follows.</span></span>

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a><span data-ttu-id="23549-173">Carregar um VHD</span><span class="sxs-lookup"><span data-stu-id="23549-173">Upload a VHD</span></span>
<span data-ttu-id="23549-174">Depois que o contêiner e a conta de armazenamento Olá são criados, você pode carregar seus VHDs preparadas.</span><span class="sxs-lookup"><span data-stu-id="23549-174">After hello storage account and container are created, you can upload your prepared VHDs.</span></span> <span data-ttu-id="23549-175">Você pode usar o PowerShell, a ferramenta de linha de comando do Linux hello ou outras ferramentas de gerenciamento de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="23549-175">You can use PowerShell, hello Linux command-line tool, or other Azure Storage management tools.</span></span>

### <a name="upload-a-vhd-via-powershell"></a><span data-ttu-id="23549-176">Carregar um VHD por meio do PowerShell</span><span class="sxs-lookup"><span data-stu-id="23549-176">Upload a VHD via PowerShell</span></span>
<span data-ttu-id="23549-177">Saudação de uso [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="23549-177">Use hello [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span></span>

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-hello-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="23549-178">Carregar um VHD usando a ferramenta de linha de comando Olá para Mac e Linux</span><span class="sxs-lookup"><span data-stu-id="23549-178">Upload a VHD by using hello command-line tool for Mac and Linux</span></span>
<span data-ttu-id="23549-179">Com hello [ferramenta de linha de comando do Linux](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), use Olá seguinte: criar a imagem da vm do azure <image name> – local <Location of hello data center> – sistema operacional Linux<LocationOfLocalVHD></span><span class="sxs-lookup"><span data-stu-id="23549-179">With hello [Linux command-line tool](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), use hello following: azure vm image create <image name> --location <Location of hello data center> --OS Linux <LocationOfLocalVHD></span></span>

## <a name="see-also"></a><span data-ttu-id="23549-180">Consulte também</span><span class="sxs-lookup"><span data-stu-id="23549-180">See also</span></span>
* [<span data-ttu-id="23549-181">Criar uma imagem de máquina virtual para Olá Marketplace</span><span class="sxs-lookup"><span data-stu-id="23549-181">Creating a virtual machine image for hello Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)
* [<span data-ttu-id="23549-182">Configurando o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="23549-182">Setting up Azure PowerShell</span></span>](marketplace-publishing-powershell-setup.md)

