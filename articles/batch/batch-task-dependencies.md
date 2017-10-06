---
title: "toorun aaaUse tarefas de dependências baseiam na conclusão de saudação de outras tarefas - lote do Azure | Microsoft Docs"
description: "Criar tarefas que dependem de conclusão de saudação de outras tarefas de processamento de estilo de MapReduce e grandes de dados semelhantes cargas de trabalho em lote do Azure."
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
ms.openlocfilehash: faf08ec38cb30b1f66acd51e256c31aea6215c62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-task-dependencies-toorun-tasks-that-depend-on-other-tasks"></a><span data-ttu-id="06fc3-103">Criar dependências toorun tarefas que dependem de outras tarefas</span><span class="sxs-lookup"><span data-stu-id="06fc3-103">Create task dependencies toorun tasks that depend on other tasks</span></span>

<span data-ttu-id="06fc3-104">Você pode definir tarefa dependências toorun uma tarefa ou um conjunto de tarefas somente depois que uma tarefa pai foi concluída.</span><span class="sxs-lookup"><span data-stu-id="06fc3-104">You can define task dependencies toorun a task or set of tasks only after a parent task has completed.</span></span> <span data-ttu-id="06fc3-105">Alguns cenários em que as dependências entre tarefas são úteis incluem:</span><span class="sxs-lookup"><span data-stu-id="06fc3-105">Some scenarios where task dependencies are useful include:</span></span>

* <span data-ttu-id="06fc3-106">Cargas de trabalho de estilo de MapReduce na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="06fc3-106">MapReduce-style workloads in hello cloud.</span></span>
* <span data-ttu-id="06fc3-107">Trabalhos cujas tarefas de processamento de dados podem ser expressas como um DAG (gráfico acíclico dirigido).</span><span class="sxs-lookup"><span data-stu-id="06fc3-107">Jobs whose data processing tasks can be expressed as a directed acyclic graph (DAG).</span></span>
* <span data-ttu-id="06fc3-108">Processos de renderização pré e pós-processamento, onde cada tarefa deve concluir antes de começar a próxima tarefa de saudação.</span><span class="sxs-lookup"><span data-stu-id="06fc3-108">Pre-rendering and post-rendering processes, where each task must complete before hello next task can begin.</span></span>
* <span data-ttu-id="06fc3-109">Qualquer outro trabalho que tarefas de downstream dependem saída Olá das tarefas de upstream.</span><span class="sxs-lookup"><span data-stu-id="06fc3-109">Any other job in which downstream tasks depend on hello output of upstream tasks.</span></span>

<span data-ttu-id="06fc3-110">Dependências de tarefa em lotes, você pode criar tarefas que estão agendadas para execução em nós de computação após a conclusão de saudação de uma ou mais tarefas de pai.</span><span class="sxs-lookup"><span data-stu-id="06fc3-110">With Batch task dependencies, you can create tasks that are scheduled for execution on compute nodes after hello completion of one or more parent tasks.</span></span> <span data-ttu-id="06fc3-111">Por exemplo, você pode criar um trabalho que processa cada quadro de um filme 3D com tarefas paralelas separadas.</span><span class="sxs-lookup"><span data-stu-id="06fc3-111">For example, you can create a job that renders each frame of a 3D movie with separate, parallel tasks.</span></span> <span data-ttu-id="06fc3-112">tarefa final do Hello – hello "tarefa de mesclagem –" hello renderizado quadros em filme completo Olá somente depois que todos os quadros de mesclagens tenham sido com êxito gerados.</span><span class="sxs-lookup"><span data-stu-id="06fc3-112">hello final task--hello "merge task"--merges hello rendered frames into hello complete movie only after all frames have been successfully rendered.</span></span>

<span data-ttu-id="06fc3-113">Por padrão, tarefas dependentes agendadas para execução após a tarefa pai de saudação foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="06fc3-113">By default, dependent tasks are scheduled for execution only after hello parent task has completed successfully.</span></span> <span data-ttu-id="06fc3-114">Você pode especificar um comportamento padrão da dependência ação toooverride hello e executar tarefas quando ocorre falha na tarefa pai de saudação.</span><span class="sxs-lookup"><span data-stu-id="06fc3-114">You can specify a dependency action toooverride hello default behavior and run tasks when hello parent task fails.</span></span> <span data-ttu-id="06fc3-115">Consulte Olá [ações de dependência](#dependency-actions) seção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="06fc3-115">See hello [Dependency actions](#dependency-actions) section for details.</span></span>  

<span data-ttu-id="06fc3-116">Você pode criar tarefas que dependem de outras tarefas em uma relação um para um ou um para muitos.</span><span class="sxs-lookup"><span data-stu-id="06fc3-116">You can create tasks that depend on other tasks in a one-to-one or one-to-many relationship.</span></span> <span data-ttu-id="06fc3-117">Você também pode criar uma dependência de intervalo em que uma tarefa depende de conclusão de saudação de um grupo de tarefas dentro de um intervalo especificado de IDs de tarefas.</span><span class="sxs-lookup"><span data-stu-id="06fc3-117">You can also create a range dependency where a task depends on hello completion of a group of tasks within a specified range of task IDs.</span></span> <span data-ttu-id="06fc3-118">Você pode combinar essas relações de muitos-para-muitos três cenários básicos toocreate.</span><span class="sxs-lookup"><span data-stu-id="06fc3-118">You can combine these three basic scenarios toocreate many-to-many relationships.</span></span>

## <a name="task-dependencies-with-batch-net"></a><span data-ttu-id="06fc3-119">Dependências de tarefas com o .NET do Lote</span><span class="sxs-lookup"><span data-stu-id="06fc3-119">Task dependencies with Batch .NET</span></span>
<span data-ttu-id="06fc3-120">Neste artigo, discutiremos como dependências tooconfigure usando Olá [Batch .NET] [ net_msdn] biblioteca.</span><span class="sxs-lookup"><span data-stu-id="06fc3-120">In this article, we discuss how tooconfigure task dependencies by using hello [Batch .NET][net_msdn] library.</span></span> <span data-ttu-id="06fc3-121">Primeiro mostraremos como muito[ativar a dependência de tarefa](#enable-task-dependencies) em seus trabalhos e, em seguida, demonstre como muito[configurar uma tarefa com dependências](#create-dependent-tasks).</span><span class="sxs-lookup"><span data-stu-id="06fc3-121">We first show you how too[enable task dependency](#enable-task-dependencies) on your jobs, and then demonstrate how too[configure a task with dependencies](#create-dependent-tasks).</span></span> <span data-ttu-id="06fc3-122">Podemos também descrevem como toospecify uma dependência ação toorun tarefas dependentes se pai Olá falhar.</span><span class="sxs-lookup"><span data-stu-id="06fc3-122">We also describe how toospecify a dependency action toorun dependent tasks if hello parent fails.</span></span> <span data-ttu-id="06fc3-123">Por fim, discutiremos Olá [situações de dependência](#dependency-scenarios) que dá suporte ao lote.</span><span class="sxs-lookup"><span data-stu-id="06fc3-123">Finally, we discuss hello [dependency scenarios](#dependency-scenarios) that Batch supports.</span></span>

## <a name="enable-task-dependencies"></a><span data-ttu-id="06fc3-124">Habilitar dependências de tarefas</span><span class="sxs-lookup"><span data-stu-id="06fc3-124">Enable task dependencies</span></span>
<span data-ttu-id="06fc3-125">dependências de tarefa toouse em seu aplicativo de lote, você deve primeiro configurar Olá trabalho toouse dependências.</span><span class="sxs-lookup"><span data-stu-id="06fc3-125">toouse task dependencies in your Batch application, you must first configure hello job toouse task dependencies.</span></span> <span data-ttu-id="06fc3-126">No .NET em lotes, habilitá-lo no seu [CloudJob] [ net_cloudjob] definindo seu [UsesTaskDependencies] [ net_usestaskdependencies] propriedade muito`true`:</span><span class="sxs-lookup"><span data-stu-id="06fc3-126">In Batch .NET, enable it on your [CloudJob][net_cloudjob] by setting its [UsesTaskDependencies][net_usestaskdependencies] property too`true`:</span></span>

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

<span data-ttu-id="06fc3-127">Olá precede o trecho de código, "batchClient" é uma instância de saudação [BatchClient] [ net_batchclient] classe.</span><span class="sxs-lookup"><span data-stu-id="06fc3-127">In hello preceding code snippet, "batchClient" is an instance of hello [BatchClient][net_batchclient] class.</span></span>

## <a name="create-dependent-tasks"></a><span data-ttu-id="06fc3-128">Criar tarefas dependentes</span><span class="sxs-lookup"><span data-stu-id="06fc3-128">Create dependent tasks</span></span>
<span data-ttu-id="06fc3-129">toocreate uma tarefa que depende de conclusão de saudação de uma ou mais tarefas de pai, você pode especificar que Olá tarefa "depende" Olá, outras tarefas.</span><span class="sxs-lookup"><span data-stu-id="06fc3-129">toocreate a task that depends on hello completion of one or more parent tasks, you can specify that hello task "depends on" hello other tasks.</span></span> <span data-ttu-id="06fc3-130">No .NET de lote configurar Olá [CloudTask][net_cloudtask].[ DependsOn] [ net_dependson] propriedade com uma instância do hello [TaskDependencies] [ net_taskdependencies] classe:</span><span class="sxs-lookup"><span data-stu-id="06fc3-130">In Batch .NET, configure hello [CloudTask][net_cloudtask].[DependsOn][net_dependson] property with an instance of hello [TaskDependencies][net_taskdependencies] class:</span></span>

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

<span data-ttu-id="06fc3-131">Este trecho de código cria uma tarefa dependente com a identificação da tarefa “Flowers”.</span><span class="sxs-lookup"><span data-stu-id="06fc3-131">This code snippet creates a dependent task with task ID "Flowers".</span></span> <span data-ttu-id="06fc3-132">Olá tarefa "Flores" depende das tarefas "Chuva" e "Sun".</span><span class="sxs-lookup"><span data-stu-id="06fc3-132">hello "Flowers" task depends on tasks "Rain" and "Sun".</span></span> <span data-ttu-id="06fc3-133">A tarefa "Flores" será toorun agendado em um nó de computação somente após tarefas "Chuva" e "Sun" foram concluídos com êxito.</span><span class="sxs-lookup"><span data-stu-id="06fc3-133">Task "Flowers" will be scheduled toorun on a compute node only after tasks "Rain" and "Sun" have completed successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="06fc3-134">Uma tarefa é considerada toobe foi concluída com êxito quando ele está em Olá **concluída** estado e seu **código de saída** é `0`.</span><span class="sxs-lookup"><span data-stu-id="06fc3-134">A task is considered toobe completed successfully when it is in hello **completed** state and its **exit code** is `0`.</span></span> <span data-ttu-id="06fc3-135">No .NET em lotes, isso significa um [CloudTask][net_cloudtask].[ Estado] [ net_taskstate] valor da propriedade `Completed` e Olá do CloudTask [TaskExecutionInformation][net_taskexecutioninformation].[ ExitCode] [ net_exitcode] é o valor da propriedade `0`.</span><span class="sxs-lookup"><span data-stu-id="06fc3-135">In Batch .NET, this means a [CloudTask][net_cloudtask].[State][net_taskstate] property value of `Completed` and hello CloudTask's [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] property value is `0`.</span></span>
> 
> 

## <a name="dependency-scenarios"></a><span data-ttu-id="06fc3-136">Cenários de dependência</span><span class="sxs-lookup"><span data-stu-id="06fc3-136">Dependency scenarios</span></span>
<span data-ttu-id="06fc3-137">Há três cenários de dependência de tarefas básicos que você pode usar no Lote do Azure: um-para-um, um-para-muitos e dependência de intervalo de IDs de tarefas.</span><span class="sxs-lookup"><span data-stu-id="06fc3-137">There are three basic task dependency scenarios that you can use in Azure Batch: one-to-one, one-to-many, and task ID range dependency.</span></span> <span data-ttu-id="06fc3-138">Eles podem ser combinados tooprovide um quarto cenário, muitos-para-muitos.</span><span class="sxs-lookup"><span data-stu-id="06fc3-138">These can be combined tooprovide a fourth scenario, many-to-many.</span></span>

| <span data-ttu-id="06fc3-139">Cenário&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="06fc3-139">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="06fc3-140">Exemplo</span><span class="sxs-lookup"><span data-stu-id="06fc3-140">Example</span></span> |  |
|:---:| --- | --- |
|  [<span data-ttu-id="06fc3-141">Um-para-um</span><span class="sxs-lookup"><span data-stu-id="06fc3-141">One-to-one</span></span>](#one-to-one) |<span data-ttu-id="06fc3-142">*tarefaB* depende de *tarefaA*</span><span class="sxs-lookup"><span data-stu-id="06fc3-142">*taskB* depends on *taskA*</span></span> <p/> <span data-ttu-id="06fc3-143">A *tarefaB* não será agendada para execução até que a *tarefaA* seja concluída com êxito</span><span class="sxs-lookup"><span data-stu-id="06fc3-143">*taskB* will not be scheduled for execution until *taskA* has completed successfully</span></span> |<span data-ttu-id="06fc3-144">![Diagrama: dependência de tarefa de um para um][1]</span><span class="sxs-lookup"><span data-stu-id="06fc3-144">![Diagram: one-to-one task dependency][1]</span></span> |
|  [<span data-ttu-id="06fc3-145">Um-para-muitos</span><span class="sxs-lookup"><span data-stu-id="06fc3-145">One-to-many</span></span>](#one-to-many) |<span data-ttu-id="06fc3-146">A *tarefaC* depende da *tarefaA* e da *tarefaB*</span><span class="sxs-lookup"><span data-stu-id="06fc3-146">*taskC* depends on both *taskA* and *taskB*</span></span> <p/> <span data-ttu-id="06fc3-147">A *tarefaC* não será agendada para execução até que a *tarefaA* e a *tarefaB* sejam concluídas com êxito</span><span class="sxs-lookup"><span data-stu-id="06fc3-147">*taskC* will not be scheduled for execution until both *taskA* and *taskB* have completed successfully</span></span> |<span data-ttu-id="06fc3-148">![Diagrama: dependência de tarefa de um para muitos][2]</span><span class="sxs-lookup"><span data-stu-id="06fc3-148">![Diagram: one-to-many task dependency][2]</span></span> |
|  [<span data-ttu-id="06fc3-149">Intervalo de IDs de tarefa</span><span class="sxs-lookup"><span data-stu-id="06fc3-149">Task ID range</span></span>](#task-id-range) |<span data-ttu-id="06fc3-150">A *taskD* depende de diversas tarefas</span><span class="sxs-lookup"><span data-stu-id="06fc3-150">*taskD* depends on a range of tasks</span></span> <p/> <span data-ttu-id="06fc3-151">*taskD* não será agendado para execução até que as tarefas de saudação com IDs *1* por meio de *10* foram concluídos com êxito</span><span class="sxs-lookup"><span data-stu-id="06fc3-151">*taskD* will not be scheduled for execution until hello tasks with IDs *1* through *10* have completed successfully</span></span> |<span data-ttu-id="06fc3-152">![Diagrama: dependência de intervalo de ids de tarefas][3]</span><span class="sxs-lookup"><span data-stu-id="06fc3-152">![Diagram: Task id range dependency][3]</span></span> |

> [!TIP]
> <span data-ttu-id="06fc3-153">Você pode criar **muitos-para-muitos** relações, como onde tarefas C, D, E e F cada dependem das tarefas A e B. Isso é útil, por exemplo, em cenários de pré-processamento em paralelo, em que as tarefas de downstream dependem de saída Olá de várias tarefas de upstream.</span><span class="sxs-lookup"><span data-stu-id="06fc3-153">You can create **many-to-many** relationships, such as where tasks C, D, E, and F each depend on tasks A and B. This is useful, for example, in parallelized preprocessing scenarios where your downstream tasks depend on hello output of multiple upstream tasks.</span></span>
> 
> <span data-ttu-id="06fc3-154">Olá exemplos nesta seção, uma tarefa dependente é executada somente depois que tarefas de pai Olá concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="06fc3-154">In hello examples in this section, a dependent task runs only after hello parent tasks complete successfully.</span></span> <span data-ttu-id="06fc3-155">Esse comportamento é o comportamento padrão de saudação para uma tarefa dependente.</span><span class="sxs-lookup"><span data-stu-id="06fc3-155">This behavior is hello default behavior for a dependent task.</span></span> <span data-ttu-id="06fc3-156">Depois que uma tarefa pai falha, especificando um comportamento padrão da dependência ação toooverride hello, você pode executar uma tarefa dependente.</span><span class="sxs-lookup"><span data-stu-id="06fc3-156">You can run a dependent task after a parent task fails by specifying a dependency action toooverride hello default behavior.</span></span> <span data-ttu-id="06fc3-157">Consulte Olá [ações de dependência](#dependency-actions) seção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="06fc3-157">See hello [Dependency actions](#dependency-actions) section for details.</span></span>

### <a name="one-to-one"></a><span data-ttu-id="06fc3-158">Um-para-um</span><span class="sxs-lookup"><span data-stu-id="06fc3-158">One-to-one</span></span>
<span data-ttu-id="06fc3-159">Em uma relação um para um, uma tarefa depende após a conclusão bem-sucedida da tarefa pai de uma saudação.</span><span class="sxs-lookup"><span data-stu-id="06fc3-159">In a one-to-one relationship, a task depends on hello successful completion of one parent task.</span></span> <span data-ttu-id="06fc3-160">toocreate Olá dependência, forneça um toohello de ID única tarefa [TaskDependencies][net_taskdependencies].[ OnId] [ net_onid] método estático ao preencher Olá [DependsOn] [ net_dependson] propriedade [CloudTask] [ net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="06fc3-160">toocreate hello dependency, provide a single task ID toohello [TaskDependencies][net_taskdependencies].[OnId][net_onid] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a><span data-ttu-id="06fc3-161">Um-para-muitos</span><span class="sxs-lookup"><span data-stu-id="06fc3-161">One-to-many</span></span>
<span data-ttu-id="06fc3-162">Em uma relação um-para-muitos, uma tarefa depende da conclusão de saudação de várias tarefas de pai.</span><span class="sxs-lookup"><span data-stu-id="06fc3-162">In a one-to-many relationship, a task depends on hello completion of multiple parent tasks.</span></span> <span data-ttu-id="06fc3-163">toocreate Olá dependência, fornecer um conjunto de tarefas IDs toohello [TaskDependencies][net_taskdependencies].[ OnIds] [ net_onids] método estático ao preencher Olá [DependsOn] [ net_dependson] propriedade [CloudTask] [ net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="06fc3-163">toocreate hello dependency, provide a collection of task IDs toohello [TaskDependencies][net_taskdependencies].[OnIds][net_onids] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

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

### <a name="task-id-range"></a><span data-ttu-id="06fc3-164">Intervalo de IDs de tarefa</span><span class="sxs-lookup"><span data-stu-id="06fc3-164">Task ID range</span></span>
<span data-ttu-id="06fc3-165">Em uma dependência em uma variedade de tarefas de pai, uma tarefa depende da conclusão de Olá Olá cujos IDs residem dentro de um intervalo de tarefas.</span><span class="sxs-lookup"><span data-stu-id="06fc3-165">In a dependency on a range of parent tasks, a task depends on hello hello completion of tasks whose IDs lie within a range.</span></span>
<span data-ttu-id="06fc3-166">dependência de saudação toocreate, forneça Olá primeiro e última tarefa IDs no hello intervalo toohello [TaskDependencies][net_taskdependencies].[ OnIdRange] [ net_onidrange] método estático ao preencher Olá [DependsOn] [ net_dependson] propriedade [CloudTask] [net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="06fc3-166">toocreate hello dependency, provide hello first and last task IDs in hello range toohello [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06fc3-167">Quando você usa os intervalos de ID de tarefa para as suas dependências, Olá IDs de tarefa no intervalo de saudação *deve* ser representações de cadeia de caracteres de valores inteiros.</span><span class="sxs-lookup"><span data-stu-id="06fc3-167">When you use task ID ranges for your dependencies, hello task IDs in hello range *must* be string representations of integer values.</span></span>
> 
> <span data-ttu-id="06fc3-168">Todas as tarefas no intervalo de saudação devem satisfazer a dependência hello, concluindo com êxito ou executando com uma falha de ação de dependência tooa mapeado definida muito**satisfação**.</span><span class="sxs-lookup"><span data-stu-id="06fc3-168">Every task in hello range must satisfy hello dependency, either by completing successfully or by completing with a failure that’s mapped tooa dependency action set too**Satisfy**.</span></span> <span data-ttu-id="06fc3-169">Consulte Olá [ações de dependência](#dependency-actions) seção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="06fc3-169">See hello [Dependency actions](#dependency-actions) section for details.</span></span>
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
    // toouse a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters tooTaskIdRange,
    // but their ids (above) are string representations of hello ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a><span data-ttu-id="06fc3-170">Ações de dependência</span><span class="sxs-lookup"><span data-stu-id="06fc3-170">Dependency actions</span></span>

<span data-ttu-id="06fc3-171">Por padrão, uma tarefa dependente ou um conjunto de tarefas é executado somente após a conclusão bem-sucedida de uma tarefa pai.</span><span class="sxs-lookup"><span data-stu-id="06fc3-171">By default, a dependent task or set of tasks runs only after a parent task has completed successfully.</span></span> <span data-ttu-id="06fc3-172">Em alguns cenários, convém tarefas dependentes toorun mesmo se a tarefa pai de saudação falha.</span><span class="sxs-lookup"><span data-stu-id="06fc3-172">In some scenarios, you may want toorun dependent tasks even if hello parent task fails.</span></span> <span data-ttu-id="06fc3-173">Você pode substituir o comportamento padrão de saudação especificando uma ação de dependência.</span><span class="sxs-lookup"><span data-stu-id="06fc3-173">You can override hello default behavior by specifying a dependency action.</span></span> <span data-ttu-id="06fc3-174">Uma ação de dependência Especifica se uma tarefa dependente toorun qualificado, com base no sucesso de saudação ou a falha da tarefa pai de saudação.</span><span class="sxs-lookup"><span data-stu-id="06fc3-174">A dependency action specifies whether a dependent task is eligible toorun, based on hello success or failure of hello parent task.</span></span> 

<span data-ttu-id="06fc3-175">Por exemplo, suponha que uma tarefa dependente está aguardando a data de conclusão de saudação da tarefa de upstream hello.</span><span class="sxs-lookup"><span data-stu-id="06fc3-175">For example, suppose that a dependent task is awaiting data from hello completion of hello upstream task.</span></span> <span data-ttu-id="06fc3-176">Se a tarefa de upstream Olá falhar, tarefa dependente Olá ainda pode ser capaz de toorun usando os dados mais antigos.</span><span class="sxs-lookup"><span data-stu-id="06fc3-176">If hello upstream task fails, hello dependent task may still be able toorun using older data.</span></span> <span data-ttu-id="06fc3-177">Nesse caso, uma ação de dependência pode especificar a que tarefa dependente Olá é elegível toorun apesar da falha de saudação da tarefa pai de saudação.</span><span class="sxs-lookup"><span data-stu-id="06fc3-177">In this case, a dependency action can specify that hello dependent task is eligible toorun despite hello failure of hello parent task.</span></span>

<span data-ttu-id="06fc3-178">Uma ação de dependência baseia-se em uma condição de saída para a tarefa pai de saudação.</span><span class="sxs-lookup"><span data-stu-id="06fc3-178">A dependency action is based on an exit condition for hello parent task.</span></span> <span data-ttu-id="06fc3-179">Você pode especificar uma ação de dependência para qualquer Olá seguintes condições de saída; para .NET, consulte Olá [ExitConditions] [ net_exitconditions] classe para obter detalhes:</span><span class="sxs-lookup"><span data-stu-id="06fc3-179">You can specify a dependency action for any of hello following exit conditions; for .NET, see hello [ExitConditions][net_exitconditions] class for details:</span></span>

- <span data-ttu-id="06fc3-180">Quando ocorre um erro de pré-processamento.</span><span class="sxs-lookup"><span data-stu-id="06fc3-180">When a pre-processing error occurs.</span></span>
- <span data-ttu-id="06fc3-181">Quando ocorre um erro de carregamento de arquivo.</span><span class="sxs-lookup"><span data-stu-id="06fc3-181">When a file upload error occurs.</span></span> <span data-ttu-id="06fc3-182">Se a tarefa de saudação for encerrada com um código de saída foi especificado por meio de **exitCodes** ou **exitCodeRanges**e, em seguida, encontra um erro de carregamento de arquivo, a ação de saudação especificado pelo Olá saída código terá precedência.</span><span class="sxs-lookup"><span data-stu-id="06fc3-182">If hello task exits with an exit code that was specified via **exitCodes** or **exitCodeRanges**, and then encounters a file upload error, hello action specified by hello exit code takes precedence.</span></span>
- <span data-ttu-id="06fc3-183">Quando a tarefa de saudação encerrada com um código de saída definido pelo Olá **ExitCodes** propriedade.</span><span class="sxs-lookup"><span data-stu-id="06fc3-183">When hello task exits with an exit code defined by hello **ExitCodes** property.</span></span>
- <span data-ttu-id="06fc3-184">Quando a tarefa de saudação encerrada com um código de saída que está em um intervalo especificado por Olá **ExitCodeRanges** propriedade.</span><span class="sxs-lookup"><span data-stu-id="06fc3-184">When hello task exits with an exit code that falls within a range specified by hello **ExitCodeRanges** property.</span></span>
- <span data-ttu-id="06fc3-185">Olá caso padrão, se Olá tarefa é encerrada com um código de saída não está definido por **ExitCodes** ou **ExitCodeRanges**, ou se Olá tarefa é encerrada com um erro de pré-processamento e Olá **PreProcessingError**  propriedade não está definida ou se hello falha de tarefa com um arquivo carregar erro e hello **FileUploadError** propriedade não está definida.</span><span class="sxs-lookup"><span data-stu-id="06fc3-185">hello default case, if hello task exits with an exit code not defined by **ExitCodes** or **ExitCodeRanges**, or if hello task exits with a pre-processing error and hello **PreProcessingError** property is not set, or if hello task fails with a file upload error and hello **FileUploadError** property is not set.</span></span> 

<span data-ttu-id="06fc3-186">toospecify uma ação de dependência no .NET, Olá conjunto [ExitOptions][net_exitoptions].[ DependencyAction] [ net_dependencyaction] propriedade para a condição de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="06fc3-186">toospecify a dependency action in .NET, set hello [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] property for hello exit condition.</span></span> <span data-ttu-id="06fc3-187">Olá **DependencyAction** propriedade tem um dos dois valores:</span><span class="sxs-lookup"><span data-stu-id="06fc3-187">hello **DependencyAction** property takes one of two values:</span></span>

- <span data-ttu-id="06fc3-188">Saudação de configuração **DependencyAction** propriedade muito**satisfação** indica que tarefas dependentes estão qualificado toorun se a tarefa pai de saudação for encerrada com um erro especificado.</span><span class="sxs-lookup"><span data-stu-id="06fc3-188">Setting hello **DependencyAction** property too**Satisfy** indicates that dependent tasks are eligible toorun if hello parent task exits with a specified error.</span></span>
- <span data-ttu-id="06fc3-189">Saudação de configuração **DependencyAction** propriedade muito**bloco** indica que as tarefas dependentes não são qualificado toorun.</span><span class="sxs-lookup"><span data-stu-id="06fc3-189">Setting hello **DependencyAction** property too**Block** indicates that dependent tasks are not eligible toorun.</span></span>

<span data-ttu-id="06fc3-190">Olá a configuração padrão para Olá **DependencyAction** é de propriedade **satisfação** para o código de saída 0, e **bloco** para todas as outras condições de saída.</span><span class="sxs-lookup"><span data-stu-id="06fc3-190">hello default setting for hello **DependencyAction** property is **Satisfy** for exit code 0, and **Block** for all other exit conditions.</span></span>

<span data-ttu-id="06fc3-191">trecho de código a seguir Hello define Olá **DependencyAction** propriedade para uma tarefa pai.</span><span class="sxs-lookup"><span data-stu-id="06fc3-191">hello following code snippet sets hello **DependencyAction** property for a parent task.</span></span> <span data-ttu-id="06fc3-192">Se tarefa pai de saudação for encerrada com um erro de pré-processamento, ou com Olá Olá dependentes a códigos de erro especificada, a tarefa é bloqueada.</span><span class="sxs-lookup"><span data-stu-id="06fc3-192">If hello parent task exits with a pre-processing error, or with hello specified error codes, hello dependent task is blocked.</span></span> <span data-ttu-id="06fc3-193">Se a tarefa pai de saudação for encerrada com qualquer outro erro diferente de zero, tarefa dependente Olá é toorun qualificado.</span><span class="sxs-lookup"><span data-stu-id="06fc3-193">If hello parent task exits with any other non-zero error, hello dependent task is eligible toorun.</span></span>

```csharp
// Task A is hello parent task.
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
        // If task A exits with hello specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible toorun 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible toorun depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a><span data-ttu-id="06fc3-194">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="06fc3-194">Code sample</span></span>
<span data-ttu-id="06fc3-195">Olá [TaskDependencies] [ github_taskdependencies] projeto de exemplo é uma saudação [exemplos de código do Azure Batch] [ github_samples] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="06fc3-195">hello [TaskDependencies][github_taskdependencies] sample project is one of hello [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="06fc3-196">Esta solução do Visual Studio demonstra:</span><span class="sxs-lookup"><span data-stu-id="06fc3-196">This Visual Studio solution demonstrates:</span></span>

- <span data-ttu-id="06fc3-197">Como tooenable dependência em um trabalho de tarefas</span><span class="sxs-lookup"><span data-stu-id="06fc3-197">How tooenable task dependency on a job</span></span>
- <span data-ttu-id="06fc3-198">Como toocreate tarefas que dependem de outras tarefas</span><span class="sxs-lookup"><span data-stu-id="06fc3-198">How toocreate tasks that depend on other tasks</span></span>
- <span data-ttu-id="06fc3-199">Como tooexecute as tarefas em um conjunto de nós de computação.</span><span class="sxs-lookup"><span data-stu-id="06fc3-199">How tooexecute those tasks on a pool of compute nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06fc3-200">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="06fc3-200">Next steps</span></span>
### <a name="application-deployment"></a><span data-ttu-id="06fc3-201">Implantação do aplicativo</span><span class="sxs-lookup"><span data-stu-id="06fc3-201">Application deployment</span></span>
<span data-ttu-id="06fc3-202">Olá [pacotes de aplicativos](batch-application-packages.md) recurso de lote fornece um modo fácil de implantar tooboth e versão aplicativos Olá as tarefas executadas em nós de computação.</span><span class="sxs-lookup"><span data-stu-id="06fc3-202">hello [application packages](batch-application-packages.md) feature of Batch provides an easy way tooboth deploy and version hello applications that your tasks execute on compute nodes.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="06fc3-203">Instalação de aplicativos e preparação de dados</span><span class="sxs-lookup"><span data-stu-id="06fc3-203">Installing applications and staging data</span></span>
<span data-ttu-id="06fc3-204">Consulte [nós de computação de instalação de aplicativos e dados em lotes de preparo] [ forum_post] no Fórum do lote do Azure Olá para uma visão geral dos métodos para preparar seus nós toorun tarefas.</span><span class="sxs-lookup"><span data-stu-id="06fc3-204">See [Installing applications and staging data on Batch compute nodes][forum_post] in hello Azure Batch forum for an overview of methods for preparing your nodes toorun tasks.</span></span> <span data-ttu-id="06fc3-205">Gravado por um dos membros da equipe do Azure Batch Olá, que esta postagem é um bom primer em aplicativos de toocopy de maneiras diferentes de hello, dados de entrada de tarefa e outros arquivos tooyour nós de computação.</span><span class="sxs-lookup"><span data-stu-id="06fc3-205">Written by one of hello Azure Batch team members, this post is a good primer on hello different ways toocopy applications, task input data, and other files tooyour compute nodes.</span></span>

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

[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagrama: dependência de um para um"
[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagrama: dependência de um para muitos"
[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagrama: dependência de intervalo de ids de tarefas"
