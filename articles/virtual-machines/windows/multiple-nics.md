---
title: "aaaCreate e gerenciar máquinas virtuais do Windows no Azure que usam várias NICs | Microsoft Docs"
description: "Saiba como toocreate e gerenciar uma VM do Windows que tenha várias NICs e anexado tooit usando modelos do Azure PowerShell ou Gerenciador de recursos."
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
ms.openlocfilehash: c3c7d7569aca6f047238146d84b2ffccf05d4079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a><span data-ttu-id="c1aaf-103">Cria e gerencia uma máquina virtual do Windows que tem várias NICs</span><span class="sxs-lookup"><span data-stu-id="c1aaf-103">Create and manage a Windows virtual machine that has multiple NICs</span></span>
<span data-ttu-id="c1aaf-104">Máquinas virtuais (VMs) no Azure pode ter vários toothem de NICs (placas) anexadas de interface de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-104">Virtual machines (VMs) in Azure can have multiple virtual network interface cards (NICs) attached toothem.</span></span> <span data-ttu-id="c1aaf-105">Um cenário comum é toohave várias sub-redes para conectividade de front-end e back-end ou uma rede dedicada tooa monitoramento ou solução de backup.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="c1aaf-106">Este artigo fornece detalhes sobre como toocreate uma máquina virtual que tem várias NICs anexado tooit.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-106">This article details how toocreate a VM that has multiple NICs attached tooit.</span></span> <span data-ttu-id="c1aaf-107">Você também aprenderá como NICs tooadd ou remover de uma VM existente.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-107">You also learn how tooadd or remove NICs from an existing VM.</span></span> <span data-ttu-id="c1aaf-108">Diferentes [tamanhos de VM](sizes.md) dão suporte a um número variável de NICs, sendo assim, dimensione sua VM adequadamente.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="c1aaf-109">Para obter informações detalhadas, incluindo como toocreate várias NICs dentro de seus próprios scripts do PowerShell, consulte [implantar VMs várias NICs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c1aaf-109">For detailed information, including how toocreate multiple NICs within your own PowerShell scripts, see [deploying multiple-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1aaf-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c1aaf-110">Prerequisites</span></span>
<span data-ttu-id="c1aaf-111">Certifique-se de que você tenha Olá [versão mais recente do PowerShell do Azure instalado e configurado](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c1aaf-111">Make sure that you have hello [latest Azure PowerShell version installed and configured](/powershell/azure/overview).</span></span>

<span data-ttu-id="c1aaf-112">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-112">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="c1aaf-113">Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *myVnet* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-113">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>


## <a name="create-a-vm-with-multiple-nics"></a><span data-ttu-id="c1aaf-114">Criar uma VM com diversos NICs</span><span class="sxs-lookup"><span data-stu-id="c1aaf-114">Create a VM with multiple NICs</span></span>
<span data-ttu-id="c1aaf-115">Em primeiro lugar, crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-115">First, create a resource group.</span></span> <span data-ttu-id="c1aaf-116">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *EastUs* local:</span><span class="sxs-lookup"><span data-stu-id="c1aaf-116">hello following example creates a resource group named *myResourceGroup* in hello *EastUs* location:</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a><span data-ttu-id="c1aaf-117">Crie a rede virtual e as sub-redes</span><span class="sxs-lookup"><span data-stu-id="c1aaf-117">Create virtual network and subnets</span></span>
<span data-ttu-id="c1aaf-118">Um cenário comum é para uma rede virtual toohave duas ou mais sub-redes.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-118">A common scenario is for a virtual network toohave two or more subnets.</span></span> <span data-ttu-id="c1aaf-119">Pode ser uma sub-rede para o tráfego de front-end, Olá para o tráfego de back-end.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-119">One subnet may be for front-end traffic, hello other for back-end traffic.</span></span> <span data-ttu-id="c1aaf-120">tooconnect tooboth sub-redes, você usar várias NICs em sua VM.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-120">tooconnect tooboth subnets, you then use multiple NICs on your VM.</span></span>

1. <span data-ttu-id="c1aaf-121">Defina duas sub-redes de rede virtual com [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="c1aaf-121">Define two virtual network subnets with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="c1aaf-122">Olá, exemplo a seguir define sub-redes Olá para *mySubnetFrontEnd* e *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="c1aaf-122">hello following example defines hello subnets for *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. <span data-ttu-id="c1aaf-123">Crie uma rede virtual e sub-redes com [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="c1aaf-123">Create your virtual network and subnets with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="c1aaf-124">Olá, exemplo a seguir cria uma rede virtual denominada *myVnet*:</span><span class="sxs-lookup"><span data-stu-id="c1aaf-124">hello following example creates a virtual network named *myVnet*:</span></span>

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a><span data-ttu-id="c1aaf-125">Crie múltiplas NICs</span><span class="sxs-lookup"><span data-stu-id="c1aaf-125">Create multiple NICs</span></span>
<span data-ttu-id="c1aaf-126">Crie duas NICs com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="c1aaf-126">Create two NICs with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="c1aaf-127">Anexe uma sub-rede front-end toohello NIC e uma sub-rede de back-end de toohello NIC.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-127">Attach one NIC toohello front-end subnet and one NIC toohello back-end subnet.</span></span> <span data-ttu-id="c1aaf-128">Olá, exemplo a seguir cria NICs denominadas *myNic1* e *myNic2*:</span><span class="sxs-lookup"><span data-stu-id="c1aaf-128">hello following example creates NICs named *myNic1* and *myNic2*:</span></span>

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

<span data-ttu-id="c1aaf-129">Normalmente você cria também uma [grupo de segurança de rede](../../virtual-network/virtual-networks-nsg.md) ou [balanceador de carga](../../load-balancer/load-balancer-overview.md) toohelp gerenciar e distribuir o tráfego entre suas VMs.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-129">Typically you also create a [network security group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) toohelp manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="c1aaf-130">Olá [mais detalhadas a VM de várias NICs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) artigo orienta você na criação de um grupo de segurança de rede e atribuindo NICs.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-130">hello [more detailed multiple-NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) article guides you through creating a network security group and assigning NICs.</span></span>

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="c1aaf-131">Criar a máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="c1aaf-131">Create hello virtual machine</span></span>
<span data-ttu-id="c1aaf-132">Inicie agora toobuild a configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-132">Now start toobuild your VM configuration.</span></span> <span data-ttu-id="c1aaf-133">O tamanho de cada VM tem um limite para o número total de saudação de NICs que você pode adicionar tooa VM.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-133">Each VM size has a limit for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="c1aaf-134">Para obter mais informações, consulte [Tamanhos da VM no Windows](sizes.md) .</span><span class="sxs-lookup"><span data-stu-id="c1aaf-134">For more information, see [Windows VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="c1aaf-135">Definir sua toohello de credenciais VM `$cred` variável da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="c1aaf-135">Set your VM credentials toohello `$cred` variable as follows:</span></span>

    ```powershell
    $cred = Get-Credential
    ```

2. <span data-ttu-id="c1aaf-136">Defina sua VM com [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span><span class="sxs-lookup"><span data-stu-id="c1aaf-136">Define your VM with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span></span> <span data-ttu-id="c1aaf-137">Olá, exemplo a seguir define uma VM denominada *myVM* e usa um tamanho VM que oferece suporte a mais de dois NICs (*Standard_DS3_v2*):</span><span class="sxs-lookup"><span data-stu-id="c1aaf-137">hello following example defines a VM named *myVM* and uses a VM size that supports more than two NICs (*Standard_DS3_v2*):</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. <span data-ttu-id="c1aaf-138">Criar rest Olá da sua configuração de VM com [conjunto AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) e [AzureRmVMSourceImage conjunto](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span><span class="sxs-lookup"><span data-stu-id="c1aaf-138">Create hello rest of your VM configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) and [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span></span> <span data-ttu-id="c1aaf-139">saudação de exemplo a seguir cria uma VM do Windows Server 2016:</span><span class="sxs-lookup"><span data-stu-id="c1aaf-139">hello following example creates a Windows Server 2016 VM:</span></span>

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

4. <span data-ttu-id="c1aaf-140">Anexar Olá duas NICs que você criou anteriormente com [adicionar AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="c1aaf-140">Attach hello two NICs that you previously created with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. <span data-ttu-id="c1aaf-141">Finalmente, crie sua VM com [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="c1aaf-141">Finally, create your VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-tooan-existing-vm"></a><span data-ttu-id="c1aaf-142">Adicionar um tooan NIC existentes de VM</span><span class="sxs-lookup"><span data-stu-id="c1aaf-142">Add a NIC tooan existing VM</span></span>
<span data-ttu-id="c1aaf-143">tooadd um tooan NIC virtual existente da VM, você desalocar Olá VM, adicionar Olá NIC virtual, em seguida, inicie o hello VM.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-143">tooadd a virtual NIC tooan existing VM, you deallocate hello VM, add hello virtual NIC, then start hello VM.</span></span>

1. <span data-ttu-id="c1aaf-144">Desalocar Olá VM com [AzureRmVM Stop](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="c1aaf-144">Deallocate hello VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="c1aaf-145">exemplo a seguir Hello desaloca Olá VM denominada *myVM* na *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="c1aaf-145">hello following example deallocates hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="c1aaf-146">Obter a configuração existente de saudação do hello VM com [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="c1aaf-146">Get hello existing configuration of hello VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="c1aaf-147">Olá, exemplo a seguir obtém informações de saudação VM denominada *myVM* na *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="c1aaf-147">hello following example gets information for hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="c1aaf-148">Olá, exemplo a seguir cria uma NIC virtual com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) chamado *myNic3* anexado muito*mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-148">hello following example creates a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) named *myNic3* that is attached too*mySubnetBackEnd*.</span></span> <span data-ttu-id="c1aaf-149">Olá NIC virtual é anexado toohello VM denominada *myVM* na *myResourceGroup* com [adicionar AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="c1aaf-149">hello virtual NIC is then attached toohello VM named *myVM* in *myResourceGroup* with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    # Get info for hello back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get hello ID of hello new virtual NIC and add tooVM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a><span data-ttu-id="c1aaf-150">NICs virtuais primárias</span><span class="sxs-lookup"><span data-stu-id="c1aaf-150">Primary virtual NICs</span></span>
    <span data-ttu-id="c1aaf-151">Uma saudação NICs em uma VM multi-NIC precisa toobe primário.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-151">One of hello NICs on a multi-NIC VM needs toobe primary.</span></span> <span data-ttu-id="c1aaf-152">Se um dos Olá NICs virtuais existentes em Olá VM já está definida como principal, você pode ignorar esta etapa.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-152">If one of hello existing virtual NICs on hello VM is already set as primary, you can skip this step.</span></span> <span data-ttu-id="c1aaf-153">Olá exemplo a seguir supõe que duas NICs virtuais agora estão presentes em uma máquina virtual e deseja tooadd Olá primeiro NIC (`[0]`) como Olá primário:</span><span class="sxs-lookup"><span data-stu-id="c1aaf-153">hello following example assumes that two virtual NICs are now present on a VM and you wish tooadd hello first NIC (`[0]`) as hello primary:</span></span>
        
    ```powershell
    # List existing NICs on hello VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 toobe primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update hello VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. <span data-ttu-id="c1aaf-154">Iniciar Olá VM com [AzureRmVm início](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="c1aaf-154">Start hello VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a><span data-ttu-id="c1aaf-155">Remover uma NIC de uma VM existente</span><span class="sxs-lookup"><span data-stu-id="c1aaf-155">Remove a NIC from an existing VM</span></span>
<span data-ttu-id="c1aaf-156">tooremove uma NIC virtual de uma VM existente, você desalocar Olá VM, remova Olá NIC virtual, em seguida, iniciar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-156">tooremove a virtual NIC from an existing VM, you deallocate hello VM, remove hello virtual NIC, then start hello VM.</span></span>

1. <span data-ttu-id="c1aaf-157">Desalocar Olá VM com [AzureRmVM Stop](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="c1aaf-157">Deallocate hello VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="c1aaf-158">exemplo a seguir Hello desaloca Olá VM denominada *myVM* na *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="c1aaf-158">hello following example deallocates hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="c1aaf-159">Obter a configuração existente de saudação do hello VM com [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="c1aaf-159">Get hello existing configuration of hello VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="c1aaf-160">Olá, exemplo a seguir obtém informações de saudação VM denominada *myVM* na *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="c1aaf-160">hello following example gets information for hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="c1aaf-161">Obter informações sobre Olá remover NIC com [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="c1aaf-161">Get information about hello NIC remove with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span></span> <span data-ttu-id="c1aaf-162">Olá exemplo a seguir obtém informações sobre *myNic3*:</span><span class="sxs-lookup"><span data-stu-id="c1aaf-162">hello following example gets information about *myNic3*:</span></span>

    ```powershell
    # List existing NICs on hello VM if you need toodetermine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. <span data-ttu-id="c1aaf-163">Remover Olá NIC com [remover AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) e atualize Olá VM com [AzureRmVm atualização](/powershell/module/azurerm.compute/update-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="c1aaf-163">Remove hello NIC with [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) and then update hello VM with [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span></span> <span data-ttu-id="c1aaf-164">Olá exemplo a seguir remove *myNic3* conforme obtidas pelo `$nicId` em Olá anterior etapa:</span><span class="sxs-lookup"><span data-stu-id="c1aaf-164">hello following example removes *myNic3* as obtained by `$nicId` in hello preceding step:</span></span>

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. <span data-ttu-id="c1aaf-165">Iniciar Olá VM com [AzureRmVm início](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="c1aaf-165">Start hello VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a><span data-ttu-id="c1aaf-166">Criar várias NICs com modelos</span><span class="sxs-lookup"><span data-stu-id="c1aaf-166">Create multiple NICs with templates</span></span>
<span data-ttu-id="c1aaf-167">Modelos do Gerenciador de recursos do Azure fornecem uma maneira toocreate várias instâncias de um recurso durante a implantação, como a criação de várias NICs.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-167">Azure Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="c1aaf-168">Modelos do Gerenciador de recursos usam toodefine declarativa de arquivos JSON seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-168">Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="c1aaf-169">Para saber mais, consulte [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c1aaf-169">For more information, see [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="c1aaf-170">Você pode usar *cópia* toospecify número de saudação do toocreate de instâncias:</span><span class="sxs-lookup"><span data-stu-id="c1aaf-170">You can use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="c1aaf-171">Para obter mais informações, consulte [criando várias instâncias usando *cópia*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="c1aaf-171">For more information, see [creating multiple instances by using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="c1aaf-172">Você também pode usar `copyIndex()` tooappend um nome de recurso tooa número.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-172">You can also use `copyIndex()` tooappend a number tooa resource name.</span></span> <span data-ttu-id="c1aaf-173">Você pode criar *myNic1*, *MyNic2* e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-173">You can then create *myNic1*, *MyNic2* and so on.</span></span> <span data-ttu-id="c1aaf-174">Olá código a seguir mostra um exemplo de acrescentar o valor de índice hello:</span><span class="sxs-lookup"><span data-stu-id="c1aaf-174">hello following code shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="c1aaf-175">Você pode ler um exemplo completo em [criando várias NICs usando modelos do Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="c1aaf-175">You can read a complete example of [creating multiple NICs by using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1aaf-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c1aaf-176">Next steps</span></span>
<span data-ttu-id="c1aaf-177">Revisão [tamanhos de VM do Windows](sizes.md) quando você estiver tentando toocreate uma máquina virtual que tem várias NICs.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-177">Review [Windows VM sizes](sizes.md) when you're trying toocreate a VM that has multiple NICs.</span></span> <span data-ttu-id="c1aaf-178">Preste atenção toohello número de NICs que dá suporte a cada tamanho VM.</span><span class="sxs-lookup"><span data-stu-id="c1aaf-178">Pay attention toohello maximum number of NICs that each VM size supports.</span></span> 


