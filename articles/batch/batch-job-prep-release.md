---
title: "Criar tarefas para preparar e concluir trabalhos em nós de computação - Lote do Azure | Microsoft Docs"
description: "Use tarefas de preparação de nível de trabalho para minimizar a transferência de dados para nós de computação do Lote do Azure e libere as tarefas para limpeza de nó na conclusão do trabalho."
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
ms.openlocfilehash: 6a2525c02ce7bd3969469d2e28a5fccc948f89b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a><span data-ttu-id="a6340-103">Executar tarefas de preparação e liberação do trabalho em nós de computação do Lote</span><span class="sxs-lookup"><span data-stu-id="a6340-103">Run job preparation and job release tasks on Batch compute nodes</span></span>

 <span data-ttu-id="a6340-104">Um trabalho do Lote do Azure geralmente requer alguma forma de configuração antes da execução das tarefas e manutenção pós-trabalho quando as tarefas são concluídas.</span><span class="sxs-lookup"><span data-stu-id="a6340-104">An Azure Batch job often requires some form of setup before its tasks are executed, and post-job maintenance when its tasks are completed.</span></span> <span data-ttu-id="a6340-105">Talvez seja necessário baixar dados de entrada de tarefas comuns nos nós de computação ou carregar dados de saída da tarefa no Armazenamento do Azure depois que o trabalho for concluído.</span><span class="sxs-lookup"><span data-stu-id="a6340-105">You might need to download common task input data to your compute nodes, or upload task output data to Azure Storage after the job completes.</span></span> <span data-ttu-id="a6340-106">Você pode usar tarefas de **preparação de trabalho** e de **liberação de trabalho** para executar essas operações.</span><span class="sxs-lookup"><span data-stu-id="a6340-106">You can use **job preparation** and **job release** tasks to perform these operations.</span></span>

## <a name="what-are-job-preparation-and-release-tasks"></a><span data-ttu-id="a6340-107">O que são as tarefas de preparação e liberação do trabalho?</span><span class="sxs-lookup"><span data-stu-id="a6340-107">What are job preparation and release tasks?</span></span>
<span data-ttu-id="a6340-108">Antes da execução de uma tarefa de trabalho, a tarefa de preparação de trabalho é executada em todos os nós computados e agendados para execução de pelo menos uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="a6340-108">Before a job's tasks run, the job preparation task runs on all compute nodes scheduled to run at least one task.</span></span> <span data-ttu-id="a6340-109">Quando o trabalho é concluído, a tarefa de liberação do trabalho é executada em cada nó no pool que executou pelo menos uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="a6340-109">Once the job is completed, the job release task runs on each node in the pool that executed at least one task.</span></span> <span data-ttu-id="a6340-110">Assim como acontece com tarefas normais de lote, você pode especificar um comando da tarefa para ser invocada quando uma tarefa de preparação ou liberação de trabalho for executada.</span><span class="sxs-lookup"><span data-stu-id="a6340-110">As with normal Batch tasks, you can specify a command line to be invoked when a job preparation or release task is run.</span></span>

<span data-ttu-id="a6340-111">As tarefas de preparação e liberação de trabalho oferecem recursos conhecidos de tarefas do Lote, como download de arquivo ([arquivos de recurso][net_job_prep_resourcefiles]), execução elevada, variáveis de ambiente personalizadas, duração máxima da execução, contagem de repetição e tempo de retenção de arquivo.</span><span class="sxs-lookup"><span data-stu-id="a6340-111">Job preparation and release tasks offer familiar Batch task features such as file download ([resource files][net_job_prep_resourcefiles]), elevated execution, custom environment variables, maximum execution duration, retry count, and file retention time.</span></span>

<span data-ttu-id="a6340-112">Nas seções a seguir, você aprenderá a usar as classes [JobPreparationTask][net_job_prep] e [JobReleaseTask][net_job_release] encontradas na biblioteca [.NET do Lote][api_net].</span><span class="sxs-lookup"><span data-stu-id="a6340-112">In the following sections, you'll learn how to use the [JobPreparationTask][net_job_prep] and [JobReleaseTask][net_job_release] classes found in the [Batch .NET][api_net] library.</span></span>

> [!TIP]
> <span data-ttu-id="a6340-113">As tarefas de preparação e de liberação são especialmente úteis em ambientes de "pool compartilhado", em que um pool de nós de computação persiste entre as execuções de trabalho e usado por vários trabalhos.</span><span class="sxs-lookup"><span data-stu-id="a6340-113">Job preparation and release tasks are especially helpful in "shared pool" environments, in which a pool of compute nodes persists between job runs and is used by many jobs.</span></span>
> 
> 

## <a name="when-to-use-job-preparation-and-release-tasks"></a><span data-ttu-id="a6340-114">Quando usar tarefas de preparação e liberação do trabalho</span><span class="sxs-lookup"><span data-stu-id="a6340-114">When to use job preparation and release tasks</span></span>
<span data-ttu-id="a6340-115">As tarefas de preparação e de liberação de trabalho são uma boa opção nas seguintes situações:</span><span class="sxs-lookup"><span data-stu-id="a6340-115">Job preparation and job release tasks are a good fit for the following situations:</span></span>

<span data-ttu-id="a6340-116">**Baixar dados de tarefas comuns**</span><span class="sxs-lookup"><span data-stu-id="a6340-116">**Download common task data**</span></span>

<span data-ttu-id="a6340-117">Os trabalhos do Lote geralmente exigem um conjunto comum de dados como entrada para as tarefas do trabalho.</span><span class="sxs-lookup"><span data-stu-id="a6340-117">Batch jobs often require a common set of data as input for the job's tasks.</span></span> <span data-ttu-id="a6340-118">Por exemplo, em cálculos diários de análise de riscos, os dados de mercado são específico do trabalho, porém, comuns a todas as tarefas no trabalho.</span><span class="sxs-lookup"><span data-stu-id="a6340-118">For example, in daily risk analysis calculations, market data is job-specific, yet common to all tasks in the job.</span></span> <span data-ttu-id="a6340-119">Esses dados de mercado, geralmente com vários gigabytes, devem ser baixados para cada nó de computação apenas uma vez, para que qualquer tarefa que seja executada no nó possa usá-los.</span><span class="sxs-lookup"><span data-stu-id="a6340-119">This market data, often several gigabytes in size, should be downloaded to each compute node only once so that any task that runs on the node can use it.</span></span> <span data-ttu-id="a6340-120">Use uma **tarefa de preparação de trabalho** para baixar esses dados para cada nó antes da execução de outras tarefas do trabalho.</span><span class="sxs-lookup"><span data-stu-id="a6340-120">Use a **job preparation task** to download this data to each node before the execution of the job's other tasks.</span></span>

<span data-ttu-id="a6340-121">**Excluir saída de tarefa e de trabalho**</span><span class="sxs-lookup"><span data-stu-id="a6340-121">**Delete job and task output**</span></span>

<span data-ttu-id="a6340-122">Em um ambiente de "pool compartilhado", em que nós de computação do pool não são encerrados entre trabalhos, talvez seja necessário excluir os dados entre as execuções do trabalho.</span><span class="sxs-lookup"><span data-stu-id="a6340-122">In a "shared pool" environment, where a pool's compute nodes are not decommissioned between jobs, you may need to delete job data between runs.</span></span> <span data-ttu-id="a6340-123">Talvez seja necessário conservar espaço em disco nos nós ou atender a políticas de segurança da sua organização.</span><span class="sxs-lookup"><span data-stu-id="a6340-123">You might need to conserve disk space on the nodes, or satisfy your organization's security policies.</span></span> <span data-ttu-id="a6340-124">Use uma **tarefa de liberação de trabalho** para excluir dados baixados por uma tarefa de preparação de trabalho ou gerados durante a execução da tarefa.</span><span class="sxs-lookup"><span data-stu-id="a6340-124">Use a **job release task** to delete data that was downloaded by a job preparation task, or generated during task execution.</span></span>

<span data-ttu-id="a6340-125">**Retenção de log**</span><span class="sxs-lookup"><span data-stu-id="a6340-125">**Log retention**</span></span>

<span data-ttu-id="a6340-126">Convém manter uma cópia dos arquivos de log gerados pelas tarefas ou talvez arquivos de despejo de memória que podem ser gerados pelos aplicativos que falharam.</span><span class="sxs-lookup"><span data-stu-id="a6340-126">You might want to keep a copy of log files that your tasks generate, or perhaps crash dump files that can be generated by failed applications.</span></span> <span data-ttu-id="a6340-127">Use uma **tarefa de liberação de trabalho** nesses casos para compactar e carregar esses dados para uma conta de [Armazenamento do Azure][azure_storage].</span><span class="sxs-lookup"><span data-stu-id="a6340-127">Use a **job release task** in such cases to compress and upload this data to an [Azure Storage][azure_storage] account.</span></span>

> [!TIP]
> <span data-ttu-id="a6340-128">Outra maneira de manter os logs e outros trabalhos e tarefas de saída de dados é usar a biblioteca [Convenções de arquivo do Lote do Azure](batch-task-output.md) .</span><span class="sxs-lookup"><span data-stu-id="a6340-128">Another way to persist logs and other job and task output data is to use the [Azure Batch File Conventions](batch-task-output.md) library.</span></span>
> 
> 

## <a name="job-preparation-task"></a><span data-ttu-id="a6340-129">tarefa de preparação de trabalho</span><span class="sxs-lookup"><span data-stu-id="a6340-129">Job preparation task</span></span>
<span data-ttu-id="a6340-130">Antes da execução de tarefas de um trabalho, o Lote executa a tarefa de preparação de trabalho em cada nó de computação agendado para executar uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="a6340-130">Before execution of a job's tasks, Batch executes the job preparation task on each compute node that is scheduled to run a task.</span></span> <span data-ttu-id="a6340-131">Por padrão, o serviço Lote aguarda a conclusão da tarefa de preparação do trabalho antes de executar as tarefas agendadas para execução no nó.</span><span class="sxs-lookup"><span data-stu-id="a6340-131">By default, the Batch service waits for the job preparation task to be completed before running the tasks scheduled to execute on the node.</span></span> <span data-ttu-id="a6340-132">No entanto, você pode configurar o serviço para não aguardar.</span><span class="sxs-lookup"><span data-stu-id="a6340-132">However, you can configure the service not to wait.</span></span> <span data-ttu-id="a6340-133">Se o nó for reiniciado, a tarefa de preparação de trabalho será executada novamente, mas você também poderá desativar esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="a6340-133">If the node restarts, the job preparation task runs again, but you can also disable this behavior.</span></span>

<span data-ttu-id="a6340-134">A tarefa de preparação de trabalho é executada apenas em nós programados para executar uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="a6340-134">The job preparation task is executed only on nodes that are scheduled to run a task.</span></span> <span data-ttu-id="a6340-135">Isso impede a execução desnecessária de uma tarefa de preparação em um nó que não recebeu uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="a6340-135">This prevents the unnecessary execution of a preparation task in case a node is not assigned a task.</span></span> <span data-ttu-id="a6340-136">Isso pode ocorrer quando o número de tarefas de um trabalho é menor do que o número de nós em um pool.</span><span class="sxs-lookup"><span data-stu-id="a6340-136">This can occur when the number of tasks for a job is less than the number of nodes in a pool.</span></span> <span data-ttu-id="a6340-137">Também se aplica quando a [execução de tarefas simultâneas](batch-parallel-node-tasks.md) é habilitada, o que deixará alguns nós ociosos se a contagem de tarefas for inferior ao total de possíveis tarefas simultâneas.</span><span class="sxs-lookup"><span data-stu-id="a6340-137">It also applies when [concurrent task execution](batch-parallel-node-tasks.md) is enabled, which leaves some nodes idle if the task count is lower than the total possible concurrent tasks.</span></span> <span data-ttu-id="a6340-138">A não execução da tarefa de preparação do trabalho em nós ociosos economiza encargos de transferência de dados.</span><span class="sxs-lookup"><span data-stu-id="a6340-138">By not running the job preparation task on idle nodes, you can spend less money on data transfer charges.</span></span>

> [!NOTE]
> <span data-ttu-id="a6340-139">[JobPreparationTask][net_job_prep_cloudjob] é diferente de [CloudPool.StartTask][pool_starttask], visto que JobPreparationTask é executado no início de cada trabalho, enquanto StartTask é executado apenas quando um nó de computação ingressa em um pool pela primeira vez ou é reiniciado.</span><span class="sxs-lookup"><span data-stu-id="a6340-139">[JobPreparationTask][net_job_prep_cloudjob] differs from [CloudPool.StartTask][pool_starttask] in that JobPreparationTask executes at the start of each job, whereas StartTask executes only when a compute node first joins a pool or restarts.</span></span>
> 
> 

## <a name="job-release-task"></a><span data-ttu-id="a6340-140">tarefa de liberação de trabalho</span><span class="sxs-lookup"><span data-stu-id="a6340-140">Job release task</span></span>
<span data-ttu-id="a6340-141">Quando um trabalho é marcado como concluído, a tarefa de liberação do trabalho é executada em cada nó no pool que executou pelo menos uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="a6340-141">Once a job is marked as completed, the job release task is executed on each node in the pool that executed at least one task.</span></span> <span data-ttu-id="a6340-142">Marcar uma tarefa como concluída emitindo uma solicitação de encerramento.</span><span class="sxs-lookup"><span data-stu-id="a6340-142">You mark a job as completed by issuing a terminate request.</span></span> <span data-ttu-id="a6340-143">Em seguida, o serviço do Lote define o estado do trabalho como *encerrando*, encerra quaisquer tarefas em execução ou ativas associadas ao trabalho e executa a tarefa de liberação do trabalho.</span><span class="sxs-lookup"><span data-stu-id="a6340-143">The Batch service then sets the job state to *terminating*, terminates any active or running tasks associated with the job, and runs the job release task.</span></span> <span data-ttu-id="a6340-144">Em seguida, o trabalho é movido para o estado *concluído* .</span><span class="sxs-lookup"><span data-stu-id="a6340-144">The job then moves to the *completed* state.</span></span>

> [!NOTE]
> <span data-ttu-id="a6340-145">A exclusão do trabalho também executa a tarefa de liberação do trabalho.</span><span class="sxs-lookup"><span data-stu-id="a6340-145">Job deletion also executes the job release task.</span></span> <span data-ttu-id="a6340-146">No entanto, se um trabalho já tiver sido encerrado, a tarefa de liberação não será executada uma segunda vez se o trabalho for excluído posteriormente.</span><span class="sxs-lookup"><span data-stu-id="a6340-146">However, if a job has already been terminated, the release task is not run a second time if the job is later deleted.</span></span>
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a><span data-ttu-id="a6340-147">Tarefas de preparação e liberação de trabalho com o Lote .NET</span><span class="sxs-lookup"><span data-stu-id="a6340-147">Job prep and release tasks with Batch .NET</span></span>
<span data-ttu-id="a6340-148">Para usar uma tarefa de preparação de trabalho, atribua um objeto [JobPreparationTask][net_job_prep] à propriedade [CloudJob.JobPreparationTask][net_job_prep_cloudjob] do seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="a6340-148">To use a job preparation task, assign a [JobPreparationTask][net_job_prep] object to your job's [CloudJob.JobPreparationTask][net_job_prep_cloudjob] property.</span></span> <span data-ttu-id="a6340-149">Da mesma forma, inicialize um [JobReleaseTask][net_job_release] e atribua-o à propriedade [CloudJob.JobReleaseTask][net_job_prep_cloudjob] para definir a tarefa de liberação do trabalho.</span><span class="sxs-lookup"><span data-stu-id="a6340-149">Similarly, initialize a [JobReleaseTask][net_job_release] and assign it to your job's [CloudJob.JobReleaseTask][net_job_prep_cloudjob] property to set the job's release task.</span></span>

<span data-ttu-id="a6340-150">Neste trecho de código, `myBatchClient` é uma instância de [BatchClient][net_batch_client] e `myPool` é um pool existente dentro da conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="a6340-150">In this code snippet, `myBatchClient` is an instance of [BatchClient][net_batch_client], and `myPool` is an existing pool within the Batch account.</span></span>

```csharp
// Create the CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify the command lines for the job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign the job preparation task to the job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign the job release task to the job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

<span data-ttu-id="a6340-151">Conforme mencionado anteriormente, a tarefa de liberação é executada quando um trabalho é encerrado ou excluído.</span><span class="sxs-lookup"><span data-stu-id="a6340-151">As mentioned earlier, the release task is executed when a job is terminated or deleted.</span></span> <span data-ttu-id="a6340-152">Encerre um trabalho com [JobOperations.TerminateJobAsync][net_job_terminate].</span><span class="sxs-lookup"><span data-stu-id="a6340-152">Terminate a job with [JobOperations.TerminateJobAsync][net_job_terminate].</span></span> <span data-ttu-id="a6340-153">Exclua um trabalho com [JobOperations.DeleteJobAsync][net_job_delete].</span><span class="sxs-lookup"><span data-stu-id="a6340-153">Delete a job with [JobOperations.DeleteJobAsync][net_job_delete].</span></span> <span data-ttu-id="a6340-154">Normalmente você encerra ou exclui um trabalho quando as tarefas são concluídas ou quando um tempo limite definido foi atingido.</span><span class="sxs-lookup"><span data-stu-id="a6340-154">You typically terminate or delete a job when its tasks are completed, or when a timeout that you've defined has been reached.</span></span>

```csharp
// Terminate the job to mark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a><span data-ttu-id="a6340-155">Exemplo de código no GitHub</span><span class="sxs-lookup"><span data-stu-id="a6340-155">Code sample on GitHub</span></span>
<span data-ttu-id="a6340-156">Para ver as tarefas de preparação e liberação de trabalho em ação, confira o projeto de exemplo [JobPrepRelease][job_prep_release_sample] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="a6340-156">To see job preparation and release tasks in action, check out the [JobPrepRelease][job_prep_release_sample] sample project on GitHub.</span></span> <span data-ttu-id="a6340-157">Esse aplicativo de console faz o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a6340-157">This console application does the following:</span></span>

1. <span data-ttu-id="a6340-158">Cria um pool com dois nós "pequenos".</span><span class="sxs-lookup"><span data-stu-id="a6340-158">Creates a pool with two "small" nodes.</span></span>
2. <span data-ttu-id="a6340-159">Cria um trabalho com tarefas de preparação, de liberação e padrão de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a6340-159">Creates a job with job preparation, release, and standard tasks.</span></span>
3. <span data-ttu-id="a6340-160">Executa a tarefa de preparação de trabalho, que primeiro grava a ID do nó em um arquivo de texto no diretório "compartilhado" do nó.</span><span class="sxs-lookup"><span data-stu-id="a6340-160">Runs the job preparation task, which first writes the node ID to a text file in a node's "shared" directory.</span></span>
4. <span data-ttu-id="a6340-161">Executa uma tarefa em cada nó que grava sua ID de tarefa no mesmo arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="a6340-161">Runs a task on each node that writes its task ID to the same text file.</span></span>
5. <span data-ttu-id="a6340-162">Depois que todas as tarefas forem concluídas (ou que o tempo limite for atingido), imprime o conteúdo do arquivo de texto de cada nó no console.</span><span class="sxs-lookup"><span data-stu-id="a6340-162">Once all tasks are completed (or the timeout is reached), prints the contents of each node's text file to the console.</span></span>
6. <span data-ttu-id="a6340-163">Quando o trabalho é concluído, executa a tarefa de liberação de trabalho para excluir o arquivo do nó.</span><span class="sxs-lookup"><span data-stu-id="a6340-163">When the job is completed, runs the job release task to delete the file from the node.</span></span>
7. <span data-ttu-id="a6340-164">Imprime os códigos de saída das tarefas de preparação e liberação de trabalho para cada nó no qual elas são executadas.</span><span class="sxs-lookup"><span data-stu-id="a6340-164">Prints the exit codes of the job preparation and release tasks for each node on which they executed.</span></span>
8. <span data-ttu-id="a6340-165">Pausa a execução para permitir a confirmação da exclusão do trabalho e/ou pool.</span><span class="sxs-lookup"><span data-stu-id="a6340-165">Pauses execution to allow confirmation of job and/or pool deletion.</span></span>

<span data-ttu-id="a6340-166">A saída do aplicativo de exemplo é semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="a6340-166">Output from the sample application is similar to the following:</span></span>

```
Attempting to create pool: JobPrepReleaseSamplePool
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

Waiting for job JobPrepReleaseSampleJob to reach state Completed
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

Sample complete, hit ENTER to exit...
```

> [!NOTE]
> <span data-ttu-id="a6340-167">Devido ao tempo variável de criação e início dos nós em um novo pool (alguns nós ficam prontos para tarefas antes de outros), você pode ver uma saída diferente.</span><span class="sxs-lookup"><span data-stu-id="a6340-167">Due to the variable creation and start time of nodes in a new pool (some nodes are ready for tasks before others), you may see different output.</span></span> <span data-ttu-id="a6340-168">Especificamente, como as tarefas são concluídas rapidamente, um dos nós do pool pode executar todas as tarefas do trabalho.</span><span class="sxs-lookup"><span data-stu-id="a6340-168">Specifically, because the tasks complete quickly, one of the pool's nodes may execute all of the job's tasks.</span></span> <span data-ttu-id="a6340-169">Se isso ocorrer, você observará que as tarefas de preparação e liberação do trabalho não existem para o nó que não executou nenhuma tarefa.</span><span class="sxs-lookup"><span data-stu-id="a6340-169">If this occurs, you will notice that the job prep and release tasks do not exist for the node that executed no tasks.</span></span>
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-the-azure-portal"></a><span data-ttu-id="a6340-170">Inspecionar as tarefas de preparação e liberação do trabalho no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a6340-170">Inspect job preparation and release tasks in the Azure portal</span></span>
<span data-ttu-id="a6340-171">Quando estiver executando o aplicativo de exemplo, você poderá usar o [portal do Azure][portal] para exibir as propriedades do trabalho e suas tarefas ou até mesmo baixar o arquivo de texto compartilhado que é modificado pelas tarefas do trabalho.</span><span class="sxs-lookup"><span data-stu-id="a6340-171">When you run the sample application, you can use the [Azure portal][portal] to view the properties of the job and its tasks, or even download the shared text file that is modified by the job's tasks.</span></span>

<span data-ttu-id="a6340-172">A captura de tela abaixo mostra a **Folha de tarefas de preparação** no portal do Azure após uma execução do aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="a6340-172">The screenshot below shows the **Preparation tasks blade** in the Azure portal after a run of the sample application.</span></span> <span data-ttu-id="a6340-173">Navegue até as propriedades *JobPrepReleaseSampleJob* após a conclusão das tarefas (mas antes de excluir seu trabalho e pool) e clique em **Tarefas de preparação** ou **Tarefas de liberação** para exibir suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="a6340-173">Navigate to the *JobPrepReleaseSampleJob* properties after your tasks have completed (but before deleting your job and pool) and click **Preparation tasks** or **Release tasks** to view their properties.</span></span>

![Propriedades de preparação de trabalho no portal do Azure][1]

## <a name="next-steps"></a><span data-ttu-id="a6340-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a6340-175">Next steps</span></span>
### <a name="application-packages"></a><span data-ttu-id="a6340-176">Pacotes de aplicativos</span><span class="sxs-lookup"><span data-stu-id="a6340-176">Application packages</span></span>
<span data-ttu-id="a6340-177">Além da tarefa de preparação de trabalho, você também pode usar o recurso de [pacotes de aplicativos](batch-application-packages.md) do Lote para preparar nós de computação para execução da tarefa.</span><span class="sxs-lookup"><span data-stu-id="a6340-177">In addition to the job preparation task, you can also use the [application packages](batch-application-packages.md) feature of Batch to prepare compute nodes for task execution.</span></span> <span data-ttu-id="a6340-178">Esse recurso é especialmente útil para implantação de aplicativos que não exigem a execução de um instalados, aplicativos que contêm muitos arquivos (mais de 100) ou aplicativos que exigem um controle de versão estrito.</span><span class="sxs-lookup"><span data-stu-id="a6340-178">This feature is especially useful for deploying applications that do not require running an installer, applications that contain many (100+) files, or applications that require strict version control.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="a6340-179">Instalação de aplicativos e preparação de dados</span><span class="sxs-lookup"><span data-stu-id="a6340-179">Installing applications and staging data</span></span>
<span data-ttu-id="a6340-180">Essa postagem no fórum da MSDN fornece uma visão geral dos vários métodos de preparação de seus nós para a execução de tarefas:</span><span class="sxs-lookup"><span data-stu-id="a6340-180">This MSDN forum post provides an overview of several methods of preparing your nodes for running tasks:</span></span>

<span data-ttu-id="a6340-181">[Instalando aplicativos e preparando dados em nós de computação do Lote][forum_post]</span><span class="sxs-lookup"><span data-stu-id="a6340-181">[Installing applications and staging data on Batch compute nodes][forum_post]</span></span>

<span data-ttu-id="a6340-182">Escrito por um dos membros da equipe do Lote do Azure, ele aborda várias técnicas que você pode usar para implantar aplicativos e dados em nós de computação.</span><span class="sxs-lookup"><span data-stu-id="a6340-182">Written by one of the Azure Batch team members, it discusses several techniques that you can use to deploy applications and data to compute nodes.</span></span>

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
