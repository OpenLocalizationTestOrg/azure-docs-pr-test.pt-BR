---
title: "Exemplo de Script do PowerShell - instantâneo de exportação/copiar como conta de armazenamento tooa VHD em uma região diferente de aaaAzure | Microsoft Docs"
description: "Exemplo de Script do PowerShell do Azure - instantâneo de exportação/copiar como conta de armazenamento do VHD tooa na mesma região diferente"
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
ms.openlocfilehash: 3b3e38c6b06bfa1e117f4e913dfc09443a795196
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-powershell"></a>Exportação/copiar gerenciado instantâneos como conta de armazenamento tooa VHD em uma região diferente com o PowerShell

Esse script exporta uma conta de armazenamento gerenciado instantâneo tooa em uma região diferente. Ele gera primeiro Olá SAS URI do instantâneo hello e, em seguida, usa-toocopy-tooa conta de armazenamento em uma região diferente. Use esse backup de toomaintain script discos gerenciados em uma região diferente para recuperação de desastres.  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]


## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa a seguinte comandos toogenerate URI SAS para uma saudação de instantâneos e cópias gerenciada instantâneo tooa conta de armazenamento usando o URI de SAS. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [Grant-AzureRmSnapshotAccess](/powershell/module/azurerm.compute/New-AzureRmDisk) | Gera o URI de SAS para um instantâneo que seja usada toocopy-tooa conta de armazenamento. |
| [New-AzureStorageContext](/powershell/module/azure.storage/New-AzureStorageContext) | Cria um contexto de conta de armazenamento usando a chave e o nome da conta de saudação. Esse contexto pode ser usado tooperform operações de leitura/gravação na conta de armazenamento hello. |
| [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | Cópias Olá VHD subjacente de uma conta de armazenamento instantâneo tooa |

## <a name="next-steps"></a>Próximas etapas

[Criar um disco gerenciado com base em um VHD](./../scripts/storage-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[Criar uma máquina virtual com base em um disco gerenciado](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).

Exemplos de script do PowerShell de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
