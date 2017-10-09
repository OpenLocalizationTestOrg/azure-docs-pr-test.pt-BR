---
title: "aaaCreate uma imagem não gerenciada de uma VM generalizada no Azure | Microsoft Docs"
description: "Crie uma imagem de unmanged de um generalizado toouse toocreate da VM do Windows várias cópias de uma VM no Azure."
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: b8a044d20313efa6dd9b9757e61154f922134476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-unmanaged-vm-image-from-an-azure-vm"></a><span data-ttu-id="a5245-103">Como toocreate uma VM não gerenciada de imagem de uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="a5245-103">How toocreate an unmanaged VM image from an Azure VM</span></span>

<span data-ttu-id="a5245-104">Este artigo abrange o uso de contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a5245-104">This article covers using storage accounts.</span></span> <span data-ttu-id="a5245-105">É recomendável que você utilize discos gerenciados e imagens gerenciadas em vez de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a5245-105">We recommend that you use managed disks and managed images instead of a storage account.</span></span> <span data-ttu-id="a5245-106">Para obter mais informações, consulte [Capture uma imagem gerenciada de uma VM generalizada no Azure](capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="a5245-106">For more information, see [Capture a managed image of a generalized VM in Azure](capture-image-resource.md).</span></span>

<span data-ttu-id="a5245-107">Este artigo mostra como toouse do Azure PowerShell toocreate uma imagem de uma VM generalizada do Azure usando uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a5245-107">This article shows you how toouse Azure PowerShell toocreate an image of a generalized Azure VM using a storage account.</span></span> <span data-ttu-id="a5245-108">Você pode usar Olá imagem toocreate outra VM.</span><span class="sxs-lookup"><span data-stu-id="a5245-108">You can then use hello image toocreate another VM.</span></span> <span data-ttu-id="a5245-109">imagem de saudação inclui o disco do sistema operacional hello e discos de dados de saudação que estão anexados toohello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a5245-109">hello image includes hello OS disk and hello data disks that are attached toohello virtual machine.</span></span> <span data-ttu-id="a5245-110">imagem de saudação não inclui recursos de rede virtual Olá, para que seja necessário tooset esses recursos quando você cria Olá nova VM.</span><span class="sxs-lookup"><span data-stu-id="a5245-110">hello image doesn't include hello virtual network resources, so you need tooset up those resources when you create hello new VM.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a5245-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a5245-111">Prerequisites</span></span>
<span data-ttu-id="a5245-112">Você precisa toohave Azure PowerShell versão 1.0. x ou posterior esteja instalado.</span><span class="sxs-lookup"><span data-stu-id="a5245-112">You need toohave Azure PowerShell version 1.0.x or newer installed.</span></span> <span data-ttu-id="a5245-113">Se você ainda não instalou PowerShell, leia [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para etapas de instalação.</span><span class="sxs-lookup"><span data-stu-id="a5245-113">If you haven't already installed PowerShell, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for installation steps.</span></span>

## <a name="generalize-hello-vm"></a><span data-ttu-id="a5245-114">Generalize Olá VM</span><span class="sxs-lookup"><span data-stu-id="a5245-114">Generalize hello VM</span></span> 
<span data-ttu-id="a5245-115">Esta seção mostra como toogeneralize sua máquina virtual do Windows para uso como uma imagem.</span><span class="sxs-lookup"><span data-stu-id="a5245-115">This section shows you how toogeneralize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="a5245-116">Generalizando uma VM remove todas as suas informações de conta pessoal, entre outras coisas e o prepara Olá máquina toobe usado como uma imagem.</span><span class="sxs-lookup"><span data-stu-id="a5245-116">Generalizing a VM removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="a5245-117">Para obter detalhes sobre o Sysprep, consulte [como tooUse Sysprep: uma introdução](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5245-117">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="a5245-118">Certifique-se de funções de servidor de saudação em execução na máquina Olá Sysprep oferece suporte.</span><span class="sxs-lookup"><span data-stu-id="a5245-118">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="a5245-119">Para obter mais informações, consulte [Suporte do Sysprep para funções de servidor](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="a5245-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a5245-120">Se você estiver carregando tooAzure seu VHD para Olá a primeira vez, verifique se você tem [preparado sua VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de executar o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="a5245-120">If you are uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

<span data-ttu-id="a5245-121">Você também pode generalizar uma VM do Linux usando `sudo waagent -deprovision+user` e, em seguida, use PowerShell toocapture Olá VM.</span><span class="sxs-lookup"><span data-stu-id="a5245-121">You can also generalize a Linux VM using `sudo waagent -deprovision+user` and then use PowerShell toocapture hello VM.</span></span> <span data-ttu-id="a5245-122">Para obter informações sobre como usar o hello CLI toocapture uma VM, consulte [como toogeneralize e capturar uma máquina virtual Linux usando Olá CLI do Azure ](../linux/capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="a5245-122">For information about using hello CLI toocapture a VM, see [How toogeneralize and capture a Linux virtual machine using hello Azure CLI ](../linux/capture-image.md).</span></span>


1. <span data-ttu-id="a5245-123">Entrar toohello máquina virtual do Windows.</span><span class="sxs-lookup"><span data-stu-id="a5245-123">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="a5245-124">Abra a janela de Prompt de comando hello como administrador.</span><span class="sxs-lookup"><span data-stu-id="a5245-124">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="a5245-125">Altere o diretório de saudação muito**%windir%\system32\sysprep**e, em seguida, execute `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="a5245-125">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="a5245-126">Em Olá **ferramenta de preparação do sistema** caixa de diálogo, selecione **Enter System Out-of-Box Experience (OOBE)**e certifique-se de que Olá **generalizar** caixa de seleção é marcada.</span><span class="sxs-lookup"><span data-stu-id="a5245-126">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="a5245-127">Em **Opções de Desligamento**, selecione **Desligar**.</span><span class="sxs-lookup"><span data-stu-id="a5245-127">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="a5245-128">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5245-128">Click **OK**.</span></span>
   
    ![Inicie o Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="a5245-130">Quando o Sysprep for concluído, desligar máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5245-130">When Sysprep completes, it shuts down hello virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="a5245-131">Não reinicie Olá VM até que você esteja concluído tooAzure VHD Olá carregar ou criar uma imagem de VM de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5245-131">Do not restart hello VM until you are done uploading hello VHD tooAzure or creating an image from hello VM.</span></span> <span data-ttu-id="a5245-132">Se acidentalmente Olá VM é reiniciada, execute Sysprep toogeneralize-a novamente.</span><span class="sxs-lookup"><span data-stu-id="a5245-132">If hello VM accidentally gets restarted, run Sysprep toogeneralize it again.</span></span>
> 
> 

## <a name="log-in-tooazure-powershell"></a><span data-ttu-id="a5245-133">Faça logon no tooAzure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5245-133">Log in tooAzure PowerShell</span></span>
1. <span data-ttu-id="a5245-134">Abra o PowerShell do Azure e entrar tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5245-134">Open Azure PowerShell and sign in tooyour Azure account.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    <span data-ttu-id="a5245-135">Uma janela pop-up é aberto para você tooenter suas credenciais de conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5245-135">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
2. <span data-ttu-id="a5245-136">Obter IDs de assinatura Olá para suas assinaturas disponíveis.</span><span class="sxs-lookup"><span data-stu-id="a5245-136">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="a5245-137">Definir Olá assinatura correto usando a ID de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5245-137">Set hello correct subscription using hello subscription ID.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-hello-vm-and-set-hello-state-toogeneralized"></a><span data-ttu-id="a5245-138">Desalocar Olá VM e defina Olá estado toogeneralized</span><span class="sxs-lookup"><span data-stu-id="a5245-138">Deallocate hello VM and set hello state toogeneralized</span></span>
1. <span data-ttu-id="a5245-139">Desalocar recursos de saudação de VM.</span><span class="sxs-lookup"><span data-stu-id="a5245-139">Deallocate hello VM resources.</span></span>
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    <span data-ttu-id="a5245-140">Olá *Status* para Olá VM em hello Azure portal muda de **parado** muito**parado (desalocado)**.</span><span class="sxs-lookup"><span data-stu-id="a5245-140">hello *Status* for hello VM in hello Azure portal changes from **Stopped** too**Stopped (deallocated)**.</span></span>
2. <span data-ttu-id="a5245-141">Definir status da saudação da máquina virtual de saudação muito**generalizado**.</span><span class="sxs-lookup"><span data-stu-id="a5245-141">Set hello status of hello virtual machine too**Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. <span data-ttu-id="a5245-142">Verificar status de saudação do hello VM.</span><span class="sxs-lookup"><span data-stu-id="a5245-142">Check hello status of hello VM.</span></span> <span data-ttu-id="a5245-143">Olá **OSState/generalizadas** seção Olá VM deve ter Olá **DisplayStatus** definido muito**VM generalizado**.</span><span class="sxs-lookup"><span data-stu-id="a5245-143">hello **OSState/generalized** section for hello VM should have hello **DisplayStatus** set too**VM generalized**.</span></span>  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-hello-image"></a><span data-ttu-id="a5245-144">Criar imagem Olá</span><span class="sxs-lookup"><span data-stu-id="a5245-144">Create hello image</span></span>

<span data-ttu-id="a5245-145">Crie uma imagem de máquina virtual não gerenciada no contêiner de armazenamento de destino hello usando este comando.</span><span class="sxs-lookup"><span data-stu-id="a5245-145">Create an unmanaged virtual machine image in hello destination storage container using this command.</span></span> <span data-ttu-id="a5245-146">Hello imagem é criada no hello mesma conta de armazenamento como Olá máquina virtual original.</span><span class="sxs-lookup"><span data-stu-id="a5245-146">hello image is created in hello same storage account as hello original virtual machine.</span></span> <span data-ttu-id="a5245-147">Olá `-Path` parâmetro salva uma cópia do modelo JSON Olá Olá computador de origem VM tooyour local.</span><span class="sxs-lookup"><span data-stu-id="a5245-147">hello `-Path` parameter saves a copy of hello JSON template for hello source VM tooyour local computer.</span></span> <span data-ttu-id="a5245-148">Olá `-DestinationContainerName` parâmetro é o nome de saudação do contêiner de saudação que você deseja toohold suas imagens.</span><span class="sxs-lookup"><span data-stu-id="a5245-148">hello `-DestinationContainerName` parameter is hello name of hello container that you want toohold your images.</span></span> <span data-ttu-id="a5245-149">Se o contêiner de saudação não existir, ele é criado para você.</span><span class="sxs-lookup"><span data-stu-id="a5245-149">If hello container doesn't exist, it is created for you.</span></span>
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
<span data-ttu-id="a5245-150">Você pode obter Olá URL da imagem de modelo de arquivo hello JSON.</span><span class="sxs-lookup"><span data-stu-id="a5245-150">You can get hello URL of your image from hello JSON file template.</span></span> <span data-ttu-id="a5245-151">Vá toohello **recursos** > **storageProfile** > **osDisk** > **imagem**  >  **uri** seção de caminho completo de saudação da imagem.</span><span class="sxs-lookup"><span data-stu-id="a5245-151">Go toohello **resources** > **storageProfile** > **osDisk** > **image** > **uri** section for hello complete path of your image.</span></span> <span data-ttu-id="a5245-152">Olá URL da imagem de saudação se parece com: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span><span class="sxs-lookup"><span data-stu-id="a5245-152">hello URL of hello image looks like: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span></span>
   
<span data-ttu-id="a5245-153">Você também pode verificar Olá URI no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5245-153">You can also verify hello URI in hello portal.</span></span> <span data-ttu-id="a5245-154">imagem de saudação é copiado tooa contêiner nomeado **sistema** em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a5245-154">hello image is copied tooa container named **system** in your storage account.</span></span> 

## <a name="create-a-vm-from-hello-image"></a><span data-ttu-id="a5245-155">Criar uma VM da imagem Olá</span><span class="sxs-lookup"><span data-stu-id="a5245-155">Create a VM from hello image</span></span>

<span data-ttu-id="a5245-156">Agora você pode criar uma ou mais máquinas virtuais de imagem de saudação não gerenciado.</span><span class="sxs-lookup"><span data-stu-id="a5245-156">Now you can create one or more VMs from hello unmanaged image.</span></span>

### <a name="set-hello-uri-of-hello-vhd"></a><span data-ttu-id="a5245-157">Saudação de conjunto de URI do VHD de saudação</span><span class="sxs-lookup"><span data-stu-id="a5245-157">Set hello URI of hello VHD</span></span>

<span data-ttu-id="a5245-158">Olá URI para Olá VHD toouse está no formato de saudação: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**. vhd.</span><span class="sxs-lookup"><span data-stu-id="a5245-158">hello URI for hello VHD toouse is in hello format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="a5245-159">Neste exemplo hello VHD denominado **myVHD** é na conta de armazenamento Olá **mystorageaccount** no contêiner Olá **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="a5245-159">In this example hello VHD named **myVHD** is in hello storage account **mystorageaccount** in hello container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="a5245-160">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="a5245-160">Create a virtual network</span></span>
<span data-ttu-id="a5245-161">Criar rede virtual de saudação e a sub-rede de saudação [rede virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a5245-161">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="a5245-162">Crie uma sub-rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5245-162">Create hello subnet.</span></span> <span data-ttu-id="a5245-163">Olá, exemplo a seguir cria uma sub-rede denominada **mySubnet** no grupo de recursos de saudação **myResourceGroup** com prefixo de endereço de saudação **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="a5245-163">hello following sample creates a subnet named **mySubnet** in hello resource group **myResourceGroup** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="a5245-164">Crie rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="a5245-164">Create hello virtual network.</span></span> <span data-ttu-id="a5245-165">Olá, exemplo a seguir cria uma rede virtual denominada **myVnet** em Olá **Oeste dos EUA** local com o prefixo de endereço de saudação **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="a5245-165">hello following sample creates a virtual network named **myVnet** in hello **West US** location with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="a5245-166">Criar um endereço IP público e um adaptador de rede</span><span class="sxs-lookup"><span data-stu-id="a5245-166">Create a public IP address and network interface</span></span>
<span data-ttu-id="a5245-167">comunicação tooenable com máquina virtual de saudação na rede virtual Olá, é necessário um [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e uma interface de rede.</span><span class="sxs-lookup"><span data-stu-id="a5245-167">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="a5245-168">Criar um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="a5245-168">Create a public IP address.</span></span> <span data-ttu-id="a5245-169">Este exemplo cria um endereço IP público chamado **myPip**.</span><span class="sxs-lookup"><span data-stu-id="a5245-169">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="a5245-170">Criar NIC hello.</span><span class="sxs-lookup"><span data-stu-id="a5245-170">Create hello NIC.</span></span> <span data-ttu-id="a5245-171">Este exemplo cria uma NIC chamada **myNic**.</span><span class="sxs-lookup"><span data-stu-id="a5245-171">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="a5245-172">Criar um grupo de segurança de rede hello e uma regra RDP</span><span class="sxs-lookup"><span data-stu-id="a5245-172">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="a5245-173">toolog capaz de toobe em tooyour VM usando o RDP, você precisa toohave uma regra de segurança que permita o acesso RDP na porta 3389.</span><span class="sxs-lookup"><span data-stu-id="a5245-173">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="a5245-174">Este exemplo cria um NSG chamado **myNsg** que contém uma regra chamada **myRdpRule** que permite tráfego RDP pela porta 3389.</span><span class="sxs-lookup"><span data-stu-id="a5245-174">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="a5245-175">Para obter mais informações sobre os NSGs, consulte [a abertura de portas tooa VM no Azure usando o PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a5245-175">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="a5245-176">Criar uma variável para a rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="a5245-176">Create a variable for hello virtual network</span></span>
<span data-ttu-id="a5245-177">Crie uma variável para a rede virtual Olá concluída.</span><span class="sxs-lookup"><span data-stu-id="a5245-177">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a><span data-ttu-id="a5245-178">Criar hello VM</span><span class="sxs-lookup"><span data-stu-id="a5245-178">Create hello VM</span></span>
<span data-ttu-id="a5245-179">Olá PowerShell a seguir conclui as configurações de máquina virtual de saudação e usa a imagem do não gerenciada como fonte de saudação para nova instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5245-179">hello following PowerShell completes hello virtual machine configurations and uses unmanaged image as hello source for hello new installation.</span></span>

</br>

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

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="a5245-180">Verifique se esse Olá que VM foi criada</span><span class="sxs-lookup"><span data-stu-id="a5245-180">Verify that hello VM was created</span></span>
<span data-ttu-id="a5245-181">Ao concluir, você deverá ver Olá recém-criado VM em Olá [portal do Azure](https://portal.azure.com) em **procurar** > **máquinas virtuais**, ou usando o seguinte Olá Comandos do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a5245-181">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="a5245-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a5245-182">Next steps</span></span>
<span data-ttu-id="a5245-183">toomanage nova máquina virtual com o Azure PowerShell, consulte [gerenciar máquinas virtuais usando o Gerenciador de recursos do Azure e PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a5245-183">toomanage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


