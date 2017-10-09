---
title: "aaaCreate e gerenciar máquinas virtuais do Windows no Azure que usam várias NICs | Microsoft Docs"
description: "Saiba como toocreate e gerenciar uma VM do Windows que tenha várias NICs e anexado tooit usando modelos do Azure PowerShell ou Gerenciador de recursos."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 9bff5b6d-79ac-476b-a68f-6f8754768413
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: c3c7d7569aca6f047238146d84b2ffccf05d4079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a>Cria e gerencia uma máquina virtual do Windows que tem várias NICs
Máquinas virtuais (VMs) no Azure pode ter vários toothem de NICs (placas) anexadas de interface de rede virtual. Um cenário comum é toohave várias sub-redes para conectividade de front-end e back-end ou uma rede dedicada tooa monitoramento ou solução de backup. Este artigo fornece detalhes sobre como toocreate uma máquina virtual que tem várias NICs anexado tooit. Você também aprenderá como NICs tooadd ou remover de uma VM existente. Diferentes [tamanhos de VM](sizes.md) dão suporte a um número variável de NICs, sendo assim, dimensione sua VM adequadamente.

Para obter informações detalhadas, incluindo como toocreate várias NICs dentro de seus próprios scripts do PowerShell, consulte [implantar VMs várias NICs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).

## <a name="prerequisites"></a>Pré-requisitos
Certifique-se de que você tenha Olá [versão mais recente do PowerShell do Azure instalado e configurado](/powershell/azure/overview).

Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores. Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *myVnet* e *myVM*.


## <a name="create-a-vm-with-multiple-nics"></a>Criar uma VM com diversos NICs
Em primeiro lugar, crie um grupo de recursos. Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *EastUs* local:

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a>Crie a rede virtual e as sub-redes
Um cenário comum é para uma rede virtual toohave duas ou mais sub-redes. Pode ser uma sub-rede para o tráfego de front-end, Olá para o tráfego de back-end. tooconnect tooboth sub-redes, você usar várias NICs em sua VM.

1. Defina duas sub-redes de rede virtual com [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig). Olá, exemplo a seguir define sub-redes Olá para *mySubnetFrontEnd* e *mySubnetBackEnd*:

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. Crie uma rede virtual e sub-redes com [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork). Olá, exemplo a seguir cria uma rede virtual denominada *myVnet*:

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a>Crie múltiplas NICs
Crie duas NICs com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface). Anexe uma sub-rede front-end toohello NIC e uma sub-rede de back-end de toohello NIC. Olá, exemplo a seguir cria NICs denominadas *myNic1* e *myNic2*:

```powershell
$frontEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetFrontEnd'}
$myNic1 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic1" `
    -Location "EastUs" `
    -SubnetId $frontEnd.Id

$backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}
$myNic2 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic2" `
    -Location "EastUs" `
    -SubnetId $backEnd.Id
```

Normalmente você cria também uma [grupo de segurança de rede](../../virtual-network/virtual-networks-nsg.md) ou [balanceador de carga](../../load-balancer/load-balancer-overview.md) toohelp gerenciar e distribuir o tráfego entre suas VMs. Olá [mais detalhadas a VM de várias NICs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) artigo orienta você na criação de um grupo de segurança de rede e atribuindo NICs.

### <a name="create-hello-virtual-machine"></a>Criar a máquina virtual de saudação
Inicie agora toobuild a configuração de VM. O tamanho de cada VM tem um limite para o número total de saudação de NICs que você pode adicionar tooa VM. Para obter mais informações, consulte [Tamanhos da VM no Windows](sizes.md) .

1. Definir sua toohello de credenciais VM `$cred` variável da seguinte maneira:

    ```powershell
    $cred = Get-Credential
    ```

2. Defina sua VM com [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig). Olá, exemplo a seguir define uma VM denominada *myVM* e usa um tamanho VM que oferece suporte a mais de dois NICs (*Standard_DS3_v2*):

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. Criar rest Olá da sua configuração de VM com [conjunto AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) e [AzureRmVMSourceImage conjunto](/powershell/module/azurerm.compute/set-azurermvmsourceimage). saudação de exemplo a seguir cria uma VM do Windows Server 2016:

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig `
        -Windows `
        -ComputerName "myVM" `
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig `
        -PublisherName "MicrosoftWindowsServer" `
        -Offer "WindowsServer" `
        -Skus "2016-Datacenter" `
        -Version "latest"
   ```

4. Anexar Olá duas NICs que você criou anteriormente com [adicionar AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. Finalmente, crie sua VM com [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-tooan-existing-vm"></a>Adicionar um tooan NIC existentes de VM
tooadd um tooan NIC virtual existente da VM, você desalocar Olá VM, adicionar Olá NIC virtual, em seguida, inicie o hello VM.

1. Desalocar Olá VM com [AzureRmVM Stop](/powershell/module/azurerm.compute/stop-azurermvm). exemplo a seguir Hello desaloca Olá VM denominada *myVM* na *myResourceGroup*:

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. Obter a configuração existente de saudação do hello VM com [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm). Olá, exemplo a seguir obtém informações de saudação VM denominada *myVM* na *myResourceGroup*:

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. Olá, exemplo a seguir cria uma NIC virtual com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) chamado *myNic3* anexado muito*mySubnetBackEnd*. Olá NIC virtual é anexado toohello VM denominada *myVM* na *myResourceGroup* com [adicionar AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

    ```powershell
    # Get info for hello back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get hello ID of hello new virtual NIC and add tooVM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a>NICs virtuais primárias
    Uma saudação NICs em uma VM multi-NIC precisa toobe primário. Se um dos Olá NICs virtuais existentes em Olá VM já está definida como principal, você pode ignorar esta etapa. Olá exemplo a seguir supõe que duas NICs virtuais agora estão presentes em uma máquina virtual e deseja tooadd Olá primeiro NIC (`[0]`) como Olá primário:
        
    ```powershell
    # List existing NICs on hello VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 toobe primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update hello VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. Iniciar Olá VM com [AzureRmVm início](/powershell/module/azurerm.compute/start-azurermvm):

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a>Remover uma NIC de uma VM existente
tooremove uma NIC virtual de uma VM existente, você desalocar Olá VM, remova Olá NIC virtual, em seguida, iniciar Olá VM.

1. Desalocar Olá VM com [AzureRmVM Stop](/powershell/module/azurerm.compute/stop-azurermvm). exemplo a seguir Hello desaloca Olá VM denominada *myVM* na *myResourceGroup*:

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. Obter a configuração existente de saudação do hello VM com [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm). Olá, exemplo a seguir obtém informações de saudação VM denominada *myVM* na *myResourceGroup*:

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. Obter informações sobre Olá remover NIC com [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface). Olá exemplo a seguir obtém informações sobre *myNic3*:

    ```powershell
    # List existing NICs on hello VM if you need toodetermine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. Remover Olá NIC com [remover AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) e atualize Olá VM com [AzureRmVm atualização](/powershell/module/azurerm.compute/update-azurermvm). Olá exemplo a seguir remove *myNic3* conforme obtidas pelo `$nicId` em Olá anterior etapa:

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. Iniciar Olá VM com [AzureRmVm início](/powershell/module/azurerm.compute/start-azurermvm):

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a>Criar várias NICs com modelos
Modelos do Gerenciador de recursos do Azure fornecem uma maneira toocreate várias instâncias de um recurso durante a implantação, como a criação de várias NICs. Modelos do Gerenciador de recursos usam toodefine declarativa de arquivos JSON seu ambiente. Para saber mais, consulte [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). Você pode usar *cópia* toospecify número de saudação do toocreate de instâncias:

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

Para obter mais informações, consulte [criando várias instâncias usando *cópia*](../../resource-group-create-multiple.md). 

Você também pode usar `copyIndex()` tooappend um nome de recurso tooa número. Você pode criar *myNic1*, *MyNic2* e assim por diante. Olá código a seguir mostra um exemplo de acrescentar o valor de índice hello:

```json
"name": "[concat('myNic', copyIndex())]", 
```

Você pode ler um exemplo completo em [criando várias NICs usando modelos do Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).

## <a name="next-steps"></a>Próximas etapas
Revisão [tamanhos de VM do Windows](sizes.md) quando você estiver tentando toocreate uma máquina virtual que tem várias NICs. Preste atenção toohello número de NICs que dá suporte a cada tamanho VM. 


