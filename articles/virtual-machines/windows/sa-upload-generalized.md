---
title: "Upload de um VHD generalizado para criar várias VMs no Azure | Microsoft Docs"
description: "Carregar um VHD generalizado para uma conta de armazenamento do Azure para criar uma VM Windows para utilizar com o modelo de implantação do Resource Manager."
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
ms.openlocfilehash: e6fc49855b449a7723a7f8a0c1c41516b3a44ee5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="upload-a-generalized-vhd-to-azure-to-create-a-new-vm"></a><span data-ttu-id="a0587-103">Upload de um VHD generalizado para o Azure para criar uma nova VM</span><span class="sxs-lookup"><span data-stu-id="a0587-103">Upload a generalized VHD to Azure to create a new VM</span></span>

<span data-ttu-id="a0587-104">Este tópico abrange o upload de um disco não gerenciado generalizado para uma conta de armazenamento e, em seguida, criar uma nova VM utilizando o disco carregado.</span><span class="sxs-lookup"><span data-stu-id="a0587-104">This topic covers uploading a generalized unmanaged disk to a storage account and then creating a new VM using the uploaded disk.</span></span> <span data-ttu-id="a0587-105">Uma imagem VHD generalizada teve todas as informações da sua conta pessoal removidas usando o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="a0587-105">A generalized VHD image has had all of your personal account information removed using Sysprep.</span></span> 

<span data-ttu-id="a0587-106">Se desejar criar uma VM com base em um VHD especializado em uma conta de armazenamento, consulte [Criar uma VM com base em um VHD especializado](sa-create-vm-specialized.md).</span><span class="sxs-lookup"><span data-stu-id="a0587-106">If you want to create a VM from a specialized VHD in a storage account, see [Create a VM from a specialized VHD](sa-create-vm-specialized.md).</span></span>

<span data-ttu-id="a0587-107">Este tópico aborda o uso de contas de armazenamento, mas é recomendável que os clientes mudem para utilizar o Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="a0587-107">This topic covers using storage accounts, but we recommend customers move to using Managed Disks instead.</span></span> <span data-ttu-id="a0587-108">Para um completo passo a passo de como preparar, carregar e criar uma nova VM usando discos gerenciados, consulte [Criar uma nova VM a partir de um VHD generalizado carregado para o Azure utilizando o Managed Disks](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="a0587-108">For a complete walk-through of how to prepare, upload and create a new VM using managed disks, see [Create a new VM from a generalized VHD uploaded to Azure using Managed Disks](upload-generalized-managed.md).</span></span>



## <a name="prepare-the-vm"></a><span data-ttu-id="a0587-109">Preparar a VM</span><span class="sxs-lookup"><span data-stu-id="a0587-109">Prepare the VM</span></span>

<span data-ttu-id="a0587-110">Um VHD generalizado teve todas as informações da sua conta pessoal removidas usando o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="a0587-110">A generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="a0587-111">Se você pretende criar novas VMs usando o VHD como uma imagem, você deve:</span><span class="sxs-lookup"><span data-stu-id="a0587-111">If you intend to use the VHD as an image to create new VMs from, you should:</span></span>
  
  * <span data-ttu-id="a0587-112">[Preparar um VHD do Windows para carregar no Azure](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="a0587-112">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md).</span></span> 
  * <span data-ttu-id="a0587-113">Generalize a máquina virtual utilizando o Sysprep</span><span class="sxs-lookup"><span data-stu-id="a0587-113">Generalize the virtual machine using Sysprep</span></span>

### <a name="generalize-a-windows-virtual-machine-using-sysprep"></a><span data-ttu-id="a0587-114">Generalizar uma máquina virtual do Windows usando o Sysprep</span><span class="sxs-lookup"><span data-stu-id="a0587-114">Generalize a Windows virtual machine using Sysprep</span></span>
<span data-ttu-id="a0587-115">Esta seção mostra como generalizar a máquina virtual do Windows para usar como uma imagem.</span><span class="sxs-lookup"><span data-stu-id="a0587-115">This section shows you how to generalize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="a0587-116">O Sysprep remove todas as informações pessoais da conta, entre outros itens, e prepara o computador para ser utilizado como uma imagem.</span><span class="sxs-lookup"><span data-stu-id="a0587-116">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="a0587-117">Para obter detalhes sobre o Sysprep, consulte [Como usar o Sysprep: uma introdução](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="a0587-117">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="a0587-118">Verifique se as funções de servidor em execução no computador são suportadas pelo Sysprep.</span><span class="sxs-lookup"><span data-stu-id="a0587-118">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="a0587-119">Para obter mais informações, consulte [Suporte do Sysprep para funções de servidor](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="a0587-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0587-120">Se você estiver executando o Sysprep antes de carregar o VHD para o Azure pela primeira vez, verifique se você [preparou sua VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de executar o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="a0587-120">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="a0587-121">Entre na máquina virtual Windows.</span><span class="sxs-lookup"><span data-stu-id="a0587-121">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="a0587-122">Abra uma janela de prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="a0587-122">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="a0587-123">Altere o diretório para **%windir%\system32\sysprep** e, a seguir, execute`sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="a0587-123">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="a0587-124">Na caixa de diálogo **Ferramenta de Preparação do Sistema**, selecione **Entrar na Configuração Inicial pelo Usuário do Sistema (OOBE)** e verifique se a caixa de seleção **Generalizar** está marcada.</span><span class="sxs-lookup"><span data-stu-id="a0587-124">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="a0587-125">Em **Opções de Desligamento**, selecione **Desligar**.</span><span class="sxs-lookup"><span data-stu-id="a0587-125">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="a0587-126">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a0587-126">Click **OK**.</span></span>
   
    ![Inicie o Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="a0587-128">Quando o Sysprep for concluído, desligará a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a0587-128">When Sysprep completes, it shuts down the virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="a0587-129">Só reinicie a VM quando concluir o carregamento do VHD no Azure ou a criação de uma imagem da VM.</span><span class="sxs-lookup"><span data-stu-id="a0587-129">Do not restart the VM until you are done uploading the VHD to Azure or creating an image from the VM.</span></span> <span data-ttu-id="a0587-130">Se a VM for reiniciada acidentalmente, execute o Sysprep para generalizá-la novamente.</span><span class="sxs-lookup"><span data-stu-id="a0587-130">If the VM accidentally gets restarted, run Sysprep to generalize it again.</span></span>
> 
> 


## <a name="upload-the-vhd"></a><span data-ttu-id="a0587-131">Carregar o VHD</span><span class="sxs-lookup"><span data-stu-id="a0587-131">Upload the VHD</span></span>

<span data-ttu-id="a0587-132">Faça upload do VHD para uma conta de armazenamento Azure.</span><span class="sxs-lookup"><span data-stu-id="a0587-132">Upload the VHD to an Azure storage account.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="a0587-133">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="a0587-133">Log in to Azure</span></span>
<span data-ttu-id="a0587-134">Se você ainda não tiver a versão 1.4 ou superior do PowerShell instalada, leia [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a0587-134">If you don't already have PowerShell version 1.4 or above installed, read [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="a0587-135">Abra o Azure PowerShell e conecte-se à sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0587-135">Open Azure PowerShell and sign in to your Azure account.</span></span> <span data-ttu-id="a0587-136">Uma janela pop-up é aberta para inserir as credenciais da conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0587-136">A pop-up window opens for you to enter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="a0587-137">Obtenha as IDs de assinatura das assinaturas disponíveis.</span><span class="sxs-lookup"><span data-stu-id="a0587-137">Get the subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="a0587-138">Defina a assinatura correta usando a ID da assinatura.</span><span class="sxs-lookup"><span data-stu-id="a0587-138">Set the correct subscription using the subscription ID.</span></span> <span data-ttu-id="a0587-139">Substitua `<subscriptionID>` com a ID da assinatura correta.</span><span class="sxs-lookup"><span data-stu-id="a0587-139">Replace `<subscriptionID>` with the ID of the correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

### <a name="get-the-storage-account"></a><span data-ttu-id="a0587-140">Obter a conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="a0587-140">Get the storage account</span></span>
<span data-ttu-id="a0587-141">Você precisa de uma conta de armazenamento no Azure para armazenar a imagem da VM carregada.</span><span class="sxs-lookup"><span data-stu-id="a0587-141">You need a storage account in Azure to store the uploaded VM image.</span></span> <span data-ttu-id="a0587-142">Você pode usar uma conta de armazenamento existente ou criar uma nova.</span><span class="sxs-lookup"><span data-stu-id="a0587-142">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="a0587-143">Para exibir as contas de armazenamento disponíveis, digite:</span><span class="sxs-lookup"><span data-stu-id="a0587-143">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="a0587-144">Se você quiser usar uma conta de armazenamento existente, vá para a seção [Carregar a imagem da VM](#upload-the-vm-vhd-to-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="a0587-144">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="a0587-145">Se você precisa criar uma conta de armazenamento, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="a0587-145">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="a0587-146">Você precisa do nome do grupo de recursos no qual a conta de armazenamento deve ser criada.</span><span class="sxs-lookup"><span data-stu-id="a0587-146">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="a0587-147">Para saber quais são todos os grupos de recursos que estão em sua assinatura, digite:</span><span class="sxs-lookup"><span data-stu-id="a0587-147">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="a0587-148">Para criar um grupo de recursos denominado **myResourceGroup** na região **Oeste dos EUA**, digite:</span><span class="sxs-lookup"><span data-stu-id="a0587-148">To create a resource group named **myResourceGroup** in the **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="a0587-149">Crie uma conta de armazenamento com o nome **mystorageaccount** neste grupo de recursos usando o cmdlet [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount):</span><span class="sxs-lookup"><span data-stu-id="a0587-149">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
 
### <a name="start-the-upload"></a><span data-ttu-id="a0587-150">Inicie o upload</span><span class="sxs-lookup"><span data-stu-id="a0587-150">Start the upload</span></span> 

<span data-ttu-id="a0587-151">Use o cmdlet [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) para carregar a imagem em um contêiner na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a0587-151">Use the [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet to upload the image to a container in your storage account.</span></span> <span data-ttu-id="a0587-152">Este exemplo carrega o arquivo **myVHD.vhd** de `"C:\Users\Public\Documents\Virtual hard disks\"` em uma conta de armazenamento denominada **mystorageaccount** no grupo de recursos **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="a0587-152">This example uploads the file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named **mystorageaccount** in the **myResourceGroup** resource group.</span></span> <span data-ttu-id="a0587-153">O arquivo será colocado em um contêiner chamado **mycontainer** e o novo nome do arquivo será **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="a0587-153">The file will be placed into the container named **mycontainer** and the new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="a0587-154">Se o comando tiver êxito, você receberá uma resposta semelhante a esta:</span><span class="sxs-lookup"><span data-stu-id="a0587-154">If successful, you get a response that looks similar to this:</span></span>

```powershell
MD5 hash is being calculated for the file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for the operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="a0587-155">Dependendo da conexão de rede e do tamanho do arquivo VHD, esse comando poderá demorar um pouco para concluir.</span><span class="sxs-lookup"><span data-stu-id="a0587-155">Depending on your network connection and the size of your VHD file, this command may take a while to complete.</span></span>


## <a name="create-a-new-vm"></a><span data-ttu-id="a0587-156">Criar uma nova VM</span><span class="sxs-lookup"><span data-stu-id="a0587-156">Create a new VM</span></span> 

<span data-ttu-id="a0587-157">Agora você pode utilizar o VHD carregado para criar uma nova VM.</span><span class="sxs-lookup"><span data-stu-id="a0587-157">You can now use the uploaded VHD to create a new VM.</span></span> 

### <a name="set-the-uri-of-the-vhd"></a><span data-ttu-id="a0587-158">Definir o URI do VHD</span><span class="sxs-lookup"><span data-stu-id="a0587-158">Set the URI of the VHD</span></span>

<span data-ttu-id="a0587-159">O URI do VHD a usar está no formato: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span><span class="sxs-lookup"><span data-stu-id="a0587-159">The URI for the VHD to use is in the format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="a0587-160">Neste exemplo, o VHD chamado **myVHD** está na conta de armazenamento **mystorageaccount** no contêiner **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="a0587-160">In this example the VHD named **myVHD** is in the storage account **mystorageaccount** in the container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="a0587-161">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="a0587-161">Create a virtual network</span></span>
<span data-ttu-id="a0587-162">Crie a vNet e a sub-rede da [rede virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0587-162">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="a0587-163">Crie a sub-rede.</span><span class="sxs-lookup"><span data-stu-id="a0587-163">Create the subnet.</span></span> <span data-ttu-id="a0587-164">O exemplo a seguir cria uma sub-rede chamada **mySubnet** no grupo de recursos **myResourceGroup** com o prefixo de endereço **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="a0587-164">The following sample creates a subnet named **mySubnet** in the resource group **myResourceGroup** with the address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="a0587-165">Crie a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="a0587-165">Create the virtual network.</span></span> <span data-ttu-id="a0587-166">O exemplo a seguir cria uma rede virtual chamada **myVnet** na localização **Oeste dos EUA** com o prefixo de endereço **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="a0587-166">The following sample creates a virtual network named **myVnet** in the **West US** location with the address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="a0587-167">Criar um endereço IP público e um adaptador de rede</span><span class="sxs-lookup"><span data-stu-id="a0587-167">Create a public IP address and network interface</span></span>
<span data-ttu-id="a0587-168">Para habilitar a comunicação com a máquina virtual na rede virtual, são necessários um [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e um adaptador de rede.</span><span class="sxs-lookup"><span data-stu-id="a0587-168">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="a0587-169">Criar um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="a0587-169">Create a public IP address.</span></span> <span data-ttu-id="a0587-170">Este exemplo cria um endereço IP público chamado **myPip**.</span><span class="sxs-lookup"><span data-stu-id="a0587-170">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="a0587-171">Crie a NIC.</span><span class="sxs-lookup"><span data-stu-id="a0587-171">Create the NIC.</span></span> <span data-ttu-id="a0587-172">Este exemplo cria uma NIC chamada **myNic**.</span><span class="sxs-lookup"><span data-stu-id="a0587-172">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="a0587-173">Criar o grupo de segurança de rede e uma regra RDP</span><span class="sxs-lookup"><span data-stu-id="a0587-173">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="a0587-174">Para fazer logon em sua VM usando RDP, é preciso ter uma regra de segurança que permita acesso RDP na porta 3389.</span><span class="sxs-lookup"><span data-stu-id="a0587-174">To be able to log in to your VM using RDP, you need to have a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="a0587-175">Este exemplo cria um NSG chamado **myNsg** que contém uma regra chamada **myRdpRule** que permite tráfego RDP pela porta 3389.</span><span class="sxs-lookup"><span data-stu-id="a0587-175">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="a0587-176">Para obter mais informações sobre NSGs, consulte [Abrir portas para uma VM no Azure usando PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a0587-176">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="a0587-177">Criar uma variável para a rede virtual</span><span class="sxs-lookup"><span data-stu-id="a0587-177">Create a variable for the virtual network</span></span>
<span data-ttu-id="a0587-178">Crie uma variável para a rede virtual concluída.</span><span class="sxs-lookup"><span data-stu-id="a0587-178">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-the-vm"></a><span data-ttu-id="a0587-179">Criar a VM</span><span class="sxs-lookup"><span data-stu-id="a0587-179">Create the VM</span></span>
<span data-ttu-id="a0587-180">O script do PowerShell a seguir mostra como definir as configurações da máquina virtual e usar a imagem da VM carregada como a fonte da nova instalação.</span><span class="sxs-lookup"><span data-stu-id="a0587-180">The following PowerShell script shows how to set up the virtual machine configurations and use the uploaded VM image as the source for the new installation.</span></span>



```powershell
# Enter a new user name and password to use as the local administrator account 
    # for remotely accessing the VM.
    $cred = Get-Credential

    # Name of the storage account where the VHD is located. This example sets the 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of the virtual machine. This example sets the VM name as "myVM".
    $vmName = "myVM"

    # Size of the virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See the VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for the VM. This examples sets the computer name as "myComputer".
    $computerName = "myComputer"

    # Name of the disk that holds the OS. This example sets the 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets the SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get the storage account where the uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set the VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set the Windows operating system configuration and add the NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create the OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure the OS disk to be created from the existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create the new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

## <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="a0587-181">Verificar se a VM foi criada</span><span class="sxs-lookup"><span data-stu-id="a0587-181">Verify that the VM was created</span></span>
<span data-ttu-id="a0587-182">Ao concluir, você deverá ver a VM recém-criada no [portal do Azure](https://portal.azure.com) em **Navegar** > **Máquinas virtuais** ou usando os seguintes comandos do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a0587-182">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="a0587-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a0587-183">Next steps</span></span>
<span data-ttu-id="a0587-184">Para gerenciar sua nova máquina virtual com o Azure PowerShell, consulte [Gerenciar máquinas virtuais usando o PowerShell e o Azure Resource Manager](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a0587-184">To manage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


