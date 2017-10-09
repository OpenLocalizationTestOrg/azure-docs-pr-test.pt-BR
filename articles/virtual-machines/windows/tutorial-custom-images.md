---
title: imagens VM personalizadas aaaCreate com hello Azure PowerShell | Microsoft Docs
description: Tutorial - criar uma imagem VM personalizada usando hello Azure PowerShell.
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 3a759fe1b7e7b72f531399b0f4a99e341713c6a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a><span data-ttu-id="cf6a1-103">Criar uma imagem personalizada de uma VM do Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf6a1-103">Create a custom image of an Azure VM using PowerShell</span></span>

<span data-ttu-id="cf6a1-104">Imagens personalizadas são como imagens do marketplace, mas você mesmo as cria.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="cf6a1-105">Imagens personalizadas podem ser usado toobootstrap configurações como pré-carregamento de aplicativos, configurações de aplicativo e outras configurações do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-105">Custom images can be used toobootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="cf6a1-106">Neste tutorial, você criará sua própria imagem personalizada de uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="cf6a1-107">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="cf6a1-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cf6a1-108">Aplicar Sysprep e generalizar VMs</span><span class="sxs-lookup"><span data-stu-id="cf6a1-108">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="cf6a1-109">Criar uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="cf6a1-109">Create a custom image</span></span>
> * <span data-ttu-id="cf6a1-110">Criar uma VM por meio de uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="cf6a1-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="cf6a1-111">Lista todas as imagens de saudação em sua assinatura</span><span class="sxs-lookup"><span data-stu-id="cf6a1-111">List all hello images in your subscription</span></span>
> * <span data-ttu-id="cf6a1-112">Excluir uma imagem</span><span class="sxs-lookup"><span data-stu-id="cf6a1-112">Delete an image</span></span>

<span data-ttu-id="cf6a1-113">Este tutorial requer hello Azure PowerShell versão 3.6 ou posterior do módulo.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="cf6a1-114">Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="cf6a1-115">Se você precisar tooupgrade, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="cf6a1-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="cf6a1-116">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="cf6a1-116">Before you begin</span></span>

<span data-ttu-id="cf6a1-117">etapas de saudação abaixo detalham como tootake uma VM existente e desative-o para um personalizado pode ser reutilizado da imagem que você podem usar toocreate novas instâncias VM.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-117">hello steps below detail how tootake an existing VM and turn it into a re-usable custom image that you can use toocreate new VM instances.</span></span>

<span data-ttu-id="cf6a1-118">exemplo de hello toocomplete neste tutorial, você deve ter uma máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-118">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="cf6a1-119">Se necessário, este [exemplo de script](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) pode criar uma para você.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-119">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="cf6a1-120">Trabalho tutorial hello, substitua VM e o grupo de recursos de saudação nomes onde for necessário.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-120">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

## <a name="prepare-vm"></a><span data-ttu-id="cf6a1-121">Preparar VM</span><span class="sxs-lookup"><span data-stu-id="cf6a1-121">Prepare VM</span></span>

<span data-ttu-id="cf6a1-122">toocreate uma imagem de uma máquina virtual, você precisa tooprepare Olá VM por Olá generalizar VM, desalocando e marcando fonte Olá VM como generalizada no Azure.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-122">toocreate an image of a virtual machine, you need tooprepare hello VM by generalizing hello VM, deallocating, and then marking hello source VM as generalized in Azure.</span></span>

### <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="cf6a1-123">Generalize Olá VM do Windows usando Sysprep</span><span class="sxs-lookup"><span data-stu-id="cf6a1-123">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="cf6a1-124">O Sysprep remove todas as suas informações de conta pessoal, entre outras coisas e prepara Olá máquina toobe usado como uma imagem.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-124">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="cf6a1-125">Para obter detalhes sobre o Sysprep, consulte [como tooUse Sysprep: uma introdução](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf6a1-125">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>


1. <span data-ttu-id="cf6a1-126">Conecte-se a máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-126">Connect toohello virtual machine.</span></span>
2. <span data-ttu-id="cf6a1-127">Abra a janela de Prompt de comando hello como administrador.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-127">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="cf6a1-128">Altere o diretório de saudação muito*%windir%\system32\sysprep*e, em seguida, execute *sysprep.exe*.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-128">Change hello directory too*%windir%\system32\sysprep*, and then run *sysprep.exe*.</span></span>
3. <span data-ttu-id="cf6a1-129">Em Olá **ferramenta de preparação do sistema** caixa de diálogo, selecione *Enter System Out-of-Box Experience (OOBE)*e certifique-se de que Olá *generalizar* caixa de seleção é marcada.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-129">In hello **System Preparation Tool** dialog box, select *Enter System Out-of-Box Experience (OOBE)*, and make sure that hello *Generalize* check box is selected.</span></span>
4. <span data-ttu-id="cf6a1-130">Em **Opções de Desligamento**, selecione *Desligar* e em **OK**.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-130">In **Shutdown Options**, select *Shutdown* and then click **OK**.</span></span>
5. <span data-ttu-id="cf6a1-131">Quando o Sysprep for concluído, desligar máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-131">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="cf6a1-132">**Não reinicie Olá VM**.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-132">**Do not restart hello VM**.</span></span>

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a><span data-ttu-id="cf6a1-133">Desalocar e marcar Olá VM como generalizado</span><span class="sxs-lookup"><span data-stu-id="cf6a1-133">Deallocate and mark hello VM as generalized</span></span>

<span data-ttu-id="cf6a1-134">toocreate uma imagem, Olá VM precisa toobe desalocadas e marcado como generalizada no Azure.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-134">toocreate an image, hello VM needs toobe deallocated and marked as generalized in Azure.</span></span>

<span data-ttu-id="cf6a1-135">Olá desalocada VM usando [AzureRmVM Stop](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="cf6a1-135">Deallocated hello VM using [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

<span data-ttu-id="cf6a1-136">Definir status da saudação da máquina virtual de saudação muito`-Generalized` usando [AzureRmVm conjunto](/powershell/module/azurerm.compute/set-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="cf6a1-136">Set hello status of hello virtual machine too`-Generalized` using [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span></span> 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-hello-image"></a><span data-ttu-id="cf6a1-137">Criar imagem Olá</span><span class="sxs-lookup"><span data-stu-id="cf6a1-137">Create hello image</span></span>

<span data-ttu-id="cf6a1-138">Agora você pode criar uma imagem de VM de saudação usando [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) e [AzureRmImage novo](/powershell/module/azurerm.compute/new-azurermimage).</span><span class="sxs-lookup"><span data-stu-id="cf6a1-138">Now you can create an image of hello VM by using [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) and [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span></span> <span data-ttu-id="cf6a1-139">Olá, exemplo a seguir cria uma imagem chamada *myImage* de uma VM denominada *myVM*.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-139">hello following example creates an image named *myImage* from a VM named *myVM*.</span></span>

<span data-ttu-id="cf6a1-140">Obtenha a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-140">Get hello virtual machine.</span></span> 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

<span data-ttu-id="cf6a1-141">Crie a configuração de imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-141">Create hello image configuration.</span></span>

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

<span data-ttu-id="cf6a1-142">Crie imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-142">Create hello image.</span></span>

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-hello-image"></a><span data-ttu-id="cf6a1-143">Criar VMs de imagem Olá</span><span class="sxs-lookup"><span data-stu-id="cf6a1-143">Create VMs from hello image</span></span>

<span data-ttu-id="cf6a1-144">Agora que você tem uma imagem, você pode criar um ou mais novas VMs de imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-144">Now that you have an image, you can create one or more new VMs from hello image.</span></span> <span data-ttu-id="cf6a1-145">Criando uma máquina virtual a partir de uma imagem personalizada é muito semelhante toocreating uma VM usando uma imagem do Marketplace.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-145">Creating a VM from a custom image is very similar toocreating a VM using a Marketplace image.</span></span> <span data-ttu-id="cf6a1-146">Quando você usar uma imagem do Marketplace, você tem tooinformation sobre imagem hello, provedor de imagens, oferta, SKU e versão.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-146">When you use a Marketplace image, you have tooinformation about hello image, image provider, offer, SKU and version.</span></span> <span data-ttu-id="cf6a1-147">Com uma imagem personalizada, você precisa apenas tooprovide Olá ID de recurso de imagem personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-147">With a custom image, you just need tooprovide hello ID of hello custom image resource.</span></span> 

<span data-ttu-id="cf6a1-148">Olá script a seguir, criamos uma variável *$image* toostore informações sobre como usar o hello imagem personalizada [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) e, em seguida, usamos [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)e especifique a ID hello usando Olá *$image* variável que acabamos de criar.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-148">In hello following script, we create a variable *$image* toostore information about hello custom image using [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) and then we use [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) and specify hello ID using hello *$image* variable we just created.</span></span> 

<span data-ttu-id="cf6a1-149">script Hello cria uma VM denominada *myVMfromImage* do nosso imagem personalizada em um novo grupo de recursos denominado *myResourceGroupFromImage* em Olá *Oeste dos EUA* local.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-149">hello script creates a VM named *myVMfromImage* from our custom image in a new resource group named *myResourceGroupFromImage* in hello *West US* location.</span></span>


```powershell
$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

New-AzureRmResourceGroup -Name myResourceGroupFromImage -Location EastUS

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name "mypublicdns$(Get-Random)" `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4

  $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

  $nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$vmConfig = New-AzureRmVMConfig `
    -VMName myVMfromImage `
    -VMSize Standard_D1 | Set-AzureRmVMOperatingSystem -Windows `
        -ComputerName myComputer `
        -Credential $cred 

# Here is where we create a variable toostore information about hello image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want toocreate hello VM from and image and provide hello image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a><span data-ttu-id="cf6a1-150">Gerenciamento de imagens</span><span class="sxs-lookup"><span data-stu-id="cf6a1-150">Image management</span></span> 

<span data-ttu-id="cf6a1-151">Aqui estão alguns exemplos de tarefas comuns de gerenciamento de imagem e como toocomplete-los usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-151">Here are some examples of common management image tasks and how toocomplete them using PowerShell.</span></span>

<span data-ttu-id="cf6a1-152">Liste todas as imagens por nome.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-152">List all images by name.</span></span>

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

<span data-ttu-id="cf6a1-153">Exclua uma imagem.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-153">Delete an image.</span></span> <span data-ttu-id="cf6a1-154">Este exemplo exclui Olá imagem chamada *myOldImage* de saudação *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-154">This example deletes hello image named *myOldImage* from hello *myResourceGroup*.</span></span>

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="cf6a1-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cf6a1-155">Next steps</span></span>

<span data-ttu-id="cf6a1-156">Neste tutorial, você criou uma imagem de VM personalizada.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-156">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="cf6a1-157">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="cf6a1-157">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cf6a1-158">Aplicar Sysprep e generalizar VMs</span><span class="sxs-lookup"><span data-stu-id="cf6a1-158">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="cf6a1-159">Criar uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="cf6a1-159">Create a custom image</span></span>
> * <span data-ttu-id="cf6a1-160">Criar uma VM por meio de uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="cf6a1-160">Create a VM from a custom image</span></span>
> * <span data-ttu-id="cf6a1-161">Lista todas as imagens de saudação em sua assinatura</span><span class="sxs-lookup"><span data-stu-id="cf6a1-161">List all hello images in your subscription</span></span>
> * <span data-ttu-id="cf6a1-162">Excluir uma imagem</span><span class="sxs-lookup"><span data-stu-id="cf6a1-162">Delete an image</span></span>

<span data-ttu-id="cf6a1-163">Avançar toohello toolearn próximo de tutorial sobre máquinas virtuais como altamente disponíveis.</span><span class="sxs-lookup"><span data-stu-id="cf6a1-163">Advance toohello next tutorial toolearn about how highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cf6a1-164">Criar VMs altamente disponíveis</span><span class="sxs-lookup"><span data-stu-id="cf6a1-164">Create highly available VMs</span></span>](tutorial-availability-sets.md)



