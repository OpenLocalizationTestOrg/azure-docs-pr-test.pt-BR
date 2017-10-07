---
title: aaaCreate uma VM do Windows em um VHD especializado no Azure | Microsoft Docs
description: "Crie uma nova VM do Windows, anexando um disco gerenciado especializado como disco do sistema operacional hello usando o modelo de implantação do Gerenciador de recursos de saudação."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cynthn
ms.openlocfilehash: c72c6f4fb650e2664e87cf38ec9be62f0b2209fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a>Criar uma VM do Windos a partir de um disco especializado

Crie uma nova VM, anexando um disco gerenciado especializado como disco do sistema operacional hello usando o Powershell. Um disco especializado é uma cópia do disco rígido virtual (VHD) de uma VM existente que mantém as contas de usuário hello, aplicativos e outros dados de estado da VM original. 

Quando você usa um toocreate especializada do VHD uma nova VM, Olá nova VM retém o nome do computador de saudação do hello VM original. Outras informações específicas do computador também são mantidas e, em alguns casos, essas informações duplicadas podem causar problemas. Lembre-se de que tipos de informações específicas do computador seus aplicativos dependem ao copiar uma VM.

Você tem duas opções:
* [Carregar um VHD](#option-1-upload-a-specialized-vhd)
* [Copiar uma VM existente do Azure](#option-2-copy-an-existing-azure-vm)

Este tópico mostra como toouse gerenciada discos. Se você tiver uma implantação herdada que requer o uso de uma conta de armazenamento, consulte [Criar uma VM em um VHD especializado em uma conta de armazenamento](sa-create-vm-specialized.md)

## <a name="before-you-begin"></a>Antes de começar
Se você usar o PowerShell, certifique-se de que você tem a versão mais recente Olá de saudação módulo AzureRM.Compute PowerShell. 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Para saber mais, confira [Azure PowerShell Versioning](/powershell/azure/overview) (Controle de versão do Azure PowerShell).


## <a name="option-1-upload-a-specialized-vhd"></a>Opção 1: Carregar um VHD especializado

Você pode carregar Olá que VHD de uma VM especializada criado com uma ferramenta de virtualização local, como o Hyper-V, ou em uma VM exportada de outra nuvem.

### <a name="prepare-hello-vm"></a>Preparar Olá VM
Se você pretende toouse Olá VHD como-é toocreate uma nova VM, certifique-se de saudação etapas forem concluída. 
  
  * [Preparar um tooAzure tooupload de VHD do Windows](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). **Não** generalizar Olá VM usando o Sysprep.
  * Remova quaisquer ferramentas de virtualização de convidado e os agentes que estão instalados na VM da saudação (como as ferramentas do VMware).
  * Certifique-se de saudação VM é configurada toopull seu endereço IP e as configurações de DNS por meio de DHCP. Isso garante que o servidor Olá obtém um endereço IP em redes de saudação quando ele é iniciado. 


### <a name="get-hello-storage-account"></a>Obter a conta de armazenamento Olá
Você precisa de um armazenamento de conta no Azure toostore Olá carregar o VHD. Você pode usar uma conta de armazenamento existente ou criar uma nova. 

as contas de armazenamento disponível Olá tooshow, digite:

```powershell
Get-AzureRmStorageAccount
```

Se você quiser toouse uma conta de armazenamento existente, vá toohello [carregamento Olá VHD](#upload-the-vhd-to-your-storage-account) seção.

Se você precisar toocreate uma conta de armazenamento, siga estas etapas:

1. Você precisará nome Olá Olá do grupo de recursos onde a conta de armazenamento Olá deve ser criada. toofind todos os grupos de recursos Olá que estão em sua assinatura, o tipo:
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    toocreate um grupo de recursos denominado *myResourceGroup* em Olá *Oeste dos EUA* região, digite:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. Criar uma conta de armazenamento denominada *mystorageaccount* neste grupo de recursos usando Olá [AzureRmStorageAccount novo](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-hello-vhd-tooyour-storage-account"></a>Carregar conta de armazenamento Olá VHD tooyour 
Saudação de uso [AzureRmVhd adicionar](/powershell/module/azurerm.compute/add-azurermvhd) contêiner de tooa do VHD do cmdlet tooupload Olá em sua conta de armazenamento. Este exemplo hello de carregamentos de arquivo *myVHD.vhd* de `"C:\Users\Public\Documents\Virtual hard disks\"` tooa conta de armazenamento denominada *mystorageaccount* em Olá *myResourceGroup* grupo de recursos. Olá arquivo é armazenado no contêiner Olá denominado *mycontainer* e o novo nome de arquivo hello serão *myUploadedVHD.vhd*.

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


Se for bem-sucedido, você receberá uma resposta que parece semelhante toothis:

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

Dependendo de sua conexão de rede e o tamanho de saudação do arquivo VHD, este comando pode demorar um pouco toocomplete

### <a name="create-a-managed-disk-from-hello-vhd"></a>Criar um disco gerenciado de saudação VHD

Criar um disco gerenciado de saudação especializado VHD em sua conta de armazenamento usando [AzureRMDisk novo](/powershell/module/azurerm.compute/new-azurermdisk). Este exemplo usa **myOSDisk1** para o nome do disco hello, coloca Olá disco em *StandardLRS* armazenamento e usa *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* como hello URI para o VHD de origem hello.

Criar um novo grupo de recursos para Olá nova VM.

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

Criar novo disco de SO Olá da saudação carregar o VHD. 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a>Opção 2: Copiar uma VM existente do Azure

Você pode criar uma cópia de uma VM que usa discos gerenciado por tirar um instantâneo de VM de saudação, em seguida, usando esse Instantâneo toocreate gerenciado um novo disco e uma nova VM.


### <a name="take-a-snapshot-of-hello-os-disk"></a>Tirar um instantâneo do disco do sistema operacional Olá

Você pode tirar um instantâneo de toda a VM (incluindo todos os discos) ou apenas um único disco. Olá etapas a seguir mostram como tootake um instantâneo do disco de saudação SO apenas do VM usando Olá [AzureRmSnapshot novo](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet. 

Defina alguns parâmetros. 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

Obtenha o objeto da VM de saudação.

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
Obter o nome do disco Olá sistema operacional.

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

Crie configuração de saudação de instantâneo. 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

Tire instantâneo hello.

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


Se você planejar toouse Olá instantâneo toocreate uma VM que precisa toobe alto desempenho, use o parâmetro hello `-AccountType Premium_LRS` com o comando Olá AzureRmSnapshot de novo. parâmetro Hello cria o instantâneo de saudação para que ela é armazenada como um disco de gerenciado para Premium. Os Discos Gerenciados Premium são mais caros que os Standard. Portanto certifique-se de que você realmente precisa Premium antes de usar o parâmetro hello.

### <a name="create-a-new-disk-from-hello-snapshot"></a>Criar um novo disco de instantâneo Olá

Criar um disco gerenciado de saudação instantâneo usando [AzureRMDisk novo](/powershell/module/azurerm.compute/new-azurermdisk). Este exemplo usa *myOSDisk* para o nome do disco hello.

Criar um novo grupo de recursos para Olá nova VM.

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

Definir nome de disco Olá sistema operacional. 

```powershell
$osDiskName = 'myOsDisk'
```

Crie disco de saudação gerenciado.

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-hello-new-vm"></a>Criar hello nova VM 

Criar rede e outros toobe de recursos VM usada pelo Olá nova VM.

### <a name="create-hello-subnet-and-vnet"></a>Criar rede virtual e a sub-rede de saudação

Criar rede virtual de saudação e a sub-rede de saudação [rede virtual](../../virtual-network/virtual-networks-overview.md).

Crie uma sub-rede de saudação. Este exemplo cria uma sub-rede denominada **mySubNet**, no grupo de recursos de saudação **myDestinationResourceGroup**, e define Olá prefixo de endereço de sub-rede muito**10.0.0.0/24**.
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

Crie rede virtual de saudação. Este exemplo define Olá toobe de nome de rede virtual **myVnetName**, Olá local muito**Oeste dos EUA**, e Olá prefixo de endereço de rede virtual Olá muito**10.0.0.0/16**. 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Criar um grupo de segurança de rede hello e uma regra RDP
toolog capaz de toobe em tooyour VM usando o RDP, você precisa toohave uma regra de segurança que permita o acesso RDP na porta 3389. Porque hello VHD para Olá nova VM foi criada a partir de uma VM especializada existente, você pode usar uma conta da máquina de virtual de origem Olá para RDP.

Este exemplo define Olá nome NSG muito**myNsg** e Olá RDP nome da regra muito**myRdpRule**.

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

Para obter mais informações sobre pontos de extremidade e regras NSG, consulte [a abertura de portas tooa VM no Azure usando o PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="create-a-public-ip-address-and-nic"></a>Criar um endereço IP público e uma NIC
comunicação tooenable com máquina virtual de saudação na rede virtual Olá, é necessário um [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e uma interface de rede.

Crie o IP público hello. Neste exemplo, nome do endereço IP público hello está definido muito**myIP**.
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

Criar NIC hello. Neste exemplo, o nome NIC do hello está definido muito**myNicName**.
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-hello-vm-name-and-size"></a>Definir nome VM hello e tamanho

Este exemplo define Olá nome da VM muito*myVM* e Olá VM muito o tamanho*Standard_A2*.

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a>Adicionar Olá NIC
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-hello-os-disk"></a>Adicionar disco Olá SO 

Adicionar configuração usando o hello OS disco toohello [AzureRmVMOSDisk conjunto](/powershell/module/azurerm.compute/set-azurermvmosdisk). Este exemplo define o tamanho de saudação do disco de saudação muito*128 GB* e anexa o disco Olá gerenciado como um *Windows* disco do sistema operacional.
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-hello-vm"></a>Concluir Olá VM 

Criar hello VM usando [AzureRMVM novo](/powershell/module/azurerm.compute/new-azurermvm)Olá configurações que acabou de criar.

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

Se o comando for bem-sucedido, você verá uma saída como esta:

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a>Verifique se esse Olá que VM foi criada
Você deve ver Olá recém-criado VM em Olá [portal do Azure](https://portal.azure.com), em **procurar** > **máquinas virtuais**, ou por meio de saudação do PowerShell a seguir comandos:

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a>Próximas etapas
toosign em tooyour nova máquina virtual toohello procurar VM em Olá [portal](https://portal.azure.com), clique em **conectar**e abra Olá o RDP. Use credenciais de conta de saudação do seu toosign de máquina virtual original na nova máquina de virtual tooyour. Para obter mais informações, consulte [como tooconnect e logon tooan virtuais do Azure do computador que executa o Windows](connect-logon.md).

