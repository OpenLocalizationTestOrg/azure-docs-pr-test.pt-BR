---
title: "aaaAzure redes virtuais e máquinas virtuais do Windows | Microsoft Docs"
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
ms.openlocfilehash: ed77d9d5873e849fcb2aaf15e41899d7ad8c781a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a><span data-ttu-id="f7231-103">Gerenciar redes virtuais do Azure e Máquinas Virtuais do Windows com o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7231-103">Manage Azure Virtual Networks and Windows Virtual Machines with Azure PowerShell</span></span>

<span data-ttu-id="f7231-104">As máquinas virtuais do Azure usam a rede do Azure para comunicação de rede interna e externa.</span><span class="sxs-lookup"><span data-stu-id="f7231-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="f7231-105">Neste tutorial, você cria várias VMs (máquinas virtuais) em uma rede virtual e configura a conectividade de rede entre elas.</span><span class="sxs-lookup"><span data-stu-id="f7231-105">In this tutorial, you create multiple virtual machines (VMs) in a virtual network and configure network connectivity between them.</span></span> <span data-ttu-id="f7231-106">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="f7231-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f7231-107">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="f7231-107">Create a virtual network</span></span>
> * <span data-ttu-id="f7231-108">Criar sub-redes de rede virtual</span><span class="sxs-lookup"><span data-stu-id="f7231-108">Create virtual network subnets</span></span>
> * <span data-ttu-id="f7231-109">Controle de tráfego de rede com grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="f7231-109">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="f7231-110">Exibir regras de tráfego em ação</span><span class="sxs-lookup"><span data-stu-id="f7231-110">View traffic rules in action</span></span>

<span data-ttu-id="f7231-111">Este tutorial requer hello Azure PowerShell versão 3.6 ou posterior do módulo.</span><span class="sxs-lookup"><span data-stu-id="f7231-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="f7231-112">Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7231-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="f7231-113">Se você precisar tooupgrade, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="f7231-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-vnet"></a><span data-ttu-id="f7231-114">Criar VNet</span><span class="sxs-lookup"><span data-stu-id="f7231-114">Create VNet</span></span>

<span data-ttu-id="f7231-115">Uma rede virtual é uma representação de sua própria rede na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="f7231-115">A VNet is a representation of your own network in hello cloud.</span></span> <span data-ttu-id="f7231-116">Uma rede virtual é uma isolamento lógico de saudação nuvem do Azure dedicado tooyour assinatura.</span><span class="sxs-lookup"><span data-stu-id="f7231-116">A VNet is a logical isolation of hello Azure cloud dedicated tooyour subscription.</span></span> <span data-ttu-id="f7231-117">Em uma rede virtual, você encontrar sub-redes, regras para conectividade toothose sub-redes e conexões de sub-redes de toohello VMs hello.</span><span class="sxs-lookup"><span data-stu-id="f7231-117">Within a VNet, you find subnets, rules for connectivity toothose subnets, and connections from hello VMs toohello subnets.</span></span>

<span data-ttu-id="f7231-118">Antes de criar todos os outros recursos do Azure, você precisa toocreate um grupo de recursos com [AzureRmResourceGroup novo](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="f7231-118">Before you can create any other Azure resources, you need toocreate a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="f7231-119">Olá, exemplo a seguir cria um grupo de recursos denominado *myRGNetwork* em Olá *EastUS* local:</span><span class="sxs-lookup"><span data-stu-id="f7231-119">hello following example creates a resource group named *myRGNetwork* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

<span data-ttu-id="f7231-120">Uma sub-rede é um recurso filho de uma VNet e ajuda a definir segmentos de espaços de endereços em um bloco CIDR, usando prefixos de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="f7231-120">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="f7231-121">As NICs podem ser adicionadas toosubnets e tooVMs conectado, fornecendo conectividade para várias cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f7231-121">NICs can be added toosubnets, and connected tooVMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="f7231-122">Crie uma sub-rede com [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="f7231-122">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="f7231-123">Crie uma rede virtual denominada *myVNet* usando *myFrontendSubnet* com [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="f7231-123">Create a VNET named *myVNet* using *myFrontendSubnet* with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a><span data-ttu-id="f7231-124">Criar VM de front-end</span><span class="sxs-lookup"><span data-stu-id="f7231-124">Create front-end VM</span></span>

<span data-ttu-id="f7231-125">Para toocommunicate uma VM em uma rede virtual, ele precisa de uma interface de rede virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="f7231-125">For a VM toocommunicate in a VNet, it needs a virtual network interface (NIC).</span></span> <span data-ttu-id="f7231-126">Olá *myFrontendVM* são acessados de saudação à internet, para que ele também precisa de um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="f7231-126">hello *myFrontendVM* is accessed from hello internet, so it also needs a public IP address.</span></span> 

<span data-ttu-id="f7231-127">Crie um endereço IP público com [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="f7231-127">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

<span data-ttu-id="f7231-128">Crie uma NIC com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="f7231-128">Create a NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

<span data-ttu-id="f7231-129">Definir Olá nome de usuário e a senha necessários para a conta de administrador Olá Olá VM com [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="f7231-129">Set hello username and password needed for hello administrator account on hello VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="f7231-130">Criar VMs Olá com [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [conjunto AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [AzureRmVMSourceImage conjunto](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [AzureRmVMNetworkInterface adicionar](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), e [AzureRmVM novo](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="f7231-130">Create hello VMs with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> 

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

## <a name="install-web-server"></a><span data-ttu-id="f7231-131">Instalar servidor Web</span><span class="sxs-lookup"><span data-stu-id="f7231-131">Install web server</span></span>

<span data-ttu-id="f7231-132">Você pode instalar o IIS em *myFrontendVM* usando uma sessão de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="f7231-132">You can install IIS on *myFrontendVM* by using a remote desktop session.</span></span> <span data-ttu-id="f7231-133">Necessário tooget Olá endereço IP público do hello VM tooaccess-lo.</span><span class="sxs-lookup"><span data-stu-id="f7231-133">You need tooget hello public IP address of hello VM tooaccess it.</span></span>

<span data-ttu-id="f7231-134">Você pode obter o endereço IP público de saudação do *myFrontendVM* com [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="f7231-134">You can get hello public IP address of *myFrontendVM* with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="f7231-135">Olá, exemplo a seguir obtém endereço IP hello *myPublicIPAddress* criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="f7231-135">hello following example obtains hello IP address for *myPublicIPAddress* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

<span data-ttu-id="f7231-136">Anote esse endereço IP para usá-lo em etapas futuras.</span><span class="sxs-lookup"><span data-stu-id="f7231-136">Take note of this IP Address so you can use it in future steps.</span></span>

<span data-ttu-id="f7231-137">Toocreate uma sessão de área de trabalho remota com o comando a seguir de saudação de uso *myFrontendVM*.</span><span class="sxs-lookup"><span data-stu-id="f7231-137">Use hello following command toocreate a remote desktop session with *myFrontendVM*.</span></span> <span data-ttu-id="f7231-138">Substituir  *<publicIPAddress>*  com endereço Olá que você registrou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f7231-138">Replace *<publicIPAddress>* with hello address that you previously recorded.</span></span> <span data-ttu-id="f7231-139">Quando solicitado, insira as credenciais Olá usadas quando você criou Olá VM.</span><span class="sxs-lookup"><span data-stu-id="f7231-139">When prompted, enter hello credentials used when you created hello VM.</span></span>

```
mstsc /v:<publicIpAddress>
``` 

<span data-ttu-id="f7231-140">Agora que você fez muito*myFrontendVM*, você pode usar uma única linha do PowerShell tooinstall IIS e permitir o tráfego da web do hello firewall local regra tooallow.</span><span class="sxs-lookup"><span data-stu-id="f7231-140">Now that you have logged in too*myFrontendVM*, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="f7231-141">Abra um prompt do PowerShell e execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7231-141">Open a PowerShell prompt and run hello following command:</span></span>

<span data-ttu-id="f7231-142">Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun extensão do script personalizado Olá que instala o servidor Web do IIS hello:</span><span class="sxs-lookup"><span data-stu-id="f7231-142">Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun hello custom script extension that installs hello IIS webserver:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="f7231-143">Agora você pode usar o hello IP endereço toobrowse toohello VM toosee Olá IIS site público.</span><span class="sxs-lookup"><span data-stu-id="f7231-143">Now you can use hello public IP address toobrowse toohello VM toosee hello IIS site.</span></span>

![Site do IIS padrão](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a><span data-ttu-id="f7231-145">Gerenciar o tráfego interno</span><span class="sxs-lookup"><span data-stu-id="f7231-145">Manage internal traffic</span></span>

<span data-ttu-id="f7231-146">Um grupo de segurança de rede (NSG) contém uma lista de regras de segurança que permitem ou negam tooa de tooresources conectado de tráfego de rede rede virtual.</span><span class="sxs-lookup"><span data-stu-id="f7231-146">A network security group (NSG) contains a list of security rules that allow or deny network traffic tooresources connected tooa VNet.</span></span> <span data-ttu-id="f7231-147">Os NSGs podem ser associados toosubnets ou NICs individuais conectados tooVMs.</span><span class="sxs-lookup"><span data-stu-id="f7231-147">NSGs can be associated toosubnets or individual NICs attached tooVMs.</span></span> <span data-ttu-id="f7231-148">Abrir ou fechar tooVMs acesso por meio de portas é feita usando as regras NSG.</span><span class="sxs-lookup"><span data-stu-id="f7231-148">Opening or closing access tooVMs through ports is done using NSG rules.</span></span> <span data-ttu-id="f7231-149">Quando você criou a *myFrontendVM*, a porta 3389 de entrada foi aberta automaticamente para conectividade RDP.</span><span class="sxs-lookup"><span data-stu-id="f7231-149">When you created *myFrontendVM*, inbound port 3389 was automatically opened for RDP connectivity.</span></span>

<span data-ttu-id="f7231-150">A comunicação interna de VMs pode ser configurada usando um NSG.</span><span class="sxs-lookup"><span data-stu-id="f7231-150">Internal communication of VMs can be configured using an NSG.</span></span> <span data-ttu-id="f7231-151">Nesta seção, você aprenderá como toocreate uma sub-rede adicional na saudação de rede e atribuir um tooallow de tooit NSG uma conexão de *myFrontendVM* muito*myBackendVM* na porta 1433.</span><span class="sxs-lookup"><span data-stu-id="f7231-151">In this section, you learn how toocreate an additional subnet in hello network and assign an NSG tooit tooallow a connection from *myFrontendVM* too*myBackendVM* on port 1433.</span></span> <span data-ttu-id="f7231-152">subrede Olá é então atribuído toohello VM quando ela é criada.</span><span class="sxs-lookup"><span data-stu-id="f7231-152">hello subnet is then assigned toohello VM when it is created.</span></span>

<span data-ttu-id="f7231-153">Você pode limitar o tráfego interno muito*myBackendVM* de apenas *myFrontendVM* criando um NSG de sub-rede de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7231-153">You can limit internal traffic too*myBackendVM* from only *myFrontendVM* by creating an NSG for hello back-end subnet.</span></span> <span data-ttu-id="f7231-154">Olá, exemplo a seguir cria uma regra NSG denominada *myBackendNSGRule* com [AzureRmNetworkSecurityRuleConfig novo](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span><span class="sxs-lookup"><span data-stu-id="f7231-154">hello following example creates an NSG rule named *myBackendNSGRule* with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span></span>

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

<span data-ttu-id="f7231-155">Adicione um grupo de segurança de rede chamado *myBackendNSG* com [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="f7231-155">Add a network security group named *myBackendNSG* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a><span data-ttu-id="f7231-156">Adicionar sub-rede back-end</span><span class="sxs-lookup"><span data-stu-id="f7231-156">Add back-end subnet</span></span>

<span data-ttu-id="f7231-157">Adicionar *myBackEndSubnet* muito*myVNet* com [adicionar AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="f7231-157">Add *myBackEndSubnet* too*myVNet* with [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span></span>

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

## <a name="create-back-end-vm"></a><span data-ttu-id="f7231-158">Criar VM back-end</span><span class="sxs-lookup"><span data-stu-id="f7231-158">Create back-end VM</span></span>

<span data-ttu-id="f7231-159">Olá Olá toocreate da maneira mais fácil a VM de back-end está usando uma imagem do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f7231-159">hello easiest way toocreate hello back-end VM is by using a SQL Server image.</span></span> <span data-ttu-id="f7231-160">Este tutorial cria Olá VM com o servidor de banco de dados de saudação apenas, mas não fornece informações sobre como acessar o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7231-160">This tutorial only creates hello VM with hello database server, but doesn't provide information about accessing hello database.</span></span>

<span data-ttu-id="f7231-161">Crie *myBackendNic*:</span><span class="sxs-lookup"><span data-stu-id="f7231-161">Create *myBackendNic*:</span></span>

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

<span data-ttu-id="f7231-162">Definir Olá nome de usuário e a senha necessários para a conta de administrador Olá Olá VM com Get-Credential:</span><span class="sxs-lookup"><span data-stu-id="f7231-162">Set hello username and password needed for hello administrator account on hello VM with Get-Credential:</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="f7231-163">Crie *myBackendVM*:</span><span class="sxs-lookup"><span data-stu-id="f7231-163">Create *myBackendVM*:</span></span>

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

<span data-ttu-id="f7231-164">imagem de saudação que é usada com o SQL Server instalado, mas não é usada neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="f7231-164">hello image that is used has SQL Server installed, but is not used in this tutorial.</span></span> <span data-ttu-id="f7231-165">Ele é incluído tooshow é como você pode configurar o tráfego de web de toohandle VM e gerenciamento de banco de dados de toohandle uma VM.</span><span class="sxs-lookup"><span data-stu-id="f7231-165">It is included tooshow you how you can configure a VM toohandle web traffic and a VM toohandle database management.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7231-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f7231-166">Next steps</span></span>

<span data-ttu-id="f7231-167">Neste tutorial, você criou e redes do Azure como máquinas toovirtual relacionados seguras.</span><span class="sxs-lookup"><span data-stu-id="f7231-167">In this tutorial, you created and secured Azure networks as related toovirtual machines.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="f7231-168">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="f7231-168">Create a virtual network</span></span>
> * <span data-ttu-id="f7231-169">Criar sub-redes de rede virtual</span><span class="sxs-lookup"><span data-stu-id="f7231-169">Create virtual network subnets</span></span>
> * <span data-ttu-id="f7231-170">Controle de tráfego de rede com grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="f7231-170">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="f7231-171">Exibir regras de tráfego em ação</span><span class="sxs-lookup"><span data-stu-id="f7231-171">View traffic rules in action</span></span>

<span data-ttu-id="f7231-172">Avançar toohello toolearn próximo de tutorial sobre como monitorar a proteção de dados em máquinas virtuais usando o backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7231-172">Advance toohello next tutorial toolearn about monitoring securing data on virtual machines using Azure backup.</span></span> <span data-ttu-id="f7231-173">.</span><span class="sxs-lookup"><span data-stu-id="f7231-173">.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f7231-174">Fazer backup de máquinas virtuais do Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="f7231-174">Back up Windows virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
