---
title: aaaAzure exemplo de Script CLI - criar uma VM do Windows Server | Microsoft Docs
description: "Exemplo de script da CLI do Azure - Criar uma máquina virtual do Windows Server"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: f4cb431a68c911f877f5af87c393849bd8d2676a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-hello-azure-cli"></a>Criar uma máquina virtual com hello CLI do Azure

Esse script cria uma Máquina Virtual do Azure que executa o Windows Server 2016. Depois de executar o script hello, você pode acessar a máquina virtual de saudação por meio de uma conexão de área de trabalho remota.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a>Limpar implantação 

Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá seguir comandos toocreate um grupo de recursos, a máquina virtual, e todos os recursos relacionados. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) | Cria uma sub-rede e uma rede virtual do Azure. |
| [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#create) | Cria um endereço IP público com um endereço IP estático e um nome DNS associado. |
| [az network nsg create](https://docs.microsoft.com/cli/azure/network/nsg#create) | Cria um grupo de segurança de rede (NSG), que é um limite de segurança entre a máquina de virtual de internet e Olá Olá. |
| [az network nic create](https://docs.microsoft.com/cli/azure/network/nic#create) | Cria uma placa de rede virtual e anexa-rede virtual toohello, sub-rede e NSG. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Cria a máquina virtual de saudação e conecta toohello placa de rede, a rede virtual, sub-rede e NSG. Esse comando também especifica Olá toobe de imagem de máquina virtual usada e as credenciais administrativas.  |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Exclui um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
