---
title: "Início Rápido do Azure – Criar PowerShell da VM do Windows | Microsoft Docs"
description: "Aprenda rapidamente criar máquinas virtuais Windows com o PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 8516cfa2272694496eb353a83eca77c13a516750
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell"></a><span data-ttu-id="750c4-103">Aprenda rapidamente a criar máquinas virtuais Windows com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="750c4-103">Create a Windows virtual machine with PowerShell</span></span>

<span data-ttu-id="750c4-104">O módulo do Azure PowerShell é usado para criar e gerenciar recursos do Azure da linha de comando do PowerShell ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="750c4-104">The Azure PowerShell module is used to create and manage Azure resources from the PowerShell command line or in scripts.</span></span> <span data-ttu-id="750c4-105">Este guia detalha o uso do PowerShell para criar uma máquina virtual do Azure executando Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="750c4-105">This guide details using PowerShell to create and Azure virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="750c4-106">Depois que a implantação for concluída, nos conectamos ao servidor e instalamos o IIS.</span><span class="sxs-lookup"><span data-stu-id="750c4-106">Once deployment is complete, we connect to the server and install IIS.</span></span>  

<span data-ttu-id="750c4-107">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="750c4-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="750c4-108">Este início rápido requer o módulo Azure PowerShell versão 3.6 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="750c4-108">This quick start requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="750c4-109">Execute ` Get-Module -ListAvailable AzureRM` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="750c4-109">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="750c4-110">Se você precisa instalar ou atualizar, confira [Instalar o módulo do Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="750c4-110">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="750c4-111">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="750c4-111">Log in to Azure</span></span>

<span data-ttu-id="750c4-112">Faça logon na sua assinatura do Azure com o comando `Login-AzureRmAccount` e siga as instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="750c4-112">Log in to your Azure subscription with the `Login-AzureRmAccount` command and follow the on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="750c4-113">Criar grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="750c4-113">Create resource group</span></span>

<span data-ttu-id="750c4-114">Crie um grupo de recursos do Azure com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="750c4-114">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="750c4-115">Um grupo de recursos é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="750c4-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a><span data-ttu-id="750c4-116">Criar recursos de rede</span><span class="sxs-lookup"><span data-stu-id="750c4-116">Create networking resources</span></span>

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a><span data-ttu-id="750c4-117">Crie uma rede virtual, sub-rede e um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="750c4-117">Create a virtual network, subnet, and a public IP address.</span></span> 
<span data-ttu-id="750c4-118">Esses recursos são usados para fornecer conectividade de rede para a máquina virtual e conectá-la à Internet.</span><span class="sxs-lookup"><span data-stu-id="750c4-118">These resources are used to provide network connectivity to the virtual machine and connect it to the internet.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location EastUS `
    -Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location EastUS `
    -AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a><span data-ttu-id="750c4-119">Crie um grupo de segurança de rede e uma regra de grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="750c4-119">Create a network security group and a network security group rule.</span></span> 
<span data-ttu-id="750c4-120">O grupo de segurança de rede protege a máquina virtual usando regras de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="750c4-120">The network security group secures the virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="750c4-121">Nesse caso, uma regra de entrada é criada para a porta 3389, que permite conexões de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="750c4-121">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span> <span data-ttu-id="750c4-122">Também queremos criar uma regra de entrada para a porta 80, que permite o tráfego de entrada da Web.</span><span class="sxs-lookup"><span data-stu-id="750c4-122">We also want to create an inbound rule for port 80, which allows incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP  -Protocol Tcp `
    -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
    -Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location EastUS `
    -Name myNetworkSecurityGroup -SecurityRules $nsgRuleRDP,$nsgRuleWeb
```

### <a name="create-a-network-card-for-the-virtual-machine"></a><span data-ttu-id="750c4-123">Criar uma placa de rede para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="750c4-123">Create a network card for the virtual machine.</span></span> 
<span data-ttu-id="750c4-124">Crie uma placa de rede com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="750c4-124">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for the virtual machine.</span></span> <span data-ttu-id="750c4-125">A placa de rede conecta a máquina virtual a uma sub-rede, um grupo de segurança de rede e um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="750c4-125">The network card connects the virtual machine to a subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="750c4-126">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="750c4-126">Create virtual machine</span></span>

<span data-ttu-id="750c4-127">Crie uma configuração de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="750c4-127">Create a virtual machine configuration.</span></span> <span data-ttu-id="750c4-128">Essa configuração inclui as configurações que são usadas ao implantar a máquina virtual como uma imagem, tamanho e configuração de autenticação de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="750c4-128">This configuration includes the settings that are used when deploying the virtual machine such as a virtual machine image, size, and authentication configuration.</span></span> <span data-ttu-id="750c4-129">Ao executar esta etapa, credenciais serão solicitadas de você.</span><span class="sxs-lookup"><span data-stu-id="750c4-129">When running this step, you are prompted for credentials.</span></span> <span data-ttu-id="750c4-130">Os valores que você insere são configurados como o nome de usuário e senha para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="750c4-130">The values that you enter are configured as the user name and password for the virtual machine.</span></span>

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

<span data-ttu-id="750c4-131">Crie a máquina virtual com [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="750c4-131">Create the virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-to-virtual-machine"></a><span data-ttu-id="750c4-132">Conectar-se à máquina virtual</span><span class="sxs-lookup"><span data-stu-id="750c4-132">Connect to virtual machine</span></span>

<span data-ttu-id="750c4-133">Após a implantação, crie uma conexão de área de trabalho remota com a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="750c4-133">After the deployment has completed, create a remote desktop connection with the virtual machine.</span></span>

<span data-ttu-id="750c4-134">Utilize o comando [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) para retornar o endereço IP público da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="750c4-134">Use the [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command to return the public IP address of the virtual machine.</span></span> <span data-ttu-id="750c4-135">Anote esse endereço IP para se conectar a ele com o navegador para testar a conectividade à Web em uma etapa futura.</span><span class="sxs-lookup"><span data-stu-id="750c4-135">Take note of this IP Address so you can connect to it with your browser to test web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="750c4-136">Use o seguinte comando para criar uma sessão de área de trabalho remota com a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="750c4-136">Use the following command to create a remote desktop session with the virtual machine.</span></span> <span data-ttu-id="750c4-137">Substitua o endereço IP pelo *publicIPAdress* da sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="750c4-137">Replace the IP address with the *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="750c4-138">Quando solicitado, insira as credenciais usadas ao criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="750c4-138">When prompted, enter the credentials used when creating the virtual machine.</span></span>

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a><span data-ttu-id="750c4-139">Instalar o IIS por meio do PowerShell</span><span class="sxs-lookup"><span data-stu-id="750c4-139">Install IIS via PowerShell</span></span>

<span data-ttu-id="750c4-140">Agora que você fez logon na VM do Azure, pode usar uma única linha do PowerShell para instalar o IIS e habilitar a regra de firewall local para permitir o tráfego da Web.</span><span class="sxs-lookup"><span data-stu-id="750c4-140">Now that you have logged in to the Azure VM, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span></span> <span data-ttu-id="750c4-141">Abra um promt do PowerShell e execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="750c4-141">Open a PowerShell prompt and run the following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="750c4-142">Exibir a página de boas-vindas do IIS</span><span class="sxs-lookup"><span data-stu-id="750c4-142">View the IIS welcome page</span></span>

<span data-ttu-id="750c4-143">Com o IIS instalado e a porta 80 que agora está aberta na sua VM da Internet, você pode usar um navegador da Web de sua escolha para exibir a página de boas-vindas do IIS padrão.</span><span class="sxs-lookup"><span data-stu-id="750c4-143">With IIS installed and port 80 now open on your VM from the Internet, you can use a web browser of your choice to view the default IIS welcome page.</span></span> <span data-ttu-id="750c4-144">Certifique-se de usar o *publicIPAdress* que você documentou acima para visitar a página padrão.</span><span class="sxs-lookup"><span data-stu-id="750c4-144">Be sure to use the *publicIpAddress* you documented above to visit the default page.</span></span> 

![Site do IIS padrão](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="750c4-146">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="750c4-146">Clean up resources</span></span>

<span data-ttu-id="750c4-147">Quando não for mais necessário, você pode usar o comando [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="750c4-147">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="750c4-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="750c4-148">Next steps</span></span>

<span data-ttu-id="750c4-149">Neste início rápido, você implantou uma máquina virtual simples, uma regra de grupo de segurança de rede e instalou um servidor Web.</span><span class="sxs-lookup"><span data-stu-id="750c4-149">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="750c4-150">Para saber mais sobre máquinas virtuais do Azure, continue o tutorial para VMs do Windows.</span><span class="sxs-lookup"><span data-stu-id="750c4-150">To learn more about Azure virtual machines, continue to the tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="750c4-151">Tutoriais de máquina virtual do Windows Azure</span><span class="sxs-lookup"><span data-stu-id="750c4-151">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
