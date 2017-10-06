---
title: aaaAvailability define o tutorial para VMs do Windows no Azure | Microsoft Docs
description: "Saiba mais sobre Olá disponibilidade conjuntos para máquinas virtuais do Windows no Azure."
documentationcenter: 
services: virtual-machines-windows
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
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 853775c5f126dd815c1933f9d71d2274a75ea661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a>Como os conjuntos de disponibilidade de toouse

Neste tutorial, você aprenderá como a disponibilidade de saudação tooincrease e a confiabilidade de suas soluções de máquina Virtual no Azure usando um recurso chamado conjuntos de disponibilidade. Conjuntos de disponibilidade garantem que Olá VMs implantar no Azure são distribuídas entre vários clusters de hardware isoladas. Isso garante que, se ocorre uma falha de hardware ou software no Azure, um sub conjunto das suas máquinas virtuais será afetado e que sua solução geral permanecerão disponíveis e operacionais da perspectiva de saudação de seus clientes usá-lo. 

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Criar um conjunto de disponibilidade
> * Criar uma VM em um conjunto de disponibilidade
> * Verificar os tamanhos de VM disponíveis

Este tutorial requer hello Azure PowerShell versão 3.6 ou posterior do módulo. Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação. Se você precisar tooupgrade, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).

## <a name="availability-set-overview"></a>Visão geral do conjunto de disponibilidade

Um conjunto de disponibilidade é um recurso de agrupamento lógico que você pode usar no Azure tooensure que recursos VM Olá que colocar nele são isolados uma da outra quando eles forem implantados em um datacenter do Azure. Azure garante que as VMs que você coloca em um conjunto de disponibilidade executado em vários servidores físicos hello, comutadores de rede, unidades de armazenamento e racks de computação. Isso garante que no caso de saudação de um hardware ou falha de software do Azure, apenas um subconjunto das suas máquinas virtuais será afetado, e geral do seu aplicativo irá continuar e continuar toobe tooyour disponíveis clientes. Usando conjuntos de disponibilidade é um recurso essencial tooleverage toobuild soluções de nuvem confiável.

Vamos considerar uma solução comum baseada em VM na qual você pode ter quatro servidores Web front-end e usar duas VMs de back-end que hospedam um banco de dados. Com o Azure, você desejaria toodefine dois conjuntos de disponibilidade antes de implantar suas VMs: conjunto de disponibilidade de um para nível de "web" hello e um conjunto de disponibilidade para camada de "banco de dados" hello. Quando você cria uma nova VM, em seguida, você pode especificar disponibilidade Olá definida como uma vm do parâmetro toohello az criar comando e Azure automaticamente garantirá que Olá VMs criar dentro Olá disponível conjunto são isolados em vários recursos de hardware físico. Isso significa que, se o hardware físico de saudação que seu servidor Web ou VMs de servidor de banco de dados está em execução no tem um problema, você sabe que Olá outras instâncias do servidor Web e VMs de banco de dados continuará em execução bem porque eles estão em um hardware diferente.

Quando você quiser toodeploy soluções confiáveis de VM com base no Azure, você sempre deve usar conjuntos de disponibilidade.

## <a name="create-an-availability-set"></a>Criar um conjunto de disponibilidade

Você pode criar um conjunto de disponibilidade usando [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset). Neste exemplo, vamos definir ambos de número de domínios de atualização e falha no hello *2* para o conjunto nomeada de disponibilidade de saudação *myAvailabilitySet* em Olá *myResourceGroupAvailability*grupo de recursos.

Crie um grupos de recursos.

```powershell
New-AzureRmResourceGroup -Name myResourceGroupAvailability -Location EastUS
```


```powershell
New-AzureRmAvailabilitySet `
   -Location EastUS `
   -Name myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability `
   -Managed `
   -PlatformFaultDomainCount 2 `
   -PlatformUpdateDomainCount 2
```

## <a name="create-vms-inside-an-availability-set"></a>Criar VMs dentro de um conjunto de disponibilidade

VMs necessário toobe criado no hello-se de que eles sejam distribuídos corretamente em hardware de saudação de toomake de conjunto de disponibilidade. Não é possível adicionar um grupo de disponibilidade de tooan VM definida depois que ela é criada. 

hardware de saudação em um local é dividida em domínios de atualização toomultiple e domínios de falha. Um **domínio de atualização** é um grupo de VMs e o hardware físico subjacente que pode ser reinicializado no hello simultaneamente. Olá de VMs no mesmo **domínio de falha** compartilhar armazenamento comuns, bem como um comutador de origem e de rede de alimentação comum. 

Quando você cria uma VM usando a configuração usando [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) especificar Olá conjunto de disponibilidade usando Olá `-AvailabilitySetId` parâmetro toospecify Olá ID do conjunto de disponibilidade de saudação.

Criar 2 VMs com [AzureRmVM novo](/powershell/module/azurerm.compute/new-azurermvm) no conjunto de disponibilidade de saudação.

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAvailability `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

for ($i=1; $i -le 2; $i++)
{
   $pip = New-AzureRmPublicIpAddress `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name "mypublicdns$(Get-Random)" `
        -AllocationMethod Static `
        -IdleTimeoutInMinutes 4

   $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
        -Name myNetworkSecurityGroupRuleRDP$i `
        -Protocol Tcp `
        -Direction Inbound `
        -Priority 1000 `
        -SourceAddressPrefix * `
        -SourcePortRange * `
        -DestinationAddressPrefix * `
        -DestinationPortRange 3389 `
        -Access Allow

   $nsg = New-AzureRmNetworkSecurityGroup `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name myNetworkSecurityGroup$i `
        -SecurityRules $nsgRuleRDP

   $nic = New-AzureRmNetworkInterface `
        -Name myNic$i `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -SubnetId $vnet.Subnets[0].Id `
        -PublicIpAddressId $pip.Id `
        -NetworkSecurityGroupId $nsg.Id

   # Here is where we specify hello availability set
   $vm = New-AzureRmVMConfig `
        -VMName myVM$i `
        -VMSize Standard_D1 `
        -AvailabilitySetId $availabilitySet.Id

   $vm = Set-AzureRmVMOperatingSystem `
        -VM $vm `
        -Windows -ComputerName myVM$i `   
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage `
        -VM $vm `
        -PublisherName MicrosoftWindowsServer `
        -Offer WindowsServer `
        -Skus 2016-Datacenter `
        -Version latest
   $vm = Set-AzureRmVMOSDisk `
        -VM $vm `
        -Name myOsDisk$i `
        -DiskSizeInGB 128 `
        -CreateOption FromImage `
        -Caching ReadWrite
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -VM $vm
}

```

Ele usa toocreate de alguns minutos e configurar as duas máquinas virtuais. Quando terminar, você terá 2 máquinas virtuais distribuídas Olá hardware subjacente. 

## <a name="check-for-available-vm-sizes"></a>Conferir os tamanhos de VM disponíveis 

Você pode adicionar mais máquinas virtuais toohello conjunto de disponibilidade posteriormente, mas é necessário tooknow quais tamanhos VM estão disponíveis em hardware de saudação. Use [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist todos os tamanhos disponíveis de Olá em hardware de saudação do cluster para o conjunto de disponibilidade hello.

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como:

> [!div class="checklist"]
> * Criar um conjunto de disponibilidade
> * Criar uma VM em um conjunto de disponibilidade
> * Verificar os tamanhos de VM disponíveis

Avançar toohello toolearn próximo de tutorial sobre conjuntos de escala de máquina virtual.

> [!div class="nextstepaction"]
> [Criar um conjunto de dimensionamento da VM](tutorial-create-vmss.md)


