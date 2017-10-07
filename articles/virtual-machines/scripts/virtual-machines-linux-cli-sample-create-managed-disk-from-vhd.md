---
title: aaaAzure exemplo de Script CLI - criar um disco gerenciado de um arquivo VHD em uma conta de armazenamento no hello mesma assinatura | Microsoft Docs
description: Script CLI do Azure de exemplo - criar um disco gerenciado de um arquivo VHD em uma conta de armazenamento no hello mesma assinatura
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
ms.openlocfilehash: 6cfb3c54a7692b0f3999c585861340c1a6b4d348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-hello-same-subscription-with-cli"></a>Criar um disco gerenciado de um arquivo VHD em uma conta de armazenamento no hello mesma assinatura com a CLI

Esse script cria um disco gerenciado de um arquivo VHD em uma conta de armazenamento no hello mesma assinatura. Use este script tooimport um especializado toocreate de disco do toomanaged SO de VHD (não generalizado/com Sysprep) uma máquina virtual. Ou então, usá-lo tooimport um disco de dados toomanaged dados VHD. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]


## <a name="script-explanation"></a>Explicação sobre o script

Esse script usará os seguintes comandos toocreate um disco gerenciado em um VHD. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [az disk create](https://docs.microsoft.com/cli/azure/disk#create) | Cria um disco gerenciado usando o URI de um VHD em uma conta de armazenamento no hello mesma assinatura |

## <a name="next-steps"></a>Próximas etapas

[Criar uma máquina virtual anexando um disco gerenciado como disco do SO](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Máquinas virtuais adicionais e exemplos de script CLI de discos gerenciados podem ser encontrados no hello [documentação de VM do Linux Azure](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
