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
# <a name="create-a-linux-virtual-machine-with-powershell"></a>Aprenda rapidamente a criar máquinas virtuais Linux com o PowerShell

módulo do PowerShell do Azure Olá é usado toocreate e gerenciar recursos do Azure, na linha de comando do PowerShell hello, ou em scripts. Esses detalhes de guia usando hello Azure PowerShell módulo toodeploy uma máquina virtual com o servidor do Ubuntu. Depois que o servidor de saudação for implantado, é criada uma conexão SSH e um servidor de Web NGINX está instalado.

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

Este guia rápido requer hello Azure PowerShell versão 3.6 ou posterior do módulo. Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).

Por fim, uma chave SSH pública com o nome da saudação *id_rsa.pub* precisa toobe armazenado em Olá *.ssh* diretório do seu perfil de usuário do Windows. Para obter informações detalhadas sobre a criação de chaves SSH para o Azure, consulte [Criar chaves SSH do Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="log-in-tooazure"></a>Faça logon no tooAzure

Fazer logon no tooyour assinatura do Azure com hello `Login-AzureRmAccount` de comando e siga o hello instruções na tela.

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a>Criar grupo de recursos

Crie um grupo de recursos do Azure com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Um grupo de recursos é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados. 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a>Criar recursos de rede

Crie uma rede virtual, sub-rede e um endereço IP público. Esses recursos são usados tooprovide rede conectividade toohello VM e conectá-lo toohello internet.

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

Crie um grupo de segurança de rede e uma regra de grupo de segurança de rede. grupo de segurança de rede Olá protege máquina virtual de saudação usando regras de entrada e saídas. Nesse caso, uma regra de entrada é criada para a porta 22, que permite conexões SSH. Também gostaríamos de toocreate uma regra de entrada para a porta 80, que permite o tráfego de entrada da web.

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

Criar uma placa de rede com [AzureRmNetworkInterface novo](/powershell/module/azurerm.network/new-azurermnetworkinterface) para a máquina virtual de saudação. placa de rede Olá conecta-se a sub-rede de tooa de máquina virtual hello, o grupo de segurança de rede e o endereço IP público.

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a>Criar máquina virtual

Crie uma configuração de máquina virtual. Essa configuração inclui configurações de saudação que são usadas ao implantar a máquina virtual de saudação como uma configuração de imagem, tamanho e autenticação de máquina virtual.

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

Criar a máquina virtual Olá [AzureRmVM novo](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a>Conectar máquina toovirtual

Após a implantação de Olá, crie uma conexão SSH com máquina virtual de saudação.

Saudação de uso [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) tooreturn Olá endereço IP público da máquina virtual de saudação do comando.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

De um sistema com SSH instalado, tooconnect toohello virtual machine de comando a seguir Olá usado. Se o trabalho no Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) pode ser usado toocreate Olá conexão. 

```bash 
ssh <Public IP Address>
```

Quando solicitado, o nome de usuário de logon de saudação é *azureuser*. Se uma frase secreta foi inserida durante a criação de chaves SSH, será necessário tooenter nesse também.


## <a name="install-nginx"></a>Instalar o NGINX

Use a seguir de saudação bash origens do pacote do script tooupdate e instala pacote NGINX mais recente de saudação. 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-ngix-welcome-page"></a>Página de boas-vindas do modo de exibição Olá NGIX

Com NGINX instalado e a porta 80 agora aberta na sua VM do hello Internet - você pode usar um navegador da web da sua página Bem-vindo escolha tooview saudação padrão NGINX. Ser se toouse Olá endereço IP público documentado acima da página do toovisit saudação padrão. 

![Site padrão NGINX](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a>Limpar recursos

Quando não é mais necessário, você pode usar o hello [AzureRmResourceGroup remover](/powershell/module/azurerm.resources/remove-azurermresourcegroup) tooremove grupo de recursos de saudação, a VM e relacionados com todos os recursos de comando.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a>Próximas etapas

Neste início rápido, você implantou uma máquina virtual simples, uma regra de grupo de segurança de rede e instalou um servidor Web. toolearn mais sobre máquinas virtuais do Azure, continuar toohello tutorial para VMs do Linux.

> [!div class="nextstepaction"]
> [Tutoriais de máquina virtual do Linux Azure](./tutorial-manage-vm.md)
