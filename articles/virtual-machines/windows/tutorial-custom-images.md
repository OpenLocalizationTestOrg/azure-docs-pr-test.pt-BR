---
title: imagens VM personalizadas aaaCreate com hello Azure PowerShell | Microsoft Docs
description: Tutorial - criar uma imagem VM personalizada usando hello Azure PowerShell.
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 3a759fe1b7e7b72f531399b0f4a99e341713c6a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a>Criar uma imagem personalizada de uma VM do Azure usando o PowerShell

Imagens personalizadas são como imagens do marketplace, mas você mesmo as cria. Imagens personalizadas podem ser usado toobootstrap configurações como pré-carregamento de aplicativos, configurações de aplicativo e outras configurações do sistema operacional. Neste tutorial, você criará sua própria imagem personalizada de uma máquina virtual do Azure. Você aprenderá como:

> [!div class="checklist"]
> * Aplicar Sysprep e generalizar VMs
> * Criar uma imagem personalizada
> * Criar uma VM por meio de uma imagem personalizada
> * Lista todas as imagens de saudação em sua assinatura
> * Excluir uma imagem

Este tutorial requer hello Azure PowerShell versão 3.6 ou posterior do módulo. Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação. Se você precisar tooupgrade, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).

## <a name="before-you-begin"></a>Antes de começar

etapas de saudação abaixo detalham como tootake uma VM existente e desative-o para um personalizado pode ser reutilizado da imagem que você podem usar toocreate novas instâncias VM.

exemplo de hello toocomplete neste tutorial, você deve ter uma máquina virtual existente. Se necessário, este [exemplo de script](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) pode criar uma para você. Trabalho tutorial hello, substitua VM e o grupo de recursos de saudação nomes onde for necessário.

## <a name="prepare-vm"></a>Preparar VM

toocreate uma imagem de uma máquina virtual, você precisa tooprepare Olá VM por Olá generalizar VM, desalocando e marcando fonte Olá VM como generalizada no Azure.

### <a name="generalize-hello-windows-vm-using-sysprep"></a>Generalize Olá VM do Windows usando Sysprep

O Sysprep remove todas as suas informações de conta pessoal, entre outras coisas e prepara Olá máquina toobe usado como uma imagem. Para obter detalhes sobre o Sysprep, consulte [como tooUse Sysprep: uma introdução](http://technet.microsoft.com/library/bb457073.aspx).


1. Conecte-se a máquina virtual de toohello.
2. Abra a janela de Prompt de comando hello como administrador. Altere o diretório de saudação muito*%windir%\system32\sysprep*e, em seguida, execute *sysprep.exe*.
3. Em Olá **ferramenta de preparação do sistema** caixa de diálogo, selecione *Enter System Out-of-Box Experience (OOBE)*e certifique-se de que Olá *generalizar* caixa de seleção é marcada.
4. Em **Opções de Desligamento**, selecione *Desligar* e em **OK**.
5. Quando o Sysprep for concluído, desligar máquina virtual de saudação. **Não reinicie Olá VM**.

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a>Desalocar e marcar Olá VM como generalizado

toocreate uma imagem, Olá VM precisa toobe desalocadas e marcado como generalizada no Azure.

Olá desalocada VM usando [AzureRmVM Stop](/powershell/module/azurerm.compute/stop-azurermvm).

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

Definir status da saudação da máquina virtual de saudação muito`-Generalized` usando [AzureRmVm conjunto](/powershell/module/azurerm.compute/set-azurermvm). 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-hello-image"></a>Criar imagem Olá

Agora você pode criar uma imagem de VM de saudação usando [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) e [AzureRmImage novo](/powershell/module/azurerm.compute/new-azurermimage). Olá, exemplo a seguir cria uma imagem chamada *myImage* de uma VM denominada *myVM*.

Obtenha a máquina virtual de saudação. 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

Crie a configuração de imagem de saudação.

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

Crie imagem de saudação.

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-hello-image"></a>Criar VMs de imagem Olá

Agora que você tem uma imagem, você pode criar um ou mais novas VMs de imagem de saudação. Criando uma máquina virtual a partir de uma imagem personalizada é muito semelhante toocreating uma VM usando uma imagem do Marketplace. Quando você usar uma imagem do Marketplace, você tem tooinformation sobre imagem hello, provedor de imagens, oferta, SKU e versão. Com uma imagem personalizada, você precisa apenas tooprovide Olá ID de recurso de imagem personalizada hello. 

Olá script a seguir, criamos uma variável *$image* toostore informações sobre como usar o hello imagem personalizada [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) e, em seguida, usamos [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)e especifique a ID hello usando Olá *$image* variável que acabamos de criar. 

script Hello cria uma VM denominada *myVMfromImage* do nosso imagem personalizada em um novo grupo de recursos denominado *myResourceGroupFromImage* em Olá *Oeste dos EUA* local.


```powershell
$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

New-AzureRmResourceGroup -Name myResourceGroupFromImage -Location EastUS

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name "mypublicdns$(Get-Random)" `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4

  $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

  $nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$vmConfig = New-AzureRmVMConfig `
    -VMName myVMfromImage `
    -VMSize Standard_D1 | Set-AzureRmVMOperatingSystem -Windows `
        -ComputerName myComputer `
        -Credential $cred 

# Here is where we create a variable toostore information about hello image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want toocreate hello VM from and image and provide hello image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a>Gerenciamento de imagens 

Aqui estão alguns exemplos de tarefas comuns de gerenciamento de imagem e como toocomplete-los usando o PowerShell.

Liste todas as imagens por nome.

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

Exclua uma imagem. Este exemplo exclui Olá imagem chamada *myOldImage* de saudação *myResourceGroup*.

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você criou uma imagem de VM personalizada. Você aprendeu como:

> [!div class="checklist"]
> * Aplicar Sysprep e generalizar VMs
> * Criar uma imagem personalizada
> * Criar uma VM por meio de uma imagem personalizada
> * Lista todas as imagens de saudação em sua assinatura
> * Excluir uma imagem

Avançar toohello toolearn próximo de tutorial sobre máquinas virtuais como altamente disponíveis.

> [!div class="nextstepaction"]
> [Criar VMs altamente disponíveis](tutorial-availability-sets.md)



