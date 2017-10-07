---
title: aaaCustomize uma VM do Windows Azure | Microsoft Docs
description: "Saiba como toouse Olá extensão do script personalizado e o Cofre de chaves toocustomize VMs do Windows no Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c03b2bb6d70875134c63ea2fe4c2e2c1777c2188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="8a477-103">Como toocustomize uma máquina virtual do Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="8a477-103">How toocustomize a Windows virtual machine in Azure</span></span>
<span data-ttu-id="8a477-104">tooconfigure (máquinas virtuais) de uma maneira rápida e consistente, alguma forma de automação geralmente é desejado.</span><span class="sxs-lookup"><span data-stu-id="8a477-104">tooconfigure virtual machines (VMs) in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="8a477-105">Um toocustomize de abordagem comum uma VM do Windows é toouse [extensão para janelas de Script personalizado](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="8a477-105">A common approach toocustomize a Windows VM is toouse [Custom Script Extension for Windows](extensions-customscript.md).</span></span> <span data-ttu-id="8a477-106">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="8a477-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8a477-107">Usar tooinstall de extensão de Script personalizado Olá IIS</span><span class="sxs-lookup"><span data-stu-id="8a477-107">Use hello Custom Script Extension tooinstall IIS</span></span>
> * <span data-ttu-id="8a477-108">Criar uma VM que utilize Olá extensão de Script personalizado</span><span class="sxs-lookup"><span data-stu-id="8a477-108">Create a VM that uses hello Custom Script Extension</span></span>
> * <span data-ttu-id="8a477-109">Exibir um site do IIS em execução depois que a extensão de saudação é aplicado</span><span class="sxs-lookup"><span data-stu-id="8a477-109">View a running IIS site after hello extension is applied</span></span>

<span data-ttu-id="8a477-110">Este tutorial requer hello Azure PowerShell versão 3.6 ou posterior do módulo.</span><span class="sxs-lookup"><span data-stu-id="8a477-110">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="8a477-111">Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="8a477-111">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="8a477-112">Se você precisar tooupgrade, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="8a477-112">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="custom-script-extension-overview"></a><span data-ttu-id="8a477-113">Visão geral da extensão de script personalizado</span><span class="sxs-lookup"><span data-stu-id="8a477-113">Custom script extension overview</span></span>
<span data-ttu-id="8a477-114">Olá extensão de Script personalizado baixa e executa scripts em VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="8a477-114">hello Custom Script Extension downloads and executes scripts on Azure VMs.</span></span> <span data-ttu-id="8a477-115">Essa extensão é útil para a configuração de implantação de postagem, instalação de software ou qualquer outra configuração/tarefa de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="8a477-115">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="8a477-116">Scripts podem ser baixados do armazenamento do Azure ou GitHub ou fornecidos toohello portal do Azure em tempo de execução de extensão.</span><span class="sxs-lookup"><span data-stu-id="8a477-116">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span>

<span data-ttu-id="8a477-117">Olá extensão de Script personalizado se integra com os modelos do Gerenciador de recursos do Azure e também pode ser executado usando Olá CLI do Azure, o PowerShell, o portal do Azure ou Olá API de REST de máquina Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="8a477-117">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="8a477-118">Você pode usar o hello extensão de Script personalizado com o Windows e VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="8a477-118">You can use hello Custom Script Extension with both Windows and Linux VMs.</span></span>


## <a name="create-virtual-machine"></a><span data-ttu-id="8a477-119">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8a477-119">Create virtual machine</span></span>
<span data-ttu-id="8a477-120">Antes de criar uma VM, crie um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="8a477-120">Before you can create a VM, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="8a477-121">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroupAutomate* em Olá *EastUS* local:</span><span class="sxs-lookup"><span data-stu-id="8a477-121">hello following example creates a resource group named *myResourceGroupAutomate* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupAutomate -Location EastUS
```

<span data-ttu-id="8a477-122">Definir um administrador de nome de usuário e senha para Olá VMs com [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="8a477-122">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="8a477-123">Agora você pode criar hello VM com [AzureRmVM novo](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="8a477-123">Now you can create hello VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="8a477-124">Olá exemplo a seguir cria componentes de rede virtual Olá necessários, configuração Olá sistema operacional e, em seguida, cria uma VM denominada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="8a477-124">hello following example creates hello required virtual network components, hello OS configuration, and then creates a VM named *myVM*:</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName myResourceGroupAutomate -Location EastUS -VM $vmConfig
```

<span data-ttu-id="8a477-125">Leva alguns minutos para recursos de saudação e toobe VM criada.</span><span class="sxs-lookup"><span data-stu-id="8a477-125">It takes a few minutes for hello resources and VM toobe created.</span></span>


## <a name="automate-iis-install"></a><span data-ttu-id="8a477-126">Automatizar a instalação do IIS</span><span class="sxs-lookup"><span data-stu-id="8a477-126">Automate IIS install</span></span>
<span data-ttu-id="8a477-127">Use [AzureRmVMExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall Olá extensão de Script personalizado.</span><span class="sxs-lookup"><span data-stu-id="8a477-127">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Custom Script Extension.</span></span> <span data-ttu-id="8a477-128">Olá execuções de extensão `powershell Add-WindowsFeature Web-Server` tooinstall Olá servidor Web do IIS e, em seguida, Olá atualizações *Default.htm* página tooshow Olá hostname de saudação VM:</span><span class="sxs-lookup"><span data-stu-id="8a477-128">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver and then updates hello *Default.htm* page tooshow hello hostname of hello VM:</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName myResourceGroupAutomate `
    -ExtensionName IIS `
    -VMName myVM `
    -Publisher Microsoft.Compute `
    -ExtensionType CustomScriptExtension `
    -TypeHandlerVersion 1.4 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
    -Location EastUS
```


## <a name="test-web-site"></a><span data-ttu-id="8a477-129">Testar o site</span><span class="sxs-lookup"><span data-stu-id="8a477-129">Test web site</span></span>
<span data-ttu-id="8a477-130">Obter o endereço IP público de saudação do balanceador de carga com [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="8a477-130">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="8a477-131">Olá, exemplo a seguir obtém endereço IP hello *myPublicIP* criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="8a477-131">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Name myPublicIP | select IpAddress
```

<span data-ttu-id="8a477-132">Você pode inserir o endereço IP público de saudação no navegador da web de tooa.</span><span class="sxs-lookup"><span data-stu-id="8a477-132">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="8a477-133">Olá site é exibido, incluindo o nome de host de saudação do hello VM balanceador de carga que Olá distribuído tooas de tráfego em Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="8a477-133">hello website is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Site do IIS em execução](./media/tutorial-automate-vm-deployment/running-iis-website.png)


## <a name="next-steps"></a><span data-ttu-id="8a477-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8a477-135">Next steps</span></span>

<span data-ttu-id="8a477-136">Neste tutorial, você automatizada hello instalar o IIS em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8a477-136">In this tutorial, you automated hello IIS install on a VM.</span></span> <span data-ttu-id="8a477-137">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="8a477-137">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8a477-138">Usar tooinstall de extensão de Script personalizado Olá IIS</span><span class="sxs-lookup"><span data-stu-id="8a477-138">Use hello Custom Script Extension tooinstall IIS</span></span>
> * <span data-ttu-id="8a477-139">Criar uma VM que utilize Olá extensão de Script personalizado</span><span class="sxs-lookup"><span data-stu-id="8a477-139">Create a VM that uses hello Custom Script Extension</span></span>
> * <span data-ttu-id="8a477-140">Exibir um site do IIS em execução depois que a extensão de saudação é aplicado</span><span class="sxs-lookup"><span data-stu-id="8a477-140">View a running IIS site after hello extension is applied</span></span>

<span data-ttu-id="8a477-141">Avançar toohello toolearn de tutorial Avançar como imagens VM personalizadas toocreate.</span><span class="sxs-lookup"><span data-stu-id="8a477-141">Advance toohello next tutorial toolearn how toocreate custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8a477-142">Criar imagens de VM personalizada</span><span class="sxs-lookup"><span data-stu-id="8a477-142">Create custom VM images</span></span>](./tutorial-custom-images.md)
