---
title: "aaaAzure exemplo de Script CLI - criar uma máquina virtual de um instantâneo | Microsoft Docs"
description: "Exemplo de script da CLI do Azure – Criar uma VM de um instantâneo"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: ddc95289dcb8a0ca7c7854d969983f96b8f4613f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-cli"></a>Criar uma máquina virtual de um instantâneo com a CLI

Esse script cria uma máquina virtual de um instantâneo de um disco do sistema operacional.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.sh "Create VM from snapshot")]

## <a name="clean-up-deployment"></a>Limpar implantação 

Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá seguir comandos toocreate um disco gerenciado, máquina virtual, e todos os recursos relacionados. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [az snapshot show](https://docs.microsoft.com/cli/azure/snapshot#show) | Obtém o instantâneo usando o nome do instantâneo e o nome do grupo de recursos. Propriedade de ID de objeto retornado de hello é usado toocreate um disco gerenciado.  |
| [az disk create](https://docs.microsoft.com/cli/azure/disk#create) | Cria discos gerenciados de um instantâneo usando ID de instantâneo, nome do disco, tipo de armazenamento e tamanho  |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Cria uma VM usando um disco do sistema operacional gerenciado |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
