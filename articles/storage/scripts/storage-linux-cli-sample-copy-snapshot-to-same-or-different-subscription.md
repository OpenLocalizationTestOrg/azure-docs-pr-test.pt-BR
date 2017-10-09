---
title: "Exemplo de Script CLI - instantâneo de cópia (mover) de um disco gerenciado toosame ou assinatura diferente com CLI de aaaAzure | Microsoft Docs"
description: "Exemplo de Script CLI do Azure - instantâneo de cópia (mover) de um disco gerenciado toosame ou assinatura diferente com CLI"
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
ms.openlocfilehash: 4a21fd2435181a033b563100888aba0c5834496d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-toosame-or-different-subscription-with-cli"></a>Copiar um instantâneo de um disco gerenciado toosame ou uma assinatura diferente com CLI

Esse script copia um instantâneo de um disco gerenciado toosame ou uma assinatura diferente. Use toomove este script uma assinatura do instantâneo toodifferent Olá mesma região que o instantâneo do hello pai.


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]


## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa a seguinte comandos toocreate um instantâneo na assinatura de destino hello usando Olá Id do instantâneo de origem hello. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [az snapshot show](https://docs.microsoft.com/cli/azure/snapshot#show) | Obtém todas as propriedades de saudação de um instantâneo usando o nome hello e propriedades de grupo de recursos de instantâneo de saudação. Propriedade ID é usada toocopy Olá instantâneo toodifferent assinatura.  |
| [az snapshot create](https://docs.microsoft.com/cli/azure/snapshot#create) | Copia um instantâneo ao criar um instantâneo na assinatura diferente usando Olá Id e nome do hello instantâneo pai.  |

## <a name="next-steps"></a>Próximas etapas

[Criar uma máquina virtual com base em um instantâneo](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Máquinas virtuais adicionais e exemplos de script CLI de discos gerenciados podem ser encontrados no hello [documentação de VM do Linux Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
