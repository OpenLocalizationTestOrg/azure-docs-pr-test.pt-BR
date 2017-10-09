---
title: aaaAzure exemplo de Script CLI - VMs reiniciar | Microsoft Docs
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
ms.openlocfilehash: a1ae07bd1d2be906553bef817385a4a333a10eca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restart-vms"></a>Reiniciar VMs

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

Este exemplo mostra duas maneiras tooget algumas VMs e reiniciá-los.

Olá primeiro reinicia todas as VMs Olá no grupo de recursos de saudação.

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

saudação de segundo obtém Hello marcados VMs usando `az resouce list` filtra toohello recursos que são as VMs e reinicia nessas VMs.

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

Este exemplo funciona em um shell Bash. Para obter opções sobre a execução de scripts de CLI do Azure no cliente do Windows, consulte [em execução Olá CLI do Azure no Windows](../windows/cli-options.md).


## <a name="sample-script"></a>Script de exemplo

exemplo Hello tem três scripts.
Olá um primeiro provisionar Olá máquinas virtuais.
Ele usa a opção de não-espera Olá comando Olá retorna sem esperar em cada toobe VM provisionado.
Olá segundo aguarda Olá VMs toobe totalmente provisionado.
script de terceiro Olá reinicia todas as VMs de saudação que foram provisionadas e, em seguida, basta Olá marcados VMs.

### <a name="provision-hello-vms"></a>Saudação de provisionar máquinas virtuais

Esse script cria um grupo de recursos e, em seguida, ele cria três toorestart de VMs.
Duas delas são marcadas.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision hello VMs")]

### <a name="wait"></a>Aguarde

Esse script verifica no hello cada 20 segundos até que todas as três VMs são provisionadas ou um deles falha tooprovision do status de provisionamento.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for hello VMs toobe provisioned")]

### <a name="restart-hello-vms"></a>Reiniciar Olá VMs

Esse script reinicia todas as VMs Olá no grupo de recursos de saudação e reinicia apenas Olá marcado VMs.

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a>Limpar implantação 

Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove Olá os grupos de recursos, VMs e recursos todos relacionados.

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá comandos toocreate um grupo de recursos, máquina virtual, o conjunto de disponibilidade, balanceador de carga e todos os recursos relacionados a seguir. Cada comando na documentação específica do toocommand Olá tabela links.

| Command | Observações |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Cria máquinas virtuais de saudação.  |
| [az vm list](https://docs.microsoft.com/cli/azure/vm#list) | Usado com `--query` tooensure Olá VMs são provisionados antes de reiniciá-los e, em seguida, tooget Olá IDs de saudação VMs toorestart-los. |
| [az resource list](https://docs.microsoft.com/cli/azure/vm#list) | Usado com `--query` tooget Olá IDs de VMs hello usando Olá marca. |
| [az vm restart](https://docs.microsoft.com/cli/azure/vm#list) | Reinicia Olá VMs. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Exclui um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script CLI de máquinas virtuais adicionais podem ser encontrados no hello [documentação de VM do Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
