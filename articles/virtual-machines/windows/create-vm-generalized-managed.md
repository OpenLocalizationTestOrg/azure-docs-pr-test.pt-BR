---
title: aaaCreate VM de uma imagem VM gerenciada no Azure | Microsoft Docs
description: "Crie uma máquina virtual do Windows de uma imagem VM gerenciada generalizada usando o PowerShell do Azure, no modelo de implantação do Gerenciador de recursos de saudação."
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
ms.date: 05/22/2017
ms.author: cynthn
ms.openlocfilehash: 5036ef1533c144a9a328e94599b359e0166f337d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-managed-image"></a><span data-ttu-id="05ce5-103">Criar uma VM por meio de uma imagem gerenciada</span><span class="sxs-lookup"><span data-stu-id="05ce5-103">Create a VM from a managed image</span></span>

<span data-ttu-id="05ce5-104">Você pode criar várias VMs de uma imagem de VM gerenciada no Azure.</span><span class="sxs-lookup"><span data-stu-id="05ce5-104">You can create multiple VMs from a managed VM image in Azure.</span></span> <span data-ttu-id="05ce5-105">Uma imagem VM gerenciada contém toocreate necessário de informações de Olá uma VM, incluindo Olá SO e discos de dados.</span><span class="sxs-lookup"><span data-stu-id="05ce5-105">A managed VM image contains hello information necessary toocreate a VM, including hello OS and data disks.</span></span> <span data-ttu-id="05ce5-106">Olá VHDs que compõem a imagem de hello, incluindo discos Olá SO e discos de dados, são armazenados como discos gerenciados.</span><span class="sxs-lookup"><span data-stu-id="05ce5-106">hello VHDs that make up hello image, including both hello OS disks and any data disks, are stored as managed disks.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="05ce5-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="05ce5-107">Prerequisites</span></span>

<span data-ttu-id="05ce5-108">Você precisa toohave já [criado de uma imagem VM gerenciada](capture-image-resource.md) toouse para a criação de Olá nova VM.</span><span class="sxs-lookup"><span data-stu-id="05ce5-108">You need toohave already [created a managed VM image](capture-image-resource.md) toouse for creating hello new VM.</span></span> 

<span data-ttu-id="05ce5-109">Certifique-se de que você tenha versões mais recentes de saudação de módulos de AzureRM.Compute e AzureRM.Network PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="05ce5-109">Make sure that you have hello latest versions of hello AzureRM.Compute and AzureRM.Network PowerShell modules.</span></span> <span data-ttu-id="05ce5-110">Abra um prompt do PowerShell como administrador e execute Olá tooinstall de comando a segui-los.</span><span class="sxs-lookup"><span data-stu-id="05ce5-110">Open a PowerShell prompt as an Administrator and run hello following command tooinstall them.</span></span>

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
<span data-ttu-id="05ce5-111">Para saber mais, confira [Azure PowerShell Versioning](/powershell/azure/overview) (Controle de versão do Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="05ce5-111">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>



## <a name="collect-information-about-hello-image"></a><span data-ttu-id="05ce5-112">Coletar informações sobre a imagem de saudação</span><span class="sxs-lookup"><span data-stu-id="05ce5-112">Collect information about hello image</span></span>

<span data-ttu-id="05ce5-113">Primeiro precisamos toogather as informações básicas sobre a imagem de saudação e criar uma variável para a imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="05ce5-113">First we need toogather basic information about hello image and create a variable for hello image.</span></span> <span data-ttu-id="05ce5-114">Este exemplo usa uma imagem VM gerenciada denominada **myImage** que é em Olá **myResourceGroup** grupo de recursos em Olá **Central Oeste dos EUA** local.</span><span class="sxs-lookup"><span data-stu-id="05ce5-114">This example uses a managed VM image named **myImage** that is in hello **myResourceGroup** resource group in hello **West Central US** location.</span></span> 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="05ce5-115">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="05ce5-115">Create a virtual network</span></span>
<span data-ttu-id="05ce5-116">Criar rede virtual de saudação e a sub-rede de saudação [rede virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="05ce5-116">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="05ce5-117">Crie uma sub-rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="05ce5-117">Create hello subnet.</span></span> <span data-ttu-id="05ce5-118">Este exemplo cria uma sub-rede denominada **mySubnet** com prefixo de endereço de saudação **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="05ce5-118">This example creates a subnet named **mySubnet** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="05ce5-119">Crie rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="05ce5-119">Create hello virtual network.</span></span> <span data-ttu-id="05ce5-120">Este exemplo cria uma rede virtual denominada **myVnet** com prefixo de endereço de saudação **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="05ce5-120">This example creates a virtual network named **myVnet** with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="05ce5-121">Criar um endereço IP público e um adaptador de rede</span><span class="sxs-lookup"><span data-stu-id="05ce5-121">Create a public IP address and network interface</span></span>

<span data-ttu-id="05ce5-122">comunicação tooenable com máquina virtual de saudação na rede virtual Olá, é necessário um [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e uma interface de rede.</span><span class="sxs-lookup"><span data-stu-id="05ce5-122">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="05ce5-123">Criar um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="05ce5-123">Create a public IP address.</span></span> <span data-ttu-id="05ce5-124">Este exemplo cria um endereço IP público chamado **myPip**.</span><span class="sxs-lookup"><span data-stu-id="05ce5-124">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="05ce5-125">Criar NIC hello.</span><span class="sxs-lookup"><span data-stu-id="05ce5-125">Create hello NIC.</span></span> <span data-ttu-id="05ce5-126">Este exemplo cria uma NIC chamada **myNic**.</span><span class="sxs-lookup"><span data-stu-id="05ce5-126">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="05ce5-127">Criar um grupo de segurança de rede hello e uma regra RDP</span><span class="sxs-lookup"><span data-stu-id="05ce5-127">Create hello network security group and an RDP rule</span></span>

<span data-ttu-id="05ce5-128">toolog capaz de toobe em tooyour VM usando o RDP, você precisa toohave uma regra de segurança de rede (NSG) que permite o acesso RDP na porta 3389.</span><span class="sxs-lookup"><span data-stu-id="05ce5-128">toobe able toolog in tooyour VM using RDP, you need toohave a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="05ce5-129">Este exemplo cria um NSG chamado **myNsg** que contém uma regra chamada **myRdpRule** que permite tráfego RDP pela porta 3389.</span><span class="sxs-lookup"><span data-stu-id="05ce5-129">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="05ce5-130">Para obter mais informações sobre os NSGs, consulte [a abertura de portas tooa VM no Azure usando o PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="05ce5-130">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="05ce5-131">Criar uma variável para a rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="05ce5-131">Create a variable for hello virtual network</span></span>

<span data-ttu-id="05ce5-132">Crie uma variável para a rede virtual Olá concluída.</span><span class="sxs-lookup"><span data-stu-id="05ce5-132">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a><span data-ttu-id="05ce5-133">Obter credenciais Olá Olá VM</span><span class="sxs-lookup"><span data-stu-id="05ce5-133">Get hello credentials for hello VM</span></span>

<span data-ttu-id="05ce5-134">Olá seguinte cmdlet abrirá uma janela onde você inserirá um novo toouse de nome e senha de usuário como conta de administrador local Olá para acessar remotamente Olá VM.</span><span class="sxs-lookup"><span data-stu-id="05ce5-134">hello following cmdlet will open a window where you will enter a new user name and password toouse as hello local administrator account for remotely accessing hello VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-hello-vm-name-computer-name-and-hello-size-of-hello-vm"></a><span data-ttu-id="05ce5-135">Variáveis definidas para Olá VM nome, nome do computador e Olá tamanho da VM de saudação</span><span class="sxs-lookup"><span data-stu-id="05ce5-135">Set variables for hello VM name, computer name and hello size of hello VM</span></span>

1. <span data-ttu-id="05ce5-136">Crie variáveis de nome VM hello e nome do computador.</span><span class="sxs-lookup"><span data-stu-id="05ce5-136">Create variables for hello VM name and computer name.</span></span> <span data-ttu-id="05ce5-137">Este exemplo define o nome da VM hello como **myVM** e o nome do computador hello como **myComputer**.</span><span class="sxs-lookup"><span data-stu-id="05ce5-137">This example sets hello VM name as **myVM** and hello computer name as **myComputer**.</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. <span data-ttu-id="05ce5-138">Definir tamanho de saudação da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="05ce5-138">Set hello size of hello virtual machine.</span></span> <span data-ttu-id="05ce5-139">Este exemplo cria a VM de tamanho **Standard_DS1_v2**.</span><span class="sxs-lookup"><span data-stu-id="05ce5-139">This example creates **Standard_DS1_v2** sized VM.</span></span> <span data-ttu-id="05ce5-140">Consulte Olá [tamanhos de VM](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentação para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="05ce5-140">See hello [VM sizes](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation for more information.</span></span>

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. <span data-ttu-id="05ce5-141">Adicione hello nome da VM e a configuração da VM toohello tamanho.</span><span class="sxs-lookup"><span data-stu-id="05ce5-141">Add hello VM name and size toohello VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a><span data-ttu-id="05ce5-142">Imagem VM do conjunto hello como imagem de origem para Olá nova VM</span><span class="sxs-lookup"><span data-stu-id="05ce5-142">Set hello VM image as source image for hello new VM</span></span>

<span data-ttu-id="05ce5-143">Definir a imagem de origem de hello usando uma ID de Olá Olá gerenciado da imagem da VM.</span><span class="sxs-lookup"><span data-stu-id="05ce5-143">Set hello source image using hello ID of hello managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a><span data-ttu-id="05ce5-144">Definir configuração de SO hello e adicionar NIC hello.</span><span class="sxs-lookup"><span data-stu-id="05ce5-144">Set hello OS configuration and add hello NIC.</span></span>

<span data-ttu-id="05ce5-145">Insira o tipo de armazenamento da saudação (PremiumLRS ou StandardLRS) e o tamanho de saudação do disco do sistema operacional hello.</span><span class="sxs-lookup"><span data-stu-id="05ce5-145">Enter hello storage type (PremiumLRS or StandardLRS) and hello size of hello OS disk.</span></span> <span data-ttu-id="05ce5-146">Este exemplo define o tipo de conta Olá muito**PremiumLRS**, Olá muito o tamanho do disco**128 GB** e cache de disco muito**ReadWrite**.</span><span class="sxs-lookup"><span data-stu-id="05ce5-146">This example sets hello account type too**PremiumLRS**, hello disk size too**128 GB** and disk caching too**ReadWrite**.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a><span data-ttu-id="05ce5-147">Criar hello VM</span><span class="sxs-lookup"><span data-stu-id="05ce5-147">Create hello VM</span></span>

<span data-ttu-id="05ce5-148">Criar hello nova Vm usando a configuração de saudação que temos criado e armazenado no hello **$vm** variável.</span><span class="sxs-lookup"><span data-stu-id="05ce5-148">Create hello new Vm using hello configuration that we have built and stored in hello **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="05ce5-149">Verifique se esse Olá que VM foi criada</span><span class="sxs-lookup"><span data-stu-id="05ce5-149">Verify that hello VM was created</span></span>
<span data-ttu-id="05ce5-150">Ao concluir, você deverá ver Olá recém-criado VM em Olá [portal do Azure](https://portal.azure.com) em **procurar** > **máquinas virtuais**, ou usando o seguinte Olá Comandos do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="05ce5-150">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="05ce5-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="05ce5-151">Next steps</span></span>
<span data-ttu-id="05ce5-152">toomanage nova máquina virtual com o Azure PowerShell, consulte [criar e gerenciar máquinas virtuais do Windows com o módulo do PowerShell do Azure Olá](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="05ce5-152">toomanage your new virtual machine with Azure PowerShell, see [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

