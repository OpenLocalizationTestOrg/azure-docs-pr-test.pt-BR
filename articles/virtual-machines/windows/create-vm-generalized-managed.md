---
title: aaaCreate VM de uma imagem VM gerenciada no Azure | Microsoft Docs
description: "Crie uma máquina virtual do Windows de uma imagem VM gerenciada generalizada usando o PowerShell do Azure, no modelo de implantação do Gerenciador de recursos de saudação."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.openlocfilehash: 5036ef1533c144a9a328e94599b359e0166f337d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-managed-image"></a>Criar uma VM por meio de uma imagem gerenciada

Você pode criar várias VMs de uma imagem de VM gerenciada no Azure. Uma imagem VM gerenciada contém toocreate necessário de informações de Olá uma VM, incluindo Olá SO e discos de dados. Olá VHDs que compõem a imagem de hello, incluindo discos Olá SO e discos de dados, são armazenados como discos gerenciados. 


## <a name="prerequisites"></a>Pré-requisitos

Você precisa toohave já [criado de uma imagem VM gerenciada](capture-image-resource.md) toouse para a criação de Olá nova VM. 

Certifique-se de que você tenha versões mais recentes de saudação de módulos de AzureRM.Compute e AzureRM.Network PowerShell hello. Abra um prompt do PowerShell como administrador e execute Olá tooinstall de comando a segui-los.

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
Para saber mais, confira [Azure PowerShell Versioning](/powershell/azure/overview) (Controle de versão do Azure PowerShell).



## <a name="collect-information-about-hello-image"></a>Coletar informações sobre a imagem de saudação

Primeiro precisamos toogather as informações básicas sobre a imagem de saudação e criar uma variável para a imagem de saudação. Este exemplo usa uma imagem VM gerenciada denominada **myImage** que é em Olá **myResourceGroup** grupo de recursos em Olá **Central Oeste dos EUA** local. 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a>Criar uma rede virtual
Criar rede virtual de saudação e a sub-rede de saudação [rede virtual](../../virtual-network/virtual-networks-overview.md).

1. Crie uma sub-rede de saudação. Este exemplo cria uma sub-rede denominada **mySubnet** com prefixo de endereço de saudação **10.0.0.0/24**.  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Crie rede virtual hello. Este exemplo cria uma rede virtual denominada **myVnet** com prefixo de endereço de saudação **10.0.0.0/16**.  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a>Criar um endereço IP público e um adaptador de rede

comunicação tooenable com máquina virtual de saudação na rede virtual Olá, é necessário um [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e uma interface de rede.

1. Criar um endereço IP público. Este exemplo cria um endereço IP público chamado **myPip**. 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Criar NIC hello. Este exemplo cria uma NIC chamada **myNic**. 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Criar um grupo de segurança de rede hello e uma regra RDP

toolog capaz de toobe em tooyour VM usando o RDP, você precisa toohave uma regra de segurança de rede (NSG) que permite o acesso RDP na porta 3389. 

Este exemplo cria um NSG chamado **myNsg** que contém uma regra chamada **myRdpRule** que permite tráfego RDP pela porta 3389. Para obter mais informações sobre os NSGs, consulte [a abertura de portas tooa VM no Azure usando o PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a>Criar uma variável para a rede virtual Olá

Crie uma variável para a rede virtual Olá concluída. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a>Obter credenciais Olá Olá VM

Olá seguinte cmdlet abrirá uma janela onde você inserirá um novo toouse de nome e senha de usuário como conta de administrador local Olá para acessar remotamente Olá VM. 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-hello-vm-name-computer-name-and-hello-size-of-hello-vm"></a>Variáveis definidas para Olá VM nome, nome do computador e Olá tamanho da VM de saudação

1. Crie variáveis de nome VM hello e nome do computador. Este exemplo define o nome da VM hello como **myVM** e o nome do computador hello como **myComputer**.

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. Definir tamanho de saudação da máquina virtual de saudação. Este exemplo cria a VM de tamanho **Standard_DS1_v2**. Consulte Olá [tamanhos de VM](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentação para obter mais informações.

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. Adicione hello nome da VM e a configuração da VM toohello tamanho.

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a>Imagem VM do conjunto hello como imagem de origem para Olá nova VM

Definir a imagem de origem de hello usando uma ID de Olá Olá gerenciado da imagem da VM.

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a>Definir configuração de SO hello e adicionar NIC hello.

Insira o tipo de armazenamento da saudação (PremiumLRS ou StandardLRS) e o tamanho de saudação do disco do sistema operacional hello. Este exemplo define o tipo de conta Olá muito**PremiumLRS**, Olá muito o tamanho do disco**128 GB** e cache de disco muito**ReadWrite**.

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a>Criar hello VM

Criar hello nova Vm usando a configuração de saudação que temos criado e armazenado no hello **$vm** variável.

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a>Verifique se esse Olá que VM foi criada
Ao concluir, você deverá ver Olá recém-criado VM em Olá [portal do Azure](https://portal.azure.com) em **procurar** > **máquinas virtuais**, ou usando o seguinte Olá Comandos do PowerShell:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Próximas etapas
toomanage nova máquina virtual com o Azure PowerShell, consulte [criar e gerenciar máquinas virtuais do Windows com o módulo do PowerShell do Azure Olá](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

