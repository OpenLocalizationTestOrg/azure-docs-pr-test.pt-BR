---
title: "aaaMove um recurso de máquina virtual do Windows no Azure | Microsoft Docs"
description: "Mova uma máquina virtual do Windows tooanother assinatura do Azure ou o grupo de recursos no modelo de implantação do Gerenciador de recursos de saudação."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 859e78dce9acf1168780d4ee8e9f6dac0e3c11cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-tooanother-azure-subscription-or-resource-group"></a>Mover uma máquina virtual do Windows tooanother assinatura do Azure ou o grupo de recursos
Este artigo orienta como toomove uma VM do Windows entre grupos de recursos ou assinaturas. Mover entre assinaturas pode ser úteis se você criou uma VM em uma assinatura pessoal e agora deseja toomove-toocontinue de assinatura da empresa tooyour seu trabalho.

> [!IMPORTANT]
>No momento, não é possível mover o Managed Disks. 
>
>Novas IDs de recurso são criados como parte da movimentação de saudação. Após hello VM tiver sido movida, você precisará tooupdate suas ferramentas e scripts toouse Olá novas IDs de recurso. 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-toomove-a-vm"></a>Use o Powershell toomove uma VM
toomove um grupo de recursos de tooanother da máquina virtual, você precisa toomake-se de que você mova também todos os recursos dependentes hello. toouse Olá Move-AzureRMResource cmdlet, que você precisa que o nome do recurso hello e Olá tipo de recurso. Você pode obter ambos Olá Find-AzureRMResource cmdlet.

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


toomove uma VM que precisamos toomove vários recursos. Podemos criar variáveis separadas para cada recurso e depois listá-las. Este exemplo inclui a maioria dos recursos básicos de saudação para uma VM, mas você pode adicionar mais conforme necessário.

    $sourceRG = "<sourceResourceGroupName>"
    $destinationRG = "<destinationResourceGroupName>"

    $vm = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Compute/virtualMachines" -ResourceName "<vmName>"
    $storageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<storageAccountName>"
    $diagStorageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<diagnosticStorageAccountName>"
    $vNet = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/virtualNetworks" -ResourceName "<vNetName>"
    $nic = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkInterfaces" -ResourceName "<nicName>"
    $ip = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/publicIPAddresses" -ResourceName "<ipName>"
    $nsg = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkSecurityGroups" -ResourceName "<nsgName>"

    Move-AzureRmResource -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId

toomove Olá assinatura de recursos de toodifferent, incluir Olá **- DestinationSubscriptionId** parâmetro. 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



Você será solicitado tooconfirm que você deseja toomove Olá especificado recursos. Tipo **Y** tooconfirm que você deseja que os recursos de saudação do toomove.

## <a name="next-steps"></a>Próximas etapas
Você pode mover vários tipos diferentes de recursos entre grupos de recursos e assinaturas. Para obter mais informações, consulte [Mover grupo de recursos toonew de recursos ou assinatura](../../resource-group-move-resources.md).    

