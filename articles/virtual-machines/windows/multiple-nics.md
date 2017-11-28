---
title: "Crie e gerencie as VMs do Windows no Azure que usam várias NICs | Microsoft Docs"
description: "Saiba como criar e gerenciar uma VM do Windows que tem várias NICs anexadas usando o Azure PowerShell ou modelos do Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 9bff5b6d-79ac-476b-a68f-6f8754768413
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: 3bd99a67dae41de3533d7f6e244eb7ee3ecc4049
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a><span data-ttu-id="d9cf7-103">Cria e gerencia uma máquina virtual do Windows que tem várias NICs</span><span class="sxs-lookup"><span data-stu-id="d9cf7-103">Create and manage a Windows virtual machine that has multiple NICs</span></span>
<span data-ttu-id="d9cf7-104">As máquinas virtuais (VMs) no Azure podem ter várias placas de interface de rede virtual (NICs) anexadas a elas.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-104">Virtual machines (VMs) in Azure can have multiple virtual network interface cards (NICs) attached to them.</span></span> <span data-ttu-id="d9cf7-105">Um cenário comum é ter sub-redes diferentes para conectividade de front-end e de back-end ou uma rede dedicada a uma solução de monitoramento ou de backup.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-105">A common scenario is to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="d9cf7-106">Este artigo fornece detalhes sobre como criar uma VM que tem várias NICs anexadas.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-106">This article details how to create a VM that has multiple NICs attached to it.</span></span> <span data-ttu-id="d9cf7-107">Você também aprenderá a adicionar ou remover as NICs de uma VM existente.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-107">You also learn how to add or remove NICs from an existing VM.</span></span> <span data-ttu-id="d9cf7-108">Diferentes [tamanhos de VM](sizes.md) dão suporte a um número variável de NICs, sendo assim, dimensione sua VM adequadamente.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="d9cf7-109">Para obter informações detalhadas, incluindo como criar várias NICs dentro de seus próprios scripts do PowerShell, consulte [implantação de VMs com várias NICs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d9cf7-109">For detailed information, including how to create multiple NICs within your own PowerShell scripts, see [deploying multiple-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9cf7-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d9cf7-110">Prerequisites</span></span>
<span data-ttu-id="d9cf7-111">Verifique se você tem [ a versão mais recente do Azure PowerShell instalada e configurada](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d9cf7-111">Make sure that you have the [latest Azure PowerShell version installed and configured](/powershell/azure/overview).</span></span>

<span data-ttu-id="d9cf7-112">Nos exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-112">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="d9cf7-113">Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *myVnet* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-113">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>


## <a name="create-a-vm-with-multiple-nics"></a><span data-ttu-id="d9cf7-114">Criar uma VM com diversos NICs</span><span class="sxs-lookup"><span data-stu-id="d9cf7-114">Create a VM with multiple NICs</span></span>
<span data-ttu-id="d9cf7-115">Em primeiro lugar, crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-115">First, create a resource group.</span></span> <span data-ttu-id="d9cf7-116">O exemplo a seguir cria um grupo de recursos chamado *myResourceGroup* no local *EastUs*:</span><span class="sxs-lookup"><span data-stu-id="d9cf7-116">The following example creates a resource group named *myResourceGroup* in the *EastUs* location:</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a><span data-ttu-id="d9cf7-117">Crie a rede virtual e as sub-redes</span><span class="sxs-lookup"><span data-stu-id="d9cf7-117">Create virtual network and subnets</span></span>
<span data-ttu-id="d9cf7-118">Um cenário comum é para uma rede virtual ter duas ou mais sub-redes.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-118">A common scenario is for a virtual network to have two or more subnets.</span></span> <span data-ttu-id="d9cf7-119">Uma sub-rede pode ser usada para o tráfego de front-end, a outra para o tráfego de back-end.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-119">One subnet may be for front-end traffic, the other for back-end traffic.</span></span> <span data-ttu-id="d9cf7-120">Para se conectar a ambas as sub-redes, você usa várias NICs em sua VM.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-120">To connect to both subnets, you then use multiple NICs on your VM.</span></span>

1. <span data-ttu-id="d9cf7-121">Defina duas sub-redes de rede virtual com [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="d9cf7-121">Define two virtual network subnets with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="d9cf7-122">O exemplo a seguir define as sub-redes, para *mySubnetFrontEnd* e *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="d9cf7-122">The following example defines the subnets for *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. <span data-ttu-id="d9cf7-123">Crie uma rede virtual e sub-redes com [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="d9cf7-123">Create your virtual network and subnets with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="d9cf7-124">O seguinte exemplo cria uma rede virtual chamada *myVnet*:</span><span class="sxs-lookup"><span data-stu-id="d9cf7-124">The following example creates a virtual network named *myVnet*:</span></span>

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a><span data-ttu-id="d9cf7-125">Crie múltiplas NICs</span><span class="sxs-lookup"><span data-stu-id="d9cf7-125">Create multiple NICs</span></span>
<span data-ttu-id="d9cf7-126">Crie duas NICs com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="d9cf7-126">Create two NICs with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="d9cf7-127">Anexe uma NIC à sub-rede de front-end e uma NIC à sub-rede de back-end.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-127">Attach one NIC to the front-end subnet and one NIC to the back-end subnet.</span></span> <span data-ttu-id="d9cf7-128">O exemplo a seguir cria NICs, chamadas *myNic1* e *myNic2*:</span><span class="sxs-lookup"><span data-stu-id="d9cf7-128">The following example creates NICs named *myNic1* and *myNic2*:</span></span>

```powershell
$frontEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetFrontEnd'}
$myNic1 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic1" `
    -Location "EastUs" `
    -SubnetId $frontEnd.Id

$backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}
$myNic2 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic2" `
    -Location "EastUs" `
    -SubnetId $backEnd.Id
```

<span data-ttu-id="d9cf7-129">Normalmente, você também criaria um [grupo de segurança de rede](../../virtual-network/virtual-networks-nsg.md) ou [balanceador de carga](../../load-balancer/load-balancer-overview.md) para ajudar a gerenciar e distribuir o tráfego entre suas VMs.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-129">Typically you also create a [network security group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) to help manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="d9cf7-130">O artigo [mais detalhado sobre VMs com várias NICs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) o orientará na criação de um grupo de segurança de rede e na atribuição de NICs.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-130">The [more detailed multiple-NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) article guides you through creating a network security group and assigning NICs.</span></span>

### <a name="create-the-virtual-machine"></a><span data-ttu-id="d9cf7-131">Criar a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d9cf7-131">Create the virtual machine</span></span>
<span data-ttu-id="d9cf7-132">Agora, comece a criar sua configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-132">Now start to build your VM configuration.</span></span> <span data-ttu-id="d9cf7-133">Cada tamanho de VM tem um limite para o número total de NICs que podem ser adicionada a uma VM.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-133">Each VM size has a limit for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="d9cf7-134">Para obter mais informações, consulte [Tamanhos da VM no Windows](sizes.md) .</span><span class="sxs-lookup"><span data-stu-id="d9cf7-134">For more information, see [Windows VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="d9cf7-135">Defina suas credenciais de VM para a variável `$cred` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d9cf7-135">Set your VM credentials to the `$cred` variable as follows:</span></span>

    ```powershell
    $cred = Get-Credential
    ```

2. <span data-ttu-id="d9cf7-136">Defina sua VM com [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span><span class="sxs-lookup"><span data-stu-id="d9cf7-136">Define your VM with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span></span> <span data-ttu-id="d9cf7-137">O exemplo a seguir define uma VM chamada *myVM* e usa um tamanho de VM que dá suporte a até duas NICs (*Standard_DS3_v2*):</span><span class="sxs-lookup"><span data-stu-id="d9cf7-137">The following example defines a VM named *myVM* and uses a VM size that supports more than two NICs (*Standard_DS3_v2*):</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. <span data-ttu-id="d9cf7-138">Cria o restante da sua configuração de VM com [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) e [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span><span class="sxs-lookup"><span data-stu-id="d9cf7-138">Create the rest of your VM configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) and [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span></span> <span data-ttu-id="d9cf7-139">O exemplo a seguir cria uma VM do Windows Server 2016:</span><span class="sxs-lookup"><span data-stu-id="d9cf7-139">The following example creates a Windows Server 2016 VM:</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig `
        -Windows `
        -ComputerName "myVM" `
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig `
        -PublisherName "MicrosoftWindowsServer" `
        -Offer "WindowsServer" `
        -Skus "2016-Datacenter" `
        -Version "latest"
   ```

4. <span data-ttu-id="d9cf7-140">Anexe as duas NICs que você criou anteriormente com [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="d9cf7-140">Attach the two NICs that you previously created with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. <span data-ttu-id="d9cf7-141">Finalmente, crie sua VM com [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="d9cf7-141">Finally, create your VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-to-an-existing-vm"></a><span data-ttu-id="d9cf7-142">Adicionar uma NIC a uma VM existente</span><span class="sxs-lookup"><span data-stu-id="d9cf7-142">Add a NIC to an existing VM</span></span>
<span data-ttu-id="d9cf7-143">Para adicionar uma NIC virtual a uma VM existente, você desalocar a VM, adiciona a NIC virtual e inicia a VM.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-143">To add a virtual NIC to an existing VM, you deallocate the VM, add the virtual NIC, then start the VM.</span></span>

1. <span data-ttu-id="d9cf7-144">Desaloque a VM com o [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="d9cf7-144">Deallocate the VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="d9cf7-145">O seguinte exemplo desaloca a VM chamada *myVM* no *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="d9cf7-145">The following example deallocates the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="d9cf7-146">Obtenha a configuração existente da VM com [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="d9cf7-146">Get the existing configuration of the VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="d9cf7-147">O exemplo a seguir obtém informações sobre a VM chamada *myVM* no *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="d9cf7-147">The following example gets information for the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="d9cf7-148">O exemplo a seguir cria uma NIC virtual com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) chamada *myNic3* que está anexada ao *mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-148">The following example creates a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) named *myNic3* that is attached to *mySubnetBackEnd*.</span></span> <span data-ttu-id="d9cf7-149">A NIC virtual é anexada a VM chamada *myVM* no *myResourceGroup* com [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="d9cf7-149">The virtual NIC is then attached to the VM named *myVM* in *myResourceGroup* with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    # Get info for the back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get the ID of the new virtual NIC and add to VM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a><span data-ttu-id="d9cf7-150">NICs virtuais primárias</span><span class="sxs-lookup"><span data-stu-id="d9cf7-150">Primary virtual NICs</span></span>
    <span data-ttu-id="d9cf7-151">Uma das NICs em uma VM com várias NICs precisa ser primária.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-151">One of the NICs on a multi-NIC VM needs to be primary.</span></span> <span data-ttu-id="d9cf7-152">Se uma das NICs virtuais existentes na VM já estiver definida como primária, você pode ignorar esta etapa.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-152">If one of the existing virtual NICs on the VM is already set as primary, you can skip this step.</span></span> <span data-ttu-id="d9cf7-153">O exemplo a seguir presume que duas NICs virtuais agora estão presentes em uma VM e você deseja adicionar a primeira NIC (`[0]`) como a primária:</span><span class="sxs-lookup"><span data-stu-id="d9cf7-153">The following example assumes that two virtual NICs are now present on a VM and you wish to add the first NIC (`[0]`) as the primary:</span></span>
        
    ```powershell
    # List existing NICs on the VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 to be primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update the VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. <span data-ttu-id="d9cf7-154">Inicie a VM com [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="d9cf7-154">Start the VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a><span data-ttu-id="d9cf7-155">Remover uma NIC de uma VM existente</span><span class="sxs-lookup"><span data-stu-id="d9cf7-155">Remove a NIC from an existing VM</span></span>
<span data-ttu-id="d9cf7-156">Para remover uma NIC virtual de uma VM existente, você desaloca a VM, remove a NIC virtual e inicia a VM.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-156">To remove a virtual NIC from an existing VM, you deallocate the VM, remove the virtual NIC, then start the VM.</span></span>

1. <span data-ttu-id="d9cf7-157">Desaloque a VM com o [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="d9cf7-157">Deallocate the VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="d9cf7-158">O seguinte exemplo desaloca a VM chamada *myVM* no *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="d9cf7-158">The following example deallocates the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="d9cf7-159">Obtenha a configuração existente da VM com [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="d9cf7-159">Get the existing configuration of the VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="d9cf7-160">O exemplo a seguir obtém informações sobre a VM chamada *myVM* no *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="d9cf7-160">The following example gets information for the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="d9cf7-161">Obter informações sobre a remoção de NIC com [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="d9cf7-161">Get information about the NIC remove with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span></span> <span data-ttu-id="d9cf7-162">O seguinte exemplo obtém informações sobre *myNic3*:</span><span class="sxs-lookup"><span data-stu-id="d9cf7-162">The following example gets information about *myNic3*:</span></span>

    ```powershell
    # List existing NICs on the VM if you need to determine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. <span data-ttu-id="d9cf7-163">Remova a NIC com [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) e, em seguida, atualize a VM com [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="d9cf7-163">Remove the NIC with [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) and then update the VM with [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span></span> <span data-ttu-id="d9cf7-164">O exemplo a seguir remove *myNic3* conforme obtidas pelo `$nicId` na etapa anterior:</span><span class="sxs-lookup"><span data-stu-id="d9cf7-164">The following example removes *myNic3* as obtained by `$nicId` in the preceding step:</span></span>

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. <span data-ttu-id="d9cf7-165">Inicie a VM com [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="d9cf7-165">Start the VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a><span data-ttu-id="d9cf7-166">Criar várias NICs com modelos</span><span class="sxs-lookup"><span data-stu-id="d9cf7-166">Create multiple NICs with templates</span></span>
<span data-ttu-id="d9cf7-167">Os modelos do Azure Resource Manager oferecem uma maneira de criar várias instâncias de um recurso durante a implantação, como a criação de várias NICs.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-167">Azure Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="d9cf7-168">Os modelos do Resource Manager usam arquivos JSON declarativos para definir o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-168">Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="d9cf7-169">Para saber mais, consulte [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d9cf7-169">For more information, see [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="d9cf7-170">Você usa *copiar* para especificar o número de instâncias a serem criadas:</span><span class="sxs-lookup"><span data-stu-id="d9cf7-170">You can use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="d9cf7-171">Para obter mais informações, consulte [criando várias instâncias usando *cópia*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="d9cf7-171">For more information, see [creating multiple instances by using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="d9cf7-172">Você também pode usar `copyIndex()` para acrescentar um número a um nome de recurso.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-172">You can also use `copyIndex()` to append a number to a resource name.</span></span> <span data-ttu-id="d9cf7-173">Você pode criar *myNic1*, *MyNic2* e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-173">You can then create *myNic1*, *MyNic2* and so on.</span></span> <span data-ttu-id="d9cf7-174">O código a seguir mostra um exemplo de como acrescentar o valor de índice:</span><span class="sxs-lookup"><span data-stu-id="d9cf7-174">The following code shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="d9cf7-175">Você pode ler um exemplo completo em [criando várias NICs usando modelos do Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="d9cf7-175">You can read a complete example of [creating multiple NICs by using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9cf7-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d9cf7-176">Next steps</span></span>
<span data-ttu-id="d9cf7-177">Analise os [tamanhos de VM do Windows](sizes.md) quando estiver tentando criar uma VM que tem várias NICs.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-177">Review [Windows VM sizes](sizes.md) when you're trying to create a VM that has multiple NICs.</span></span> <span data-ttu-id="d9cf7-178">Preste atenção ao número máximo de NICs a que cada VM dá suporte.</span><span class="sxs-lookup"><span data-stu-id="d9cf7-178">Pay attention to the maximum number of NICs that each VM size supports.</span></span> 


