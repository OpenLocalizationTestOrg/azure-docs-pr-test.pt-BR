---
title: aaaCreate VM de um disco especializado no Azure | Microsoft Docs
description: "Crie uma nova VM anexando um disco especializado não gerenciado, no modelo de implantação do Gerenciador de recursos de saudação."
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: c88f213b6629a6c1d6ff5845e76c2f7719672714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a>Criar uma VM a partir de um VHD especializado em uma conta de armazenamento

Crie uma nova VM anexando um disco especializado de não gerenciado, como o disco do sistema operacional hello usando o Powershell. Um disco especializado é uma cópia do VHD de uma VM existente que mantém as contas de usuário hello, aplicativos e outros dados de estado da VM original. 

Você tem duas opções:
* [Carregar um VHD](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [Copiar Olá VHD de uma VM existente do Azure](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a>Antes de começar
Se você usar o PowerShell, certifique-se de que você tem a versão mais recente Olá de saudação módulo AzureRM.Compute PowerShell. Executar Olá tooinstall de comando a seguir.

```powershell
Install-Module AzureRM.Compute 
```
Para saber mais, confira [Azure PowerShell Versioning](/powershell/azure/overview) (Controle de versão do Azure PowerShell).


## <a name="option-1-upload-a-specialized-vhd"></a>Opção 1: Carregar um VHD especializado

Você pode carregar Olá que VHD de uma VM especializada criado com uma ferramenta de virtualização local, como o Hyper-V, ou em uma VM exportada de outra nuvem.

### <a name="prepare-hello-vm"></a>Preparar Olá VM
Você pode carregar um VHD especializado que foi criado usando uma VM local ou um VHD exportado de outra nuvem. Um VHD especializado mantém as contas de usuário hello, aplicativos e outros dados de estado da VM original. Se você pretende toouse Olá VHD como-é toocreate uma nova VM, certifique-se de saudação etapas forem concluída. 
  
  * [Preparar um tooAzure tooupload de VHD do Windows](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). **Não** generalizar Olá VM usando o Sysprep.
  * Remova quaisquer ferramentas de virtualização de convidado e os agentes instalados em Olá VM (ou seja, as ferramentas do VMware).
  * Certifique-se de saudação VM é configurada toopull seu endereço IP e as configurações de DNS por meio de DHCP. Isso garante que o servidor Olá obtém um endereço IP em redes de saudação quando ele é iniciado. 


### <a name="get-hello-storage-account"></a>Obter a conta de armazenamento Olá
Você precisa de uma conta de armazenamento na imagem VM do Azure toostore Olá carregado. Você pode usar uma conta de armazenamento existente ou criar uma nova. 

as contas de armazenamento disponível Olá tooshow, digite:

```powershell
Get-AzureRmStorageAccount
```

Se você quiser toouse uma conta de armazenamento existente, vá toohello [carregar imagem VM Olá](#upload-the-vm-vhd-to-your-storage-account) seção.

Se você precisar toocreate uma conta de armazenamento, siga estas etapas:

1. Você precisará nome Olá Olá do grupo de recursos onde a conta de armazenamento Olá deve ser criada. toofind todos os grupos de recursos Olá que estão em sua assinatura, o tipo:
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    toocreate um grupo de recursos denominado **myResourceGroup** em Olá **Oeste dos EUA** região, digite:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. Criar uma conta de armazenamento denominada **mystorageaccount** neste grupo de recursos usando Olá [AzureRmStorageAccount novo](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
### <a name="upload-hello-vhd-tooyour-storage-account"></a>Carregar conta de armazenamento Olá VHD tooyour
Saudação de uso [AzureRmVhd adicionar](/powershell/module/azurerm.compute/add-azurermvhd) contêiner do cmdlet tooupload Olá imagem tooa na sua conta de armazenamento. Este exemplo hello de carregamentos de arquivo **myVHD.vhd** de `"C:\Users\Public\Documents\Virtual hard disks\"` tooa conta de armazenamento denominada **mystorageaccount** em Olá **myResourceGroup** grupo de recursos. arquivo Hello será colocado no contêiner Olá denominado **mycontainer** e o novo nome de arquivo hello serão **myUploadedVHD.vhd**.

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
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

Dependendo de sua conexão de rede e o tamanho de saudação do arquivo VHD, este comando pode demorar um pouco toocomplete.


## <a name="option-2-copy-hello-vhd-from-an-existing-azure-vm"></a>Opção 2: Copiar Olá VHD de uma VM existente do Azure

Você pode copiar um toouse de conta de armazenamento do VHD tooanother ao criar uma VM de novo, duplicada.

### <a name="before-you-begin"></a>Antes de começar
Lembre-se de:

* Obter informações sobre a saudação **contas de armazenamento de origem e destino**. Para saudação de VM de origem, você precisa de nomes de conta e o contêiner de armazenamento de saudação do toohave. Normalmente, o nome de contêiner de Olá será **vhds**. Você também precisa toohave uma conta de armazenamento de destino. Se você ainda não tiver um, você pode criar um usando o portal de saudação (**mais serviços** > contas de armazenamento > Adicionar) ou usando Olá [AzureRmStorageAccount novo](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet. 
* Baixar e instalar Olá [ferramenta AzCopy](../../storage/common/storage-use-azcopy.md). 

### <a name="deallocate-hello-vm"></a>Desalocar Olá VM
Desaloque Olá VM, o que libera Olá VHD toobe copiado. 

* **Portal**: clique em **Máquinas virtuais** > **myVM** > Parar
* **PowerShell**: Use [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (desalocar) Olá VM denominada **myVM** no grupo de recursos **myResourceGroup**.

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

Olá **Status** para Olá VM em hello Azure portal muda de **parado** muito**parado (desalocado)**.

### <a name="get-hello-storage-account-urls"></a>Obter Olá URLs de conta de armazenamento
Você precisa de URLs Olá Olá origem e destino de contas de armazenamento. Olá URLs se parecer com: `https://<storageaccount>.blob.core.windows.net/<containerName>/`. Se você já souber o nome da conta e o contêiner de armazenamento hello, pode apenas substituir Olá informações entre Olá colchetes toocreate sua URL. 

Você pode usar o hello portal do Azure ou Azure Powershell tooget Olá URL:

* **Portal**: clique em Olá  **>**  para **mais serviços** > **contas de armazenamento**  >   *conta de armazenamento* > **Blobs** e seu arquivo VHD de origem provavelmente está em Olá **vhds** contêiner. Clique em **propriedades** para contêiner hello e copiar texto de saudação rotulada **URL**. Você precisará Olá URLs de ambos os contêineres de origem e destino hello. 
* **PowerShell**: Use [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget informações Olá VM denominada **myVM** no grupo de recursos de saudação **myResourceGroup**. Nos resultados de hello, examinar Olá **perfil de armazenamento** seção para Olá **Uri do Vhd**. primeira parte Olá Olá Uri é contêiner de toohello URL hello e Olá última parte é Olá nome do VHD do sistema operacional para Olá VM.

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-hello-storage-access-keys"></a>Obter chaves de acesso de armazenamento Olá
Localize chaves de acesso de saudação para Olá contas de armazenamento de origem e de destino. Para obter mais informações sobre as chaves de acesso, consulte [Sobre as contas de armazenamento do Azure](../../storage/common/storage-create-storage-account.md).

* **Portal**: Clique em **Mais serviços** > **Contas de armazenamento** > *conta de armazenamento* > **Chaves de acesso**. Copiar a chave de saudação rotulado como **key1**.
* **PowerShell**: Use [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget Olá armazenamento chave Olá conta de armazenamento **mystorageaccount** no grupo de recursos de saudação  **myResourceGroup**. Copiar chave de saudação rotulada **key1**.

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-hello-vhd"></a>Copiar Olá VHD
Você pode copiar arquivos entre as contas de armazenamento usando o AzCopy. Para o contêiner de destino hello, se o contêiner de saudação especificado não existir, ele será criado para você. 

toouse AzCopy, abra um prompt de comando no computador local e navegue pasta toohello onde AzCopy é instalado. Ele será semelhante a muito*C:\Program Files (x86) \Microsoft SDKs\Azure\AzCopy*. 

toocopy todos Olá arquivos dentro de um contêiner, que você usar o hello **/S** alternar. Isso pode ser usado toocopy Olá VHD do sistema operacional e todos os discos de dados Olá se eles estiverem em Olá mesmo contêiner. Este exemplo mostra como toocopy todos Olá arquivos no contêiner Olá **mysourcecontainer** na conta de armazenamento **mysourcestorageaccount** toohello contêiner **mydestinationcontainer**  em Olá **mydestinationstorageaccount** conta de armazenamento. Substitua os nomes de saudação de contas de armazenamento hello e contêineres com seus próprios. Substitua `<sourceStorageAccountKey1>` e `<destinationStorageAccountKey1>` pelas suas próprias chaves.

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

Se você desejar somente toocopy um VHD específico em um contêiner com vários arquivos, você também pode especificar nome do arquivo hello usando Olá /Pattern comutador. Neste exemplo, Olá somente o arquivo chamado **myFileName.vhd** serão copiados.

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


Quando ele for concluído, você receberá uma mensagem como a seguinte:

```
Finished 2 of total 2 file(s).
[2016/10/07 17:37:41] Transfer summary:
-----------------
Total files transferred: 2
Transfer successfully:   2
Transfer skipped:        0
Transfer failed:         0
Elapsed time:            00.00:13:07
```

### <a name="troubleshooting"></a>Solucionar problemas
* Quando você usa AZCopy, se você vir o erro hello "Servidor falha na solicitação de saudação tooauthenticate", certifique-se de valor de saudação do cabeçalho de autorização hello está formado corretamente e inclui assinatura hello. Se você estiver usando a chave 2 ou a chave de armazenamento secundário hello, tente usar chave de armazenamento principal ou 1º hello.

## <a name="create-hello-new-vm"></a>Criar hello nova VM 

Você precisa de rede toocreate e outros toobe de recursos VM usada pelo Olá nova VM.

### <a name="create-hello-subnet-and-vnet"></a>Criar rede virtual e a sub-rede de saudação

Criar rede virtual de saudação e a sub-rede de saudação [rede virtual](../../virtual-network/virtual-networks-overview.md).

1. Crie uma sub-rede de saudação. Este exemplo cria uma sub-rede denominada **mySubNet**, no grupo de recursos de saudação **myResourceGroup**, e define Olá prefixo de endereço de sub-rede muito**10.0.0.0/24**.
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Crie rede virtual de saudação. Este exemplo define Olá toobe de nome de rede virtual **myVnetName**, Olá local muito**Oeste dos EUA**, e Olá prefixo de endereço de rede virtual Olá muito**10.0.0.0/16**. 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a>Criar um endereço IP público e uma NIC
comunicação tooenable com máquina virtual de saudação na rede virtual Olá, é necessário um [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e uma interface de rede.

1. Crie o IP público hello. Neste exemplo, nome do endereço IP público hello está definido muito**myIP**.
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Criar NIC hello. Neste exemplo, o nome NIC do hello está definido muito**myNicName**.
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Criar um grupo de segurança de rede hello e uma regra RDP
toolog capaz de toobe em tooyour VM usando o RDP, você precisa toohave uma regra de segurança que permita o acesso RDP na porta 3389. Porque hello VHD para Olá que nova VM foi criada a partir de um existente especializado VM, depois Olá VM for criado, você pode usar uma conta existente na máquina de virtual de origem Olá que tiveram permissão toolog sobre como usar o RDP.
Este exemplo define Olá nome NSG muito**myNsg** e Olá RDP nome da regra muito**myRdpRule**.

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

Para obter mais informações sobre pontos de extremidade e regras NSG, consulte [a abertura de portas tooa VM no Azure usando o PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="set-hello-vm-name-and-size"></a>Definir nome VM hello e tamanho

Este exemplo define Olá nome da VM muito "myVM" e Olá VM tamanho muito "Standard_A2".
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a>Adicionar Olá NIC
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-hello-os-disk"></a>Configurar o disco Olá SO

1. Defina hello URI para Olá VHD carregado ou copiado. Neste exemplo, Olá arquivo do VHD chamado **myOsDisk.vhd** é mantido em uma conta de armazenamento denominada **myStorageAccount** em um contêiner chamado **myContainer**.

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. Adicione disco Olá sistema operacional. Neste exemplo, quando Olá disco do sistema operacional é criado, Olá termo "osDisk" é appened toohello VM nome toocreate Olá SO nome do disco. Este exemplo também especifica que este VHD com base em Windows deve ser anexado toohello VM como disco Olá sistema operacional.
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

Opcional: Se você tiver os discos de dados que toobe necessidade anexado toohello VM, adicione discos de dados hello usando URLs de saudação de dados VHDs e Olá número de unidade lógica (Lun) apropriado.

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

Ao usar uma conta de armazenamento, URLs de disco do sistema operacional e dados de saudação algo parecido com isto: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`. Você pode encontrar isso no portal de saudação navegando toohello contêiner de armazenamento de destino, clicando em sistema operacional de saudação ou dados VHD que foi copiada e, em seguida, copiar o conteúdo de saudação da URL de saudação.


### <a name="complete-hello-vm"></a>Concluir Olá VM 

Criar hello VM usando as configurações de saudação que acabou de criar.

```powershell
#Create hello new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
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
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a>Próximas etapas
toosign em tooyour nova máquina virtual toohello procurar VM em Olá [portal](https://portal.azure.com), clique em **conectar**e abra Olá o RDP. Use credenciais de conta de saudação do seu toosign de máquina virtual original na nova máquina de virtual tooyour. Para obter mais informações, consulte [como tooconnect e logon tooan virtuais do Azure do computador que executa o Windows](connect-logon.md).

