---
title: aaaAzure exemplo de Script CLI - Gerenciando Pools em lote | Microsoft Docs
description: "Amostra de Script da CLI do Azure – Gerenciando Pools no Lote"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 6c9ca9515565aff42752231a080943be8e4c810b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a>Gerenciando pools do Lote do Azure com CLI do Azure

Esses scripts demonstra algumas das ferramentas de saudação disponíveis no hello CLI do Azure toocreate e gerenciar pools de nós de computação no serviço de lote do Azure hello.

> [!NOTE]
> comandos de saudação neste exemplo criam máquinas virtuais do Azure. VMs em execução se acumulam cobra tooyour conta. toominimize esses encargos, excluir VMs hello quando você terminar de exemplo de hello em execução. Consulte [Limpar pools](#clean-up-pools).

Pools de Lote podem ser configurados de duas maneiras, com uma configuração de Serviços de Nuvem (somente Windows) ou com uma configuração de Máquina Virtual (Windows e Linux). scripts de exemplo Hello abaixo mostram como pools de toocreate com ambas as configurações.

## <a name="prerequisites"></a>Pré-requisitos

- Instalar Olá CLI do Azure com instruções Olá no hello [guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), se você ainda não tiver feito isso.
- Crie uma conta do lote do Azure caso ainda não tenha uma. Consulte [criar uma conta de lote com hello CLI do Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) para um script de exemplo que cria uma conta.
- Se você ainda não tiver feito isso, configure toorun um aplicativo de uma tarefa de início. Consulte [adicionar aplicativos tooAzure lote com a CLI do Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) para um script de exemplo que cria um aplicativo e os carrega um tooAzure do pacote de aplicativo.

## <a name="pool-with-cloud-service-configuration-sample-script"></a>Pool com o script de exemplo de configuração de serviço de nuvem

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a>Pool com o script de exemplo de configuração de máquina virtual

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]

## <a name="clean-up-pools"></a>Limpar pools

Depois de executar Olá acima script de exemplo, execute Olá seguintes pools de saudação do comando toodelete.
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá toocreate comandos a seguir e manipular os pools de lote.
Cada comando na tabela Olá vincula a documentação específica do toocommand.

| Command | Observações |
|---|---|
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | Autentique em uma conta do Lote.  |
| [az batch application summary list](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | Lista os aplicativos disponíveis na conta do lote de saudação hello.  |
| [az batch pool create](https://docs.microsoft.com/cli/azure/batch/pool#create) | Crie um pool de VMs.  |
| [az batch pool set](https://docs.microsoft.com/cli/azure/batch/pool#set) | Atualize as propriedades de um pool.  |
| [az batch pool node-agent-skus list](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | Liste as informações de imagem e SKUs do agente de nó disponíveis.  |
| [az batch pool resize](https://docs.microsoft.com/cli/azure/batch/pool#resize) | Redimensionamento Olá número de VMs em execução Olá especificado pool.  |
| [az batch pool show](https://docs.microsoft.com/cli/azure/batch/pool#show) | Exibir as propriedades de saudação de um pool.  |
| [az batch pool delete](https://docs.microsoft.com/cli/azure/batch/pool#delete) | Excluir Olá especificado pool.  |
| [az batch pool autoscale enable](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | Habilite o dimensionamento automático em um pool e aplique uma fórmula.  |
| [az batch pool autoscale disable](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | Desabilite o dimensionamento automático em um pool.  |
| [az batch node list](https://docs.microsoft.com/cli/azure/batch/node#list) | Lista todos os nó de computação Olá Olá especificado pool.  |
| [az batch node reboot](https://docs.microsoft.com/cli/azure/batch/node#reboot) | Reinicialize o nó de computação especificado hello.  |
| [az batch node delete](https://docs.microsoft.com/cli/azure/batch/node#delete) | Excluir Olá listado nós de saudação especificado pool.  |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script em lotes CLI adicionais podem ser encontrados no hello [documentação CLI de lote do Azure](../batch-cli-samples.md).

