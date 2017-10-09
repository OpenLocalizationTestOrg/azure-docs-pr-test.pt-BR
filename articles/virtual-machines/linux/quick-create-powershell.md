---
title: "aaaAzure início rápido - criar VM PowerShell | Microsoft Docs"
description: "Aprenda rapidamente toocreate um máquinas virtuais do Linux com o PowerShell"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: f05ea7fedafe4fda660dc6084ae57ebf9dced473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-powershell"></a><span data-ttu-id="0b8a9-103">Aprenda rapidamente a criar máquinas virtuais Linux com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b8a9-103">Create a Linux virtual machine with PowerShell</span></span>

<span data-ttu-id="0b8a9-104">módulo do PowerShell do Azure Olá é usado toocreate e gerenciar recursos do Azure, na linha de comando do PowerShell hello, ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-104">hello Azure PowerShell module is used toocreate and manage Azure resources from hello PowerShell command line or in scripts.</span></span> <span data-ttu-id="0b8a9-105">Esses detalhes de guia usando hello Azure PowerShell módulo toodeploy uma máquina virtual com o servidor do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-105">This guide details using hello Azure PowerShell module toodeploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="0b8a9-106">Depois que o servidor de saudação for implantado, é criada uma conexão SSH e um servidor de Web NGINX está instalado.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-106">Once hello server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="0b8a9-107">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="0b8a9-108">Este guia rápido requer hello Azure PowerShell versão 3.6 ou posterior do módulo.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-108">This quick start requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="0b8a9-109">Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="0b8a9-110">Se você precisar tooinstall ou atualização, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="0b8a9-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="0b8a9-111">Por fim, uma chave SSH pública com o nome da saudação *id_rsa.pub* precisa toobe armazenado em Olá *.ssh* diretório do seu perfil de usuário do Windows.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-111">Finally, a public SSH key with hello name *id_rsa.pub* needs toobe stored in hello *.ssh* directory of your Windows user profile.</span></span> <span data-ttu-id="0b8a9-112">Para obter informações detalhadas sobre a criação de chaves SSH para o Azure, consulte [Criar chaves SSH do Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0b8a9-112">For detailed information on creating SSH keys for Azure, see [Create SSH keys for Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="0b8a9-113">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="0b8a9-113">Log in tooAzure</span></span>

<span data-ttu-id="0b8a9-114">Fazer logon no tooyour assinatura do Azure com hello `Login-AzureRmAccount` de comando e siga o hello instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-114">Log in tooyour Azure subscription with hello `Login-AzureRmAccount` command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="0b8a9-115">Criar grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="0b8a9-115">Create resource group</span></span>

<span data-ttu-id="0b8a9-116">Crie um grupo de recursos do Azure com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="0b8a9-116">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="0b8a9-117">Um grupo de recursos é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-117">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a><span data-ttu-id="0b8a9-118">Criar recursos de rede</span><span class="sxs-lookup"><span data-stu-id="0b8a9-118">Create networking resources</span></span>

<span data-ttu-id="0b8a9-119">Crie uma rede virtual, sub-rede e um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-119">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="0b8a9-120">Esses recursos são usados tooprovide rede conectividade toohello VM e conectá-lo toohello internet.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-120">These resources are used tooprovide network connectivity toohello virtual machine and connect it toohello internet.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location eastus `
-Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location eastus `
-AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

<span data-ttu-id="0b8a9-121">Crie um grupo de segurança de rede e uma regra de grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-121">Create a network security group and a network security group rule.</span></span> <span data-ttu-id="0b8a9-122">grupo de segurança de rede Olá protege máquina virtual de saudação usando regras de entrada e saídas.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-122">hello network security group secures hello virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="0b8a9-123">Nesse caso, uma regra de entrada é criada para a porta 22, que permite conexões SSH.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-123">In this case, an inbound rule is created for port 22, which allows incoming SSH connections.</span></span> <span data-ttu-id="0b8a9-124">Também gostaríamos de toocreate uma regra de entrada para a porta 80, que permite o tráfego de entrada da web.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-124">We also want toocreate an inbound rule for port 80, which allows incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 22
$nsgRuleSSH = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleSSH  -Protocol Tcp `
-Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 22 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
-Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location eastus `
-Name myNetworkSecurityGroup -SecurityRules $nsgRuleSSH,$nsgRuleWeb
```

<span data-ttu-id="0b8a9-125">Criar uma placa de rede com [AzureRmNetworkInterface novo](/powershell/module/azurerm.network/new-azurermnetworkinterface) para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-125">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for hello virtual machine.</span></span> <span data-ttu-id="0b8a9-126">placa de rede Olá conecta-se a sub-rede de tooa de máquina virtual hello, o grupo de segurança de rede e o endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-126">hello network card connects hello virtual machine tooa subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="0b8a9-127">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0b8a9-127">Create virtual machine</span></span>

<span data-ttu-id="0b8a9-128">Crie uma configuração de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-128">Create a virtual machine configuration.</span></span> <span data-ttu-id="0b8a9-129">Essa configuração inclui configurações de saudação que são usadas ao implantar a máquina virtual de saudação como uma configuração de imagem, tamanho e autenticação de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-129">This configuration includes hello settings that are used when deploying hello virtual machine such as a virtual machine image, size, and authentication configuration.</span></span>

```powershell
# Define a credential object
$securePassword = ConvertTo-SecureString ' ' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ("azureuser", $securePassword)

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Linux -ComputerName myVM -Credential $cred -DisablePasswordAuthentication | `
Set-AzureRmVMSourceImage -PublisherName Canonical -Offer UbuntuServer -Skus 14.04.2-LTS -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Configure SSH Keys
$sshPublicKey = Get-Content "$env:USERPROFILE\.ssh\id_rsa.pub"
Add-AzureRmVMSshPublicKey -VM $vmconfig -KeyData $sshPublicKey -Path "/home/azureuser/.ssh/authorized_keys"
```

<span data-ttu-id="0b8a9-130">Criar a máquina virtual Olá [AzureRmVM novo](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="0b8a9-130">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a><span data-ttu-id="0b8a9-131">Conectar máquina toovirtual</span><span class="sxs-lookup"><span data-stu-id="0b8a9-131">Connect toovirtual machine</span></span>

<span data-ttu-id="0b8a9-132">Após a implantação de Olá, crie uma conexão SSH com máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-132">After hello deployment has completed, create an SSH connection with hello virtual machine.</span></span>

<span data-ttu-id="0b8a9-133">Saudação de uso [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) tooreturn Olá endereço IP público da máquina virtual de saudação do comando.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-133">Use hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command tooreturn hello public IP address of hello virtual machine.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="0b8a9-134">De um sistema com SSH instalado, tooconnect toohello virtual machine de comando a seguir Olá usado.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-134">From a system with SSH installed, used hello following command tooconnect toohello virtual machine.</span></span> <span data-ttu-id="0b8a9-135">Se o trabalho no Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) pode ser usado toocreate Olá conexão.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-135">If working on Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) can be used toocreate hello connection.</span></span> 

```bash 
ssh <Public IP Address>
```

<span data-ttu-id="0b8a9-136">Quando solicitado, o nome de usuário de logon de saudação é *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-136">When prompted, hello login user name is *azureuser*.</span></span> <span data-ttu-id="0b8a9-137">Se uma frase secreta foi inserida durante a criação de chaves SSH, será necessário tooenter nesse também.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-137">If a passphrase was entered when creating SSH keys, you need tooenter this as well.</span></span>


## <a name="install-nginx"></a><span data-ttu-id="0b8a9-138">Instalar o NGINX</span><span class="sxs-lookup"><span data-stu-id="0b8a9-138">Install NGINX</span></span>

<span data-ttu-id="0b8a9-139">Use a seguir de saudação bash origens do pacote do script tooupdate e instala pacote NGINX mais recente de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-139">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-ngix-welcome-page"></a><span data-ttu-id="0b8a9-140">Página de boas-vindas do modo de exibição Olá NGIX</span><span class="sxs-lookup"><span data-stu-id="0b8a9-140">View hello NGIX welcome page</span></span>

<span data-ttu-id="0b8a9-141">Com NGINX instalado e a porta 80 agora aberta na sua VM do hello Internet - você pode usar um navegador da web da sua página Bem-vindo escolha tooview saudação padrão NGINX.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-141">With NGINX installed and port 80 now open on your VM from hello Internet - you can use a web browser of your choice tooview hello default NGINX welcome page.</span></span> <span data-ttu-id="0b8a9-142">Ser se toouse Olá endereço IP público documentado acima da página do toovisit saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-142">Be sure toouse hello public IP address you documented above toovisit hello default page.</span></span> 

![Site padrão NGINX](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="0b8a9-144">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="0b8a9-144">Clean up resources</span></span>

<span data-ttu-id="0b8a9-145">Quando não é mais necessário, você pode usar o hello [AzureRmResourceGroup remover](/powershell/module/azurerm.resources/remove-azurermresourcegroup) tooremove grupo de recursos de saudação, a VM e relacionados com todos os recursos de comando.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-145">When no longer needed, you can use hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="0b8a9-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0b8a9-146">Next steps</span></span>

<span data-ttu-id="0b8a9-147">Neste início rápido, você implantou uma máquina virtual simples, uma regra de grupo de segurança de rede e instalou um servidor Web.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-147">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="0b8a9-148">toolearn mais sobre máquinas virtuais do Azure, continuar toohello tutorial para VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="0b8a9-148">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0b8a9-149">Tutoriais de máquina virtual do Linux Azure</span><span class="sxs-lookup"><span data-stu-id="0b8a9-149">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
