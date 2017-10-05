---
title: "Criar e gerenciar VMs do Windows com o módulo do Azure PowerShell | Microsoft Docs"
description: "Tutorial - Criar e gerenciar VMs do Windows com o módulo do Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ec1bb7834beb66dc28dd5b1db764bd358243292c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-windows-vms-with-the-azure-powershell-module"></a><span data-ttu-id="43301-103">Criar e gerenciar VMs do Windows com o módulo do Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="43301-103">Create and Manage Windows VMs with the Azure PowerShell module</span></span>

<span data-ttu-id="43301-104">Máquinas virtuais do Azure fornecem um ambiente de computação totalmente configurável e flexível.</span><span class="sxs-lookup"><span data-stu-id="43301-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="43301-105">Este tutorial aborda itens básicos de implantação de máquina virtual do Azure, como a seleção de um tamanho de VM, seleção de uma imagem de VM e implantação de uma VM.</span><span class="sxs-lookup"><span data-stu-id="43301-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="43301-106">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="43301-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="43301-107">Criar e conectar-se a uma VM</span><span class="sxs-lookup"><span data-stu-id="43301-107">Create and connect to a VM</span></span>
> * <span data-ttu-id="43301-108">Selecionar e usar imagens de VM</span><span class="sxs-lookup"><span data-stu-id="43301-108">Select and use VM images</span></span>
> * <span data-ttu-id="43301-109">Exibir e usar tamanhos específicos de VM</span><span class="sxs-lookup"><span data-stu-id="43301-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="43301-110">Redimensionar uma VM</span><span class="sxs-lookup"><span data-stu-id="43301-110">Resize a VM</span></span>
> * <span data-ttu-id="43301-111">Exibir e compreender o estado da VM</span><span class="sxs-lookup"><span data-stu-id="43301-111">View and understand VM state</span></span>

<span data-ttu-id="43301-112">Este tutorial requer o módulo do Azure PowerShell, versão 3.6 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="43301-112">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="43301-113">Execute ` Get-Module -ListAvailable AzureRM` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="43301-113">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="43301-114">Se você precisa atualizar, consulte [Instalar o módulo do Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="43301-114">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="43301-115">Criar grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="43301-115">Create resource group</span></span>

<span data-ttu-id="43301-116">Crie um grupo de recursos com o comando [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="43301-116">Create a resource group with the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> 

<span data-ttu-id="43301-117">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="43301-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="43301-118">Você deve criar um grupo de recursos antes de criar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="43301-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="43301-119">Neste exemplo, criaremos um grupo de recursos chamado *myResourceGroupVM* na região *EastUS*.</span><span class="sxs-lookup"><span data-stu-id="43301-119">In this example, a resource group named *myResourceGroupVM* is created in the *EastUS* region.</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

<span data-ttu-id="43301-120">O grupo de recursos é especificado ao criar ou modificar uma VM, que pode ser visto durante este tutorial.</span><span class="sxs-lookup"><span data-stu-id="43301-120">The resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="43301-121">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="43301-121">Create virtual machine</span></span>

<span data-ttu-id="43301-122">Uma máquina virtual precisa estar conectada a uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="43301-122">A virtual machine must be connected to a virtual network.</span></span> <span data-ttu-id="43301-123">Você se comunica com a máquina virtual usando um endereço IP público por meio de uma placa da interface de rede.</span><span class="sxs-lookup"><span data-stu-id="43301-123">You communicate with the virtual machine using a public IP address through a network interface card.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="43301-124">Criar rede virtual</span><span class="sxs-lookup"><span data-stu-id="43301-124">Create virtual network</span></span>

<span data-ttu-id="43301-125">Crie uma sub-rede com [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="43301-125">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="43301-126">Crie uma rede virtual com [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="43301-126">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a><span data-ttu-id="43301-127">Criar um endereço IP público</span><span class="sxs-lookup"><span data-stu-id="43301-127">Create public IP address</span></span>

<span data-ttu-id="43301-128">Crie um endereço IP público com [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="43301-128">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a><span data-ttu-id="43301-129">Criar a placa da interface de rede</span><span class="sxs-lookup"><span data-stu-id="43301-129">Create network interface card</span></span>

<span data-ttu-id="43301-130">Crie a placa de interface de rede com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="43301-130">Create a network interface card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a><span data-ttu-id="43301-131">Criar um grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="43301-131">Create network security group</span></span>

<span data-ttu-id="43301-132">Um [grupo de segurança de rede](../../virtual-network/virtual-networks-nsg.md) (NSG) do Azure controla o tráfego de entrada e saída em uma ou mais máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="43301-132">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="43301-133">As regras de grupo de segurança de rede permitem ou negam o tráfego de rede em uma porta específica ou em um intervalo de porta.</span><span class="sxs-lookup"><span data-stu-id="43301-133">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="43301-134">Essas regras também podem incluir um prefixo do endereço de origem para que somente o tráfego originado em uma fonte predefinida possa se comunicar com uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="43301-134">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span> <span data-ttu-id="43301-135">Para acessar o servidor da Web do IIS que você está instalando, adicione uma regra NSG de entrada.</span><span class="sxs-lookup"><span data-stu-id="43301-135">To access the IIS webserver that you are installing, you must add an inbound NSG rule.</span></span>

<span data-ttu-id="43301-136">Para criar uma regra NSG de entrada, use [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="43301-136">To create an inbound NSG rule, use [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="43301-137">O exemplo a seguir cria uma regra NSG chamada *myNSGRule* que abre a porta *3389* para a máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="43301-137">The following example creates an NSG rule named *myNSGRule* that opens port *3389* for the virtual machine:</span></span>

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 3389 `
  -Access Allow
```

<span data-ttu-id="43301-138">Crie a NSG usando *myNSGRule* com [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="43301-138">Create the NSG using *myNSGRule* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

<span data-ttu-id="43301-139">Adicione a NSG à sub-rede na rede virtual com [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="43301-139">Add the NSG to the subnet in the virtual network with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="43301-140">Atualize a rede virtual com [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="43301-140">Update the virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a><span data-ttu-id="43301-141">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="43301-141">Create virtual machine</span></span>

<span data-ttu-id="43301-142">Há várias opções disponíveis ao criar uma máquina virtual, como a imagem do sistema operacional, as credenciais administrativas e o dimensionamento do disco.</span><span class="sxs-lookup"><span data-stu-id="43301-142">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="43301-143">Neste exemplo, uma máquina virtual é criada com um nome de *myVM* executando a versão mais recente do Windows Server 2016 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="43301-143">In this example, a virtual machine is created with a name of *myVM* running the latest version of Windows Server 2016 Datacenter.</span></span>

<span data-ttu-id="43301-144">Defina o nome de usuário e a senha necessários para a conta de administrador na máquina virtual com [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="43301-144">Set the username and password needed for the administrator account on the virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="43301-145">Crie a configuração inicial para a máquina virtual com [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span><span class="sxs-lookup"><span data-stu-id="43301-145">Create the initial configuration for the virtual machine with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

<span data-ttu-id="43301-146">Adicione as informações do sistema operacional à configuração da máquina virtual com [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span><span class="sxs-lookup"><span data-stu-id="43301-146">Add the operating system information to the virtual machine configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span></span>

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="43301-147">Adicione as informações da imagem á configuração da máquina virtual com [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span><span class="sxs-lookup"><span data-stu-id="43301-147">Add the image information to the virtual machine configuration with [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

<span data-ttu-id="43301-148">Adicione as configurações de disco do sistema operacional à configuração da máquina virtual com [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span><span class="sxs-lookup"><span data-stu-id="43301-148">Add the operating system disk settings to the virtual machine configuration with [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

<span data-ttu-id="43301-149">Adicione a placa de interface de rede que você criou anteriormente à configuração da máquina virtual com [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="43301-149">Add the network interface card that you previously created to the virtual machine configuration with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="43301-150">Crie a máquina virtual com [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="43301-150">Create the virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-to-vm"></a><span data-ttu-id="43301-151">Conectar-se a uma VM</span><span class="sxs-lookup"><span data-stu-id="43301-151">Connect to VM</span></span>

<span data-ttu-id="43301-152">Após a implantação, crie uma conexão de área de trabalho remota com a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="43301-152">After the deployment has completed, create a remote desktop connection with the virtual machine.</span></span>

<span data-ttu-id="43301-153">Execute os comandos a seguir para retornar o endereço IP público da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="43301-153">Run the following commands to return the public IP address of the virtual machine.</span></span> <span data-ttu-id="43301-154">Anote esse endereço IP para se conectar a ele com o navegador para testar a conectividade à Web em uma etapa futura.</span><span class="sxs-lookup"><span data-stu-id="43301-154">Take note of this IP Address so you can connect to it with your browser to test web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

<span data-ttu-id="43301-155">Use o seguinte comando para criar uma sessão de área de trabalho remota com a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="43301-155">Use the following command to create a remote desktop session with the virtual machine.</span></span> <span data-ttu-id="43301-156">Substitua o endereço IP pelo *publicIPAdress* da sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="43301-156">Replace the IP address with the *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="43301-157">Quando solicitado, insira as credenciais usadas ao criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="43301-157">When prompted, enter the credentials used when creating the virtual machine.</span></span>

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a><span data-ttu-id="43301-158">Entender as imagens de VM</span><span class="sxs-lookup"><span data-stu-id="43301-158">Understand VM images</span></span>

<span data-ttu-id="43301-159">O Azure Marketplace inclui várias imagens de máquina virtual que podem ser usadas para criar uma nova máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="43301-159">The Azure marketplace includes many virtual machine images that can be used to create a new virtual machine.</span></span> <span data-ttu-id="43301-160">Nas etapas anteriores, uma máquina virtual foi criada usando a imagem do Windows Server 2016-Datacenter.</span><span class="sxs-lookup"><span data-stu-id="43301-160">In the previous steps, a virtual machine was created using the Windows Server 2016-Datacenter image.</span></span> <span data-ttu-id="43301-161">Nesta etapa, o módulo do PowerShell é usado para pesquisar no marketplace por outras imagens do Windows, que também pode servir como base para novas VMs.</span><span class="sxs-lookup"><span data-stu-id="43301-161">In this step, the PowerShell module is used to search the marketplace for other Windows images, which can also as a base for new VMs.</span></span> <span data-ttu-id="43301-162">Esse processo consiste em localizar o nome do editor, da oferta e da imagem (Sku).</span><span class="sxs-lookup"><span data-stu-id="43301-162">This process consists of finding the publisher, offer, and the image name (Sku).</span></span> 

<span data-ttu-id="43301-163">Use o comando [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) para retornar uma lista de editores de imagem.</span><span class="sxs-lookup"><span data-stu-id="43301-163">Use the [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) command to return a list of image publishers.</span></span>  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

<span data-ttu-id="43301-164">Use o comando [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) para retornar uma lista de ofertas de imagem.</span><span class="sxs-lookup"><span data-stu-id="43301-164">Use the [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) to return a list of image offers.</span></span> <span data-ttu-id="43301-165">Com este comando, a lista retornada é filtrada no editor especificado.</span><span class="sxs-lookup"><span data-stu-id="43301-165">With this command, the returned list is filtered on the specified publisher.</span></span> 

```powershell
Get-AzureRmVMImageOffer -Location "EastUS" -PublisherName "MicrosoftWindowsServer"
```

```powershell
Offer             PublisherName          Location
-----             -------------          -------- 
Windows-HUB       MicrosoftWindowsServer EastUS 
WindowsServer     MicrosoftWindowsServer EastUS   
WindowsServer-HUB MicrosoftWindowsServer EastUS   
```

<span data-ttu-id="43301-166">O comando [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) filtrará o nome do editor e da oferta para retornar uma lista com nomes de imagem.</span><span class="sxs-lookup"><span data-stu-id="43301-166">The [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) command will then filter on the publisher and offer name to return a list of image names.</span></span>

```powershell
Get-AzureRmVMImageSku -Location "EastUS" -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer"
```

```powershell
Skus                            Offer         PublisherName          Location
----                            -----         -------------          --------
2008-R2-SP1                     WindowsServer MicrosoftWindowsServer EastUS  
2008-R2-SP1-BYOL                WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter-BYOL            WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter              WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter-BYOL         WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-Server-Core     WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-with-Containers WindowsServer MicrosoftWindowsServer EastUS  
2016-Nano-Server                WindowsServer MicrosoftWindowsServer EastUS
```

<span data-ttu-id="43301-167">Essas informações podem ser usadas para implantar uma VM com uma imagem específica.</span><span class="sxs-lookup"><span data-stu-id="43301-167">This information can be used to deploy a VM with a specific image.</span></span> <span data-ttu-id="43301-168">Este exemplo define o nome da imagem no objeto da VM.</span><span class="sxs-lookup"><span data-stu-id="43301-168">This example sets the image name on the VM object.</span></span> <span data-ttu-id="43301-169">Consulte os exemplos anteriores neste tutorial para obter as etapas completas de implantação.</span><span class="sxs-lookup"><span data-stu-id="43301-169">Refer to the previous examples in this tutorial for complete deployment steps.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="43301-170">Entender os tamanhos de VM</span><span class="sxs-lookup"><span data-stu-id="43301-170">Understand VM sizes</span></span>

<span data-ttu-id="43301-171">Um tamanho de máquina virtual determina a quantidade de recursos de computação, como memória, CPU e GPU que estão disponíveis para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="43301-171">A virtual machine size determines the amount of compute resources such as CPU, GPU, and memory that are made available to the virtual machine.</span></span> <span data-ttu-id="43301-172">As máquinas virtuais precisam ser criadas com um tamanho apropriado para a carga de trabalho esperada.</span><span class="sxs-lookup"><span data-stu-id="43301-172">Virtual machines need to be created with a size appropriate for the expect work load.</span></span> <span data-ttu-id="43301-173">Se a carga de trabalho aumentar, uma máquina virtual existente pode ser redimensionada.</span><span class="sxs-lookup"><span data-stu-id="43301-173">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="43301-174">Tamanhos de VM</span><span class="sxs-lookup"><span data-stu-id="43301-174">VM Sizes</span></span>

<span data-ttu-id="43301-175">A tabela a seguir categoriza tamanhos em casos de uso.</span><span class="sxs-lookup"><span data-stu-id="43301-175">The following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="43301-176">Tipo</span><span class="sxs-lookup"><span data-stu-id="43301-176">Type</span></span>                     | <span data-ttu-id="43301-177">Tamanhos</span><span class="sxs-lookup"><span data-stu-id="43301-177">Sizes</span></span>           |    <span data-ttu-id="43301-178">Descrição</span><span class="sxs-lookup"><span data-stu-id="43301-178">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="43301-179">Propósito geral</span><span class="sxs-lookup"><span data-stu-id="43301-179">General purpose</span></span>         |<span data-ttu-id="43301-180">DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="43301-180">DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="43301-181">CPU/memória equilibrados.</span><span class="sxs-lookup"><span data-stu-id="43301-181">Balanced CPU-to-memory.</span></span> <span data-ttu-id="43301-182">Ideal para desenvolvimento/teste e para aplicativos de pequeno a médio porte e soluções de dados.</span><span class="sxs-lookup"><span data-stu-id="43301-182">Ideal for dev / test and small to medium applications and data solutions.</span></span>  |
| <span data-ttu-id="43301-183">Otimizado para computação</span><span class="sxs-lookup"><span data-stu-id="43301-183">Compute optimized</span></span>      | <span data-ttu-id="43301-184">Fs, F</span><span class="sxs-lookup"><span data-stu-id="43301-184">Fs, F</span></span>             | <span data-ttu-id="43301-185">Relação de CPU/memória alta.</span><span class="sxs-lookup"><span data-stu-id="43301-185">High CPU-to-memory.</span></span> <span data-ttu-id="43301-186">Boa para aplicativos de tráfego médio, dispositivos de rede e processos em lote.</span><span class="sxs-lookup"><span data-stu-id="43301-186">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| <span data-ttu-id="43301-187">Otimizado para memória</span><span class="sxs-lookup"><span data-stu-id="43301-187">Memory optimized</span></span>       | <span data-ttu-id="43301-188">GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="43301-188">GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="43301-189">Relação de memória/núcleo alta.</span><span class="sxs-lookup"><span data-stu-id="43301-189">High memory-to-core.</span></span> <span data-ttu-id="43301-190">Ótima para banco de dados relacionais, caches médios a grandes e análises na memória.</span><span class="sxs-lookup"><span data-stu-id="43301-190">Great for relational databases, medium to large caches, and in-memory analytics.</span></span>                 |
| <span data-ttu-id="43301-191">Otimizado para armazenamento</span><span class="sxs-lookup"><span data-stu-id="43301-191">Storage optimized</span></span>       | <span data-ttu-id="43301-192">Ls</span><span class="sxs-lookup"><span data-stu-id="43301-192">Ls</span></span>                | <span data-ttu-id="43301-193">Alta taxa de transferência de disco e de E/S.</span><span class="sxs-lookup"><span data-stu-id="43301-193">High disk throughput and IO.</span></span> <span data-ttu-id="43301-194">Ideal para Big Data, SQL e bancos de dados NoSQL.</span><span class="sxs-lookup"><span data-stu-id="43301-194">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| <span data-ttu-id="43301-195">GPU</span><span class="sxs-lookup"><span data-stu-id="43301-195">GPU</span></span>           | <span data-ttu-id="43301-196">NV, NC</span><span class="sxs-lookup"><span data-stu-id="43301-196">NV, NC</span></span>            | <span data-ttu-id="43301-197">VMs especializadas, destinadas para renderização gráfica e edição de vídeo pesadas.</span><span class="sxs-lookup"><span data-stu-id="43301-197">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| <span data-ttu-id="43301-198">Alto desempenho</span><span class="sxs-lookup"><span data-stu-id="43301-198">High performance</span></span> | <span data-ttu-id="43301-199">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="43301-199">H, A8-11</span></span>          | <span data-ttu-id="43301-200">Nossas VMs de CPU mais potentes com adaptadores de rede de alto rendimento (RDMA) opcionais.</span><span class="sxs-lookup"><span data-stu-id="43301-200">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="43301-201">Encontrar tamanhos de VM disponíveis</span><span class="sxs-lookup"><span data-stu-id="43301-201">Find available VM sizes</span></span>

<span data-ttu-id="43301-202">Para ver uma lista de tamanhos de VM disponíveis em uma região específica, use o comando [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize).</span><span class="sxs-lookup"><span data-stu-id="43301-202">To see a list of VM sizes available in a particular region, use the [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command.</span></span>

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a><span data-ttu-id="43301-203">Redimensionar uma VM</span><span class="sxs-lookup"><span data-stu-id="43301-203">Resize a VM</span></span>

<span data-ttu-id="43301-204">Após a implantação de uma VM, ela pode ser redimensionada para aumentar ou diminuir a alocação de recursos.</span><span class="sxs-lookup"><span data-stu-id="43301-204">After a VM has been deployed, it can be resized to increase or decrease resource allocation.</span></span>

<span data-ttu-id="43301-205">Antes de redimensionar uma VM, verifique se o tamanho desejado está disponível no cluster da VM atual.</span><span class="sxs-lookup"><span data-stu-id="43301-205">Before resizing a VM, check if the desired size is available on the current VM cluster.</span></span> <span data-ttu-id="43301-206">O comando [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) retorna uma lista de tamanhos.</span><span class="sxs-lookup"><span data-stu-id="43301-206">The [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command returns a list of sizes.</span></span> 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

<span data-ttu-id="43301-207">Se o tamanho desejado estiver disponível, a VM poderá ser redimensionada a partir de um estado ligado. No entanto, ela é reinicializada durante a operação.</span><span class="sxs-lookup"><span data-stu-id="43301-207">If the desired size is available, the VM can be resized from a powered-on state, however it is rebooted during the operation.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

<span data-ttu-id="43301-208">Se o tamanho desejado não estiver no cluster atual, a VM precisará ser desalocada antes que a operação de redimensionamento ocorra.</span><span class="sxs-lookup"><span data-stu-id="43301-208">If the desired size is not on the current cluster, the VM needs to be deallocated before the resize operation can occur.</span></span> <span data-ttu-id="43301-209">Observe que quando a VM é ligada novamente, quaisquer dados no disco temporário são removidos, e o endereço IP público muda, a menos que um endereço IP estático esteja sendo usado.</span><span class="sxs-lookup"><span data-stu-id="43301-209">Note, when the VM is powered back on, any data on the temp disk are removed, and the public IP address change unless a static IP address is being used.</span></span> 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a><span data-ttu-id="43301-210">Estados de energia da VM</span><span class="sxs-lookup"><span data-stu-id="43301-210">VM power states</span></span>

<span data-ttu-id="43301-211">Uma VM do Azure pode ter um dentre vários estados de energia.</span><span class="sxs-lookup"><span data-stu-id="43301-211">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="43301-212">Esse estado representa o estado atual da VM do ponto de vista do hipervisor.</span><span class="sxs-lookup"><span data-stu-id="43301-212">This state represents the current state of the VM from the standpoint of the hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="43301-213">Estados de energia</span><span class="sxs-lookup"><span data-stu-id="43301-213">Power states</span></span>

| <span data-ttu-id="43301-214">Estado de energia</span><span class="sxs-lookup"><span data-stu-id="43301-214">Power State</span></span> | <span data-ttu-id="43301-215">Descrição</span><span class="sxs-lookup"><span data-stu-id="43301-215">Description</span></span>
|----|----|
| <span data-ttu-id="43301-216">Iniciando</span><span class="sxs-lookup"><span data-stu-id="43301-216">Starting</span></span> | <span data-ttu-id="43301-217">Indica que a máquina virtual está sendo iniciada.</span><span class="sxs-lookup"><span data-stu-id="43301-217">Indicates the virtual machine is being started.</span></span> |
| <span data-ttu-id="43301-218">Executando</span><span class="sxs-lookup"><span data-stu-id="43301-218">Running</span></span> | <span data-ttu-id="43301-219">Indica que a máquina virtual está em execução.</span><span class="sxs-lookup"><span data-stu-id="43301-219">Indicates that the virtual machine is running.</span></span> |
| <span data-ttu-id="43301-220">Parando</span><span class="sxs-lookup"><span data-stu-id="43301-220">Stopping</span></span> | <span data-ttu-id="43301-221">Indica que a máquina virtual está sendo interrompida.</span><span class="sxs-lookup"><span data-stu-id="43301-221">Indicates that the virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="43301-222">Parada</span><span class="sxs-lookup"><span data-stu-id="43301-222">Stopped</span></span> | <span data-ttu-id="43301-223">Indica que a máquina virtual foi parada.</span><span class="sxs-lookup"><span data-stu-id="43301-223">Indicates that the virtual machine is stopped.</span></span> <span data-ttu-id="43301-224">Observe que máquinas virtuais no estado parado ainda incorrem em encargos de computação.</span><span class="sxs-lookup"><span data-stu-id="43301-224">Note that virtual machines in the stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="43301-225">Desalocando</span><span class="sxs-lookup"><span data-stu-id="43301-225">Deallocating</span></span> | <span data-ttu-id="43301-226">Indica que a máquina virtual está sendo desalocada.</span><span class="sxs-lookup"><span data-stu-id="43301-226">Indicates that the virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="43301-227">Desalocada</span><span class="sxs-lookup"><span data-stu-id="43301-227">Deallocated</span></span> | <span data-ttu-id="43301-228">Indica que a máquina virtual foi completamente removidos do hipervisor, mas ainda está disponível no plano de controle.</span><span class="sxs-lookup"><span data-stu-id="43301-228">Indicates that the virtual machine is completely removed from the hypervisor but still available in the control plane.</span></span> <span data-ttu-id="43301-229">Máquinas virtuais no estado Desalocado não incorrem em encargos de computação.</span><span class="sxs-lookup"><span data-stu-id="43301-229">Virtual machines in the Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="43301-230">Indica que o estado de energia da máquina virtual é desconhecido.</span><span class="sxs-lookup"><span data-stu-id="43301-230">Indicates that the power state of the virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="43301-231">Localizar o estado de energia</span><span class="sxs-lookup"><span data-stu-id="43301-231">Find power state</span></span>

<span data-ttu-id="43301-232">Para recuperar o estado de uma VM específica, use o comando [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="43301-232">To retrieve the state of a particular VM, use the [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span> <span data-ttu-id="43301-233">Especifique um nome válido para uma máquina virtual e grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="43301-233">Be sure to specify a valid name for a virtual machine and resource group.</span></span> 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

<span data-ttu-id="43301-234">Saída:</span><span class="sxs-lookup"><span data-stu-id="43301-234">Output:</span></span>

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a><span data-ttu-id="43301-235">Tarefas de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="43301-235">Management tasks</span></span>

<span data-ttu-id="43301-236">Durante o ciclo de vida de uma máquina virtual, é possível que você queira executar tarefas de gerenciamento, como inicialização, interrupção ou exclusão de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="43301-236">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="43301-237">Além disso, é possível que você queira criar scripts para automatizar tarefas repetitivas ou complexas.</span><span class="sxs-lookup"><span data-stu-id="43301-237">Additionally, you may want to create scripts to automate repetitive or complex tasks.</span></span> <span data-ttu-id="43301-238">Usando o Azure PowerShell, muitas tarefas comuns de gerenciamento podem ser executadas em linha de comando ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="43301-238">Using Azure PowerShell, many common management tasks can be run from the command line or in scripts.</span></span>

### <a name="stop-virtual-machine"></a><span data-ttu-id="43301-239">Como interromper uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="43301-239">Stop virtual machine</span></span>

<span data-ttu-id="43301-240">Pare e desaloque uma máquina virtual com [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="43301-240">Stop and deallocate a virtual machine with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

<span data-ttu-id="43301-241">Se você quiser manter a máquina virtual em um estado de provisionamento, use o parâmetro -StayProvisioned.</span><span class="sxs-lookup"><span data-stu-id="43301-241">If you want to keep the virtual machine in a provisioned state, use the -StayProvisioned parameter.</span></span>

### <a name="start-virtual-machine"></a><span data-ttu-id="43301-242">Como iniciar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="43301-242">Start virtual machine</span></span>

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="43301-243">Excluir grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="43301-243">Delete resource group</span></span>

<span data-ttu-id="43301-244">Excluir um grupo de recursos exclui todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="43301-244">Deleting a resource group also deletes all resources contained within.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a><span data-ttu-id="43301-245">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="43301-245">Next steps</span></span>

<span data-ttu-id="43301-246">Neste tutorial, você aprendeu sobre a criação e o gerenciamento básico de VM e como:</span><span class="sxs-lookup"><span data-stu-id="43301-246">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="43301-247">Criar e conectar-se a uma VM</span><span class="sxs-lookup"><span data-stu-id="43301-247">Create and connect to a VM</span></span>
> * <span data-ttu-id="43301-248">Selecionar e usar imagens de VM</span><span class="sxs-lookup"><span data-stu-id="43301-248">Select and use VM images</span></span>
> * <span data-ttu-id="43301-249">Exibir e usar tamanhos específicos de VM</span><span class="sxs-lookup"><span data-stu-id="43301-249">View and use specific VM sizes</span></span>
> * <span data-ttu-id="43301-250">Redimensionar uma VM</span><span class="sxs-lookup"><span data-stu-id="43301-250">Resize a VM</span></span>
> * <span data-ttu-id="43301-251">Exibir e compreender o estado da VM</span><span class="sxs-lookup"><span data-stu-id="43301-251">View and understand VM state</span></span>

<span data-ttu-id="43301-252">Avança para o próximo tutorial para saber mais sobre os discos de VM.</span><span class="sxs-lookup"><span data-stu-id="43301-252">Advance to the next tutorial to learn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="43301-253">Criar e gerenciar discos de VM</span><span class="sxs-lookup"><span data-stu-id="43301-253">Create and Manage VM disks</span></span>](./tutorial-manage-data-disk.md)
