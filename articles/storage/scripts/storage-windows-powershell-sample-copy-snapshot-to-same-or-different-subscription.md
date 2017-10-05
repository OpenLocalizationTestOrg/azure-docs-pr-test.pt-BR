---
title: "Amostra de script do Azure PowerShell – Copiar (mover) um instantâneo de um disco gerenciado para a mesma assinatura ou outra assinatura | Microsoft Docs"
description: "Amostra de script do Azure PowerShell – Copiar (mover) um instantâneo de um disco gerenciado para a mesma assinatura ou outra assinatura"
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
ms.date: 06/06/2017
ms.author: ramankum
ms.openlocfilehash: 69b9b4ed86117f7fe561e7e70227e60e6a9d858e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a>Copiar um instantâneo de um disco gerenciado para a mesma assinatura ou outra assinatura com o PowerShell

Esse script cria uma cópia de um instantâneo na mesma assinatura ou em outra assinatura. Use esse script para mover um instantâneo para outra assinatura para a retenção de dados. O armazenamento de instantâneos em outra assinatura protege contra a exclusão acidental de instantâneos em sua assinatura principal. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copiar instantâneo")]


## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa os comandos a seguir para criar um instantâneo na assinatura de destino usando a ID do instantâneo de origem. Cada comando na tabela redireciona para a documentação específica do comando.

| Command | Observações |
|---|---|
| [New-AzureRmSnapshotConfig](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | Cria uma configuração de instantâneo que é usada para a criação do instantâneo. Inclui a ID do recurso do instantâneo pai e o local que é o mesmo local do instantâneo pai.  |
| [New-AzureRmSnapshot](/powershell/module/azurerm.compute/New-AzureRmDisk) | Cria um instantâneo usando uma configuração de instantâneo, o nome do instantâneo e o nome do grupo de recursos passados como parâmetros. |


## <a name="next-steps"></a>Próximas etapas

[Criar uma máquina virtual com base em um instantâneo](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Para obter mais informações sobre o módulo do Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).

Amostras de script do PowerShell da máquina virtual adicionais podem ser encontrados na [documentação da VM Windows do Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).