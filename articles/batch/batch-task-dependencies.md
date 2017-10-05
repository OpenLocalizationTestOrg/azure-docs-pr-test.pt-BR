---
title: "Usar dependências de tarefas para executar tarefas com base na conclusão de outras tarefas - Lote do Azure | Microsoft Docs"
description: "Crie tarefas que dependem da conclusão de outras tarefas para o processamento em estilo MapReduce e cargas de trabalho de big data semelhantes no Lote do Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: b8d12db5-ca30-4c7d-993a-a05af9257210
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 465306d2de8d1dbe6ba1f0cd74be720b78a50de3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-task-dependencies-to-run-tasks-that-depend-on-other-tasks"></a><span data-ttu-id="e8d68-103">Crie dependências de tarefas para executar tarefas que dependam de outras tarefas</span><span class="sxs-lookup"><span data-stu-id="e8d68-103">Create task dependencies to run tasks that depend on other tasks</span></span>

<span data-ttu-id="e8d68-104">É possível definir dependências entre tarefas para executar uma tarefa ou um conjunto de tarefas somente após a conclusão de uma tarefa pai.</span><span class="sxs-lookup"><span data-stu-id="e8d68-104">You can define task dependencies to run a task or set of tasks only after a parent task has completed.</span></span> <span data-ttu-id="e8d68-105">Alguns cenários em que as dependências entre tarefas são úteis incluem:</span><span class="sxs-lookup"><span data-stu-id="e8d68-105">Some scenarios where task dependencies are useful include:</span></span>

* <span data-ttu-id="e8d68-106">Cargas de trabalho de estilo MapReduce na nuvem.</span><span class="sxs-lookup"><span data-stu-id="e8d68-106">MapReduce-style workloads in the cloud.</span></span>
* <span data-ttu-id="e8d68-107">Trabalhos cujas tarefas de processamento de dados podem ser expressas como um DAG (gráfico acíclico dirigido).</span><span class="sxs-lookup"><span data-stu-id="e8d68-107">Jobs whose data processing tasks can be expressed as a directed acyclic graph (DAG).</span></span>
* <span data-ttu-id="e8d68-108">Processos de pré-renderização e pós-renderização, em que cada tarefa deve ser concluída antes do início da próxima.</span><span class="sxs-lookup"><span data-stu-id="e8d68-108">Pre-rendering and post-rendering processes, where each task must complete before the next task can begin.</span></span>
* <span data-ttu-id="e8d68-109">Qualquer outro trabalho no qual tarefas downstream dependem da saída das tarefas upstream.</span><span class="sxs-lookup"><span data-stu-id="e8d68-109">Any other job in which downstream tasks depend on the output of upstream tasks.</span></span>

<span data-ttu-id="e8d68-110">Com dependências entre tarefas do Lote, é possível criar tarefas que estão agendadas para execução em nós de computação após a conclusão de uma ou mais tarefas pai.</span><span class="sxs-lookup"><span data-stu-id="e8d68-110">With Batch task dependencies, you can create tasks that are scheduled for execution on compute nodes after the completion of one or more parent tasks.</span></span> <span data-ttu-id="e8d68-111">Por exemplo, você pode criar um trabalho que processa cada quadro de um filme 3D com tarefas paralelas separadas.</span><span class="sxs-lookup"><span data-stu-id="e8d68-111">For example, you can create a job that renders each frame of a 3D movie with separate, parallel tasks.</span></span> <span data-ttu-id="e8d68-112">A tarefa final, a "tarefa de mesclagem", mescla os quadros renderizados no filme completo somente depois que todos os quadros são gerados com êxito.</span><span class="sxs-lookup"><span data-stu-id="e8d68-112">The final task--the "merge task"--merges the rendered frames into the complete movie only after all frames have been successfully rendered.</span></span>

<span data-ttu-id="e8d68-113">Por padrão, as tarefas dependentes estão agendadas para execução somente após a conclusão bem-sucedida da tarefa pai.</span><span class="sxs-lookup"><span data-stu-id="e8d68-113">By default, dependent tasks are scheduled for execution only after the parent task has completed successfully.</span></span> <span data-ttu-id="e8d68-114">É possível especificar uma ação de dependência para substituir o comportamento padrão e executar tarefas quando a tarefa pai falha.</span><span class="sxs-lookup"><span data-stu-id="e8d68-114">You can specify a dependency action to override the default behavior and run tasks when the parent task fails.</span></span> <span data-ttu-id="e8d68-115">Consulte a seção [Ações de dependência](#dependency-actions) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="e8d68-115">See the [Dependency actions](#dependency-actions) section for details.</span></span>  

<span data-ttu-id="e8d68-116">Você pode criar tarefas que dependem de outras tarefas em uma relação um para um ou um para muitos.</span><span class="sxs-lookup"><span data-stu-id="e8d68-116">You can create tasks that depend on other tasks in a one-to-one or one-to-many relationship.</span></span> <span data-ttu-id="e8d68-117">Também é possível criar uma dependência entre intervalos, em que uma tarefa depende da conclusão de um grupo de tarefas em um intervalo especificado de identificações da tarefa.</span><span class="sxs-lookup"><span data-stu-id="e8d68-117">You can also create a range dependency where a task depends on the completion of a group of tasks within a specified range of task IDs.</span></span> <span data-ttu-id="e8d68-118">Você pode combinar esses três cenários básicos para criar relações muitos-para-muitos.</span><span class="sxs-lookup"><span data-stu-id="e8d68-118">You can combine these three basic scenarios to create many-to-many relationships.</span></span>

## <a name="task-dependencies-with-batch-net"></a><span data-ttu-id="e8d68-119">Dependências de tarefas com o .NET do Lote</span><span class="sxs-lookup"><span data-stu-id="e8d68-119">Task dependencies with Batch .NET</span></span>
<span data-ttu-id="e8d68-120">Neste artigo, discutimos como configurar dependências de tarefas usando a biblioteca [.NET do Lote][net_msdn].</span><span class="sxs-lookup"><span data-stu-id="e8d68-120">In this article, we discuss how to configure task dependencies by using the [Batch .NET][net_msdn] library.</span></span> <span data-ttu-id="e8d68-121">Primeiro mostramos como [habilitar a dependência de tarefa](#enable-task-dependencies) nos trabalhos. Em seguida, demonstramos brevemente como [configurar uma tarefa com dependências](#create-dependent-tasks).</span><span class="sxs-lookup"><span data-stu-id="e8d68-121">We first show you how to [enable task dependency](#enable-task-dependencies) on your jobs, and then demonstrate how to [configure a task with dependencies](#create-dependent-tasks).</span></span> <span data-ttu-id="e8d68-122">Também descrevemos como especificar uma ação de dependência para executar tarefas dependentes em caso de falha do pai.</span><span class="sxs-lookup"><span data-stu-id="e8d68-122">We also describe how to specify a dependency action to run dependent tasks if the parent fails.</span></span> <span data-ttu-id="e8d68-123">Finalmente, discutiremos os [cenários de dependência](#dependency-scenarios) aos quais o Lote dá suporte.</span><span class="sxs-lookup"><span data-stu-id="e8d68-123">Finally, we discuss the [dependency scenarios](#dependency-scenarios) that Batch supports.</span></span>

## <a name="enable-task-dependencies"></a><span data-ttu-id="e8d68-124">Habilitar dependências de tarefas</span><span class="sxs-lookup"><span data-stu-id="e8d68-124">Enable task dependencies</span></span>
<span data-ttu-id="e8d68-125">Para usar dependências entre tarefas no aplicativo do Lote, é necessário primeiro configurar o trabalho para usar dependências entre tarefas.</span><span class="sxs-lookup"><span data-stu-id="e8d68-125">To use task dependencies in your Batch application, you must first configure the job to use task dependencies.</span></span> <span data-ttu-id="e8d68-126">No .NET do Lote, habilite-o no [CloudJob][net_cloudjob] configurando a propriedade [UsesTaskDependencies][net_usestaskdependencies] como `true`:</span><span class="sxs-lookup"><span data-stu-id="e8d68-126">In Batch .NET, enable it on your [CloudJob][net_cloudjob] by setting its [UsesTaskDependencies][net_usestaskdependencies] property to `true`:</span></span>

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

<span data-ttu-id="e8d68-127">No trecho de código anterior, "batchClient" é uma instância da classe [BatchClient][net_batchclient].</span><span class="sxs-lookup"><span data-stu-id="e8d68-127">In the preceding code snippet, "batchClient" is an instance of the [BatchClient][net_batchclient] class.</span></span>

## <a name="create-dependent-tasks"></a><span data-ttu-id="e8d68-128">Criar tarefas dependentes</span><span class="sxs-lookup"><span data-stu-id="e8d68-128">Create dependent tasks</span></span>
<span data-ttu-id="e8d68-129">Para criar uma tarefa que depende da conclusão de uma ou mais tarefas pai, é possível especificar que a tarefa “depende” das outras tarefas.</span><span class="sxs-lookup"><span data-stu-id="e8d68-129">To create a task that depends on the completion of one or more parent tasks, you can specify that the task "depends on" the other tasks.</span></span> <span data-ttu-id="e8d68-130">No .NET do Lote, configure a propriedade [CloudTask][net_cloudtask].[DependsOn][net_dependson] com uma instância da classe [TaskDependencies][net_taskdependencies]:</span><span class="sxs-lookup"><span data-stu-id="e8d68-130">In Batch .NET, configure the [CloudTask][net_cloudtask].[DependsOn][net_dependson] property with an instance of the [TaskDependencies][net_taskdependencies] class:</span></span>

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

<span data-ttu-id="e8d68-131">Este trecho de código cria uma tarefa dependente com a identificação da tarefa “Flowers”.</span><span class="sxs-lookup"><span data-stu-id="e8d68-131">This code snippet creates a dependent task with task ID "Flowers".</span></span> <span data-ttu-id="e8d68-132">A tarefa “Flowers” depende das tarefas “Rain” e “Sun”.</span><span class="sxs-lookup"><span data-stu-id="e8d68-132">The "Flowers" task depends on tasks "Rain" and "Sun".</span></span> <span data-ttu-id="e8d68-133">A tarefa “Flowers” será agendada para execução em um nó de computação somente após a conclusão bem-sucedida das tarefas “Rain” e “Sun”.</span><span class="sxs-lookup"><span data-stu-id="e8d68-133">Task "Flowers" will be scheduled to run on a compute node only after tasks "Rain" and "Sun" have completed successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="e8d68-134">Uma tarefa é considerada concluída com êxito quando está no estado **concluído** e seu **código de saída** é `0`.</span><span class="sxs-lookup"><span data-stu-id="e8d68-134">A task is considered to be completed successfully when it is in the **completed** state and its **exit code** is `0`.</span></span> <span data-ttu-id="e8d68-135">No .NET do Lote, isso significa que o valor da propriedade [CloudTask][net_cloudtask].[State][net_taskstate] é `Completed` e o valor da propriedade [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] de CloudTask é `0`.</span><span class="sxs-lookup"><span data-stu-id="e8d68-135">In Batch .NET, this means a [CloudTask][net_cloudtask].[State][net_taskstate] property value of `Completed` and the CloudTask's [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] property value is `0`.</span></span>
> 
> 

## <a name="dependency-scenarios"></a><span data-ttu-id="e8d68-136">Cenários de dependência</span><span class="sxs-lookup"><span data-stu-id="e8d68-136">Dependency scenarios</span></span>
<span data-ttu-id="e8d68-137">Há três cenários de dependência de tarefas básicos que você pode usar no Lote do Azure: um-para-um, um-para-muitos e dependência de intervalo de IDs de tarefas.</span><span class="sxs-lookup"><span data-stu-id="e8d68-137">There are three basic task dependency scenarios that you can use in Azure Batch: one-to-one, one-to-many, and task ID range dependency.</span></span> <span data-ttu-id="e8d68-138">Eles podem ser combinados para fornecer um quarto cenário, muitos-para-muitos.</span><span class="sxs-lookup"><span data-stu-id="e8d68-138">These can be combined to provide a fourth scenario, many-to-many.</span></span>

| <span data-ttu-id="e8d68-139">Cenário&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="e8d68-139">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="e8d68-140">Exemplo</span><span class="sxs-lookup"><span data-stu-id="e8d68-140">Example</span></span> |  |
|:---:| --- | --- |
|  [<span data-ttu-id="e8d68-141">Um-para-um</span><span class="sxs-lookup"><span data-stu-id="e8d68-141">One-to-one</span></span>](#one-to-one) |<span data-ttu-id="e8d68-142">*tarefaB* depende de *tarefaA*</span><span class="sxs-lookup"><span data-stu-id="e8d68-142">*taskB* depends on *taskA*</span></span> <p/> <span data-ttu-id="e8d68-143">A *tarefaB* não será agendada para execução até que a *tarefaA* seja concluída com êxito</span><span class="sxs-lookup"><span data-stu-id="e8d68-143">*taskB* will not be scheduled for execution until *taskA* has completed successfully</span></span> |<span data-ttu-id="e8d68-144">![Diagrama: dependência de tarefa de um para um][1]</span><span class="sxs-lookup"><span data-stu-id="e8d68-144">![Diagram: one-to-one task dependency][1]</span></span> |
|  [<span data-ttu-id="e8d68-145">Um-para-muitos</span><span class="sxs-lookup"><span data-stu-id="e8d68-145">One-to-many</span></span>](#one-to-many) |<span data-ttu-id="e8d68-146">A *tarefaC* depende da *tarefaA* e da *tarefaB*</span><span class="sxs-lookup"><span data-stu-id="e8d68-146">*taskC* depends on both *taskA* and *taskB*</span></span> <p/> <span data-ttu-id="e8d68-147">A *tarefaC* não será agendada para execução até que a *tarefaA* e a *tarefaB* sejam concluídas com êxito</span><span class="sxs-lookup"><span data-stu-id="e8d68-147">*taskC* will not be scheduled for execution until both *taskA* and *taskB* have completed successfully</span></span> |<span data-ttu-id="e8d68-148">![Diagrama: dependência de tarefa de um para muitos][2]</span><span class="sxs-lookup"><span data-stu-id="e8d68-148">![Diagram: one-to-many task dependency][2]</span></span> |
|  [<span data-ttu-id="e8d68-149">Intervalo de IDs de tarefa</span><span class="sxs-lookup"><span data-stu-id="e8d68-149">Task ID range</span></span>](#task-id-range) |<span data-ttu-id="e8d68-150">A *taskD* depende de diversas tarefas</span><span class="sxs-lookup"><span data-stu-id="e8d68-150">*taskD* depends on a range of tasks</span></span> <p/> <span data-ttu-id="e8d68-151">A *tarefaD* não será agendada para execução até que as tarefas com as IDs *1* a *10* sejam concluídas com êxito</span><span class="sxs-lookup"><span data-stu-id="e8d68-151">*taskD* will not be scheduled for execution until the tasks with IDs *1* through *10* have completed successfully</span></span> |<span data-ttu-id="e8d68-152">![Diagrama: dependência de intervalo de ids de tarefas][3]</span><span class="sxs-lookup"><span data-stu-id="e8d68-152">![Diagram: Task id range dependency][3]</span></span> |

> [!TIP]
> <span data-ttu-id="e8d68-153">Você pode criar relações **muitos para muitos**, como uma em que as tarefas C, D, E e F dependem das tarefas A e B. Isso é útil, por exemplo, em cenários de pré-processamento em paralelo em que as tarefas downstream dependem da saída de várias tarefas upstream.</span><span class="sxs-lookup"><span data-stu-id="e8d68-153">You can create **many-to-many** relationships, such as where tasks C, D, E, and F each depend on tasks A and B. This is useful, for example, in parallelized preprocessing scenarios where your downstream tasks depend on the output of multiple upstream tasks.</span></span>
> 
> <span data-ttu-id="e8d68-154">Nos exemplos desta seção, uma tarefa dependente é executada somente após a conclusão bem-sucedida das tarefas pai.</span><span class="sxs-lookup"><span data-stu-id="e8d68-154">In the examples in this section, a dependent task runs only after the parent tasks complete successfully.</span></span> <span data-ttu-id="e8d68-155">Esse comportamento é o comportamento padrão de uma tarefa dependente.</span><span class="sxs-lookup"><span data-stu-id="e8d68-155">This behavior is the default behavior for a dependent task.</span></span> <span data-ttu-id="e8d68-156">É possível executar uma tarefa dependente após uma falha da tarefa pai especificando uma ação de dependência para substituir o comportamento padrão.</span><span class="sxs-lookup"><span data-stu-id="e8d68-156">You can run a dependent task after a parent task fails by specifying a dependency action to override the default behavior.</span></span> <span data-ttu-id="e8d68-157">Consulte a seção [Ações de dependência](#dependency-actions) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="e8d68-157">See the [Dependency actions](#dependency-actions) section for details.</span></span>

### <a name="one-to-one"></a><span data-ttu-id="e8d68-158">Um-para-um</span><span class="sxs-lookup"><span data-stu-id="e8d68-158">One-to-one</span></span>
<span data-ttu-id="e8d68-159">Em uma relação um-para-um, uma tarefa depende da conclusão bem-sucedida de uma tarefa pai.</span><span class="sxs-lookup"><span data-stu-id="e8d68-159">In a one-to-one relationship, a task depends on the successful completion of one parent task.</span></span> <span data-ttu-id="e8d68-160">Para criar a dependência, forneça uma única identificação da tarefa para o método estático [TaskDependencies][net_taskdependencies].[OnId][net_onid] ao popular a propriedade [DependsOn][net_dependson] de [CloudTask][net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="e8d68-160">To create the dependency, provide a single task ID to the [TaskDependencies][net_taskdependencies].[OnId][net_onid] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a><span data-ttu-id="e8d68-161">Um-para-muitos</span><span class="sxs-lookup"><span data-stu-id="e8d68-161">One-to-many</span></span>
<span data-ttu-id="e8d68-162">Em uma relação um-para-muitos, uma tarefa depende da conclusão de várias tarefas pai.</span><span class="sxs-lookup"><span data-stu-id="e8d68-162">In a one-to-many relationship, a task depends on the completion of multiple parent tasks.</span></span> <span data-ttu-id="e8d68-163">Para criar a dependência, forneça uma coleção de identificações da tarefa para o método estático [TaskDependencies][net_taskdependencies].[OnIds][net_onids] ao popular a propriedade [DependsOn][net_dependson] de [CloudTask][net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="e8d68-163">To create the dependency, provide a collection of task IDs to the [TaskDependencies][net_taskdependencies].[OnIds][net_onids] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// 'Rain' and 'Sun' don't depend on any other tasks
new CloudTask("Rain", "cmd.exe /c echo Rain"),
new CloudTask("Sun", "cmd.exe /c echo Sun"),

// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
``` 

### <a name="task-id-range"></a><span data-ttu-id="e8d68-164">Intervalo de IDs de tarefa</span><span class="sxs-lookup"><span data-stu-id="e8d68-164">Task ID range</span></span>
<span data-ttu-id="e8d68-165">Em uma dependência em um intervalo de tarefas pai, uma tarefa depende da conclusão de tarefas cujas IDs estão em um intervalo.</span><span class="sxs-lookup"><span data-stu-id="e8d68-165">In a dependency on a range of parent tasks, a task depends on the the completion of tasks whose IDs lie within a range.</span></span>
<span data-ttu-id="e8d68-166">Para criar a dependência, forneça a primeira e a última identificação da tarefa no intervalo para o método estático [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] ao popular a propriedade [DependsOn][net_dependson] de [CloudTask][net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="e8d68-166">To create the dependency, provide the first and last task IDs in the range to the [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8d68-167">Quando você usa intervalos de IDs de tarefas para dependências, as IDs de tarefas no intervalo *devem* ser representações de cadeia de caracteres de valores inteiros.</span><span class="sxs-lookup"><span data-stu-id="e8d68-167">When you use task ID ranges for your dependencies, the task IDs in the range *must* be string representations of integer values.</span></span>
> 
> <span data-ttu-id="e8d68-168">Cada tarefa no intervalo deve atender à dependência, concluindo com êxito ou concluindo com uma falha que é mapeada para uma ação de dependência definida como **Atender**.</span><span class="sxs-lookup"><span data-stu-id="e8d68-168">Every task in the range must satisfy the dependency, either by completing successfully or by completing with a failure that’s mapped to a dependency action set to **Satisfy**.</span></span> <span data-ttu-id="e8d68-169">Consulte a seção [Ações de dependência](#dependency-actions) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="e8d68-169">See the [Dependency actions](#dependency-actions) section for details.</span></span>
>
>

```csharp
// Tasks 1, 2, and 3 don't depend on any other tasks. Because
// we will be using them for a task range dependency, we must
// specify string representations of integers as their ids.
new CloudTask("1", "cmd.exe /c echo 1"),
new CloudTask("2", "cmd.exe /c echo 2"),
new CloudTask("3", "cmd.exe /c echo 3"),

// Task 4 depends on a range of tasks, 1 through 3
new CloudTask("4", "cmd.exe /c echo 4")
{
    // To use a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters to TaskIdRange,
    // but their ids (above) are string representations of the ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a><span data-ttu-id="e8d68-170">Ações de dependência</span><span class="sxs-lookup"><span data-stu-id="e8d68-170">Dependency actions</span></span>

<span data-ttu-id="e8d68-171">Por padrão, uma tarefa dependente ou um conjunto de tarefas é executado somente após a conclusão bem-sucedida de uma tarefa pai.</span><span class="sxs-lookup"><span data-stu-id="e8d68-171">By default, a dependent task or set of tasks runs only after a parent task has completed successfully.</span></span> <span data-ttu-id="e8d68-172">Em alguns cenários, talvez você deseje executar tarefas dependentes mesmo se houver uma falha da tarefa pai.</span><span class="sxs-lookup"><span data-stu-id="e8d68-172">In some scenarios, you may want to run dependent tasks even if the parent task fails.</span></span> <span data-ttu-id="e8d68-173">É possível substituir o comportamento padrão especificando uma ação de dependência.</span><span class="sxs-lookup"><span data-stu-id="e8d68-173">You can override the default behavior by specifying a dependency action.</span></span> <span data-ttu-id="e8d68-174">Uma ação de dependência especifica se uma tarefa dependente é qualificada para execução, de acordo com o sucesso ou a falha da tarefa pai.</span><span class="sxs-lookup"><span data-stu-id="e8d68-174">A dependency action specifies whether a dependent task is eligible to run, based on the success or failure of the parent task.</span></span> 

<span data-ttu-id="e8d68-175">Por exemplo, suponha que uma tarefa dependente está aguardando dados da conclusão da tarefa upstream.</span><span class="sxs-lookup"><span data-stu-id="e8d68-175">For example, suppose that a dependent task is awaiting data from the completion of the upstream task.</span></span> <span data-ttu-id="e8d68-176">Se a tarefa upstream falhar, a tarefa dependente ainda poderá ser executada usando dados mais antigos.</span><span class="sxs-lookup"><span data-stu-id="e8d68-176">If the upstream task fails, the dependent task may still be able to run using older data.</span></span> <span data-ttu-id="e8d68-177">Nesse caso, uma ação de dependência pode especificar que a tarefa dependente é qualificada para execução, apesar da falha da tarefa pai.</span><span class="sxs-lookup"><span data-stu-id="e8d68-177">In this case, a dependency action can specify that the dependent task is eligible to run despite the failure of the parent task.</span></span>

<span data-ttu-id="e8d68-178">Uma ação de dependência baseia-se em uma condição de saída da tarefa pai.</span><span class="sxs-lookup"><span data-stu-id="e8d68-178">A dependency action is based on an exit condition for the parent task.</span></span> <span data-ttu-id="e8d68-179">É possível especificar uma ação de dependência para qualquer uma das condições de saída a seguir; para o .NET, consulte a classe [ExitConditions][net_exitconditions] para obter detalhes:</span><span class="sxs-lookup"><span data-stu-id="e8d68-179">You can specify a dependency action for any of the following exit conditions; for .NET, see the [ExitConditions][net_exitconditions] class for details:</span></span>

- <span data-ttu-id="e8d68-180">Quando ocorre um erro de pré-processamento.</span><span class="sxs-lookup"><span data-stu-id="e8d68-180">When a pre-processing error occurs.</span></span>
- <span data-ttu-id="e8d68-181">Quando ocorre um erro de carregamento de arquivo.</span><span class="sxs-lookup"><span data-stu-id="e8d68-181">When a file upload error occurs.</span></span> <span data-ttu-id="e8d68-182">Se a tarefa é encerrada com um código de saída especificado por meio de **exitCodes** ou **exitCodeRanges**, e, em seguida, encontra erro de carregamento de arquivo, a ação especificada pelo código de saída tem precedência.</span><span class="sxs-lookup"><span data-stu-id="e8d68-182">If the task exits with an exit code that was specified via **exitCodes** or **exitCodeRanges**, and then encounters a file upload error, the action specified by the exit code takes precedence.</span></span>
- <span data-ttu-id="e8d68-183">Quando a tarefa é encerrada com um código de saída definido pela propriedade **ExitCodes**.</span><span class="sxs-lookup"><span data-stu-id="e8d68-183">When the task exits with an exit code defined by the **ExitCodes** property.</span></span>
- <span data-ttu-id="e8d68-184">Quando a tarefa é encerrada com um código de saída que está dentro de um intervalo especificado pela propriedade **ExitCodeRanges**.</span><span class="sxs-lookup"><span data-stu-id="e8d68-184">When the task exits with an exit code that falls within a range specified by the **ExitCodeRanges** property.</span></span>
- <span data-ttu-id="e8d68-185">No caso padrão, se a tarefa for encerrada com um código de saída não definido por **ExitCodes** ou **ExitCodeRanges**, ou se a tarefa for encerrada com um erro de pré-processamento e a propriedade **PreProcessingError** não for definida, ou se houver erro de carregamento de arquivo e a propriedade **FileUploadError** não estiver definida.</span><span class="sxs-lookup"><span data-stu-id="e8d68-185">The default case, if the task exits with an exit code not defined by **ExitCodes** or **ExitCodeRanges**, or if the task exits with a pre-processing error and the **PreProcessingError** property is not set, or if the task fails with a file upload error and the **FileUploadError** property is not set.</span></span> 

<span data-ttu-id="e8d68-186">Para especificar uma ação de dependência no .NET, defina a propriedade [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] da condição de saída.</span><span class="sxs-lookup"><span data-stu-id="e8d68-186">To specify a dependency action in .NET, set the [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] property for the exit condition.</span></span> <span data-ttu-id="e8d68-187">A propriedade **DependencyAction** usa um dos dois valores:</span><span class="sxs-lookup"><span data-stu-id="e8d68-187">The **DependencyAction** property takes one of two values:</span></span>

- <span data-ttu-id="e8d68-188">A configuração da propriedade **DependencyAction** como **Atender** indica que as tarefas dependentes estão qualificadas para execução se a tarefa pai é encerrada com um erro especificado.</span><span class="sxs-lookup"><span data-stu-id="e8d68-188">Setting the **DependencyAction** property to **Satisfy** indicates that dependent tasks are eligible to run if the parent task exits with a specified error.</span></span>
- <span data-ttu-id="e8d68-189">A configuração da propriedade **DependencyAction** como **Bloquear** indica que as tarefas dependentes não estão qualificadas para execução.</span><span class="sxs-lookup"><span data-stu-id="e8d68-189">Setting the **DependencyAction** property to **Block** indicates that dependent tasks are not eligible to run.</span></span>

<span data-ttu-id="e8d68-190">A configuração padrão da propriedade **DependencyAction** é **Atender** para o código de saída 0 e **Bloquear** para todas as outras condições de saída.</span><span class="sxs-lookup"><span data-stu-id="e8d68-190">The default setting for the **DependencyAction** property is **Satisfy** for exit code 0, and **Block** for all other exit conditions.</span></span>

<span data-ttu-id="e8d68-191">O trecho de código a seguir define a propriedade **DependencyAction** de uma tarefa pai.</span><span class="sxs-lookup"><span data-stu-id="e8d68-191">The following code snippet sets the **DependencyAction** property for a parent task.</span></span> <span data-ttu-id="e8d68-192">Se a tarefa pai é encerrada com um erro de pré-processamento ou com os códigos de erro especificados, a tarefa dependente é bloqueada.</span><span class="sxs-lookup"><span data-stu-id="e8d68-192">If the parent task exits with a pre-processing error, or with the specified error codes, the dependent task is blocked.</span></span> <span data-ttu-id="e8d68-193">Se a tarefa pai é encerrada com qualquer outro erro diferente de zero, a tarefa dependente é qualificada para execução.</span><span class="sxs-lookup"><span data-stu-id="e8d68-193">If the parent task exits with any other non-zero error, the dependent task is eligible to run.</span></span>

```csharp
// Task A is the parent task.
new CloudTask("A", "cmd.exe /c echo A")
{
    // Specify exit conditions for task A and their dependency actions.
    ExitConditions = new ExitConditions
    {
        // If task A exits with a pre-processing error, block any downstream tasks (in this example, task B).
        PreProcessingError = new ExitOptions
        {
            DependencyAction = DependencyAction.Block
        },
        // If task A exits with the specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible to run 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible to run depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a><span data-ttu-id="e8d68-194">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="e8d68-194">Code sample</span></span>
<span data-ttu-id="e8d68-195">O projeto de exemplo [TaskDependencies][github_taskdependencies] é um dos [exemplos de código do Lote do Azure][github_samples] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="e8d68-195">The [TaskDependencies][github_taskdependencies] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="e8d68-196">Esta solução do Visual Studio demonstra:</span><span class="sxs-lookup"><span data-stu-id="e8d68-196">This Visual Studio solution demonstrates:</span></span>

- <span data-ttu-id="e8d68-197">Como habilitar a dependência entre tarefas em um trabalho</span><span class="sxs-lookup"><span data-stu-id="e8d68-197">How to enable task dependency on a job</span></span>
- <span data-ttu-id="e8d68-198">Como criar tarefas que dependem de outras tarefas</span><span class="sxs-lookup"><span data-stu-id="e8d68-198">How to create tasks that depend on other tasks</span></span>
- <span data-ttu-id="e8d68-199">Como executar essas tarefas em um pool de nós de computação.</span><span class="sxs-lookup"><span data-stu-id="e8d68-199">How to execute those tasks on a pool of compute nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8d68-200">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e8d68-200">Next steps</span></span>
### <a name="application-deployment"></a><span data-ttu-id="e8d68-201">Implantação do aplicativo</span><span class="sxs-lookup"><span data-stu-id="e8d68-201">Application deployment</span></span>
<span data-ttu-id="e8d68-202">O recurso de [pacotes de aplicativos](batch-application-packages.md) do lote fornece uma maneira fácil de implantar e controlar a versão dos aplicativos que as tarefas executam em nós de computação.</span><span class="sxs-lookup"><span data-stu-id="e8d68-202">The [application packages](batch-application-packages.md) feature of Batch provides an easy way to both deploy and version the applications that your tasks execute on compute nodes.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="e8d68-203">Instalação de aplicativos e preparação de dados</span><span class="sxs-lookup"><span data-stu-id="e8d68-203">Installing applications and staging data</span></span>
<span data-ttu-id="e8d68-204">Consulte [Instalando aplicativos e preparando dados em nós de computação do Lote][forum_post] no fórum do Lote do Azure para obter uma visão geral de métodos para preparar os nós para execução de tarefas.</span><span class="sxs-lookup"><span data-stu-id="e8d68-204">See [Installing applications and staging data on Batch compute nodes][forum_post] in the Azure Batch forum for an overview of methods for preparing your nodes to run tasks.</span></span> <span data-ttu-id="e8d68-205">Escrita por um dos membros da equipe do Lote do Azure, essa postagem é um bom guia sobre as diferentes maneiras de copiar aplicativos, dados de entrada de tarefa e outros arquivos nos nós de computação.</span><span class="sxs-lookup"><span data-stu-id="e8d68-205">Written by one of the Azure Batch team members, this post is a good primer on the different ways to copy applications, task input data, and other files to your compute nodes.</span></span>

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_taskdependencies]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_dependson]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.dependson.aspx
[net_exitcode]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.exitcode.aspx
[net_exitconditions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitconditions
[net_exitoptions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions
[net_dependencyaction]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions#Microsoft_Azure_Batch_ExitOptions_DependencyAction
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_onid]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onid.aspx
[net_onids]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onids.aspx
[net_onidrange]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onidrange.aspx
[net_taskexecutioninformation]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_usestaskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.usestaskdependencies.aspx
[net_taskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskdependencies.aspx

<span data-ttu-id="e8d68-206">[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagrama: dependência de um para um"</span><span class="sxs-lookup"><span data-stu-id="e8d68-206">[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagram: one-to-one dependency"</span></span>
<span data-ttu-id="e8d68-207">[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagrama: dependência de um para muitos"</span><span class="sxs-lookup"><span data-stu-id="e8d68-207">[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagram: one-to-many dependency"</span></span>
<span data-ttu-id="e8d68-208">[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagrama: dependência de intervalo de ids de tarefas"</span><span class="sxs-lookup"><span data-stu-id="e8d68-208">[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagram: task id range dependency"</span></span>
