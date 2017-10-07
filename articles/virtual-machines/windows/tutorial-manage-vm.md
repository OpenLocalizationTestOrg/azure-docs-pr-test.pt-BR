---
title: "aaaCreate e gerenciar máquinas virtuais do Windows com hello módulo PowerShell do Azure | Microsoft Docs"
description: "Tutorial - criar e gerenciar máquinas virtuais do Windows com hello módulo PowerShell do Azure"
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
ms.openlocfilehash: 20adcb673ef4de683e6ad82d048a9625a1dc838c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-with-hello-azure-powershell-module"></a><span data-ttu-id="244c5-103">Criar e gerenciar máquinas virtuais do Windows com hello módulo PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="244c5-103">Create and Manage Windows VMs with hello Azure PowerShell module</span></span>

<span data-ttu-id="244c5-104">Máquinas virtuais do Azure fornecem um ambiente de computação totalmente configurável e flexível.</span><span class="sxs-lookup"><span data-stu-id="244c5-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="244c5-105">Este tutorial aborda itens básicos de implantação de máquina virtual do Azure, como a seleção de um tamanho de VM, seleção de uma imagem de VM e implantação de uma VM.</span><span class="sxs-lookup"><span data-stu-id="244c5-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="244c5-106">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="244c5-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="244c5-107">Criar e conectar tooa VM</span><span class="sxs-lookup"><span data-stu-id="244c5-107">Create and connect tooa VM</span></span>
> * <span data-ttu-id="244c5-108">Selecionar e usar imagens de VM</span><span class="sxs-lookup"><span data-stu-id="244c5-108">Select and use VM images</span></span>
> * <span data-ttu-id="244c5-109">Exibir e usar tamanhos específicos de VM</span><span class="sxs-lookup"><span data-stu-id="244c5-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="244c5-110">Redimensionar uma VM</span><span class="sxs-lookup"><span data-stu-id="244c5-110">Resize a VM</span></span>
> * <span data-ttu-id="244c5-111">Exibir e compreender o estado da VM</span><span class="sxs-lookup"><span data-stu-id="244c5-111">View and understand VM state</span></span>

<span data-ttu-id="244c5-112">Este tutorial requer hello Azure PowerShell versão 3.6 ou posterior do módulo.</span><span class="sxs-lookup"><span data-stu-id="244c5-112">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="244c5-113">Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="244c5-113">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="244c5-114">Se você precisar tooupgrade, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="244c5-114">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="244c5-115">Criar grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="244c5-115">Create resource group</span></span>

<span data-ttu-id="244c5-116">Criar um grupo de recursos com hello [AzureRmResourceGroup novo](/powershell/module/azurerm.resources/new-azurermresourcegroup) comando.</span><span class="sxs-lookup"><span data-stu-id="244c5-116">Create a resource group with hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> 

<span data-ttu-id="244c5-117">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="244c5-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="244c5-118">Você deve criar um grupo de recursos antes de criar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="244c5-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="244c5-119">Neste exemplo, um grupo de recursos denominado *myResourceGroupVM* é criado no hello *EastUS* região.</span><span class="sxs-lookup"><span data-stu-id="244c5-119">In this example, a resource group named *myResourceGroupVM* is created in hello *EastUS* region.</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

<span data-ttu-id="244c5-120">grupo de recursos de saudação é especificado ao criar ou modificar uma VM, que pode ser vista em todo este tutorial.</span><span class="sxs-lookup"><span data-stu-id="244c5-120">hello resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="244c5-121">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="244c5-121">Create virtual machine</span></span>

<span data-ttu-id="244c5-122">Uma máquina virtual deve ser uma rede virtual tooa conectado.</span><span class="sxs-lookup"><span data-stu-id="244c5-122">A virtual machine must be connected tooa virtual network.</span></span> <span data-ttu-id="244c5-123">Você se comunicar com a máquina virtual de saudação usando um endereço IP público por meio de uma placa de interface de rede.</span><span class="sxs-lookup"><span data-stu-id="244c5-123">You communicate with hello virtual machine using a public IP address through a network interface card.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="244c5-124">Criar rede virtual</span><span class="sxs-lookup"><span data-stu-id="244c5-124">Create virtual network</span></span>

<span data-ttu-id="244c5-125">Crie uma sub-rede com [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="244c5-125">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="244c5-126">Crie uma rede virtual com [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="244c5-126">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a><span data-ttu-id="244c5-127">Criar um endereço IP público</span><span class="sxs-lookup"><span data-stu-id="244c5-127">Create public IP address</span></span>

<span data-ttu-id="244c5-128">Crie um endereço IP público com [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="244c5-128">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a><span data-ttu-id="244c5-129">Criar a placa da interface de rede</span><span class="sxs-lookup"><span data-stu-id="244c5-129">Create network interface card</span></span>

<span data-ttu-id="244c5-130">Crie a placa de interface de rede com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="244c5-130">Create a network interface card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a><span data-ttu-id="244c5-131">Criar um grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="244c5-131">Create network security group</span></span>

<span data-ttu-id="244c5-132">Um [grupo de segurança de rede](../../virtual-network/virtual-networks-nsg.md) (NSG) do Azure controla o tráfego de entrada e saída em uma ou mais máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="244c5-132">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="244c5-133">As regras de grupo de segurança de rede permitem ou negam o tráfego de rede em uma porta específica ou em um intervalo de porta.</span><span class="sxs-lookup"><span data-stu-id="244c5-133">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="244c5-134">Essas regras também podem incluir um prefixo do endereço de origem para que somente o tráfego originado em uma fonte predefinida possa se comunicar com uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="244c5-134">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span> <span data-ttu-id="244c5-135">tooaccess Olá IIS Web farm que você está instalando, você deve adicionar uma regra de entrada do NSG.</span><span class="sxs-lookup"><span data-stu-id="244c5-135">tooaccess hello IIS webserver that you are installing, you must add an inbound NSG rule.</span></span>

<span data-ttu-id="244c5-136">toocreate uma regra de entrada NSG, use [AzureRmNetworkSecurityRuleConfig adicionar](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="244c5-136">toocreate an inbound NSG rule, use [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="244c5-137">Olá, exemplo a seguir cria uma regra NSG denominada *myNSGRule* que abre a porta *3389* para a máquina virtual de saudação:</span><span class="sxs-lookup"><span data-stu-id="244c5-137">hello following example creates an NSG rule named *myNSGRule* that opens port *3389* for hello virtual machine:</span></span>

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

<span data-ttu-id="244c5-138">Criar hello NSG usando *myNSGRule* com [AzureRmNetworkSecurityGroup novo](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="244c5-138">Create hello NSG using *myNSGRule* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

<span data-ttu-id="244c5-139">Adicionar sub-rede de toohello NSG Olá na rede virtual de saudação com [AzureRmVirtualNetworkSubnetConfig conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="244c5-139">Add hello NSG toohello subnet in hello virtual network with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="244c5-140">Rede virtual de saudação de atualização com [AzureRmVirtualNetwork conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="244c5-140">Update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a><span data-ttu-id="244c5-141">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="244c5-141">Create virtual machine</span></span>

<span data-ttu-id="244c5-142">Há várias opções disponíveis ao criar uma máquina virtual, como a imagem do sistema operacional, as credenciais administrativas e o dimensionamento do disco.</span><span class="sxs-lookup"><span data-stu-id="244c5-142">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="244c5-143">Neste exemplo, uma máquina virtual é criada com um nome de *myVM* versão mais recente de execução saudação do Datacenter do Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="244c5-143">In this example, a virtual machine is created with a name of *myVM* running hello latest version of Windows Server 2016 Datacenter.</span></span>

<span data-ttu-id="244c5-144">Definir Olá nome de usuário e a senha necessários para a conta de administrador de saudação em máquina virtual Olá [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="244c5-144">Set hello username and password needed for hello administrator account on hello virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="244c5-145">Criar a configuração inicial da máquina virtual de saudação com hello [AzureRmVMConfig novo](/powershell/module/azurerm.compute/new-azurermvmconfig):</span><span class="sxs-lookup"><span data-stu-id="244c5-145">Create hello initial configuration for hello virtual machine with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

<span data-ttu-id="244c5-146">Adicionar sistema operacional Olá informações sobre configuração de máquina virtual toohello com [AzureRmVMOperatingSystem conjunto](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span><span class="sxs-lookup"><span data-stu-id="244c5-146">Add hello operating system information toohello virtual machine configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span></span>

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="244c5-147">Adicionar configuração da máquina virtual Olá imagem informações toohello com [AzureRmVMSourceImage conjunto](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span><span class="sxs-lookup"><span data-stu-id="244c5-147">Add hello image information toohello virtual machine configuration with [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

<span data-ttu-id="244c5-148">Adicionar configurações do hello sistema operacional disco toohello máquina virtual com [AzureRmVMOSDisk conjunto](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span><span class="sxs-lookup"><span data-stu-id="244c5-148">Add hello operating system disk settings toohello virtual machine configuration with [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

<span data-ttu-id="244c5-149">Adicionar Olá placa de rede que você criou anteriormente toohello configuração da máquina virtual com [adicionar AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="244c5-149">Add hello network interface card that you previously created toohello virtual machine configuration with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="244c5-150">Criar a máquina virtual Olá [AzureRmVM novo](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="244c5-150">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-toovm"></a><span data-ttu-id="244c5-151">Conecte-se tooVM</span><span class="sxs-lookup"><span data-stu-id="244c5-151">Connect tooVM</span></span>

<span data-ttu-id="244c5-152">Após a implantação de hello, crie uma conexão de área de trabalho remota com a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="244c5-152">After hello deployment has completed, create a remote desktop connection with hello virtual machine.</span></span>

<span data-ttu-id="244c5-153">Execute Olá comandos tooreturn Olá endereço IP público da máquina virtual de saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="244c5-153">Run hello following commands tooreturn hello public IP address of hello virtual machine.</span></span> <span data-ttu-id="244c5-154">Anote esse endereço IP para tooit possa se conectar com a conectividade do navegador tootest web em uma etapa futura.</span><span class="sxs-lookup"><span data-stu-id="244c5-154">Take note of this IP Address so you can connect tooit with your browser tootest web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

<span data-ttu-id="244c5-155">A seguir Olá Use o comando toocreate uma sessão de área de trabalho remota com a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="244c5-155">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="244c5-156">Substitua o endereço IP de saudação com hello *publicIPAddress* de sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="244c5-156">Replace hello IP address with hello *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="244c5-157">Quando solicitado, insira as credenciais de saudação usadas ao criar a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="244c5-157">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a><span data-ttu-id="244c5-158">Entender as imagens de VM</span><span class="sxs-lookup"><span data-stu-id="244c5-158">Understand VM images</span></span>

<span data-ttu-id="244c5-159">Olá marketplace do Azure inclui várias imagens de máquinas virtuais que podem ser usada toocreate uma nova máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="244c5-159">hello Azure marketplace includes many virtual machine images that can be used toocreate a new virtual machine.</span></span> <span data-ttu-id="244c5-160">Nas etapas anteriores do hello, uma máquina virtual foi criada usando a imagem do Windows Server 2016-Datacenter hello.</span><span class="sxs-lookup"><span data-stu-id="244c5-160">In hello previous steps, a virtual machine was created using hello Windows Server 2016-Datacenter image.</span></span> <span data-ttu-id="244c5-161">Nesta etapa, o módulo do PowerShell de saudação está marketplace de saudação toosearch usado para outras imagens do Windows, que pode também como base para novas VMs.</span><span class="sxs-lookup"><span data-stu-id="244c5-161">In this step, hello PowerShell module is used toosearch hello marketplace for other Windows images, which can also as a base for new VMs.</span></span> <span data-ttu-id="244c5-162">Esse processo consiste em localizar publicador hello, oferta e nome da imagem hello (Sku).</span><span class="sxs-lookup"><span data-stu-id="244c5-162">This process consists of finding hello publisher, offer, and hello image name (Sku).</span></span> 

<span data-ttu-id="244c5-163">Saudação de uso [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) tooreturn comando uma lista de editores de imagem.</span><span class="sxs-lookup"><span data-stu-id="244c5-163">Use hello [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) command tooreturn a list of image publishers.</span></span>  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

<span data-ttu-id="244c5-164">Saudação de uso [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn uma lista de ofertas de imagem.</span><span class="sxs-lookup"><span data-stu-id="244c5-164">Use hello [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn a list of image offers.</span></span> <span data-ttu-id="244c5-165">Com este comando, Olá retornado lista é filtrada no publicador especificado hello.</span><span class="sxs-lookup"><span data-stu-id="244c5-165">With this command, hello returned list is filtered on hello specified publisher.</span></span> 

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

<span data-ttu-id="244c5-166">Olá [AzureRmVMImageSku Get](/powershell/module/azurerm.compute/get-azurermvmimagesku) comando, em seguida, filtrará Olá tooreturn de nome de publicador e oferecem uma lista de nomes de imagem.</span><span class="sxs-lookup"><span data-stu-id="244c5-166">hello [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) command will then filter on hello publisher and offer name tooreturn a list of image names.</span></span>

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

<span data-ttu-id="244c5-167">Essas informações podem ser usada toodeploy uma VM com uma imagem específica.</span><span class="sxs-lookup"><span data-stu-id="244c5-167">This information can be used toodeploy a VM with a specific image.</span></span> <span data-ttu-id="244c5-168">Este exemplo define o nome da imagem Olá no objeto da VM hello.</span><span class="sxs-lookup"><span data-stu-id="244c5-168">This example sets hello image name on hello VM object.</span></span> <span data-ttu-id="244c5-169">Consulte os exemplos anteriores toohello neste tutorial para etapas de implantação completa.</span><span class="sxs-lookup"><span data-stu-id="244c5-169">Refer toohello previous examples in this tutorial for complete deployment steps.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="244c5-170">Entender os tamanhos de VM</span><span class="sxs-lookup"><span data-stu-id="244c5-170">Understand VM sizes</span></span>

<span data-ttu-id="244c5-171">Um tamanho de máquina virtual determina a quantidade de saudação de recursos de computação, como memória, CPU e GPU que são feitas a máquina virtual de toohello disponíveis.</span><span class="sxs-lookup"><span data-stu-id="244c5-171">A virtual machine size determines hello amount of compute resources such as CPU, GPU, and memory that are made available toohello virtual machine.</span></span> <span data-ttu-id="244c5-172">Máquinas virtuais precisam toobe criado com um tamanho apropriado para Olá espera que a carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="244c5-172">Virtual machines need toobe created with a size appropriate for hello expect work load.</span></span> <span data-ttu-id="244c5-173">Se a carga de trabalho aumentar, uma máquina virtual existente pode ser redimensionada.</span><span class="sxs-lookup"><span data-stu-id="244c5-173">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="244c5-174">Tamanhos de VM</span><span class="sxs-lookup"><span data-stu-id="244c5-174">VM Sizes</span></span>

<span data-ttu-id="244c5-175">Olá, a tabela a seguir categoriza tamanhos em casos de uso.</span><span class="sxs-lookup"><span data-stu-id="244c5-175">hello following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="244c5-176">Tipo</span><span class="sxs-lookup"><span data-stu-id="244c5-176">Type</span></span>                     | <span data-ttu-id="244c5-177">Tamanhos</span><span class="sxs-lookup"><span data-stu-id="244c5-177">Sizes</span></span>           |    <span data-ttu-id="244c5-178">Descrição</span><span class="sxs-lookup"><span data-stu-id="244c5-178">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="244c5-179">Propósito geral</span><span class="sxs-lookup"><span data-stu-id="244c5-179">General purpose</span></span>         |<span data-ttu-id="244c5-180">DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="244c5-180">DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="244c5-181">CPU/memória equilibrados.</span><span class="sxs-lookup"><span data-stu-id="244c5-181">Balanced CPU-to-memory.</span></span> <span data-ttu-id="244c5-182">Ideal para desenvolvimento / teste e pequenas toomedium soluções de aplicativos e dados.</span><span class="sxs-lookup"><span data-stu-id="244c5-182">Ideal for dev / test and small toomedium applications and data solutions.</span></span>  |
| <span data-ttu-id="244c5-183">Otimizado para computação</span><span class="sxs-lookup"><span data-stu-id="244c5-183">Compute optimized</span></span>      | <span data-ttu-id="244c5-184">Fs, F</span><span class="sxs-lookup"><span data-stu-id="244c5-184">Fs, F</span></span>             | <span data-ttu-id="244c5-185">Relação de CPU/memória alta.</span><span class="sxs-lookup"><span data-stu-id="244c5-185">High CPU-to-memory.</span></span> <span data-ttu-id="244c5-186">Boa para aplicativos de tráfego médio, dispositivos de rede e processos em lote.</span><span class="sxs-lookup"><span data-stu-id="244c5-186">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| <span data-ttu-id="244c5-187">Otimizado para memória</span><span class="sxs-lookup"><span data-stu-id="244c5-187">Memory optimized</span></span>       | <span data-ttu-id="244c5-188">GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="244c5-188">GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="244c5-189">Relação de memória/núcleo alta.</span><span class="sxs-lookup"><span data-stu-id="244c5-189">High memory-to-core.</span></span> <span data-ttu-id="244c5-190">Excelente para bancos de dados relacionais, caches toolarge médios e análise de memória.</span><span class="sxs-lookup"><span data-stu-id="244c5-190">Great for relational databases, medium toolarge caches, and in-memory analytics.</span></span>                 |
| <span data-ttu-id="244c5-191">Otimizado para armazenamento</span><span class="sxs-lookup"><span data-stu-id="244c5-191">Storage optimized</span></span>       | <span data-ttu-id="244c5-192">Ls</span><span class="sxs-lookup"><span data-stu-id="244c5-192">Ls</span></span>                | <span data-ttu-id="244c5-193">Alta taxa de transferência de disco e de E/S.</span><span class="sxs-lookup"><span data-stu-id="244c5-193">High disk throughput and IO.</span></span> <span data-ttu-id="244c5-194">Ideal para Big Data, SQL e bancos de dados NoSQL.</span><span class="sxs-lookup"><span data-stu-id="244c5-194">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| <span data-ttu-id="244c5-195">GPU</span><span class="sxs-lookup"><span data-stu-id="244c5-195">GPU</span></span>           | <span data-ttu-id="244c5-196">NV, NC</span><span class="sxs-lookup"><span data-stu-id="244c5-196">NV, NC</span></span>            | <span data-ttu-id="244c5-197">VMs especializadas, destinadas para renderização gráfica e edição de vídeo pesadas.</span><span class="sxs-lookup"><span data-stu-id="244c5-197">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| <span data-ttu-id="244c5-198">Alto desempenho</span><span class="sxs-lookup"><span data-stu-id="244c5-198">High performance</span></span> | <span data-ttu-id="244c5-199">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="244c5-199">H, A8-11</span></span>          | <span data-ttu-id="244c5-200">Nossas VMs de CPU mais potentes com adaptadores de rede de alto rendimento (RDMA) opcionais.</span><span class="sxs-lookup"><span data-stu-id="244c5-200">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="244c5-201">Encontrar tamanhos de VM disponíveis</span><span class="sxs-lookup"><span data-stu-id="244c5-201">Find available VM sizes</span></span>

<span data-ttu-id="244c5-202">toosee uma lista de VM tamanhos disponíveis em uma determinada região, use Olá [AzureRmVMSize Get](/powershell/module/azurerm.compute/get-azurermvmsize) comando.</span><span class="sxs-lookup"><span data-stu-id="244c5-202">toosee a list of VM sizes available in a particular region, use hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command.</span></span>

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a><span data-ttu-id="244c5-203">Redimensionar uma VM</span><span class="sxs-lookup"><span data-stu-id="244c5-203">Resize a VM</span></span>

<span data-ttu-id="244c5-204">Depois que uma máquina virtual foi implantada, pode ser redimensionada tooincrease ou diminuir a alocação de recursos.</span><span class="sxs-lookup"><span data-stu-id="244c5-204">After a VM has been deployed, it can be resized tooincrease or decrease resource allocation.</span></span>

<span data-ttu-id="244c5-205">Antes de redimensionar uma VM, verifique se hello tamanho desejado está disponível no cluster da VM atual hello.</span><span class="sxs-lookup"><span data-stu-id="244c5-205">Before resizing a VM, check if hello desired size is available on hello current VM cluster.</span></span> <span data-ttu-id="244c5-206">Olá [AzureRmVMSize Get](/powershell/module/azurerm.compute/get-azurermvmsize) comando retorna uma lista de tamanhos.</span><span class="sxs-lookup"><span data-stu-id="244c5-206">hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command returns a list of sizes.</span></span> 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

<span data-ttu-id="244c5-207">Se Olá desejado tamanho estiver disponível, hello VM pode ser redimensionada de um estado ligado, mas ele é reinicializado durante a operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="244c5-207">If hello desired size is available, hello VM can be resized from a powered-on state, however it is rebooted during hello operation.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

<span data-ttu-id="244c5-208">Se o tamanho desejado de saudação não está em cluster atual hello, Olá VM necessidades toobe desalocada antes da operação de redimensionamento Olá pode ocorrer.</span><span class="sxs-lookup"><span data-stu-id="244c5-208">If hello desired size is not on hello current cluster, hello VM needs toobe deallocated before hello resize operation can occur.</span></span> <span data-ttu-id="244c5-209">Observe que, quando Olá VM está ligada novamente, os dados no disco temporário Olá são removidos e endereço IP público de saudação alterar, a menos que um endereço IP estático está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="244c5-209">Note, when hello VM is powered back on, any data on hello temp disk are removed, and hello public IP address change unless a static IP address is being used.</span></span> 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a><span data-ttu-id="244c5-210">Estados de energia da VM</span><span class="sxs-lookup"><span data-stu-id="244c5-210">VM power states</span></span>

<span data-ttu-id="244c5-211">Uma VM do Azure pode ter um dentre vários estados de energia.</span><span class="sxs-lookup"><span data-stu-id="244c5-211">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="244c5-212">Nesse estado representa o estado atual de saudação do hello VM do ponto de vista de saudação do hipervisor Olá.</span><span class="sxs-lookup"><span data-stu-id="244c5-212">This state represents hello current state of hello VM from hello standpoint of hello hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="244c5-213">Estados de energia</span><span class="sxs-lookup"><span data-stu-id="244c5-213">Power states</span></span>

| <span data-ttu-id="244c5-214">Estado de energia</span><span class="sxs-lookup"><span data-stu-id="244c5-214">Power State</span></span> | <span data-ttu-id="244c5-215">Descrição</span><span class="sxs-lookup"><span data-stu-id="244c5-215">Description</span></span>
|----|----|
| <span data-ttu-id="244c5-216">Iniciando</span><span class="sxs-lookup"><span data-stu-id="244c5-216">Starting</span></span> | <span data-ttu-id="244c5-217">Indica a máquina virtual de hello está sendo iniciada.</span><span class="sxs-lookup"><span data-stu-id="244c5-217">Indicates hello virtual machine is being started.</span></span> |
| <span data-ttu-id="244c5-218">Executando</span><span class="sxs-lookup"><span data-stu-id="244c5-218">Running</span></span> | <span data-ttu-id="244c5-219">Indica que a máquina virtual hello está em execução.</span><span class="sxs-lookup"><span data-stu-id="244c5-219">Indicates that hello virtual machine is running.</span></span> |
| <span data-ttu-id="244c5-220">Parando</span><span class="sxs-lookup"><span data-stu-id="244c5-220">Stopping</span></span> | <span data-ttu-id="244c5-221">Indica que a máquina virtual hello está sendo interrompida.</span><span class="sxs-lookup"><span data-stu-id="244c5-221">Indicates that hello virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="244c5-222">Parada</span><span class="sxs-lookup"><span data-stu-id="244c5-222">Stopped</span></span> | <span data-ttu-id="244c5-223">Indica que a máquina virtual hello está parada.</span><span class="sxs-lookup"><span data-stu-id="244c5-223">Indicates that hello virtual machine is stopped.</span></span> <span data-ttu-id="244c5-224">Observe que máquinas virtuais no estado interrompido de saudação ainda incorrerá em encargos de computação.</span><span class="sxs-lookup"><span data-stu-id="244c5-224">Note that virtual machines in hello stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="244c5-225">Desalocando</span><span class="sxs-lookup"><span data-stu-id="244c5-225">Deallocating</span></span> | <span data-ttu-id="244c5-226">Indica que a máquina virtual hello está sendo desalocada.</span><span class="sxs-lookup"><span data-stu-id="244c5-226">Indicates that hello virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="244c5-227">Desalocada</span><span class="sxs-lookup"><span data-stu-id="244c5-227">Deallocated</span></span> | <span data-ttu-id="244c5-228">Indica que a máquina virtual Olá foi completamente removida do hipervisor Olá mas ainda estará disponível no plano de controle de saudação.</span><span class="sxs-lookup"><span data-stu-id="244c5-228">Indicates that hello virtual machine is completely removed from hello hypervisor but still available in hello control plane.</span></span> <span data-ttu-id="244c5-229">Máquinas virtuais no estado desalocada da saudação não incorrerá em encargos de computação.</span><span class="sxs-lookup"><span data-stu-id="244c5-229">Virtual machines in hello Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="244c5-230">Indica que o estado de energia de saudação da máquina virtual de saudação é desconhecido.</span><span class="sxs-lookup"><span data-stu-id="244c5-230">Indicates that hello power state of hello virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="244c5-231">Localizar o estado de energia</span><span class="sxs-lookup"><span data-stu-id="244c5-231">Find power state</span></span>

<span data-ttu-id="244c5-232">estado de saudação tooretrieve de uma VM específica, use Olá [AzureRmVM Get](/powershell/module/azurerm.compute/get-azurermvm) comando.</span><span class="sxs-lookup"><span data-stu-id="244c5-232">tooretrieve hello state of a particular VM, use hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span> <span data-ttu-id="244c5-233">Ser toospecify se um nome válido para uma máquina virtual e o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="244c5-233">Be sure toospecify a valid name for a virtual machine and resource group.</span></span> 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

<span data-ttu-id="244c5-234">Saída:</span><span class="sxs-lookup"><span data-stu-id="244c5-234">Output:</span></span>

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a><span data-ttu-id="244c5-235">Tarefas de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="244c5-235">Management tasks</span></span>

<span data-ttu-id="244c5-236">Durante a saudação do ciclo de vida de uma máquina virtual, talvez você queira toorun tarefas de gerenciamento como iniciar, parar ou excluir uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="244c5-236">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="244c5-237">Além disso, talvez você queira toocreate scripts tooautomate repetitivas ou complexas tarefas.</span><span class="sxs-lookup"><span data-stu-id="244c5-237">Additionally, you may want toocreate scripts tooautomate repetitive or complex tasks.</span></span> <span data-ttu-id="244c5-238">Usando o Azure PowerShell, muitas tarefas comuns de gerenciamento podem ser executadas da linha de comando hello, ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="244c5-238">Using Azure PowerShell, many common management tasks can be run from hello command line or in scripts.</span></span>

### <a name="stop-virtual-machine"></a><span data-ttu-id="244c5-239">Como interromper uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="244c5-239">Stop virtual machine</span></span>

<span data-ttu-id="244c5-240">Pare e desaloque uma máquina virtual com [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="244c5-240">Stop and deallocate a virtual machine with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

<span data-ttu-id="244c5-241">Se você quiser tookeep Olá VM em um estado de provisionamento, use o parâmetro de - StayProvisioned de saudação.</span><span class="sxs-lookup"><span data-stu-id="244c5-241">If you want tookeep hello virtual machine in a provisioned state, use hello -StayProvisioned parameter.</span></span>

### <a name="start-virtual-machine"></a><span data-ttu-id="244c5-242">Como iniciar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="244c5-242">Start virtual machine</span></span>

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="244c5-243">Excluir grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="244c5-243">Delete resource group</span></span>

<span data-ttu-id="244c5-244">Excluir um grupo de recursos exclui todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="244c5-244">Deleting a resource group also deletes all resources contained within.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a><span data-ttu-id="244c5-245">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="244c5-245">Next steps</span></span>

<span data-ttu-id="244c5-246">Neste tutorial, você aprendeu sobre a criação e o gerenciamento básico de VM e como:</span><span class="sxs-lookup"><span data-stu-id="244c5-246">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="244c5-247">Criar e conectar tooa VM</span><span class="sxs-lookup"><span data-stu-id="244c5-247">Create and connect tooa VM</span></span>
> * <span data-ttu-id="244c5-248">Selecionar e usar imagens de VM</span><span class="sxs-lookup"><span data-stu-id="244c5-248">Select and use VM images</span></span>
> * <span data-ttu-id="244c5-249">Exibir e usar tamanhos específicos de VM</span><span class="sxs-lookup"><span data-stu-id="244c5-249">View and use specific VM sizes</span></span>
> * <span data-ttu-id="244c5-250">Redimensionar uma VM</span><span class="sxs-lookup"><span data-stu-id="244c5-250">Resize a VM</span></span>
> * <span data-ttu-id="244c5-251">Exibir e compreender o estado da VM</span><span class="sxs-lookup"><span data-stu-id="244c5-251">View and understand VM state</span></span>

<span data-ttu-id="244c5-252">Avançar toohello toolearn próximo de tutorial sobre discos de VM.</span><span class="sxs-lookup"><span data-stu-id="244c5-252">Advance toohello next tutorial toolearn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="244c5-253">Criar e gerenciar discos de VM</span><span class="sxs-lookup"><span data-stu-id="244c5-253">Create and Manage VM disks</span></span>](./tutorial-manage-data-disk.md)
