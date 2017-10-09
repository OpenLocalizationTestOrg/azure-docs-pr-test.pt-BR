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
# <a name="create-a-windows-virtual-machine-with-powershell"></a>Aprenda rapidamente a criar máquinas virtuais Windows com o PowerShell

módulo do PowerShell do Azure Olá é usado toocreate e gerenciar recursos do Azure, na linha de comando do PowerShell hello, ou em scripts. Esses detalhes de guia usando o PowerShell toocreate e a máquina virtual do Azure executando o Windows Server 2016. Depois que a implantação for concluída, vamos conectar toohello servidor e instale o IIS.  

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

Este guia rápido requer hello Azure PowerShell versão 3.6 ou posterior do módulo. Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).

## <a name="log-in-tooazure"></a>Faça logon no tooAzure

Fazer logon no tooyour assinatura do Azure com hello `Login-AzureRmAccount` de comando e siga o hello instruções na tela.

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a>Criar grupo de recursos

Crie um grupo de recursos do Azure com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Um grupo de recursos é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados. 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a>Criar recursos de rede

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a>Crie uma rede virtual, sub-rede e um endereço IP público. 
Esses recursos são usados tooprovide rede conectividade toohello VM e conectá-lo toohello internet.

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

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a>Crie um grupo de segurança de rede e uma regra de grupo de segurança de rede. 
grupo de segurança de rede Olá protege máquina virtual de saudação usando regras de entrada e saídas. Nesse caso, uma regra de entrada é criada para a porta 3389, que permite conexões de área de trabalho remota. Também gostaríamos de toocreate uma regra de entrada para a porta 80, que permite o tráfego de entrada da web.

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

### <a name="create-a-network-card-for-hello-virtual-machine"></a>Crie uma placa de rede da máquina virtual de saudação. 
Criar uma placa de rede com [AzureRmNetworkInterface novo](/powershell/module/azurerm.network/new-azurermnetworkinterface) para a máquina virtual de saudação. placa de rede Olá conecta-se a sub-rede de tooa de máquina virtual hello, o grupo de segurança de rede e o endereço IP público.

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a>Criar máquina virtual

Crie uma configuração de máquina virtual. Essa configuração inclui configurações de saudação que são usadas ao implantar a máquina virtual de saudação como uma configuração de imagem, tamanho e autenticação de máquina virtual. Ao executar esta etapa, credenciais serão solicitadas de você. valores Hello inseridos são configurados como Olá nome e a senha para a máquina virtual de saudação.

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

Criar a máquina virtual Olá [AzureRmVM novo](/powershell/module/azurerm.compute/new-azurermvm).

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a>Conectar máquina toovirtual

Após a implantação de hello, crie uma conexão de área de trabalho remota com a máquina virtual de saudação.

Saudação de uso [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) tooreturn Olá endereço IP público da máquina virtual de saudação do comando. Anote esse endereço IP para tooit possa se conectar com a conectividade do navegador tootest web em uma etapa futura.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

A seguir Olá Use o comando toocreate uma sessão de área de trabalho remota com a máquina virtual de saudação. Substitua o endereço IP de saudação com hello *publicIPAddress* de sua máquina virtual. Quando solicitado, insira as credenciais de saudação usadas ao criar a máquina virtual de saudação.

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a>Instalar o IIS por meio do PowerShell

Agora que você fez no toohello VM do Azure, você pode usar uma única linha do PowerShell tooinstall IIS e permitir o tráfego da web do hello firewall local regra tooallow. Abra um prompt do PowerShell e execute Olá comando a seguir:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a>Olá exibir página de boas-vindas do IIS

Com o IIS instalado e a porta 80 agora aberta na sua VM de saudação à Internet, você pode usar um navegador da web da sua página Bem-vindo do tooview choice saudação padrão IIS. Ser Olá-se de toouse *publicIpAddress* documentado acima da página do toovisit saudação padrão. 

![Site do IIS padrão](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>Limpar recursos

Quando não é mais necessário, você pode usar o hello [AzureRmResourceGroup remover](/powershell/module/azurerm.resources/remove-azurermresourcegroup) tooremove grupo de recursos de saudação, a VM e relacionados com todos os recursos de comando.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a>Próximas etapas

Neste início rápido, você implantou uma máquina virtual simples, uma regra de grupo de segurança de rede e instalou um servidor Web. toolearn mais sobre máquinas virtuais do Azure, continuar toohello tutorial para VMs do Windows.

> [!div class="nextstepaction"]
> [Tutoriais de máquina virtual do Windows Azure](./tutorial-manage-vm.md)
