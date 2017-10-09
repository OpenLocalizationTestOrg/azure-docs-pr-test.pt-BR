---
title: "aaaAzure exemplo de Script do PowerShell - criar um disco gerenciado de um instantâneo | Microsoft Docs"
description: "Amostra de script do Azure PowerShell – Criar um disco gerenciado com base em um instantâneo"
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
ms.openlocfilehash: 4fa34a8d6c67171083fba9a9ad73ecca5e0f0229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a>Criar um disco gerenciado com base em um instantâneo com o PowerShell

Esse script cria um disco gerenciado com base em um instantâneo. Use-toorestore uma máquina virtual de instantâneos do sistema operacional e discos de dados. Crie discos gerenciados do sistema operacional e de dados com base nos respectivos instantâneos e, em seguida, crie uma nova máquina virtual anexando os discos gerenciados. Restaure também discos de dados de uma VM existente anexando os discos de dados criados com base em instantâneos.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Create managed disk from snapshot")]


## <a name="script-explanation"></a>Explicação sobre o script

Esse script usará os seguintes comandos toocreate um disco gerenciado de um instantâneo. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [Get-AzureRmSnapshot](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | Obtém as propriedades do instantâneo.  |
| [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Cria a configuração do disco que é usada para criação do disco. Ele inclui recursos Olá Id do instantâneo Olá pai local que é o mesmo local de saudação do tipo de armazenamento de instantâneo e hello pai.  |
| [New-AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | Cria um disco utilizando a configuração do disco, o nome do disco e o nome do grupo de recursos passados como parâmetros. |


## <a name="next-steps"></a>Próximas etapas

[Criar uma máquina virtual com base em um disco gerenciado](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).

Exemplos de script do PowerShell de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
