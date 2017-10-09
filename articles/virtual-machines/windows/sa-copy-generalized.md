---
title: "aaaCreate uma imagem não gerenciada de uma VM generalizada no Azure | Microsoft Docs"
description: "Crie uma imagem de unmanged de um generalizado toouse toocreate da VM do Windows várias cópias de uma VM no Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: b8a044d20313efa6dd9b9757e61154f922134476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-unmanaged-vm-image-from-an-azure-vm"></a>Como toocreate uma VM não gerenciada de imagem de uma VM do Azure

Este artigo abrange o uso de contas de armazenamento. É recomendável que você utilize discos gerenciados e imagens gerenciadas em vez de uma conta de armazenamento. Para obter mais informações, consulte [Capture uma imagem gerenciada de uma VM generalizada no Azure](capture-image-resource.md).

Este artigo mostra como toouse do Azure PowerShell toocreate uma imagem de uma VM generalizada do Azure usando uma conta de armazenamento. Você pode usar Olá imagem toocreate outra VM. imagem de saudação inclui o disco do sistema operacional hello e discos de dados de saudação que estão anexados toohello virtual machine. imagem de saudação não inclui recursos de rede virtual Olá, para que seja necessário tooset esses recursos quando você cria Olá nova VM. 

## <a name="prerequisites"></a>Pré-requisitos
Você precisa toohave Azure PowerShell versão 1.0. x ou posterior esteja instalado. Se você ainda não instalou PowerShell, leia [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) para etapas de instalação.

## <a name="generalize-hello-vm"></a>Generalize Olá VM 
Esta seção mostra como toogeneralize sua máquina virtual do Windows para uso como uma imagem. Generalizando uma VM remove todas as suas informações de conta pessoal, entre outras coisas e o prepara Olá máquina toobe usado como uma imagem. Para obter detalhes sobre o Sysprep, consulte [como tooUse Sysprep: uma introdução](http://technet.microsoft.com/library/bb457073.aspx).

Certifique-se de funções de servidor de saudação em execução na máquina Olá Sysprep oferece suporte. Para obter mais informações, consulte [Suporte do Sysprep para funções de servidor](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Se você estiver carregando tooAzure seu VHD para Olá a primeira vez, verifique se você tem [preparado sua VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de executar o Sysprep. 
> 
> 

Você também pode generalizar uma VM do Linux usando `sudo waagent -deprovision+user` e, em seguida, use PowerShell toocapture Olá VM. Para obter informações sobre como usar o hello CLI toocapture uma VM, consulte [como toogeneralize e capturar uma máquina virtual Linux usando Olá CLI do Azure ](../linux/capture-image.md).


1. Entrar toohello máquina virtual do Windows.
2. Abra a janela de Prompt de comando hello como administrador. Altere o diretório de saudação muito**%windir%\system32\sysprep**e, em seguida, execute `sysprep.exe`.
3. Em Olá **ferramenta de preparação do sistema** caixa de diálogo, selecione **Enter System Out-of-Box Experience (OOBE)**e certifique-se de que Olá **generalizar** caixa de seleção é marcada.
4. Em **Opções de Desligamento**, selecione **Desligar**.
5. Clique em **OK**.
   
    ![Inicie o Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. Quando o Sysprep for concluído, desligar máquina virtual de saudação. 

> [!IMPORTANT]
> Não reinicie Olá VM até que você esteja concluído tooAzure VHD Olá carregar ou criar uma imagem de VM de saudação. Se acidentalmente Olá VM é reiniciada, execute Sysprep toogeneralize-a novamente.
> 
> 

## <a name="log-in-tooazure-powershell"></a>Faça logon no tooAzure PowerShell
1. Abra o PowerShell do Azure e entrar tooyour conta do Azure.
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    Uma janela pop-up é aberto para você tooenter suas credenciais de conta do Azure.
2. Obter IDs de assinatura Olá para suas assinaturas disponíveis.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Definir Olá assinatura correto usando a ID de assinatura de saudação.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-hello-vm-and-set-hello-state-toogeneralized"></a>Desalocar Olá VM e defina Olá estado toogeneralized
1. Desalocar recursos de saudação de VM.
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    Olá *Status* para Olá VM em hello Azure portal muda de **parado** muito**parado (desalocado)**.
2. Definir status da saudação da máquina virtual de saudação muito**generalizado**. 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. Verificar status de saudação do hello VM. Olá **OSState/generalizadas** seção Olá VM deve ter Olá **DisplayStatus** definido muito**VM generalizado**.  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-hello-image"></a>Criar imagem Olá

Crie uma imagem de máquina virtual não gerenciada no contêiner de armazenamento de destino hello usando este comando. Hello imagem é criada no hello mesma conta de armazenamento como Olá máquina virtual original. Olá `-Path` parâmetro salva uma cópia do modelo JSON Olá Olá computador de origem VM tooyour local. Olá `-DestinationContainerName` parâmetro é o nome de saudação do contêiner de saudação que você deseja toohold suas imagens. Se o contêiner de saudação não existir, ele é criado para você.
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
Você pode obter Olá URL da imagem de modelo de arquivo hello JSON. Vá toohello **recursos** > **storageProfile** > **osDisk** > **imagem**  >  **uri** seção de caminho completo de saudação da imagem. Olá URL da imagem de saudação se parece com: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.
   
Você também pode verificar Olá URI no portal de saudação. imagem de saudação é copiado tooa contêiner nomeado **sistema** em sua conta de armazenamento. 

## <a name="create-a-vm-from-hello-image"></a>Criar uma VM da imagem Olá

Agora você pode criar uma ou mais máquinas virtuais de imagem de saudação não gerenciado.

### <a name="set-hello-uri-of-hello-vhd"></a>Saudação de conjunto de URI do VHD de saudação

Olá URI para Olá VHD toouse está no formato de saudação: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**. vhd. Neste exemplo hello VHD denominado **myVHD** é na conta de armazenamento Olá **mystorageaccount** no contêiner Olá **mycontainer**.

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a>Criar uma rede virtual
Criar rede virtual de saudação e a sub-rede de saudação [rede virtual](../../virtual-network/virtual-networks-overview.md).

1. Crie uma sub-rede de saudação. Olá, exemplo a seguir cria uma sub-rede denominada **mySubnet** no grupo de recursos de saudação **myResourceGroup** com prefixo de endereço de saudação **10.0.0.0/24**.  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Crie rede virtual hello. Olá, exemplo a seguir cria uma rede virtual denominada **myVnet** em Olá **Oeste dos EUA** local com o prefixo de endereço de saudação **10.0.0.0/16**.  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a>Criar um endereço IP público e um adaptador de rede
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

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Criar um grupo de segurança de rede hello e uma regra RDP
toolog capaz de toobe em tooyour VM usando o RDP, você precisa toohave uma regra de segurança que permita o acesso RDP na porta 3389. 

Este exemplo cria um NSG chamado **myNsg** que contém uma regra chamada **myRdpRule** que permite tráfego RDP pela porta 3389. Para obter mais informações sobre os NSGs, consulte [a abertura de portas tooa VM no Azure usando o PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a>Criar uma variável para a rede virtual Olá
Crie uma variável para a rede virtual Olá concluída. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a>Criar hello VM
Olá PowerShell a seguir conclui as configurações de máquina virtual de saudação e usa a imagem do não gerenciada como fonte de saudação para nova instalação de saudação.

</br>

```powershell
    # Enter a new user name and password toouse as hello local administrator account 
    # for remotely accessing hello VM.
    $cred = Get-Credential

    # Name of hello storage account where hello VHD is located. This example sets hello 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of hello virtual machine. This example sets hello VM name as "myVM".
    $vmName = "myVM"

    # Size of hello virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See hello VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for hello VM. This examples sets hello computer name as "myComputer".
    $computerName = "myComputer"

    # Name of hello disk that holds hello OS. This example sets hello 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets hello SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get hello storage account where hello uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set hello VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set hello Windows operating system configuration and add hello NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create hello OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure hello OS disk toobe created from hello existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create hello new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

### <a name="verify-that-hello-vm-was-created"></a>Verifique se esse Olá que VM foi criada
Ao concluir, você deverá ver Olá recém-criado VM em Olá [portal do Azure](https://portal.azure.com) em **procurar** > **máquinas virtuais**, ou usando o seguinte Olá Comandos do PowerShell:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Próximas etapas
toomanage nova máquina virtual com o Azure PowerShell, consulte [gerenciar máquinas virtuais usando o Gerenciador de recursos do Azure e PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


