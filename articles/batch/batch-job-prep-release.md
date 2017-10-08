---
title: "tarefas de aaaCreate tooprepare e os trabalhos completos em nós de computação - lote do Azure | Microsoft Docs"
description: "Usar dados de toominimize de tarefas de preparação de trabalho de nível transferir tooAzure nós de computação de lote e tarefas de limpeza de nó na conclusão do trabalho de versão."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 63d9d4f1-8521-4bbb-b95a-c4cad73692d3
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fd5fb47ae6700281e63048c49a1241f4e935baba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a>Executar tarefas de preparação e liberação do trabalho em nós de computação do Lote

 Um trabalho do Lote do Azure geralmente requer alguma forma de configuração antes da execução das tarefas e manutenção pós-trabalho quando as tarefas são concluídas. Talvez você precise toodownload comuns tarefa dados de entrada tooyour nós de computação, ou carregar tooAzure de dados de saída de tarefa armazenamento Olá trabalho concluído. Você pode usar **preparação de trabalho** e **trabalho versão** tarefas tooperform essas operações.

## <a name="what-are-job-preparation-and-release-tasks"></a>O que são as tarefas de preparação e liberação do trabalho?
Antes de executam tarefas do trabalho, tarefa de preparação de trabalho Olá executa em todos os toorun agendado de nós de computação pelo menos uma tarefa. Após a conclusão do trabalho hello, tarefa de liberação de trabalho Olá é executado em cada nó no pool de saudação executado pelo menos uma tarefa. Assim como acontece com as tarefas em lote normal, você pode especificar um toobe de linha de comando chamado quando uma preparação de trabalho ou tarefa de versão é executada.

As tarefas de preparação e liberação de trabalho oferecem recursos conhecidos de tarefas do Lote, como download de arquivo ([arquivos de recurso][net_job_prep_resourcefiles]), execução elevada, variáveis de ambiente personalizadas, duração máxima da execução, contagem de repetição e tempo de retenção de arquivo.

Olá seções a seguir, você aprenderá como Olá toouse [JobPreparationTask] [ net_job_prep] e [JobReleaseTask] [ net_job_release] classes encontradas no Olá [Batch .NET] [ api_net] biblioteca.

> [!TIP]
> As tarefas de preparação e de liberação são especialmente úteis em ambientes de "pool compartilhado", em que um pool de nós de computação persiste entre as execuções de trabalho e usado por vários trabalhos.
> 
> 

## <a name="when-toouse-job-preparation-and-release-tasks"></a>Quando toouse preparação de trabalho e tarefas de versão
Preparação de trabalho e tarefas de versão de trabalho são uma boa opção para Olá situações a seguir:

**Baixar dados de tarefas comuns**

Trabalhos de lote geralmente exigem um conjunto comum de dados como entrada para tarefas de saudação do trabalho. Por exemplo, em cálculos de análise de risco diária, dados de mercado são tarefas de tooall trabalho específico, mas comum no trabalho hello. Esses dados de mercado, geralmente vários gigabytes de tamanho, devem ser baixado tooeach do nó de computação somente uma vez para que qualquer tarefa que é executado no nó Olá pode usá-lo. Use um **tarefa de preparação de trabalho** toodownload esse nó tooeach de dados antes de execução de saudação do trabalho de saudação de outras tarefas.

**Excluir saída de tarefa e de trabalho**

Em um ambiente de "compartilhado pool", onde nós de computação do pool não são encerrados entre os trabalhos, talvez seja necessário toodelete dados de trabalho entre as execuções. Talvez seja necessário tooconserve espaço em disco em nós de saudação ou atender a políticas de segurança da sua organização. Use um **tarefa de liberação de trabalho** dados toodelete que foi baixados por uma tarefa de preparação de trabalho ou gerados durante a execução da tarefa.

**Retenção de log**

Talvez você queira tookeep uma cópia de arquivos de log que geram as tarefas, ou talvez arquivos de despejo falhas que podem ser gerados por aplicativos com falha. Use um **tarefa de liberação de trabalho** em tais casos toocompress e carregar esse dados tooan [armazenamento do Azure] [ azure_storage] conta.

> [!TIP]
> Outro toopersist de maneira logs e outros trabalhos e tarefas de saída de dados são Olá toouse [convenções de arquivo de lote do Azure](batch-task-output.md) biblioteca.
> 
> 

## <a name="job-preparation-task"></a>tarefa de preparação de trabalho
Antes da execução de tarefas do trabalho, o lote executa tarefas de preparação de trabalho Olá em cada nó de computação é agendado toorun uma tarefa. Por padrão, Olá serviço de lote aguarda Olá trabalho preparação tarefa toobe concluída antes de executar Olá tarefas agendadas tooexecute no nó de saudação. No entanto, você pode configurar o serviço de saudação não toowait. Se o nó de saudação for reiniciado, Olá tarefa de preparação de trabalho é executada novamente, mas você também pode desativar esse comportamento.

tarefa de preparação de trabalho Olá é executada somente em nós que são agendado toorun uma tarefa. Isso impede a execução de desnecessária de saudação de uma tarefa de preparação no caso de um nó não está atribuído a uma tarefa. Isso pode ocorrer quando o número de Olá de tarefas para um trabalho é menor que o número de saudação de nós em um pool. Ela também se aplica quando [execução de tarefas simultâneas](batch-parallel-node-tasks.md) estiver habilitado, que deixa alguns nós ocioso se a contagem de tarefas de saudação é inferior ao total tarefas simultâneas possíveis hello. Não executando tarefa de preparação de trabalho Olá em nós ociosos, você pode gastar menos em encargos de transferência de dados.

> [!NOTE]
> [JobPreparationTask] [ net_job_prep_cloudjob] difere [CloudPool.StartTask] [ pool_starttask] que JobPreparationTask executa no início de saudação de cada trabalho, enquanto StartTask executa somente quando um nó de computação primeiro une um pool ou for reiniciado.
> 
> 

## <a name="job-release-task"></a>tarefa de liberação de trabalho
Depois que um trabalho é marcado como concluída, tarefa de liberação de trabalho Olá é executada em cada nó no pool de saudação executado pelo menos uma tarefa. Marcar uma tarefa como concluída emitindo uma solicitação de encerramento. Olá serviço de lote e conjuntos de estado do trabalho de Olá muito*encerrando*finaliza as tarefas de ativas ou em execução associadas ao trabalho hello e executa a tarefa de liberação de trabalho hello. Olá trabalho muda toohello *concluída* estado.

> [!NOTE]
> Exclusão de trabalho também executa a tarefa de liberação de trabalho hello. No entanto, se um trabalho já foi encerrado, tarefa de liberação de saudação não é executada novamente se o trabalho de saudação é excluído.
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a>Tarefas de preparação e liberação de trabalho com o Lote .NET
toouse uma tarefa de preparação de trabalho, atribuir uma [JobPreparationTask] [ net_job_prep] do trabalho do objeto tooyour [CloudJob.JobPreparationTask] [ net_job_prep_cloudjob] propriedade . Da mesma forma, inicializar um [JobReleaseTask] [ net_job_release] e atribuí-la do trabalho tooyour [CloudJob.JobReleaseTask] [ net_job_prep_cloudjob] Olá de tooset de propriedade tarefa de liberação do trabalho.

No trecho de código, `myBatchClient` é uma instância de [BatchClient][net_batch_client], e `myPool` é um pool existente em Olá conta do lote.

```csharp
// Create hello CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify hello command lines for hello job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign hello job preparation task toohello job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign hello job release task toohello job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

Como mencionado anteriormente, tarefa de liberação de saudação é executada quando um trabalho é encerrado ou excluído. Encerre um trabalho com [JobOperations.TerminateJobAsync][net_job_terminate]. Exclua um trabalho com [JobOperations.DeleteJobAsync][net_job_delete]. Normalmente você encerra ou exclui um trabalho quando as tarefas são concluídas ou quando um tempo limite definido foi atingido.

```csharp
// Terminate hello job toomark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a>Exemplo de código no GitHub
tarefas de preparação e a versão de trabalho de toosee em ação, confira Olá [JobPrepRelease] [ job_prep_release_sample] projeto de exemplo no GitHub. Este aplicativo de console Olá a seguir:

1. Cria um pool com dois nós "pequenos".
2. Cria um trabalho com tarefas de preparação, de liberação e padrão de trabalho.
3. Executa Olá tarefa de preparação de trabalho, que grava primeiro o arquivo de texto Olá nó ID tooa no diretório "compartilhado" do nó.
4. Executa uma tarefa em cada nó que grava seu toohello de ID de tarefa mesmo arquivo de texto.
5. Depois que todas as tarefas são concluídas (ou tempo limite de saudação for atingido), imprime o conteúdo de saudação do console de toohello de arquivos de texto de cada nó.
6. Quando Olá trabalho é concluído, é executado arquivo da saudação trabalho versão tarefa toodelete saudação do nó de saudação.
7. Olá imprime códigos de preparação de trabalho de saudação de saída e versão de tarefas para cada nó no qual eles executados.
8. Confirmação de tooallow pausa a execução de exclusão de trabalho e/ou pool.

Saída do aplicativo de exemplo hello é a seguir toohello semelhante:

```
Attempting toocreate pool: JobPrepReleaseSamplePool
Created pool JobPrepReleaseSamplePool with 2 small nodes
Checking for existing job JobPrepReleaseSampleJob...
Job JobPrepReleaseSampleJob not found, creating...
Submitting tasks and awaiting completion...
All tasks completed.

Contents of shared\job_prep_and_release.txt on tvm-2434664350_1-20160623t173951z:
-------------------------------------------
tvm-2434664350_1-20160623t173951z tasks:
  task001
  task004
  task005
  task006

Contents of shared\job_prep_and_release.txt on tvm-2434664350_2-20160623t173951z:
-------------------------------------------
tvm-2434664350_2-20160623t173951z tasks:
  task008
  task002
  task003
  task007

Waiting for job JobPrepReleaseSampleJob tooreach state Completed
...

tvm-2434664350_1-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

tvm-2434664350_2-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

Delete job? [yes] no
yes
Delete pool? [yes] no
yes

Sample complete, hit ENTER tooexit...
```

> [!NOTE]
> Devido a toohello variável criação e hora inicial de nós em um novo pool (alguns nós estão prontos para tarefas antes de outros), você verá uma saída diferente. Especificamente, como tarefas Olá concluir rapidamente, um de nós do pool de saudação pode executar todas as tarefas do trabalho hello. Se isso ocorrer, você observará que Olá preparação de trabalho e tarefas de versão não existem para o nó de saudação que não há tarefas executadas.
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-hello-azure-portal"></a>Inspecione a preparação de trabalho e tarefas de versão no hello portal do Azure
Quando você executa o aplicativo de exemplo hello, você pode usar o hello [portal do Azure] [ portal] tooview Olá propriedades do trabalho hello e suas tarefas, ou até mesmo baixar o arquivo de texto compartilhada de Olá modificada por tarefas do trabalho hello.

saudação de captura de tela abaixo mostra Olá **folha de tarefas de preparação** em Olá portal do Azure após uma execução do aplicativo de exemplo hello. Navegue toohello *JobPrepReleaseSampleJob* propriedades depois de concluíram as tarefas (mas antes de excluir seu trabalho e pool) e clique em **tarefas de preparação** ou **tarefasdeversão** tooview suas propriedades.

![Propriedades de preparação de trabalho no portal do Azure][1]

## <a name="next-steps"></a>Próximas etapas
### <a name="application-packages"></a>pacotes de aplicativos
Tarefa de preparação de trabalho de toohello de adição, você também pode usar o hello [pacotes de aplicativos](batch-application-packages.md) nós para execução de tarefas de computação do recurso de tooprepare de lote. Esse recurso é especialmente útil para implantação de aplicativos que não exigem a execução de um instalados, aplicativos que contêm muitos arquivos (mais de 100) ou aplicativos que exigem um controle de versão estrito.

### <a name="installing-applications-and-staging-data"></a>Instalação de aplicativos e preparação de dados
Essa postagem no fórum da MSDN fornece uma visão geral dos vários métodos de preparação de seus nós para a execução de tarefas:

[Instalando aplicativos e preparando dados em nós de computação do Lote][forum_post]

Escrita por um dos membros da equipe do Azure Batch hello, ele discute várias técnicas que você pode usar toodeploy nós de toocompute de aplicativos e dados.

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[azure_storage]: https://azure.microsoft.com/services/storage/
[portal]: https://portal.azure.com
[job_prep_release_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/JobPrepRelease
[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]:https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_prep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_job_prep_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_job_prep_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.resourcefiles.aspx
[net_job_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.deletejobasync.aspx
[net_job_terminate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_job_release]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobreleasetask.aspx
[net_job_release_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[1]: ./media/batch-job-prep-release/portal-jobprep-01.png
