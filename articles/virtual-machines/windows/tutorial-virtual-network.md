---
title: "Redes virtuais do Azure e Máquinas Virtuais do Windows | Microsoft Docs"
description: "Tutorial – Gerenciar redes virtuais do Azure e Máquinas Virtuais do Windows com o Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: c71c07f8ecd123a7e27848ba5043d46e315fcf03
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a><span data-ttu-id="f4505-103">Gerenciar redes virtuais do Azure e Máquinas Virtuais do Windows com o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4505-103">Manage Azure Virtual Networks and Windows Virtual Machines with Azure PowerShell</span></span>

<span data-ttu-id="f4505-104">As máquinas virtuais do Azure usam a rede do Azure para comunicação de rede interna e externa.</span><span class="sxs-lookup"><span data-stu-id="f4505-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="f4505-105">Neste tutorial, você cria várias VMs (máquinas virtuais) em uma rede virtual e configura a conectividade de rede entre elas.</span><span class="sxs-lookup"><span data-stu-id="f4505-105">In this tutorial, you create multiple virtual machines (VMs) in a virtual network and configure network connectivity between them.</span></span> <span data-ttu-id="f4505-106">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="f4505-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f4505-107">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="f4505-107">Create a virtual network</span></span>
> * <span data-ttu-id="f4505-108">Criar sub-redes de rede virtual</span><span class="sxs-lookup"><span data-stu-id="f4505-108">Create virtual network subnets</span></span>
> * <span data-ttu-id="f4505-109">Controle de tráfego de rede com grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="f4505-109">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="f4505-110">Exibir regras de tráfego em ação</span><span class="sxs-lookup"><span data-stu-id="f4505-110">View traffic rules in action</span></span>

<span data-ttu-id="f4505-111">Este tutorial requer o módulo do Azure PowerShell, versão 3.6 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f4505-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="f4505-112">Execute ` Get-Module -ListAvailable AzureRM` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="f4505-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="f4505-113">Se você precisa atualizar, consulte [Instalar o módulo do Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="f4505-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-vnet"></a><span data-ttu-id="f4505-114">Criar VNet</span><span class="sxs-lookup"><span data-stu-id="f4505-114">Create VNet</span></span>

<span data-ttu-id="f4505-115">Uma VNet é uma representação da sua própria rede na nuvem.</span><span class="sxs-lookup"><span data-stu-id="f4505-115">A VNet is a representation of your own network in the cloud.</span></span> <span data-ttu-id="f4505-116">Uma VNet é um isolamento lógico da nuvem do Azure dedicada à sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="f4505-116">A VNet is a logical isolation of the Azure cloud dedicated to your subscription.</span></span> <span data-ttu-id="f4505-117">Em uma rede virtual, você deve encontrar sub-redes, regras de conectividade para essas sub-redes e conexões das VMs para as sub-redes.</span><span class="sxs-lookup"><span data-stu-id="f4505-117">Within a VNet, you find subnets, rules for connectivity to those subnets, and connections from the VMs to the subnets.</span></span>

<span data-ttu-id="f4505-118">Antes de criar outros recursos do Azure, será necessário criar um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="f4505-118">Before you can create any other Azure resources, you need to create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="f4505-119">O exemplo abaixo cria um grupo de recursos denominado *myRGNetwork* no local *EastUS*:</span><span class="sxs-lookup"><span data-stu-id="f4505-119">The following example creates a resource group named *myRGNetwork* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

<span data-ttu-id="f4505-120">Uma sub-rede é um recurso filho de uma VNet e ajuda a definir segmentos de espaços de endereços em um bloco CIDR, usando prefixos de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="f4505-120">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="f4505-121">As NICs podem ser adicionadas a sub-redes e conectadas a VMs, fornecendo conectividade para diversas cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f4505-121">NICs can be added to subnets, and connected to VMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="f4505-122">Crie uma sub-rede com [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="f4505-122">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="f4505-123">Crie uma rede virtual denominada *myVNet* usando *myFrontendSubnet* com [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="f4505-123">Create a VNET named *myVNet* using *myFrontendSubnet* with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a><span data-ttu-id="f4505-124">Criar VM de front-end</span><span class="sxs-lookup"><span data-stu-id="f4505-124">Create front-end VM</span></span>

<span data-ttu-id="f4505-125">Para uma VM se comunicar em uma VNet, ela precisará de uma interface de rede virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="f4505-125">For a VM to communicate in a VNet, it needs a virtual network interface (NIC).</span></span> <span data-ttu-id="f4505-126">A *myFrontendVM* é acessada pela Internet, então ela também precisa de um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="f4505-126">The *myFrontendVM* is accessed from the internet, so it also needs a public IP address.</span></span> 

<span data-ttu-id="f4505-127">Crie um endereço IP público com [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="f4505-127">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

<span data-ttu-id="f4505-128">Crie uma NIC com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="f4505-128">Create a NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

<span data-ttu-id="f4505-129">Defina o nome de usuário e a senha necessários para a conta de administrador na VM com [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="f4505-129">Set the username and password needed for the administrator account on the VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="f4505-130">Crie as VMs com [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) e [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="f4505-130">Create the VMs with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> 

```powershell
$frontendVM = New-AzureRmVMConfig `
    -VMName myFrontendVM `
    -VMSize Standard_D1
$frontendVM = Set-AzureRmVMOperatingSystem `
    -VM $frontendVM `
    -Windows `
    -ComputerName myFrontendVM `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
$frontendVM = Set-AzureRmVMSourceImage `
    -VM $frontendVM `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
$frontendVM = Set-AzureRmVMOSDisk `
    -VM $frontendVM `
    -Name myFrontendOSDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
$frontendVM = Add-AzureRmVMNetworkInterface `
    -VM $frontendVM `
    -Id $frontendNic.Id
New-AzureRmVM `
    -ResourceGroupName myRGNetwork `
    -Location EastUS `
    -VM $frontendVM
```

## <a name="install-web-server"></a><span data-ttu-id="f4505-131">Instalar servidor Web</span><span class="sxs-lookup"><span data-stu-id="f4505-131">Install web server</span></span>

<span data-ttu-id="f4505-132">Você pode instalar o IIS em *myFrontendVM* usando uma sessão de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="f4505-132">You can install IIS on *myFrontendVM* by using a remote desktop session.</span></span> <span data-ttu-id="f4505-133">Você precisa obter o endereço IP público da VM para acessá-la.</span><span class="sxs-lookup"><span data-stu-id="f4505-133">You need to get the public IP address of the VM to access it.</span></span>

<span data-ttu-id="f4505-134">Você pode utilizar o endereço IP público da *myFrontendVM* com [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="f4505-134">You can get the public IP address of *myFrontendVM* with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="f4505-135">O exemplo a seguir obtém o endereço IP para *myPublicIPAddress* criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="f4505-135">The following example obtains the IP address for *myPublicIPAddress* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

<span data-ttu-id="f4505-136">Anote esse endereço IP para usá-lo em etapas futuras.</span><span class="sxs-lookup"><span data-stu-id="f4505-136">Take note of this IP Address so you can use it in future steps.</span></span>

<span data-ttu-id="f4505-137">Use o seguinte comando para criar uma sessão de área de trabalho remota com *myFrontendVM*.</span><span class="sxs-lookup"><span data-stu-id="f4505-137">Use the following command to create a remote desktop session with *myFrontendVM*.</span></span> <span data-ttu-id="f4505-138">Substitua *<publicIPAddress>* pelo endereço que você registrou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f4505-138">Replace *<publicIPAddress>* with the address that you previously recorded.</span></span> <span data-ttu-id="f4505-139">Quando solicitado, insira as credenciais usadas quando você criou a VM.</span><span class="sxs-lookup"><span data-stu-id="f4505-139">When prompted, enter the credentials used when you created the VM.</span></span>

```
mstsc /v:<publicIpAddress>
``` 

<span data-ttu-id="f4505-140">Agora que você fez logon na *myFrontendVM*, pode usar uma única linha do PowerShell para instalar o IIS e habilitar a regra de firewall local para permitir o tráfego da Web.</span><span class="sxs-lookup"><span data-stu-id="f4505-140">Now that you have logged in to *myFrontendVM*, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span></span> <span data-ttu-id="f4505-141">Abra um promt do PowerShell e execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="f4505-141">Open a PowerShell prompt and run the following command:</span></span>

<span data-ttu-id="f4505-142">Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) para executar a extensão do script personalizado que instala o servidor da Web do IIS:</span><span class="sxs-lookup"><span data-stu-id="f4505-142">Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) to run the custom script extension that installs the IIS webserver:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="f4505-143">Agora você pode usar o endereço IP público para navegar até a VM para ver o site do IIS.</span><span class="sxs-lookup"><span data-stu-id="f4505-143">Now you can use the public IP address to browse to the VM to see the IIS site.</span></span>

![Site do IIS padrão](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a><span data-ttu-id="f4505-145">Gerenciar o tráfego interno</span><span class="sxs-lookup"><span data-stu-id="f4505-145">Manage internal traffic</span></span>

<span data-ttu-id="f4505-146">Um NSG (grupo de segurança de rede) contém uma lista de regras de segurança que permitem ou negam o tráfego de rede para recursos conectados a uma VNet.</span><span class="sxs-lookup"><span data-stu-id="f4505-146">A network security group (NSG) contains a list of security rules that allow or deny network traffic to resources connected to a VNet.</span></span> <span data-ttu-id="f4505-147">Os NSGs podem ser associados a sub-redes ou NICs individuais anexadas às VMs.</span><span class="sxs-lookup"><span data-stu-id="f4505-147">NSGs can be associated to subnets or individual NICs attached to VMs.</span></span> <span data-ttu-id="f4505-148">Abrir ou fechar o acesso às VMs por meio de portas é feito usando regras de NSG.</span><span class="sxs-lookup"><span data-stu-id="f4505-148">Opening or closing access to VMs through ports is done using NSG rules.</span></span> <span data-ttu-id="f4505-149">Quando você criou a *myFrontendVM*, a porta 3389 de entrada foi aberta automaticamente para conectividade RDP.</span><span class="sxs-lookup"><span data-stu-id="f4505-149">When you created *myFrontendVM*, inbound port 3389 was automatically opened for RDP connectivity.</span></span>

<span data-ttu-id="f4505-150">A comunicação interna de VMs pode ser configurada usando um NSG.</span><span class="sxs-lookup"><span data-stu-id="f4505-150">Internal communication of VMs can be configured using an NSG.</span></span> <span data-ttu-id="f4505-151">Nesta seção, você aprenderá a criar uma sub-rede adicional na rede e atribuir um NSG a ela para permitir uma conexão de *myFrontendVM* para *myBackendVM* na porta 1433.</span><span class="sxs-lookup"><span data-stu-id="f4505-151">In this section, you learn how to create an additional subnet in the network and assign an NSG to it to allow a connection from *myFrontendVM* to *myBackendVM* on port 1433.</span></span> <span data-ttu-id="f4505-152">A sub-rede é então atribuída à VM quando ela é criada.</span><span class="sxs-lookup"><span data-stu-id="f4505-152">The subnet is then assigned to the VM when it is created.</span></span>

<span data-ttu-id="f4505-153">Você pode limitar o tráfego interno para *myBackendVM* apenas de *myFrontendVM* criando um NSG para a sub-rede de back-end.</span><span class="sxs-lookup"><span data-stu-id="f4505-153">You can limit internal traffic to *myBackendVM* from only *myFrontendVM* by creating an NSG for the back-end subnet.</span></span> <span data-ttu-id="f4505-154">O exemplo a seguir cria uma regra NSG chamada *myBackendNSGRule* com [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span><span class="sxs-lookup"><span data-stu-id="f4505-154">The following example creates an NSG rule named *myBackendNSGRule* with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span></span>

```powershell
$nsgBackendRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myBackendNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 100 `
  -SourceAddressPrefix 10.0.0.0/24 `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 1433 `
  -Access Allow
```

<span data-ttu-id="f4505-155">Adicione um grupo de segurança de rede chamado *myBackendNSG* com [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="f4505-155">Add a network security group named *myBackendNSG* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a><span data-ttu-id="f4505-156">Adicionar sub-rede back-end</span><span class="sxs-lookup"><span data-stu-id="f4505-156">Add back-end subnet</span></span>

<span data-ttu-id="f4505-157">Adicione *myBackEndSubnet* à *myVNet* com [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="f4505-157">Add *myBackEndSubnet* to *myVNet* with [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig `
  -Name myBackendSubnet `
  -VirtualNetwork $vnet `
  -AddressPrefix 10.0.1.0/24 `
  -NetworkSecurityGroup $nsgBackend
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Name myVNet
```

## <a name="create-back-end-vm"></a><span data-ttu-id="f4505-158">Criar VM back-end</span><span class="sxs-lookup"><span data-stu-id="f4505-158">Create back-end VM</span></span>

<span data-ttu-id="f4505-159">A maneira mais fácil de criar a máquina virtual de back-end é usar uma imagem do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f4505-159">The easiest way to create the back-end VM is by using a SQL Server image.</span></span> <span data-ttu-id="f4505-160">Este tutorial apenas cria a VM com o servidor de banco de dados, mas não fornece informações sobre como acessá-lo.</span><span class="sxs-lookup"><span data-stu-id="f4505-160">This tutorial only creates the VM with the database server, but doesn't provide information about accessing the database.</span></span>

<span data-ttu-id="f4505-161">Crie *myBackendNic*:</span><span class="sxs-lookup"><span data-stu-id="f4505-161">Create *myBackendNic*:</span></span>

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

<span data-ttu-id="f4505-162">Defina o nome de usuário e a senha necessários para a conta de administrador na VM com Get-Credential:</span><span class="sxs-lookup"><span data-stu-id="f4505-162">Set the username and password needed for the administrator account on the VM with Get-Credential:</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="f4505-163">Crie *myBackendVM*:</span><span class="sxs-lookup"><span data-stu-id="f4505-163">Create *myBackendVM*:</span></span>

```powershell
$backendVM = New-AzureRmVMConfig `
  -VMName myBackendVM `
  -VMSize Standard_D1
$backendVM = Set-AzureRmVMOperatingSystem `
  -VM $backendVM `
  -Windows `
  -ComputerName myBackendVM `
  -Credential $cred `
  -ProvisionVMAgent `
  -EnableAutoUpdate
$backendVM = Set-AzureRmVMSourceImage `
  -VM $backendVM `
  -PublisherName MicrosoftSQLServer `
  -Offer SQL2016SP1-WS2016 `
  -Skus Enterprise `
  -Version latest
$backendVM = Set-AzureRmVMOSDisk `
  -VM $backendVM `
  -Name myBackendOSDisk `
  -DiskSizeInGB 128 `
  -CreateOption FromImage `
  -Caching ReadWrite
$backendVM = Add-AzureRmVMNetworkInterface `
  -VM $backendVM `
  -Id $backendNic.Id
New-AzureRmVM `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -VM $backendVM
```

<span data-ttu-id="f4505-164">A imagem que é usada tem o SQL Server instalado, mas não é usada neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="f4505-164">The image that is used has SQL Server installed, but is not used in this tutorial.</span></span> <span data-ttu-id="f4505-165">Ela está incluída para mostrar como você pode configurar uma VM para lidar com o tráfego da Web e uma VM para lidar com o gerenciamento de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f4505-165">It is included to show you how you can configure a VM to handle web traffic and a VM to handle database management.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4505-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f4505-166">Next steps</span></span>

<span data-ttu-id="f4505-167">Neste tutorial, você criou e protegeu redes do Azure em relação às máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="f4505-167">In this tutorial, you created and secured Azure networks as related to virtual machines.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="f4505-168">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="f4505-168">Create a virtual network</span></span>
> * <span data-ttu-id="f4505-169">Criar sub-redes de rede virtual</span><span class="sxs-lookup"><span data-stu-id="f4505-169">Create virtual network subnets</span></span>
> * <span data-ttu-id="f4505-170">Controle de tráfego de rede com grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="f4505-170">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="f4505-171">Exibir regras de tráfego em ação</span><span class="sxs-lookup"><span data-stu-id="f4505-171">View traffic rules in action</span></span>

<span data-ttu-id="f4505-172">Avance para o próximo tutorial a fim de aprender sobre como monitorar e proteger dados em máquinas virtuais usando o backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4505-172">Advance to the next tutorial to learn about monitoring securing data on virtual machines using Azure backup.</span></span> <span data-ttu-id="f4505-173">.</span><span class="sxs-lookup"><span data-stu-id="f4505-173">.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f4505-174">Fazer backup de máquinas virtuais do Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="f4505-174">Back up Windows virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
