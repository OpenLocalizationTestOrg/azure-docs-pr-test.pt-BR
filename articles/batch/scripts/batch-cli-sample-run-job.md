---
title: aaaAzure exemplo de Script CLI - com um trabalho em lotes | Microsoft Docs
description: "Amostra de Script da CLI do Azure – Executar um trabalho com o Lote"
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
ms.openlocfilehash: f73a7cb341e550fd1c92f92201e20b27fa20d238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a>Executar trabalhos no Lote do Azure com a CLI do Azure

Esse script cria um trabalho em lotes e adiciona uma série de trabalho de toohello de tarefas. Ele também demonstra como toomonitor um trabalho e suas tarefas. Finalmente, ele mostra como tooquery Olá serviço de lote com eficiência para obter informações sobre tarefas de saudação do trabalho.

## <a name="prerequisites"></a>Pré-requisitos

- Instalar Olá CLI do Azure com instruções Olá no hello [guia de instalação da CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), se você ainda não tiver feito isso.
- Crie uma conta do lote do Azure caso ainda não tenha uma. Consulte [criar uma conta de lote com hello CLI do Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) para um script de exemplo que cria uma conta.
- Se você ainda não tiver feito isso, configure toorun um aplicativo de uma tarefa de início. Consulte [adicionar aplicativos tooAzure lote com a CLI do Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) para um script de exemplo que cria um aplicativo e os carrega um tooAzure do pacote de aplicativo.
- Configure um pool no qual Olá trabalho será executado. Consulte [Gerenciando pools de Lote do Azure com a CLI do Azure](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) para obter um script de exemplo que cria um pool com uma Configuração de serviço de nuvem ou uma Configuração de máquina virtual.

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-job"></a>Trabalho de limpeza

Depois de executar Olá acima script de exemplo, execute Olá tooremove de comando a seguir, o trabalho e todas as suas tarefas. Observe que o pool de saudação precisará toobe excluído separadamente. Consulte [Gerenciando pools de Lote do Azure com a CLI do Azure](./batch-cli-sample-manage-pool.md) para obter mais informações sobre como criar e excluir grupos.

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a>Explicação sobre o script

Esse script usa Olá toocreate comandos a seguir, um trabalho em lotes e tarefas. Cada comando na tabela Olá vincula a documentação específica do toocommand.

| Command | Observações |
|---|---|
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | Autentica em uma conta do Lote.  |
| [az batch job create](https://docs.microsoft.com/cli/azure/batch/job#create) | Cria um trabalho do Lote.  |
| [az batch job set](https://docs.microsoft.com/cli/azure/batch/job#set) | Atualiza as propriedades de um trabalho do Lote.  |
| [az batch job show](https://docs.microsoft.com/cli/azure/batch/job#show) | Recupera detalhes de um trabalho especificado do Lote.  |
| [az batch task create](https://docs.microsoft.com/cli/azure/batch/task#create) | Adiciona que uma tarefa toohello especificado trabalho em lotes.  |
| [az batch task show](https://docs.microsoft.com/cli/azure/batch/task#show) | Recupera Olá detalhes de uma tarefa de saudação especificado trabalho em lotes.  |
| [az batch task list](https://docs.microsoft.com/cli/azure/batch/task#list) | Lista as tarefas de saudação associadas ao trabalho especificado hello.  |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script em lotes CLI adicionais podem ser encontrados no hello [documentação CLI de lote do Azure](../batch-cli-samples.md).
