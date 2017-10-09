---
title: aaaAzure exemplo de Script CLI - Copy (mover) gerenciado toosame discos ou assinatura diferente | Microsoft Docs
description: Exemplo de Script CLI do Azure - Copy (mover) gerenciados discos toosame ou assinatura diferente
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: 8581169baa0fd0e0eec1c72eab77b657f48b1cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-toosame-or-different-subscription-with-cli"></a>Copiar toosame discos gerenciados ou uma assinatura diferente com CLI

Esse script copia um disco gerenciado toosame ou uma assinatura diferente, mas em Olá mesmo região. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli[main](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]


## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa a seguinte comandos toocreate um novo disco gerenciado na assinatura usando o destino Olá Olá Id da fonte de saudação gerenciados em disco. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [az disk show](https://docs.microsoft.com/cli/azure/disk#show) | Obtém todas as propriedades de saudação de um disco gerenciado usando as propriedades do grupo de recursos e o nome do hello de disco gerenciado hello. Propriedade ID é usada toocopy Olá gerenciado disco toodifferent assinatura.  |
| [az disk create](https://docs.microsoft.com/cli/azure/disk#create) | Copia um disco gerenciado ao criar um novo disco gerenciado na assinatura diferente usando Id e nome do pai Olá gerenciados em disco.  |

## <a name="next-steps"></a>Próximas etapas

[Criar uma máquina virtual com base em um disco gerenciado](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Máquinas virtuais adicionais e exemplos de script CLI de discos gerenciados podem ser encontrados no hello [documentação de VM do Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
