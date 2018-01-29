---
title: "Amostra de script da CLI do Azure – Reinicializar VMs | Microsoft Docs"
description: "Amostra de script da CLI do Azure – Reinicializar VMs por marcação e ID"
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
ms.date: 03/01/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: ea114f484c774573b7d219cff9102a7308af356e
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2017
---
# <a name="restart-vms"></a>Reiniciar VMs

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

Este exemplo mostra duas maneiras para obter algumas VMs e reiniciá-las.

A primeira reinicia todas as VMs no grupo de recursos.

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

A segunda obtém as VMs marcadas usando `az resouce list`, filtra os recursos que são VMs e reinicia essas VMs.

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

Este exemplo funciona em um shell Bash. Para opções sobre como executar scripts da CLI do Azure no cliente Windows, veja [Execução da CLI do Azure no Windows](../windows/cli-options.md).


## <a name="sample-script"></a>Script de exemplo

A amostra tem três scripts.
O primeiro provisiona as máquinas virtuais.
Ele usa a opção de não espera para que o comando retorne sem aguardar em cada VM a ser provisionada.
O segundo aguarda que as VMs seja totalmente provisionadas.
O terceiro script reinicia todas as VMs que foram provisionadas e, em seguida, apenas as VMs marcadas.

### <a name="provision-the-vms"></a>Provisionar as VMs

Esse script cria um grupo de recursos e, em seguida, cria três VMs para reiniciar.
Duas delas são marcadas.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision the VMs")]

### <a name="wait"></a>Aguarde

Esse script verifica o status de provisionamento a cada 20 segundos até que todas as três VMs sejam provisionadas ou uma delas falhe ao ser provisionada.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for the VMs to be provisioned")]

### <a name="restart-the-vms"></a>Reiniciar as VMs

Esse script reinicia todas as VMs no grupo de recursos e então reinicia apenas as VMs marcadas.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a>Limpar implantação 

Após a execução da amostra de script, o comando a seguir pode ser usado para remover os grupos de recursos, as VMs e todos os recursos relacionados.

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa os seguintes comandos para criar um grupo de recursos, uma máquina virtual, um conjunto de disponibilidade, um balanceador de carga e todos os recursos relacionados. Cada comando na tabela redireciona para a documentação específica do comando.

| Command | Observações |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#az_group_create) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#az_vm_availability_set_create) | Cria as máquinas virtuais.  |
| [az vm list](https://docs.microsoft.com/cli/azure/vm#az_vm_list) | Usado com `--query` para garantir que as VMs sejam provisionadas antes de reiniciá-las e, em seguida, para obter as IDs das VMs para reiniciá-las. |
| [az resource list](https://docs.microsoft.com/cli/azure/vm#az_vm_list) | Usado com `--query` para obter as IDs das VMs usando a marcação. |
| [az vm restart](https://docs.microsoft.com/cli/azure/vm#az_vm_list) | Reinicia as VMs. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#az_vm_extension_set) | Exclui um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Os exemplos de script da CLI de máquina virtual adicionais podem ser encontrados na [documentação da VM Linux do Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
