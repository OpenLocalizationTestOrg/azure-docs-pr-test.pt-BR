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
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a>Gerenciar redes virtuais do Azure e Máquinas Virtuais do Windows com o Azure PowerShell

As máquinas virtuais do Azure usam a rede do Azure para comunicação de rede interna e externa. Neste tutorial, você cria várias VMs (máquinas virtuais) em uma rede virtual e configura a conectividade de rede entre elas. Você aprenderá como:

> [!div class="checklist"]
> * Criar uma rede virtual
> * Criar sub-redes de rede virtual
> * Controle de tráfego de rede com grupos de segurança de rede
> * Exibir regras de tráfego em ação

Este tutorial requer hello Azure PowerShell versão 3.6 ou posterior do módulo. Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação. Se você precisar tooupgrade, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).

## <a name="create-vnet"></a>Criar VNet

Uma rede virtual é uma representação de sua própria rede na nuvem hello. Uma rede virtual é uma isolamento lógico de saudação nuvem do Azure dedicado tooyour assinatura. Em uma rede virtual, você encontrar sub-redes, regras para conectividade toothose sub-redes e conexões de sub-redes de toohello VMs hello.

Antes de criar todos os outros recursos do Azure, você precisa toocreate um grupo de recursos com [AzureRmResourceGroup novo](/powershell/module/azurerm.resources/new-azurermresourcegroup). Olá, exemplo a seguir cria um grupo de recursos denominado *myRGNetwork* em Olá *EastUS* local:

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

Uma sub-rede é um recurso filho de uma VNet e ajuda a definir segmentos de espaços de endereços em um bloco CIDR, usando prefixos de endereços IP. As NICs podem ser adicionadas toosubnets e tooVMs conectado, fornecendo conectividade para várias cargas de trabalho.

Crie uma sub-rede com [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

Crie uma rede virtual denominada *myVNet* usando *myFrontendSubnet* com [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a>Criar VM de front-end

Para toocommunicate uma VM em uma rede virtual, ele precisa de uma interface de rede virtual (NIC). Olá *myFrontendVM* são acessados de saudação à internet, para que ele também precisa de um endereço IP público. 

Crie um endereço IP público com [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

Crie uma NIC com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

Definir Olá nome de usuário e a senha necessários para a conta de administrador Olá Olá VM com [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Criar VMs Olá com [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [conjunto AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [AzureRmVMSourceImage conjunto](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [AzureRmVMNetworkInterface adicionar](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), e [AzureRmVM novo](/powershell/module/azurerm.compute/new-azurermvm). 

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

## <a name="install-web-server"></a>Instalar servidor Web

Você pode instalar o IIS em *myFrontendVM* usando uma sessão de área de trabalho remota. Necessário tooget Olá endereço IP público do hello VM tooaccess-lo.

Você pode obter o endereço IP público de saudação do *myFrontendVM* com [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Olá, exemplo a seguir obtém endereço IP hello *myPublicIPAddress* criado anteriormente:

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

Anote esse endereço IP para usá-lo em etapas futuras.

Toocreate uma sessão de área de trabalho remota com o comando a seguir de saudação de uso *myFrontendVM*. Substituir  *<publicIPAddress>*  com endereço Olá que você registrou anteriormente. Quando solicitado, insira as credenciais Olá usadas quando você criou Olá VM.

```
mstsc /v:<publicIpAddress>
``` 

Agora que você fez muito*myFrontendVM*, você pode usar uma única linha do PowerShell tooinstall IIS e permitir o tráfego da web do hello firewall local regra tooallow. Abra um prompt do PowerShell e execute Olá comando a seguir:

Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun extensão do script personalizado Olá que instala o servidor Web do IIS hello:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

Agora você pode usar o hello IP endereço toobrowse toohello VM toosee Olá IIS site público.

![Site do IIS padrão](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a>Gerenciar o tráfego interno

Um grupo de segurança de rede (NSG) contém uma lista de regras de segurança que permitem ou negam tooa de tooresources conectado de tráfego de rede rede virtual. Os NSGs podem ser associados toosubnets ou NICs individuais conectados tooVMs. Abrir ou fechar tooVMs acesso por meio de portas é feita usando as regras NSG. Quando você criou a *myFrontendVM*, a porta 3389 de entrada foi aberta automaticamente para conectividade RDP.

A comunicação interna de VMs pode ser configurada usando um NSG. Nesta seção, você aprenderá como toocreate uma sub-rede adicional na saudação de rede e atribuir um tooallow de tooit NSG uma conexão de *myFrontendVM* muito*myBackendVM* na porta 1433. subrede Olá é então atribuído toohello VM quando ela é criada.

Você pode limitar o tráfego interno muito*myBackendVM* de apenas *myFrontendVM* criando um NSG de sub-rede de back-end de saudação. Olá, exemplo a seguir cria uma regra NSG denominada *myBackendNSGRule* com [AzureRmNetworkSecurityRuleConfig novo](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):

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

Adicione um grupo de segurança de rede chamado *myBackendNSG* com [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a>Adicionar sub-rede back-end

Adicionar *myBackEndSubnet* muito*myVNet* com [adicionar AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):

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

## <a name="create-back-end-vm"></a>Criar VM back-end

Olá Olá toocreate da maneira mais fácil a VM de back-end está usando uma imagem do SQL Server. Este tutorial cria Olá VM com o servidor de banco de dados de saudação apenas, mas não fornece informações sobre como acessar o banco de dados de saudação.

Crie *myBackendNic*:

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

Definir Olá nome de usuário e a senha necessários para a conta de administrador Olá Olá VM com Get-Credential:

```powershell
$cred = Get-Credential
```

Crie *myBackendVM*:

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

imagem de saudação que é usada com o SQL Server instalado, mas não é usada neste tutorial. Ele é incluído tooshow é como você pode configurar o tráfego de web de toohandle VM e gerenciamento de banco de dados de toohandle uma VM.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você criou e redes do Azure como máquinas toovirtual relacionados seguras. 

> [!div class="checklist"]
> * Criar uma rede virtual
> * Criar sub-redes de rede virtual
> * Controle de tráfego de rede com grupos de segurança de rede
> * Exibir regras de tráfego em ação

Avançar toohello toolearn próximo de tutorial sobre como monitorar a proteção de dados em máquinas virtuais usando o backup do Azure. .

> [!div class="nextstepaction"]
> [Fazer backup de máquinas virtuais do Windows no Azure](./tutorial-backup-vms.md)
