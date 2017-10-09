---
title: "aaaUpload um toocreate VHD generalizar várias VMs no Azure | Microsoft Docs"
description: "Carregar um generalizado toocreate de conta do armazenamento do Azure de tooan VHD toouse uma máquina virtual do Windows com o modelo de implantação do Gerenciador de recursos de saudação."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: cynthn
ms.openlocfilehash: aa1af2a0acf81685e62853de71afa51e819cb696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-tooazure-toocreate-a-new-vm"></a><span data-ttu-id="bae72-103">Carregar um toocreate de tooAzure VHD generalizado uma nova VM</span><span class="sxs-lookup"><span data-stu-id="bae72-103">Upload a generalized VHD tooAzure toocreate a new VM</span></span>

<span data-ttu-id="bae72-104">Este tópico aborda o carregamento de uma conta de armazenamento do disco não gerenciado generalizado tooa e, em seguida, criar uma nova VM usando disco Olá carregado.</span><span class="sxs-lookup"><span data-stu-id="bae72-104">This topic covers uploading a generalized unmanaged disk tooa storage account and then creating a new VM using hello uploaded disk.</span></span> <span data-ttu-id="bae72-105">Uma imagem VHD generalizada teve todas as informações da sua conta pessoal removidas usando o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="bae72-105">A generalized VHD image has had all of your personal account information removed using Sysprep.</span></span> 

<span data-ttu-id="bae72-106">Se você quiser toocreate uma VM em um VHD especializada em uma conta de armazenamento, consulte [criar uma máquina virtual em um VHD especializado](sa-create-vm-specialized.md).</span><span class="sxs-lookup"><span data-stu-id="bae72-106">If you want toocreate a VM from a specialized VHD in a storage account, see [Create a VM from a specialized VHD](sa-create-vm-specialized.md).</span></span>

<span data-ttu-id="bae72-107">Este tópico aborda o uso de contas de armazenamento, mas é recomendável que os clientes movem toousing gerenciados discos em vez disso.</span><span class="sxs-lookup"><span data-stu-id="bae72-107">This topic covers using storage accounts, but we recommend customers move toousing Managed Disks instead.</span></span> <span data-ttu-id="bae72-108">Para uma passo a passo completa de como tooprepare, carregar e criar uma nova VM usando discos gerenciado, consulte [criar uma nova VM de um tooAzure VHD carregado generalizado usando discos gerenciados](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="bae72-108">For a complete walk-through of how tooprepare, upload and create a new VM using managed disks, see [Create a new VM from a generalized VHD uploaded tooAzure using Managed Disks](upload-generalized-managed.md).</span></span>



## <a name="prepare-hello-vm"></a><span data-ttu-id="bae72-109">Preparar Olá VM</span><span class="sxs-lookup"><span data-stu-id="bae72-109">Prepare hello VM</span></span>

<span data-ttu-id="bae72-110">Um VHD generalizado teve todas as informações da sua conta pessoal removidas usando o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="bae72-110">A generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="bae72-111">Se você pretende toouse Olá VHD como uma imagem toocreate novas VMs do, você deve:</span><span class="sxs-lookup"><span data-stu-id="bae72-111">If you intend toouse hello VHD as an image toocreate new VMs from, you should:</span></span>
  
  * <span data-ttu-id="bae72-112">[Preparar um tooAzure tooupload de VHD do Windows](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="bae72-112">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md).</span></span> 
  * <span data-ttu-id="bae72-113">Generalize a máquina virtual de saudação usando Sysprep</span><span class="sxs-lookup"><span data-stu-id="bae72-113">Generalize hello virtual machine using Sysprep</span></span>

### <a name="generalize-a-windows-virtual-machine-using-sysprep"></a><span data-ttu-id="bae72-114">Generalizar uma máquina virtual do Windows usando o Sysprep</span><span class="sxs-lookup"><span data-stu-id="bae72-114">Generalize a Windows virtual machine using Sysprep</span></span>
<span data-ttu-id="bae72-115">Esta seção mostra como toogeneralize sua máquina virtual do Windows para uso como uma imagem.</span><span class="sxs-lookup"><span data-stu-id="bae72-115">This section shows you how toogeneralize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="bae72-116">O Sysprep remove todas as suas informações de conta pessoal, entre outras coisas e prepara Olá máquina toobe usado como uma imagem.</span><span class="sxs-lookup"><span data-stu-id="bae72-116">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="bae72-117">Para obter detalhes sobre o Sysprep, consulte [como tooUse Sysprep: uma introdução](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="bae72-117">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="bae72-118">Certifique-se de funções de servidor de saudação em execução na máquina Olá Sysprep oferece suporte.</span><span class="sxs-lookup"><span data-stu-id="bae72-118">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="bae72-119">Para obter mais informações, consulte [Suporte do Sysprep para funções de servidor](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="bae72-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bae72-120">Se você estiver executando o Sysprep antes de carregar seu tooAzure VHD para Olá primeira vez, verifique se você tem [preparado sua VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de executar o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="bae72-120">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="bae72-121">Entrar toohello máquina virtual do Windows.</span><span class="sxs-lookup"><span data-stu-id="bae72-121">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="bae72-122">Abra a janela de Prompt de comando hello como administrador.</span><span class="sxs-lookup"><span data-stu-id="bae72-122">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="bae72-123">Altere o diretório de saudação muito**%windir%\system32\sysprep**e, em seguida, execute `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="bae72-123">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="bae72-124">Em Olá **ferramenta de preparação do sistema** caixa de diálogo, selecione **Enter System Out-of-Box Experience (OOBE)**e certifique-se de que Olá **generalizar** caixa de seleção é marcada.</span><span class="sxs-lookup"><span data-stu-id="bae72-124">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="bae72-125">Em **Opções de Desligamento**, selecione **Desligar**.</span><span class="sxs-lookup"><span data-stu-id="bae72-125">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="bae72-126">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="bae72-126">Click **OK**.</span></span>
   
    ![Inicie o Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="bae72-128">Quando o Sysprep for concluído, desligar máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="bae72-128">When Sysprep completes, it shuts down hello virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="bae72-129">Não reinicie Olá VM até que você esteja concluído tooAzure VHD Olá carregar ou criar uma imagem de VM de saudação.</span><span class="sxs-lookup"><span data-stu-id="bae72-129">Do not restart hello VM until you are done uploading hello VHD tooAzure or creating an image from hello VM.</span></span> <span data-ttu-id="bae72-130">Se acidentalmente Olá VM é reiniciada, execute Sysprep toogeneralize-a novamente.</span><span class="sxs-lookup"><span data-stu-id="bae72-130">If hello VM accidentally gets restarted, run Sysprep toogeneralize it again.</span></span>
> 
> 


## <a name="upload-hello-vhd"></a><span data-ttu-id="bae72-131">Carregar Olá VHD</span><span class="sxs-lookup"><span data-stu-id="bae72-131">Upload hello VHD</span></span>

<span data-ttu-id="bae72-132">Carregar Olá VHD tooan conta de armazenamento Azure.</span><span class="sxs-lookup"><span data-stu-id="bae72-132">Upload hello VHD tooan Azure storage account.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="bae72-133">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="bae72-133">Log in tooAzure</span></span>
<span data-ttu-id="bae72-134">Se você ainda não tiver o PowerShell versão 1.4 ou superior instalado, leia [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bae72-134">If you don't already have PowerShell version 1.4 or above installed, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="bae72-135">Abra o PowerShell do Azure e entrar tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="bae72-135">Open Azure PowerShell and sign in tooyour Azure account.</span></span> <span data-ttu-id="bae72-136">Uma janela pop-up é aberto para você tooenter suas credenciais de conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="bae72-136">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="bae72-137">Obter IDs de assinatura Olá para suas assinaturas disponíveis.</span><span class="sxs-lookup"><span data-stu-id="bae72-137">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="bae72-138">Definir Olá assinatura correto usando a ID de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="bae72-138">Set hello correct subscription using hello subscription ID.</span></span> <span data-ttu-id="bae72-139">Substituir `<subscriptionID>` com ID Olá Olá corrigir a assinatura.</span><span class="sxs-lookup"><span data-stu-id="bae72-139">Replace `<subscriptionID>` with hello ID of hello correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

### <a name="get-hello-storage-account"></a><span data-ttu-id="bae72-140">Obter a conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="bae72-140">Get hello storage account</span></span>
<span data-ttu-id="bae72-141">Você precisa de uma conta de armazenamento na imagem VM do Azure toostore Olá carregado.</span><span class="sxs-lookup"><span data-stu-id="bae72-141">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="bae72-142">Você pode usar uma conta de armazenamento existente ou criar uma nova.</span><span class="sxs-lookup"><span data-stu-id="bae72-142">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="bae72-143">as contas de armazenamento disponível Olá tooshow, digite:</span><span class="sxs-lookup"><span data-stu-id="bae72-143">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="bae72-144">Se você quiser toouse uma conta de armazenamento existente, vá toohello [carregar imagem VM Olá](#upload-the-vm-vhd-to-your-storage-account) seção.</span><span class="sxs-lookup"><span data-stu-id="bae72-144">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="bae72-145">Se você precisar toocreate uma conta de armazenamento, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="bae72-145">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="bae72-146">Você precisará nome Olá Olá do grupo de recursos onde a conta de armazenamento Olá deve ser criada.</span><span class="sxs-lookup"><span data-stu-id="bae72-146">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="bae72-147">toofind todos os grupos de recursos Olá que estão em sua assinatura, o tipo:</span><span class="sxs-lookup"><span data-stu-id="bae72-147">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="bae72-148">toocreate um grupo de recursos denominado **myResourceGroup** em Olá **Oeste dos EUA** região, digite:</span><span class="sxs-lookup"><span data-stu-id="bae72-148">toocreate a resource group named **myResourceGroup** in hello **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="bae72-149">Criar uma conta de armazenamento denominada **mystorageaccount** neste grupo de recursos usando Olá [AzureRmStorageAccount novo](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bae72-149">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
 
### <a name="start-hello-upload"></a><span data-ttu-id="bae72-150">Carregamento de saudação inicial</span><span class="sxs-lookup"><span data-stu-id="bae72-150">Start hello upload</span></span> 

<span data-ttu-id="bae72-151">Saudação de uso [AzureRmVhd adicionar](/powershell/module/azurerm.compute/add-azurermvhd) contêiner do cmdlet tooupload Olá imagem tooa na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bae72-151">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello image tooa container in your storage account.</span></span> <span data-ttu-id="bae72-152">Este exemplo hello de carregamentos de arquivo **myVHD.vhd** de `"C:\Users\Public\Documents\Virtual hard disks\"` tooa conta de armazenamento denominada **mystorageaccount** em Olá **myResourceGroup** grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="bae72-152">This example uploads hello file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named **mystorageaccount** in hello **myResourceGroup** resource group.</span></span> <span data-ttu-id="bae72-153">arquivo Hello será colocado no contêiner Olá denominado **mycontainer** e o novo nome de arquivo hello serão **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="bae72-153">hello file will be placed into hello container named **mycontainer** and hello new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="bae72-154">Se for bem-sucedido, você receberá uma resposta que parece semelhante toothis:</span><span class="sxs-lookup"><span data-stu-id="bae72-154">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="bae72-155">Dependendo de sua conexão de rede e o tamanho de saudação do arquivo VHD, este comando pode demorar um pouco toocomplete.</span><span class="sxs-lookup"><span data-stu-id="bae72-155">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete.</span></span>


## <a name="create-a-new-vm"></a><span data-ttu-id="bae72-156">Criar uma nova VM</span><span class="sxs-lookup"><span data-stu-id="bae72-156">Create a new VM</span></span> 

<span data-ttu-id="bae72-157">Você pode agora usar Olá carregado VHD toocreate uma nova VM.</span><span class="sxs-lookup"><span data-stu-id="bae72-157">You can now use hello uploaded VHD toocreate a new VM.</span></span> 

### <a name="set-hello-uri-of-hello-vhd"></a><span data-ttu-id="bae72-158">Saudação de conjunto de URI do VHD de saudação</span><span class="sxs-lookup"><span data-stu-id="bae72-158">Set hello URI of hello VHD</span></span>

<span data-ttu-id="bae72-159">Olá URI para Olá VHD toouse está no formato de saudação: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**. vhd.</span><span class="sxs-lookup"><span data-stu-id="bae72-159">hello URI for hello VHD toouse is in hello format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="bae72-160">Neste exemplo hello VHD denominado **myVHD** é na conta de armazenamento Olá **mystorageaccount** no contêiner Olá **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="bae72-160">In this example hello VHD named **myVHD** is in hello storage account **mystorageaccount** in hello container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="bae72-161">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="bae72-161">Create a virtual network</span></span>
<span data-ttu-id="bae72-162">Criar rede virtual de saudação e a sub-rede de saudação [rede virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bae72-162">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="bae72-163">Crie uma sub-rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="bae72-163">Create hello subnet.</span></span> <span data-ttu-id="bae72-164">Olá, exemplo a seguir cria uma sub-rede denominada **mySubnet** no grupo de recursos de saudação **myResourceGroup** com prefixo de endereço de saudação **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="bae72-164">hello following sample creates a subnet named **mySubnet** in hello resource group **myResourceGroup** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="bae72-165">Crie rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="bae72-165">Create hello virtual network.</span></span> <span data-ttu-id="bae72-166">Olá, exemplo a seguir cria uma rede virtual denominada **myVnet** em Olá **Oeste dos EUA** local com o prefixo de endereço de saudação **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="bae72-166">hello following sample creates a virtual network named **myVnet** in hello **West US** location with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="bae72-167">Criar um endereço IP público e um adaptador de rede</span><span class="sxs-lookup"><span data-stu-id="bae72-167">Create a public IP address and network interface</span></span>
<span data-ttu-id="bae72-168">comunicação tooenable com máquina virtual de saudação na rede virtual Olá, é necessário um [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e uma interface de rede.</span><span class="sxs-lookup"><span data-stu-id="bae72-168">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="bae72-169">Criar um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="bae72-169">Create a public IP address.</span></span> <span data-ttu-id="bae72-170">Este exemplo cria um endereço IP público chamado **myPip**.</span><span class="sxs-lookup"><span data-stu-id="bae72-170">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="bae72-171">Criar NIC hello.</span><span class="sxs-lookup"><span data-stu-id="bae72-171">Create hello NIC.</span></span> <span data-ttu-id="bae72-172">Este exemplo cria uma NIC chamada **myNic**.</span><span class="sxs-lookup"><span data-stu-id="bae72-172">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="bae72-173">Criar um grupo de segurança de rede hello e uma regra RDP</span><span class="sxs-lookup"><span data-stu-id="bae72-173">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="bae72-174">toolog capaz de toobe em tooyour VM usando o RDP, você precisa toohave uma regra de segurança que permita o acesso RDP na porta 3389.</span><span class="sxs-lookup"><span data-stu-id="bae72-174">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="bae72-175">Este exemplo cria um NSG chamado **myNsg** que contém uma regra chamada **myRdpRule** que permite tráfego RDP pela porta 3389.</span><span class="sxs-lookup"><span data-stu-id="bae72-175">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="bae72-176">Para obter mais informações sobre os NSGs, consulte [a abertura de portas tooa VM no Azure usando o PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bae72-176">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="bae72-177">Criar uma variável para a rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="bae72-177">Create a variable for hello virtual network</span></span>
<span data-ttu-id="bae72-178">Crie uma variável para a rede virtual Olá concluída.</span><span class="sxs-lookup"><span data-stu-id="bae72-178">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a><span data-ttu-id="bae72-179">Criar hello VM</span><span class="sxs-lookup"><span data-stu-id="bae72-179">Create hello VM</span></span>
<span data-ttu-id="bae72-180">Olá PowerShell script a seguir mostra como tooset configurações de máquina virtual hello e use Olá carregado a imagem da VM como fonte de saudação para nova instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="bae72-180">hello following PowerShell script shows how tooset up hello virtual machine configurations and use hello uploaded VM image as hello source for hello new installation.</span></span>



```powershell
# Enter a new user name and password toouse as hello local administrator account 
    # for remotely accessing hello VM.
    $cred = Get-Credential

    # Name of hello storage account where hello VHD is located. This example sets hello 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of hello virtual machine. This example sets hello VM name as "myVM".
    $vmName = "myVM"

    # Size of hello virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See hello VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for hello VM. This examples sets hello computer name as "myComputer".
    $computerName = "myComputer"

    # Name of hello disk that holds hello OS. This example sets hello 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets hello SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get hello storage account where hello uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set hello VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set hello Windows operating system configuration and add hello NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create hello OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure hello OS disk toobe created from hello existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create hello new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="bae72-181">Verifique se esse Olá que VM foi criada</span><span class="sxs-lookup"><span data-stu-id="bae72-181">Verify that hello VM was created</span></span>
<span data-ttu-id="bae72-182">Ao concluir, você deverá ver Olá recém-criado VM em Olá [portal do Azure](https://portal.azure.com) em **procurar** > **máquinas virtuais**, ou usando o seguinte Olá Comandos do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bae72-182">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="bae72-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bae72-183">Next steps</span></span>
<span data-ttu-id="bae72-184">toomanage nova máquina virtual com o Azure PowerShell, consulte [gerenciar máquinas virtuais usando o Gerenciador de recursos do Azure e PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bae72-184">toomanage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


