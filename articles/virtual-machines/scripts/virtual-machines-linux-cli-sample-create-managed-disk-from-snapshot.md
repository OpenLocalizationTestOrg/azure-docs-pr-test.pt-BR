---
title: "aaaAzure exemplo de Script CLI - criar um disco gerenciado de um instantâneo | Microsoft Docs"
description: "Amostra de script da CLI do Azure – Criar um disco gerenciado com base em um instantâneo"
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
ms.openlocfilehash: 549692f5027b3f50b0dd89fe701ebbf0f51d6031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a>Criar um disco gerenciado com base em um instantâneo com a CLI

Esse script cria um disco gerenciado com base em um instantâneo. Use-toorestore uma máquina virtual de instantâneos do sistema operacional e discos de dados. Crie discos gerenciados do sistema operacional e de dados com base nos respectivos instantâneos e, em seguida, crie uma nova máquina virtual anexando os discos gerenciados. Restaure também discos de dados de uma VM existente anexando os discos de dados criados com base em instantâneos.


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]


## <a name="script-explanation"></a>Explicação sobre o script

Esse script usará os seguintes comandos toocreate um disco gerenciado de um instantâneo. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [az snapshot show](https://docs.microsoft.com/cli/azure/snapshot#show) | Obtém todas as propriedades de saudação de um instantâneo usando o nome hello e propriedades de grupo de recursos de instantâneo de saudação. Propriedade ID é um disco gerenciado toocreate usado.  |
| [az disk create](https://docs.microsoft.com/cli/azure/disk#create) | Cria um disco gerenciado usando a Id de instantâneo de um instantâneo gerenciado |

## <a name="next-steps"></a>Próximas etapas

[Criar uma máquina virtual anexando um disco gerenciado como disco do SO](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Máquinas virtuais adicionais e exemplos de script CLI de discos gerenciados podem ser encontrados no hello [documentação de VM do Linux Azure](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
