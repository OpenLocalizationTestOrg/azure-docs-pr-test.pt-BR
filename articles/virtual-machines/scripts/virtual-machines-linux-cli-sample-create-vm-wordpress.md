---
title: aaaAzure exemplo de Script CLI - criar uma VM do Linux com WordPress | Microsoft Docs
description: "Exemplo de script da CLI do Azure - Criar uma máquina virtual Linux com WordPress"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2c5c03d08b6d5d27eb8c505b1dbd817eda5f2fc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-wordpress"></a>Criar uma máquina virtual com WordPress

Esse script cria uma máquina virtual e, em seguida, usa Olá Máquina Virtual do Azure script personalizado extensão tooinstall WordPress. Após script hello em execução, você pode acessar o site de configuração do WordPress Olá em `http://<public IP of VM>/wordpress`. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a>Limpar implantação 

Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá seguir comandos toocreate um grupo de recursos, a máquina virtual, e todos os recursos relacionados. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Cria a máquina virtual de saudação e conecta toohello placa de rede, a rede virtual, sub-rede e NSG. Esse comando também especifica Olá toobe de imagem de máquina virtual usada e as credenciais administrativas.  |
| [az vm open-port](https://docs.microsoft.com/cli/azure/vm#open-port) | Cria um tooallow de regra de grupo de segurança de rede o tráfego de entrada. Neste exemplo, a porta 80 está aberta para tráfego HTTP. |
| [az vm extension set](https://docs.microsoft.com/cli/azure/vm#create) | Adicione a máquina virtual do hello extensão de Script personalizado toohello, que chama um script tooinstall WordPress. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Exclui um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
