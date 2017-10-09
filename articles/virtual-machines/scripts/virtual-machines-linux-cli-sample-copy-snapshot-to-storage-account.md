---
title: "Exemplo de Script CLI - instantâneo de exportação/copiar como conta de armazenamento tooa VHD em uma região diferente de aaaAzure | Microsoft Docs"
description: "Exemplo de Script CLI do Azure - instantâneo de exportação/copiar como conta de armazenamento do VHD tooa na assinatura igual ou diferente"
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
ms.openlocfilehash: 945f83d2ed715642156ca7b252af08559c652b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-cli"></a>Exportação/copiar gerenciado instantâneos como conta de armazenamento tooa VHD em uma região diferente com CLI

Esse script exporta uma conta de armazenamento gerenciado instantâneo tooa em uma região diferente. Ele gera primeiro Olá SAS URI do instantâneo hello e, em seguida, usa-toocopy-tooa conta de armazenamento em uma região diferente. Use esse backup de toomaintain script discos gerenciados em uma região diferente para recuperação de desastres. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]


## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa a seguinte comandos toogenerate URI SAS para uma saudação de instantâneos e cópias gerenciada instantâneo tooa conta de armazenamento usando o URI de SAS. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [az snapshot grant-access](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | Gera SAS somente leitura que é usado toocopy conta de armazenamento de tooa de arquivo VHD de base ou baixá-lo tooon local  |
| [az storage blob copy start](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | Copia um blob de forma assíncrona de um tooanother de conta de armazenamento |

## <a name="next-steps"></a>Próximas etapas

[Criar um disco gerenciado com base em um VHD](virtual-machines-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[Criar uma máquina virtual com base em um disco gerenciado](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Máquinas virtuais adicionais e exemplos de script CLI de discos gerenciados podem ser encontrados no hello [documentação de VM do Linux Azure](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
