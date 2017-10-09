---
title: "aaaAzure exemplo de Script CLI - criar uma máquina virtual, anexando um disco gerenciado como disco do sistema operacional | Microsoft Docs"
description: "Exemplo de script da CLI do Azure – Criar uma VM, anexando um disco gerenciado como disco do sistema operacional"
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
ms.openlocfilehash: 71fc5c6a577c64b913cfa35e99b2b9b75dea0c31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a>Criar uma máquina virtual usando um disco de sistema operacional gerenciado existente com a CLI

Esse script cria uma máquina virtual anexando um disco gerenciado existente como disco do sistema operacional. Use esse script em cenários anteriores:
* Criar uma VM de um disco de sistema operacional gerenciado existente que foi copiado de um disco gerenciado em uma assinatura diferente
* Criar uma VM de um disco gerenciado existente que foi criado de um arquivo VHD especializado 
* Criar uma VM de um disco do sistema operacional gerenciado existente que foi criado de um instantâneo 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]

## <a name="clean-up-deployment"></a>Limpar implantação 

Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá comandos tooget gerenciado disco propriedades a seguir, anexar um disco gerenciado tooa nova VM e criar uma máquina virtual. Cada item na tabela de saudação vincula a documentação específica do toocommand.

| Command | Observações |
|---|---|
| [az disk show](https://docs.microsoft.com/cli/azure/disk#show) | Obtém propriedades de disco gerenciado usando o nome do disco e o nome do grupo de recursos. Propriedade ID é usada tooattach tooa um disco gerenciado nova VM |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Cria uma VM usando um disco do sistema operacional gerenciado |
## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
