---
title: "aaaAzure exemplo de Script CLI - criar uma máquina virtual com um VHD | Microsoft Docs"
description: "Amostra de script da CLI do Azure – criar uma VM usando um disco rígido virtual."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/09/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: ce39092697a51e4e8a8e59ba8eb919955f616458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a>Criar uma VM com um disco rígido virtual

Este exemplo cria uma máquina virtual usando um VHD.
Cria um grupo de recursos, uma conta de armazenamento e um contêiner, e em seguida, cria uma VM, carregando o contêiner de toohello VHD Olá.
Ele substitui Olá ssh pública da chave com sua chave pública para que você tenha acesso toohello VM.

Você precisará de um VHD inicializável.
Você pode baixar Olá VHD que usamos de https://azclisamples.blob.core.windows.net/vhds/sample.vhd ou usar seu próprio VHD. script Hello procura `~/sample.vhd`.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]

## <a name="clean-up-deployment"></a>Limpar implantação 

Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá comandos toocreate um grupo de recursos, máquina virtual, o conjunto de disponibilidade, balanceador de carga e todos os recursos relacionados a seguir. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az storage account list](https://docs.microsoft.com/cli/azure/storage/account#list) | Lista contas de armazenamento |
| [az storage account check-name](https://docs.microsoft.com/cli/azure/storage/account#check-name) | Verifica se um nome de conta de armazenamento é válido e se já não existe |
| [az storage account keys list](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | Lista de chaves para as contas de armazenamento Olá |
| [az storage blob exists](https://docs.microsoft.com/cli/azure/storage/blob#exists) | Verifica se o blob Olá existe |
| [az storage container create](https://docs.microsoft.com/cli/azure/storage/container#create) | Cria um contêiner em uma conta de armazenamento. |
| [az storage blob upload](https://docs.microsoft.com/cli/azure/storage/blob#upload) | Cria um blob no contêiner Olá Olá carregar VHD. |
| [az vm list](https://docs.microsoft.com/cli/azure/vm#list) | Usado com `--query` Verifique se o nome da VM hello está em uso. | 
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Cria máquinas virtuais de saudação. |
| [az vm access set-linux-user](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | Redefine Olá SSH toogive chave Olá atual usuário acesso toohello VM. |
| [az vm list-ip-addresses](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | Obtém o endereço IP Olá Olá VM que foi criado. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
