---
title: "AAA \"variáveis de ambiente do nó de computação do Azure Batch | Microsoft Docs\""
description: "Referência de variável de ambiente do nó de computação para análise de lote do Azure."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/05/2017
ms.author: tamram
ms.openlocfilehash: 860f34b530579a81fbd5cf8ffa31df79d917c080
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-compute-node-environment-variables"></a>Variáveis de ambiente do nó de computação do Lote do Azure
Olá [serviço do Azure Batch](https://azure.microsoft.com/services/batch/) define Olá seguintes variáveis de ambiente em nós de computação. Você pode fazer referência a essas variáveis de ambiente em linhas de comando da tarefa, em programas hello e scripts executados por Olá linhas de comando.

Para informações adicionais sobre como usar as variáveis de ambiente com lote, consulte [Configurações de ambiente para tarefas](https://docs.microsoft.com/azure/batch/batch-api-basics#environment-settings-for-tasks).

## <a name="environment-variable-visibility"></a>Visibilidade de variável de ambiente

Essas variáveis de ambiente são visíveis somente no contexto Olá Olá **usuário da tarefa**, Olá a conta de usuário no nó Olá sob a qual uma tarefa é executada. Você vai *não* vê-los se você [se conectar remotamente](https://azure.microsoft.com/documentation/articles/batch-api-basics/#connecting-to-compute-nodes) tooa nó por meio do protocolo de área de trabalho remota (RDP) ou Secure Shell (SSH) e lista de variáveis de ambiente de saudação de computação. Isso é porque a conta de usuário de saudação que é usada para conexão remota não é Olá igual a conta Olá que é usada pela tarefa de saudação.

## <a name="command-line-expansion-of-environment-variables"></a>Expansão de linha de comando de variáveis de ambiente

Olá linhas de comando executadas pelas tarefas em nós não são executados em um shell de computação. Portanto, essas linhas de comando nativamente não pode tirar proveito dos recursos de shell como expansão de variáveis de ambiente (Isso inclui Olá `PATH`). tootake proveito desses recursos, você deve **invocar shell Olá** na linha de comando hello. Por exemplo, inicie `cmd.exe` em nós de computação do Windows ou `/bin/sh` em nós do Linux:

`cmd /c MyTaskApplication.exe %MY_ENV_VAR%`

`/bin/sh -c MyTaskApplication $MY_ENV_VAR`

## <a name="environment-variables"></a>Variáveis de ambiente

| Nome da variável                     | Descrição                                                              | Disponibilidade | Exemplo |
|-----------------------------------|--------------------------------------------------------------------------|--------------|---------|
| AZ_BATCH_ACCOUNT_NAME           | nome de saudação da conta de lote de Olá Olá tarefa pertence.                  | Todas as tarefas.   | mybatchaccount |
| AZ_BATCH_CERTIFICATES_DIR       | Um diretório no hello [diretório de trabalho da tarefa] [ files_dirs] nós de computação em que os certificados são armazenados para Linux. Observe que essa variável de ambiente não se aplica a nós de computação tooWindows.                                                  | Todas as tarefas.   |  /mnt/batch/tasks/workitems/batchjob001/job-1/task001/certs |
| AZ_BATCH_JOB_ID                 | Olá ID do trabalho Olá Olá tarefa pertence. | Todas as tarefas exceto a tarefa de inicialização. | batchjob001 |
| AZ_BATCH_JOB_PREP_DIR           | caminho completo de saudação de preparação de trabalho Olá [diretório tarefas] [ files_dirs] no nó de saudação. | Todas as tarefas, exceto a tarefa de inicialização e de preparação do trabalho. Disponível somente se o trabalho de saudação é configurado com uma tarefa de preparação de trabalho. | C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation |
| AZ_BATCH_JOB_PREP_DIR   | caminho completo de saudação de preparação de trabalho Olá [diretório de trabalho da tarefa] [ files_dirs] no nó de saudação. | Todas as tarefas, exceto a tarefa de inicialização e de preparação do trabalho. Disponível somente se o trabalho de saudação é configurado com uma tarefa de preparação de trabalho. | C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation\wd |
| AZ_BATCH_NODE_ID                | ID de saudação do nó Olá Olá tarefa é atribuído a. | Todas as tarefas. | Tvm-1219235766_3-20160919t172711z |
| AZ_BATCH_NODE_ROOT_DIR          | caminho completo de saudação da raiz de saudação de todos os [lote diretórios] [ files_dirs] no nó de saudação. | Todas as tarefas. | C:\user\tasks |
| AZ_BATCH_NODE_SHARED_DIR        | caminho completo Olá Olá [diretório compartilhado] [ files_dirs] no nó de saudação. Todas as tarefas executadas em um nó tem um diretório de toothis de acesso de leitura/gravação. Tarefas executadas em outros nós não ter o diretório de toothis de acesso remoto (não é um diretório de rede "compartilhado"). | Todas as tarefas. | C:\user\tasks\shared |
| AZ_BATCH_NODE_STARTUP_DIR       | caminho completo Olá Olá [iniciar diretório tarefas] [ files_dirs] no nó de saudação. | Todas as tarefas. | C:\user\tasks\startup |
| AZ_BATCH_POOL_ID                | ID de saudação do pool Olá Olá tarefa está em execução. | Todas as tarefas. | batchpool001 |
| AZ_BATCH_TASK_DIR               | caminho completo Olá Olá [diretório tarefas] [ files_dirs] no nó de saudação. Este diretório contém Olá `stdout.txt` e `stderr.txt` de tarefa hello e Olá AZ_BATCH_TASK_WORKING_DIR. | Todas as tarefas. | C:\user\tasks\workitems\batchjob001\job-1\task001 |
| AZ_BATCH_TASK_ID                | Olá ID da tarefa atual hello. | Todas as tarefas exceto a tarefa de inicialização. | task001 |
| AZ_BATCH_TASK_WORKING_DIR       | caminho completo Olá Olá [diretório de trabalho da tarefa] [ files_dirs] no nó de saudação. Olá executando tarefa tem um diretório de toothis de acesso de leitura/gravação. | Todas as tarefas. | C:\user\tasks\workitems\batchjob001\job-1\task001\wd |
| CCP_NODES                       | lista de saudação de nós e o número de núcleos por nó alocados tooa [tarefas de várias instâncias][multi_instance]. Nós e núcleos são listados no formato de saudação`numNodes<space>node1IP<space>node1Cores<space>`<br/>`node2IP<space>node2Cores<space> ...`, onde o número de saudação de nós é seguido por um ou mais endereços IP de nó e o número de saudação de núcleos para cada um. |  Várias instâncias principais e subtarefas. |`2 10.0.0.4 1 10.0.0.5 1` |
| AZ_BATCH_NODE_LIST              | lista de saudação de nós que estão alocados tooa [tarefas de várias instâncias] [ multi_instance] no formato de saudação `nodeIP;nodeIP`. | Várias instâncias principais e subtarefas. | `10.0.0.4;10.0.0.5` |
| AZ_BATCH_HOST_LIST              | lista de saudação de nós que estão alocados tooa [tarefas de várias instâncias] [ multi_instance] no formato de saudação `nodeIP,nodeIP`. | Várias instâncias principais e subtarefas. | `10.0.0.4,10.0.0.5` |
| AZ_BATCH_MASTER_NODE            | Olá endereço IP e porta de saudação nó de computação no qual tarefa principal de saudação de um [tarefas de várias instâncias] [ multi_instance] é executado. | Várias instâncias principais e subtarefas. | `10.0.0.4:6000`|
| AZ_BATCH_TASK_SHARED_DIR | Um caminho de diretório é idêntico para tarefa primária hello e cada subtarefa de uma [tarefas de várias instâncias][multi_instance]. Hello caminho existe em cada nó no qual várias instâncias a saudação tarefa é executada e é acessível toohello comandos de tarefas em execução no nó de leitura/gravação (ambos Olá [comando coordenação] [ coord_cmd] e hello [comando aplicativo][app_cmd]). Subtarefas ou uma tarefa primária que execute em outros nós não tem o diretório de toothis de acesso remoto (não é um diretório de rede "compartilhado"). | Várias instâncias principais e subtarefas. | C:\user\tasks\workitems\multiinstancesamplejob\job-1\multiinstancesampletask |
| AZ_BATCH_IS_CURRENT_NODE_MASTER | Especifica se o nó atual Olá é nó mestre Olá um [tarefas de várias instâncias][multi_instance]. Os valores possíveis são `true` e `false`.| Várias instâncias principais e subtarefas. | `true` |
| AZ_BATCH_NODE_IS_DEDICATED | Se `true`, Olá atual é um nó dedicado. Se `false`, ele é um [nó de baixa prioridade](batch-low-pri-vms.md). | Todas as tarefas. | `true` |

[files_dirs]: https://azure.microsoft.com/documentation/articles/batch-api-basics/#files-and-directories
[multi_instance]: https://azure.microsoft.com/documentation/articles/batch-mpi/
[coord_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#coordination-command
[app_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#application-command
