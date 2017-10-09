---
title: aaaAzure exemplo de Script do PowerShell - criar um disco gerenciado de um arquivo VHD em uma conta de armazenamento na assinatura iguais ou diferente | Microsoft Docs
description: "Amostra de script do Azure PowerShell – Criar um disco gerenciado com base em um arquivo VHD em uma conta de armazenamento na mesma assinatura ou em outra assinatura"
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
ms.openlocfilehash: 47acff274cdf79d6fc3cd685cda01cad3d14ca8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a>Criar um disco gerenciado com base em um arquivo VHD em uma conta de armazenamento na mesma assinatura ou em outra assinatura com o PowerShell

Esse script cria um disco gerenciado com base em um arquivo VHD em uma conta de armazenamento na mesma assinatura ou em outra assinatura. Use este script tooimport um especializado toocreate de disco do toomanaged SO de VHD (não generalizado/com Sysprep) uma máquina virtual. Além disso, use tooimport um disco de dados toomanaged dados VHD. 

Não crie vários discos gerenciados idênticos com base em um arquivo VHD em um curto período. toocreate discos gerenciado de um arquivo vhd, instantâneo de blob do arquivo de vhd Olá é criado e, em seguida, é usado toocreate gerenciado discos. Instantâneo de blob apenas uma pode ser criado em um minuto que causa falhas na criação do disco toothrottling vencimento. tooavoid essa limitação, criar um [gerenciado instantâneo de arquivo de vhd Olá](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) e, em seguida, use Olá gerenciados instantâneo toocreate vários discos gerenciados em curto período de tempo. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]


## <a name="script-explanation"></a>Explicação sobre o script

Esse script usará os seguintes comandos toocreate um disco gerenciado em um VHD em assinatura diferente. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Cria a configuração do disco que é usada para criação do disco. Ele inclui o tipo de armazenamento, local, Id Olá da conta de armazenamento onde o VHD pai de saudação está armazenada, URI do VHD de VHD pai de saudação do recurso. |
| [New-AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | Cria um disco utilizando a configuração do disco, o nome do disco e o nome do grupo de recursos passados como parâmetros. |

## <a name="next-steps"></a>Próximas etapas

[Criar uma máquina virtual anexando um disco gerenciado como disco do SO](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).

Exemplos de script do PowerShell de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
