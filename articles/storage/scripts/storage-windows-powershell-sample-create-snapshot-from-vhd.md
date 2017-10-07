---
title: "aaaAzure exemplo de Script do PowerShell - criar um instantâneo de um VHD toocreate vários discos gerenciados idênticos em pouco tempo | Microsoft Docs"
description: "Script do PowerShell do Azure de exemplo - criar um instantâneo de um VHD toocreate vários discos gerenciados idênticos em pouco tempo"
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: 0a13e399b692f32b3772add39fe5b5c023808c5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-snapshot-from-a-vhd-toocreate-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a>Criar um instantâneo de um VHD toocreate vários discos gerenciados idênticos em pouco tempo com o PowerShell

Esse script cria um instantâneo de um arquivo VHD em uma conta de armazenamento na mesma assinatura ou em uma diferente. Use este script tooimport um instantâneo de tooa especializado (não generalizado/com Sysprep) VHD e use Olá instantâneo toocreate vários discos gerenciados idênticos em pouco tempo. Além disso, use tooimport um instantâneo dos dados VHD tooa e use Olá instantâneo toocreate vários discos gerenciados em pouco tempo. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/storage/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]


## <a name="script-explanation"></a>Explicação sobre o script

Esse script usará os seguintes comandos toocreate um disco gerenciado em um VHD em assinatura diferente. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Cria a configuração do disco que é usada para criação do disco. Inclui o tipo de armazenamento, local, Id Olá da conta de armazenamento onde está armazenado o VHD pai de saudação do recurso e URI do VHD do pai Olá VHD. |
| [New-AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | Cria um disco utilizando a configuração do disco, o nome do disco e o nome do grupo de recursos passados como parâmetros. |

## <a name="next-steps"></a>Próximas etapas

[Criar um disco gerenciado a partir do instantâneo](./../../storage/scripts/storage-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[Criar uma máquina virtual anexando um disco gerenciado como disco do SO](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).

Exemplos de script do PowerShell de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
