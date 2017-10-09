---
title: "aaaAzure início rápido - criar VM de Windows PowerShell | Microsoft Docs"
description: "Aprenda rapidamente toocreate um máquinas virtuais do Windows com o PowerShell"
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
ms.openlocfilehash: 5e92435bf7ee443a01c158fed91c356363e2f425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell"></a><span data-ttu-id="f7de5-103">Aprenda rapidamente a criar máquinas virtuais Windows com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7de5-103">Create a Windows virtual machine with PowerShell</span></span>

<span data-ttu-id="f7de5-104">módulo do PowerShell do Azure Olá é usado toocreate e gerenciar recursos do Azure, na linha de comando do PowerShell hello, ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="f7de5-104">hello Azure PowerShell module is used toocreate and manage Azure resources from hello PowerShell command line or in scripts.</span></span> <span data-ttu-id="f7de5-105">Esses detalhes de guia usando o PowerShell toocreate e a máquina virtual do Azure executando o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="f7de5-105">This guide details using PowerShell toocreate and Azure virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="f7de5-106">Depois que a implantação for concluída, vamos conectar toohello servidor e instale o IIS.</span><span class="sxs-lookup"><span data-stu-id="f7de5-106">Once deployment is complete, we connect toohello server and install IIS.</span></span>  

<span data-ttu-id="f7de5-107">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="f7de5-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="f7de5-108">Este guia rápido requer hello Azure PowerShell versão 3.6 ou posterior do módulo.</span><span class="sxs-lookup"><span data-stu-id="f7de5-108">This quick start requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="f7de5-109">Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7de5-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="f7de5-110">Se você precisar tooinstall ou atualização, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="f7de5-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="f7de5-111">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="f7de5-111">Log in tooAzure</span></span>

<span data-ttu-id="f7de5-112">Fazer logon no tooyour assinatura do Azure com hello `Login-AzureRmAccount` de comando e siga o hello instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="f7de5-112">Log in tooyour Azure subscription with hello `Login-AzureRmAccount` command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="f7de5-113">Criar grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f7de5-113">Create resource group</span></span>

<span data-ttu-id="f7de5-114">Crie um grupo de recursos do Azure com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="f7de5-114">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="f7de5-115">Um grupo de recursos é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="f7de5-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a><span data-ttu-id="f7de5-116">Criar recursos de rede</span><span class="sxs-lookup"><span data-stu-id="f7de5-116">Create networking resources</span></span>

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a><span data-ttu-id="f7de5-117">Crie uma rede virtual, sub-rede e um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="f7de5-117">Create a virtual network, subnet, and a public IP address.</span></span> 
<span data-ttu-id="f7de5-118">Esses recursos são usados tooprovide rede conectividade toohello VM e conectá-lo toohello internet.</span><span class="sxs-lookup"><span data-stu-id="f7de5-118">These resources are used tooprovide network connectivity toohello virtual machine and connect it toohello internet.</span></span>

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

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a><span data-ttu-id="f7de5-119">Crie um grupo de segurança de rede e uma regra de grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="f7de5-119">Create a network security group and a network security group rule.</span></span> 
<span data-ttu-id="f7de5-120">grupo de segurança de rede Olá protege máquina virtual de saudação usando regras de entrada e saídas.</span><span class="sxs-lookup"><span data-stu-id="f7de5-120">hello network security group secures hello virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="f7de5-121">Nesse caso, uma regra de entrada é criada para a porta 3389, que permite conexões de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="f7de5-121">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span> <span data-ttu-id="f7de5-122">Também gostaríamos de toocreate uma regra de entrada para a porta 80, que permite o tráfego de entrada da web.</span><span class="sxs-lookup"><span data-stu-id="f7de5-122">We also want toocreate an inbound rule for port 80, which allows incoming web traffic.</span></span>

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

### <a name="create-a-network-card-for-hello-virtual-machine"></a><span data-ttu-id="f7de5-123">Crie uma placa de rede da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7de5-123">Create a network card for hello virtual machine.</span></span> 
<span data-ttu-id="f7de5-124">Criar uma placa de rede com [AzureRmNetworkInterface novo](/powershell/module/azurerm.network/new-azurermnetworkinterface) para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7de5-124">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for hello virtual machine.</span></span> <span data-ttu-id="f7de5-125">placa de rede Olá conecta-se a sub-rede de tooa de máquina virtual hello, o grupo de segurança de rede e o endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="f7de5-125">hello network card connects hello virtual machine tooa subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="f7de5-126">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="f7de5-126">Create virtual machine</span></span>

<span data-ttu-id="f7de5-127">Crie uma configuração de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f7de5-127">Create a virtual machine configuration.</span></span> <span data-ttu-id="f7de5-128">Essa configuração inclui configurações de saudação que são usadas ao implantar a máquina virtual de saudação como uma configuração de imagem, tamanho e autenticação de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f7de5-128">This configuration includes hello settings that are used when deploying hello virtual machine such as a virtual machine image, size, and authentication configuration.</span></span> <span data-ttu-id="f7de5-129">Ao executar esta etapa, credenciais serão solicitadas de você.</span><span class="sxs-lookup"><span data-stu-id="f7de5-129">When running this step, you are prompted for credentials.</span></span> <span data-ttu-id="f7de5-130">valores Hello inseridos são configurados como Olá nome e a senha para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7de5-130">hello values that you enter are configured as hello user name and password for hello virtual machine.</span></span>

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

<span data-ttu-id="f7de5-131">Criar a máquina virtual Olá [AzureRmVM novo](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="f7de5-131">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a><span data-ttu-id="f7de5-132">Conectar máquina toovirtual</span><span class="sxs-lookup"><span data-stu-id="f7de5-132">Connect toovirtual machine</span></span>

<span data-ttu-id="f7de5-133">Após a implantação de hello, crie uma conexão de área de trabalho remota com a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7de5-133">After hello deployment has completed, create a remote desktop connection with hello virtual machine.</span></span>

<span data-ttu-id="f7de5-134">Saudação de uso [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) tooreturn Olá endereço IP público da máquina virtual de saudação do comando.</span><span class="sxs-lookup"><span data-stu-id="f7de5-134">Use hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command tooreturn hello public IP address of hello virtual machine.</span></span> <span data-ttu-id="f7de5-135">Anote esse endereço IP para tooit possa se conectar com a conectividade do navegador tootest web em uma etapa futura.</span><span class="sxs-lookup"><span data-stu-id="f7de5-135">Take note of this IP Address so you can connect tooit with your browser tootest web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="f7de5-136">A seguir Olá Use o comando toocreate uma sessão de área de trabalho remota com a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7de5-136">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="f7de5-137">Substitua o endereço IP de saudação com hello *publicIPAddress* de sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f7de5-137">Replace hello IP address with hello *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="f7de5-138">Quando solicitado, insira as credenciais de saudação usadas ao criar a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7de5-138">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a><span data-ttu-id="f7de5-139">Instalar o IIS por meio do PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7de5-139">Install IIS via PowerShell</span></span>

<span data-ttu-id="f7de5-140">Agora que você fez no toohello VM do Azure, você pode usar uma única linha do PowerShell tooinstall IIS e permitir o tráfego da web do hello firewall local regra tooallow.</span><span class="sxs-lookup"><span data-stu-id="f7de5-140">Now that you have logged in toohello Azure VM, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="f7de5-141">Abra um prompt do PowerShell e execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7de5-141">Open a PowerShell prompt and run hello following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="f7de5-142">Olá exibir página de boas-vindas do IIS</span><span class="sxs-lookup"><span data-stu-id="f7de5-142">View hello IIS welcome page</span></span>

<span data-ttu-id="f7de5-143">Com o IIS instalado e a porta 80 agora aberta na sua VM de saudação à Internet, você pode usar um navegador da web da sua página Bem-vindo do tooview choice saudação padrão IIS.</span><span class="sxs-lookup"><span data-stu-id="f7de5-143">With IIS installed and port 80 now open on your VM from hello Internet, you can use a web browser of your choice tooview hello default IIS welcome page.</span></span> <span data-ttu-id="f7de5-144">Ser Olá-se de toouse *publicIpAddress* documentado acima da página do toovisit saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="f7de5-144">Be sure toouse hello *publicIpAddress* you documented above toovisit hello default page.</span></span> 

![Site do IIS padrão](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="f7de5-146">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="f7de5-146">Clean up resources</span></span>

<span data-ttu-id="f7de5-147">Quando não é mais necessário, você pode usar o hello [AzureRmResourceGroup remover](/powershell/module/azurerm.resources/remove-azurermresourcegroup) tooremove grupo de recursos de saudação, a VM e relacionados com todos os recursos de comando.</span><span class="sxs-lookup"><span data-stu-id="f7de5-147">When no longer needed, you can use hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="f7de5-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f7de5-148">Next steps</span></span>

<span data-ttu-id="f7de5-149">Neste início rápido, você implantou uma máquina virtual simples, uma regra de grupo de segurança de rede e instalou um servidor Web.</span><span class="sxs-lookup"><span data-stu-id="f7de5-149">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="f7de5-150">toolearn mais sobre máquinas virtuais do Azure, continuar toohello tutorial para VMs do Windows.</span><span class="sxs-lookup"><span data-stu-id="f7de5-150">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f7de5-151">Tutoriais de máquina virtual do Windows Azure</span><span class="sxs-lookup"><span data-stu-id="f7de5-151">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
