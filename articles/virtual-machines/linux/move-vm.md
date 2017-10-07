---
title: aaaMove uma VM do Linux no Azure | Microsoft Docs
description: "Mova uma VM do Linux tooanother assinatura do Azure ou o grupo de recursos no modelo de implantação do Gerenciador de recursos de saudação."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d635f0a5-4458-4b95-a5f8-eed4f41eb4d4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 938d04234059111912f03e72d14dabd338bc0678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-linux-vm-tooanother-subscription-or-resource-group"></a>Mover um VM do Linux tooanother assinatura ou grupo de recursos
Este artigo orienta como toomove uma VM do Linux entre grupos de recursos ou assinaturas. Mover uma VM entre as assinaturas pode ser úteis se você tiver criado uma VM em uma assinatura pessoal e agora deseja toomove-assinatura tooyour da empresa.

> [!IMPORTANT]
>No momento, não é possível mover o Managed Disks. 
>
>Novas IDs de recurso são criados como parte da movimentação de saudação. Após hello VM tiver sido movida, você precisará tooupdate suas ferramentas e scripts toouse Olá novas IDs de recurso. 
> 
> 

## <a name="use-hello-azure-cli-toomove-a-vm"></a>Use Olá CLI do Azure toomove uma VM
toosuccessfully mover uma máquina virtual, é necessário toomove Olá VM e todos os seus recursos de suporte. Saudação de uso **Mostrar de grupo do azure** comando toolist todos os recursos de saudação em um grupo de recursos e suas IDs. Ele ajuda a saída de hello toopipe este tooa do arquivo de comando para que você pode copiar e colar Olá IDs em comandos posteriores.

    azure group show <resourceGroupName>

toomove uma máquina virtual e seu grupo de recursos de tooanother de recursos, use Olá **mover recursos do azure** comando CLI. saudação de exemplo a seguir mostra como toomove uma máquina virtual e os recursos mais comuns do hello requer. Usamos Olá **-i** parâmetro e passar uma separada por vírgulas lista (sem espaços) de IDs para Olá toomove de recursos.

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

Se você quiser toomove Olá VM e sua assinatura de recursos diferentes de tooa, adicione Olá **– destino subscriptionId &#60; destinationSubscriptionID &#62;** assinatura de destino do parâmetro toospecify hello.

Se você estiver trabalhando de saudação de Prompt de comando em um computador Windows, é necessário tooadd um  **$**  na frente dos nomes de variável hello quando você declará-los. Isso não é necessário no Linux.

Você será solicitado tooconfirm que você deseja toomove Olá o recurso especificado. Tipo **Y** tooconfirm que você deseja que os recursos de saudação do toomove.

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a>Próximas etapas
Você pode mover vários tipos diferentes de recursos entre grupos de recursos e assinaturas. Para obter mais informações, consulte [Mover grupo de recursos toonew de recursos ou assinatura](../../resource-group-move-resources.md).    

