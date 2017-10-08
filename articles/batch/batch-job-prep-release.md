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
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a><span data-ttu-id="5f3ee-103">Executar tarefas de preparação e liberação do trabalho em nós de computação do Lote</span><span class="sxs-lookup"><span data-stu-id="5f3ee-103">Run job preparation and job release tasks on Batch compute nodes</span></span>

 <span data-ttu-id="5f3ee-104">Um trabalho do Lote do Azure geralmente requer alguma forma de configuração antes da execução das tarefas e manutenção pós-trabalho quando as tarefas são concluídas.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-104">An Azure Batch job often requires some form of setup before its tasks are executed, and post-job maintenance when its tasks are completed.</span></span> <span data-ttu-id="5f3ee-105">Talvez você precise toodownload comuns tarefa dados de entrada tooyour nós de computação, ou carregar tooAzure de dados de saída de tarefa armazenamento Olá trabalho concluído.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-105">You might need toodownload common task input data tooyour compute nodes, or upload task output data tooAzure Storage after hello job completes.</span></span> <span data-ttu-id="5f3ee-106">Você pode usar **preparação de trabalho** e **trabalho versão** tarefas tooperform essas operações.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-106">You can use **job preparation** and **job release** tasks tooperform these operations.</span></span>

## <a name="what-are-job-preparation-and-release-tasks"></a><span data-ttu-id="5f3ee-107">O que são as tarefas de preparação e liberação do trabalho?</span><span class="sxs-lookup"><span data-stu-id="5f3ee-107">What are job preparation and release tasks?</span></span>
<span data-ttu-id="5f3ee-108">Antes de executam tarefas do trabalho, tarefa de preparação de trabalho Olá executa em todos os toorun agendado de nós de computação pelo menos uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-108">Before a job's tasks run, hello job preparation task runs on all compute nodes scheduled toorun at least one task.</span></span> <span data-ttu-id="5f3ee-109">Após a conclusão do trabalho hello, tarefa de liberação de trabalho Olá é executado em cada nó no pool de saudação executado pelo menos uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-109">Once hello job is completed, hello job release task runs on each node in hello pool that executed at least one task.</span></span> <span data-ttu-id="5f3ee-110">Assim como acontece com as tarefas em lote normal, você pode especificar um toobe de linha de comando chamado quando uma preparação de trabalho ou tarefa de versão é executada.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-110">As with normal Batch tasks, you can specify a command line toobe invoked when a job preparation or release task is run.</span></span>

<span data-ttu-id="5f3ee-111">As tarefas de preparação e liberação de trabalho oferecem recursos conhecidos de tarefas do Lote, como download de arquivo ([arquivos de recurso][net_job_prep_resourcefiles]), execução elevada, variáveis de ambiente personalizadas, duração máxima da execução, contagem de repetição e tempo de retenção de arquivo.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-111">Job preparation and release tasks offer familiar Batch task features such as file download ([resource files][net_job_prep_resourcefiles]), elevated execution, custom environment variables, maximum execution duration, retry count, and file retention time.</span></span>

<span data-ttu-id="5f3ee-112">Olá seções a seguir, você aprenderá como Olá toouse [JobPreparationTask] [ net_job_prep] e [JobReleaseTask] [ net_job_release] classes encontradas no Olá [Batch .NET] [ api_net] biblioteca.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-112">In hello following sections, you'll learn how toouse hello [JobPreparationTask][net_job_prep] and [JobReleaseTask][net_job_release] classes found in hello [Batch .NET][api_net] library.</span></span>

> [!TIP]
> <span data-ttu-id="5f3ee-113">As tarefas de preparação e de liberação são especialmente úteis em ambientes de "pool compartilhado", em que um pool de nós de computação persiste entre as execuções de trabalho e usado por vários trabalhos.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-113">Job preparation and release tasks are especially helpful in "shared pool" environments, in which a pool of compute nodes persists between job runs and is used by many jobs.</span></span>
> 
> 

## <a name="when-toouse-job-preparation-and-release-tasks"></a><span data-ttu-id="5f3ee-114">Quando toouse preparação de trabalho e tarefas de versão</span><span class="sxs-lookup"><span data-stu-id="5f3ee-114">When toouse job preparation and release tasks</span></span>
<span data-ttu-id="5f3ee-115">Preparação de trabalho e tarefas de versão de trabalho são uma boa opção para Olá situações a seguir:</span><span class="sxs-lookup"><span data-stu-id="5f3ee-115">Job preparation and job release tasks are a good fit for hello following situations:</span></span>

<span data-ttu-id="5f3ee-116">**Baixar dados de tarefas comuns**</span><span class="sxs-lookup"><span data-stu-id="5f3ee-116">**Download common task data**</span></span>

<span data-ttu-id="5f3ee-117">Trabalhos de lote geralmente exigem um conjunto comum de dados como entrada para tarefas de saudação do trabalho.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-117">Batch jobs often require a common set of data as input for hello job's tasks.</span></span> <span data-ttu-id="5f3ee-118">Por exemplo, em cálculos de análise de risco diária, dados de mercado são tarefas de tooall trabalho específico, mas comum no trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-118">For example, in daily risk analysis calculations, market data is job-specific, yet common tooall tasks in hello job.</span></span> <span data-ttu-id="5f3ee-119">Esses dados de mercado, geralmente vários gigabytes de tamanho, devem ser baixado tooeach do nó de computação somente uma vez para que qualquer tarefa que é executado no nó Olá pode usá-lo.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-119">This market data, often several gigabytes in size, should be downloaded tooeach compute node only once so that any task that runs on hello node can use it.</span></span> <span data-ttu-id="5f3ee-120">Use um **tarefa de preparação de trabalho** toodownload esse nó tooeach de dados antes de execução de saudação do trabalho de saudação de outras tarefas.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-120">Use a **job preparation task** toodownload this data tooeach node before hello execution of hello job's other tasks.</span></span>

<span data-ttu-id="5f3ee-121">**Excluir saída de tarefa e de trabalho**</span><span class="sxs-lookup"><span data-stu-id="5f3ee-121">**Delete job and task output**</span></span>

<span data-ttu-id="5f3ee-122">Em um ambiente de "compartilhado pool", onde nós de computação do pool não são encerrados entre os trabalhos, talvez seja necessário toodelete dados de trabalho entre as execuções.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-122">In a "shared pool" environment, where a pool's compute nodes are not decommissioned between jobs, you may need toodelete job data between runs.</span></span> <span data-ttu-id="5f3ee-123">Talvez seja necessário tooconserve espaço em disco em nós de saudação ou atender a políticas de segurança da sua organização.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-123">You might need tooconserve disk space on hello nodes, or satisfy your organization's security policies.</span></span> <span data-ttu-id="5f3ee-124">Use um **tarefa de liberação de trabalho** dados toodelete que foi baixados por uma tarefa de preparação de trabalho ou gerados durante a execução da tarefa.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-124">Use a **job release task** toodelete data that was downloaded by a job preparation task, or generated during task execution.</span></span>

<span data-ttu-id="5f3ee-125">**Retenção de log**</span><span class="sxs-lookup"><span data-stu-id="5f3ee-125">**Log retention**</span></span>

<span data-ttu-id="5f3ee-126">Talvez você queira tookeep uma cópia de arquivos de log que geram as tarefas, ou talvez arquivos de despejo falhas que podem ser gerados por aplicativos com falha.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-126">You might want tookeep a copy of log files that your tasks generate, or perhaps crash dump files that can be generated by failed applications.</span></span> <span data-ttu-id="5f3ee-127">Use um **tarefa de liberação de trabalho** em tais casos toocompress e carregar esse dados tooan [armazenamento do Azure] [ azure_storage] conta.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-127">Use a **job release task** in such cases toocompress and upload this data tooan [Azure Storage][azure_storage] account.</span></span>

> [!TIP]
> <span data-ttu-id="5f3ee-128">Outro toopersist de maneira logs e outros trabalhos e tarefas de saída de dados são Olá toouse [convenções de arquivo de lote do Azure](batch-task-output.md) biblioteca.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-128">Another way toopersist logs and other job and task output data is toouse hello [Azure Batch File Conventions](batch-task-output.md) library.</span></span>
> 
> 

## <a name="job-preparation-task"></a><span data-ttu-id="5f3ee-129">tarefa de preparação de trabalho</span><span class="sxs-lookup"><span data-stu-id="5f3ee-129">Job preparation task</span></span>
<span data-ttu-id="5f3ee-130">Antes da execução de tarefas do trabalho, o lote executa tarefas de preparação de trabalho Olá em cada nó de computação é agendado toorun uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-130">Before execution of a job's tasks, Batch executes hello job preparation task on each compute node that is scheduled toorun a task.</span></span> <span data-ttu-id="5f3ee-131">Por padrão, Olá serviço de lote aguarda Olá trabalho preparação tarefa toobe concluída antes de executar Olá tarefas agendadas tooexecute no nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-131">By default, hello Batch service waits for hello job preparation task toobe completed before running hello tasks scheduled tooexecute on hello node.</span></span> <span data-ttu-id="5f3ee-132">No entanto, você pode configurar o serviço de saudação não toowait.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-132">However, you can configure hello service not toowait.</span></span> <span data-ttu-id="5f3ee-133">Se o nó de saudação for reiniciado, Olá tarefa de preparação de trabalho é executada novamente, mas você também pode desativar esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-133">If hello node restarts, hello job preparation task runs again, but you can also disable this behavior.</span></span>

<span data-ttu-id="5f3ee-134">tarefa de preparação de trabalho Olá é executada somente em nós que são agendado toorun uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-134">hello job preparation task is executed only on nodes that are scheduled toorun a task.</span></span> <span data-ttu-id="5f3ee-135">Isso impede a execução de desnecessária de saudação de uma tarefa de preparação no caso de um nó não está atribuído a uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-135">This prevents hello unnecessary execution of a preparation task in case a node is not assigned a task.</span></span> <span data-ttu-id="5f3ee-136">Isso pode ocorrer quando o número de Olá de tarefas para um trabalho é menor que o número de saudação de nós em um pool.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-136">This can occur when hello number of tasks for a job is less than hello number of nodes in a pool.</span></span> <span data-ttu-id="5f3ee-137">Ela também se aplica quando [execução de tarefas simultâneas](batch-parallel-node-tasks.md) estiver habilitado, que deixa alguns nós ocioso se a contagem de tarefas de saudação é inferior ao total tarefas simultâneas possíveis hello.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-137">It also applies when [concurrent task execution](batch-parallel-node-tasks.md) is enabled, which leaves some nodes idle if hello task count is lower than hello total possible concurrent tasks.</span></span> <span data-ttu-id="5f3ee-138">Não executando tarefa de preparação de trabalho Olá em nós ociosos, você pode gastar menos em encargos de transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-138">By not running hello job preparation task on idle nodes, you can spend less money on data transfer charges.</span></span>

> [!NOTE]
> <span data-ttu-id="5f3ee-139">[JobPreparationTask] [ net_job_prep_cloudjob] difere [CloudPool.StartTask] [ pool_starttask] que JobPreparationTask executa no início de saudação de cada trabalho, enquanto StartTask executa somente quando um nó de computação primeiro une um pool ou for reiniciado.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-139">[JobPreparationTask][net_job_prep_cloudjob] differs from [CloudPool.StartTask][pool_starttask] in that JobPreparationTask executes at hello start of each job, whereas StartTask executes only when a compute node first joins a pool or restarts.</span></span>
> 
> 

## <a name="job-release-task"></a><span data-ttu-id="5f3ee-140">tarefa de liberação de trabalho</span><span class="sxs-lookup"><span data-stu-id="5f3ee-140">Job release task</span></span>
<span data-ttu-id="5f3ee-141">Depois que um trabalho é marcado como concluída, tarefa de liberação de trabalho Olá é executada em cada nó no pool de saudação executado pelo menos uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-141">Once a job is marked as completed, hello job release task is executed on each node in hello pool that executed at least one task.</span></span> <span data-ttu-id="5f3ee-142">Marcar uma tarefa como concluída emitindo uma solicitação de encerramento.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-142">You mark a job as completed by issuing a terminate request.</span></span> <span data-ttu-id="5f3ee-143">Olá serviço de lote e conjuntos de estado do trabalho de Olá muito*encerrando*finaliza as tarefas de ativas ou em execução associadas ao trabalho hello e executa a tarefa de liberação de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-143">hello Batch service then sets hello job state too*terminating*, terminates any active or running tasks associated with hello job, and runs hello job release task.</span></span> <span data-ttu-id="5f3ee-144">Olá trabalho muda toohello *concluída* estado.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-144">hello job then moves toohello *completed* state.</span></span>

> [!NOTE]
> <span data-ttu-id="5f3ee-145">Exclusão de trabalho também executa a tarefa de liberação de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-145">Job deletion also executes hello job release task.</span></span> <span data-ttu-id="5f3ee-146">No entanto, se um trabalho já foi encerrado, tarefa de liberação de saudação não é executada novamente se o trabalho de saudação é excluído.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-146">However, if a job has already been terminated, hello release task is not run a second time if hello job is later deleted.</span></span>
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a><span data-ttu-id="5f3ee-147">Tarefas de preparação e liberação de trabalho com o Lote .NET</span><span class="sxs-lookup"><span data-stu-id="5f3ee-147">Job prep and release tasks with Batch .NET</span></span>
<span data-ttu-id="5f3ee-148">toouse uma tarefa de preparação de trabalho, atribuir uma [JobPreparationTask] [ net_job_prep] do trabalho do objeto tooyour [CloudJob.JobPreparationTask] [ net_job_prep_cloudjob] propriedade .</span><span class="sxs-lookup"><span data-stu-id="5f3ee-148">toouse a job preparation task, assign a [JobPreparationTask][net_job_prep] object tooyour job's [CloudJob.JobPreparationTask][net_job_prep_cloudjob] property.</span></span> <span data-ttu-id="5f3ee-149">Da mesma forma, inicializar um [JobReleaseTask] [ net_job_release] e atribuí-la do trabalho tooyour [CloudJob.JobReleaseTask] [ net_job_prep_cloudjob] Olá de tooset de propriedade tarefa de liberação do trabalho.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-149">Similarly, initialize a [JobReleaseTask][net_job_release] and assign it tooyour job's [CloudJob.JobReleaseTask][net_job_prep_cloudjob] property tooset hello job's release task.</span></span>

<span data-ttu-id="5f3ee-150">No trecho de código, `myBatchClient` é uma instância de [BatchClient][net_batch_client], e `myPool` é um pool existente em Olá conta do lote.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-150">In this code snippet, `myBatchClient` is an instance of [BatchClient][net_batch_client], and `myPool` is an existing pool within hello Batch account.</span></span>

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

<span data-ttu-id="5f3ee-151">Como mencionado anteriormente, tarefa de liberação de saudação é executada quando um trabalho é encerrado ou excluído.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-151">As mentioned earlier, hello release task is executed when a job is terminated or deleted.</span></span> <span data-ttu-id="5f3ee-152">Encerre um trabalho com [JobOperations.TerminateJobAsync][net_job_terminate].</span><span class="sxs-lookup"><span data-stu-id="5f3ee-152">Terminate a job with [JobOperations.TerminateJobAsync][net_job_terminate].</span></span> <span data-ttu-id="5f3ee-153">Exclua um trabalho com [JobOperations.DeleteJobAsync][net_job_delete].</span><span class="sxs-lookup"><span data-stu-id="5f3ee-153">Delete a job with [JobOperations.DeleteJobAsync][net_job_delete].</span></span> <span data-ttu-id="5f3ee-154">Normalmente você encerra ou exclui um trabalho quando as tarefas são concluídas ou quando um tempo limite definido foi atingido.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-154">You typically terminate or delete a job when its tasks are completed, or when a timeout that you've defined has been reached.</span></span>

```csharp
// Terminate hello job toomark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a><span data-ttu-id="5f3ee-155">Exemplo de código no GitHub</span><span class="sxs-lookup"><span data-stu-id="5f3ee-155">Code sample on GitHub</span></span>
<span data-ttu-id="5f3ee-156">tarefas de preparação e a versão de trabalho de toosee em ação, confira Olá [JobPrepRelease] [ job_prep_release_sample] projeto de exemplo no GitHub.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-156">toosee job preparation and release tasks in action, check out hello [JobPrepRelease][job_prep_release_sample] sample project on GitHub.</span></span> <span data-ttu-id="5f3ee-157">Este aplicativo de console Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="5f3ee-157">This console application does hello following:</span></span>

1. <span data-ttu-id="5f3ee-158">Cria um pool com dois nós "pequenos".</span><span class="sxs-lookup"><span data-stu-id="5f3ee-158">Creates a pool with two "small" nodes.</span></span>
2. <span data-ttu-id="5f3ee-159">Cria um trabalho com tarefas de preparação, de liberação e padrão de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-159">Creates a job with job preparation, release, and standard tasks.</span></span>
3. <span data-ttu-id="5f3ee-160">Executa Olá tarefa de preparação de trabalho, que grava primeiro o arquivo de texto Olá nó ID tooa no diretório "compartilhado" do nó.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-160">Runs hello job preparation task, which first writes hello node ID tooa text file in a node's "shared" directory.</span></span>
4. <span data-ttu-id="5f3ee-161">Executa uma tarefa em cada nó que grava seu toohello de ID de tarefa mesmo arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-161">Runs a task on each node that writes its task ID toohello same text file.</span></span>
5. <span data-ttu-id="5f3ee-162">Depois que todas as tarefas são concluídas (ou tempo limite de saudação for atingido), imprime o conteúdo de saudação do console de toohello de arquivos de texto de cada nó.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-162">Once all tasks are completed (or hello timeout is reached), prints hello contents of each node's text file toohello console.</span></span>
6. <span data-ttu-id="5f3ee-163">Quando Olá trabalho é concluído, é executado arquivo da saudação trabalho versão tarefa toodelete saudação do nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-163">When hello job is completed, runs hello job release task toodelete hello file from hello node.</span></span>
7. <span data-ttu-id="5f3ee-164">Olá imprime códigos de preparação de trabalho de saudação de saída e versão de tarefas para cada nó no qual eles executados.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-164">Prints hello exit codes of hello job preparation and release tasks for each node on which they executed.</span></span>
8. <span data-ttu-id="5f3ee-165">Confirmação de tooallow pausa a execução de exclusão de trabalho e/ou pool.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-165">Pauses execution tooallow confirmation of job and/or pool deletion.</span></span>

<span data-ttu-id="5f3ee-166">Saída do aplicativo de exemplo hello é a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="5f3ee-166">Output from hello sample application is similar toohello following:</span></span>

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
> <span data-ttu-id="5f3ee-167">Devido a toohello variável criação e hora inicial de nós em um novo pool (alguns nós estão prontos para tarefas antes de outros), você verá uma saída diferente.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-167">Due toohello variable creation and start time of nodes in a new pool (some nodes are ready for tasks before others), you may see different output.</span></span> <span data-ttu-id="5f3ee-168">Especificamente, como tarefas Olá concluir rapidamente, um de nós do pool de saudação pode executar todas as tarefas do trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-168">Specifically, because hello tasks complete quickly, one of hello pool's nodes may execute all of hello job's tasks.</span></span> <span data-ttu-id="5f3ee-169">Se isso ocorrer, você observará que Olá preparação de trabalho e tarefas de versão não existem para o nó de saudação que não há tarefas executadas.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-169">If this occurs, you will notice that hello job prep and release tasks do not exist for hello node that executed no tasks.</span></span>
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-hello-azure-portal"></a><span data-ttu-id="5f3ee-170">Inspecione a preparação de trabalho e tarefas de versão no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="5f3ee-170">Inspect job preparation and release tasks in hello Azure portal</span></span>
<span data-ttu-id="5f3ee-171">Quando você executa o aplicativo de exemplo hello, você pode usar o hello [portal do Azure] [ portal] tooview Olá propriedades do trabalho hello e suas tarefas, ou até mesmo baixar o arquivo de texto compartilhada de Olá modificada por tarefas do trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-171">When you run hello sample application, you can use hello [Azure portal][portal] tooview hello properties of hello job and its tasks, or even download hello shared text file that is modified by hello job's tasks.</span></span>

<span data-ttu-id="5f3ee-172">saudação de captura de tela abaixo mostra Olá **folha de tarefas de preparação** em Olá portal do Azure após uma execução do aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-172">hello screenshot below shows hello **Preparation tasks blade** in hello Azure portal after a run of hello sample application.</span></span> <span data-ttu-id="5f3ee-173">Navegue toohello *JobPrepReleaseSampleJob* propriedades depois de concluíram as tarefas (mas antes de excluir seu trabalho e pool) e clique em **tarefas de preparação** ou **tarefasdeversão** tooview suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-173">Navigate toohello *JobPrepReleaseSampleJob* properties after your tasks have completed (but before deleting your job and pool) and click **Preparation tasks** or **Release tasks** tooview their properties.</span></span>

![Propriedades de preparação de trabalho no portal do Azure][1]

## <a name="next-steps"></a><span data-ttu-id="5f3ee-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5f3ee-175">Next steps</span></span>
### <a name="application-packages"></a><span data-ttu-id="5f3ee-176">pacotes de aplicativos</span><span class="sxs-lookup"><span data-stu-id="5f3ee-176">Application packages</span></span>
<span data-ttu-id="5f3ee-177">Tarefa de preparação de trabalho de toohello de adição, você também pode usar o hello [pacotes de aplicativos](batch-application-packages.md) nós para execução de tarefas de computação do recurso de tooprepare de lote.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-177">In addition toohello job preparation task, you can also use hello [application packages](batch-application-packages.md) feature of Batch tooprepare compute nodes for task execution.</span></span> <span data-ttu-id="5f3ee-178">Esse recurso é especialmente útil para implantação de aplicativos que não exigem a execução de um instalados, aplicativos que contêm muitos arquivos (mais de 100) ou aplicativos que exigem um controle de versão estrito.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-178">This feature is especially useful for deploying applications that do not require running an installer, applications that contain many (100+) files, or applications that require strict version control.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="5f3ee-179">Instalação de aplicativos e preparação de dados</span><span class="sxs-lookup"><span data-stu-id="5f3ee-179">Installing applications and staging data</span></span>
<span data-ttu-id="5f3ee-180">Essa postagem no fórum da MSDN fornece uma visão geral dos vários métodos de preparação de seus nós para a execução de tarefas:</span><span class="sxs-lookup"><span data-stu-id="5f3ee-180">This MSDN forum post provides an overview of several methods of preparing your nodes for running tasks:</span></span>

<span data-ttu-id="5f3ee-181">[Instalando aplicativos e preparando dados em nós de computação do Lote][forum_post]</span><span class="sxs-lookup"><span data-stu-id="5f3ee-181">[Installing applications and staging data on Batch compute nodes][forum_post]</span></span>

<span data-ttu-id="5f3ee-182">Escrita por um dos membros da equipe do Azure Batch hello, ele discute várias técnicas que você pode usar toodeploy nós de toocompute de aplicativos e dados.</span><span class="sxs-lookup"><span data-stu-id="5f3ee-182">Written by one of hello Azure Batch team members, it discusses several techniques that you can use toodeploy applications and data toocompute nodes.</span></span>

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
