---
title: "Executar tarefas em paralelo para usar recursos de computação com eficiência - Lote do Azure | Microsoft Docs"
description: "Aumente a eficiência e reduza os custos usando menos nós de computação e executando tarefas simultâneas em cada nó em um pool do Lote do Azure"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 538a067c-1f6e-44eb-a92b-8d51c33d3e1a
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6903552d907a1ddb21d3b678e2d224b4b5e35b77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="run-tasks-concurrently-to-maximize-usage-of-batch-compute-nodes"></a><span data-ttu-id="c72dc-103">Execute tarefas simultaneamente para maximizar o uso dos nós de computação do Lote</span><span class="sxs-lookup"><span data-stu-id="c72dc-103">Run tasks concurrently to maximize usage of Batch compute nodes</span></span> 

<span data-ttu-id="c72dc-104">Executando simultaneamente mais de uma tarefa em cada nó de computação no pool de Lotes do Azure, você pode maximizar o uso dos recursos em um número menor de nós no pool.</span><span class="sxs-lookup"><span data-stu-id="c72dc-104">By running more than one task simultaneously on each compute node in your Azure Batch pool, you can maximize resource usage on a smaller number of nodes in the pool.</span></span> <span data-ttu-id="c72dc-105">Para algumas cargas de trabalho, isso pode resultar em tempos mais curtos de trabalho e reduzir os custos.</span><span class="sxs-lookup"><span data-stu-id="c72dc-105">For some workloads, this can result in shorter job times and lower cost.</span></span>

<span data-ttu-id="c72dc-106">Embora alguns cenários se beneficiem de dedicar todos os recursos de um nó para uma única tarefa, algumas situações se beneficiam de permitir que várias tarefas compartilhem esses recursos:</span><span class="sxs-lookup"><span data-stu-id="c72dc-106">While some scenarios benefit from dedicating all of a node's resources to a single task, several situations benefit from allowing multiple tasks to share those resources:</span></span>

* <span data-ttu-id="c72dc-107">**Minimização da transferência de dados** quando as tarefas puderem compartilhar dados.</span><span class="sxs-lookup"><span data-stu-id="c72dc-107">**Minimizing data transfer** when tasks are able to share data.</span></span> <span data-ttu-id="c72dc-108">Nesse cenário, é possível reduzir drasticamente os encargos de transferência de dados copiando dados compartilhados em uma quantidade menor de nós e executando tarefas em paralelo em cada nó.</span><span class="sxs-lookup"><span data-stu-id="c72dc-108">In this scenario, you can dramatically reduce data transfer charges by copying shared data to a smaller number of nodes and executing tasks in parallel on each node.</span></span> <span data-ttu-id="c72dc-109">Isso se aplicará especialmente se os dados que devem ser copiados em cada nó precisarem ser transferidos entre regiões geográficas.</span><span class="sxs-lookup"><span data-stu-id="c72dc-109">This especially applies if the data to be copied to each node must be transferred between geographic regions.</span></span>
* <span data-ttu-id="c72dc-110">**Maximização do uso de memória** quando as tarefas exigirem uma grande quantidade de memória, mas somente durante curtos períodos de tempo, e em momentos variáveis durante a execução.</span><span class="sxs-lookup"><span data-stu-id="c72dc-110">**Maximizing memory usage** when tasks require a large amount of memory, but only during short periods of time, and at variable times during execution.</span></span> <span data-ttu-id="c72dc-111">Você pode empregar menos nós de computação, porém maiores, com mais memória para lidar de forma eficiente com esses picos.</span><span class="sxs-lookup"><span data-stu-id="c72dc-111">You can employ fewer, but larger, compute nodes with more memory to efficiently handle such spikes.</span></span> <span data-ttu-id="c72dc-112">Esses nós teriam várias tarefas executadas em paralelo em cada nó, mas cada tarefa aproveitaria a grande quantidade de memória dos nós em momentos diferentes.</span><span class="sxs-lookup"><span data-stu-id="c72dc-112">These nodes would have multiple tasks running in parallel on each node, but each task would take advantage of the nodes' plentiful memory at different times.</span></span>
* <span data-ttu-id="c72dc-113">**Redução dos limites do número de nós** quando a comunicação entre nós for necessária em um pool.</span><span class="sxs-lookup"><span data-stu-id="c72dc-113">**Mitigating node number limits** when inter-node communication is required within a pool.</span></span> <span data-ttu-id="c72dc-114">Atualmente, os pools configurados para comunicação entre nós estão limitados a 50 nós de computação.</span><span class="sxs-lookup"><span data-stu-id="c72dc-114">Currently, pools configured for inter-node communication are limited to 50 compute nodes.</span></span> <span data-ttu-id="c72dc-115">Se cada nó desse pool for capaz de executar tarefas em paralelo, será possível executar um número maior de tarefas em paralelo.</span><span class="sxs-lookup"><span data-stu-id="c72dc-115">If each node in such a pool is able to execute tasks in parallel, a greater number of tasks can be executed simultaneously.</span></span>
* <span data-ttu-id="c72dc-116">**Replicação de um cluster de computação local**, como na primeira movimentação de um ambiente de computação para o Azure.</span><span class="sxs-lookup"><span data-stu-id="c72dc-116">**Replicating an on-premises compute cluster**, such as when you first move a compute environment to Azure.</span></span> <span data-ttu-id="c72dc-117">Se sua solução local atual executar várias tarefas por nó de computação, você poderá aumentar o número máximo de tarefas de nó para espelhar mais de perto a configuração.</span><span class="sxs-lookup"><span data-stu-id="c72dc-117">If your current on-premises solution executes multiple tasks per compute node, you can increase the maximum number of node tasks to more closely mirror that configuration.</span></span>

## <a name="example-scenario"></a><span data-ttu-id="c72dc-118">Cenário de exemplo</span><span class="sxs-lookup"><span data-stu-id="c72dc-118">Example scenario</span></span>
<span data-ttu-id="c72dc-119">Para ilustrar os benefícios de execução das tarefas paralelas, digamos que seu aplicativo de tarefa tenha requisitos de CPU e memória de forma que os nós [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) sejam suficientes.</span><span class="sxs-lookup"><span data-stu-id="c72dc-119">As an example to illustrate the benefits of parallel task execution, let's say that your task application has CPU and memory requirements such that [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nodes are sufficient.</span></span> <span data-ttu-id="c72dc-120">Mas, para concluir o trabalho no tempo necessário, 1.000 nós são necessários.</span><span class="sxs-lookup"><span data-stu-id="c72dc-120">But, in order to finish the job in the required time, 1,000 of these nodes are needed.</span></span>

<span data-ttu-id="c72dc-121">Em vez de usar os nós Standard\_D1, que têm um núcleo de CPU, você poderia utilizar os nós [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) com 16 núcleos cada e permitir a execução de tarefas paralelas.</span><span class="sxs-lookup"><span data-stu-id="c72dc-121">Instead of using Standard\_D1 nodes that have 1 CPU core, you could use [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes that have 16 cores each, and enable parallel task execution.</span></span> <span data-ttu-id="c72dc-122">Portanto, *16 vezes menos nós* poderiam ser usados; em vez de 1.000 nós, somente 63 seriam necessários.</span><span class="sxs-lookup"><span data-stu-id="c72dc-122">Therefore, *16 times fewer nodes* could be used--instead of 1,000 nodes, only 63 would be required.</span></span> <span data-ttu-id="c72dc-123">Além disso, se arquivos do aplicativo grandes ou dados de referência forem necessários para cada nó, eficiência e a duração do trabalho serão novamente aperfeiçoadas, uma vez que os dados são copiados para apenas 16 nós.</span><span class="sxs-lookup"><span data-stu-id="c72dc-123">Additionally, if large application files or reference data are required for each node, job duration and efficiency are again improved since the data is copied to only 16 nodes.</span></span>

## <a name="enable-parallel-task-execution"></a><span data-ttu-id="c72dc-124">Habilitar a execução de tarefas paralelas</span><span class="sxs-lookup"><span data-stu-id="c72dc-124">Enable parallel task execution</span></span>
<span data-ttu-id="c72dc-125">Você configura os nós de computação para a execução paralela das tarefas no nível do pool.</span><span class="sxs-lookup"><span data-stu-id="c72dc-125">You configure compute nodes for parallel task execution at the pool level.</span></span> <span data-ttu-id="c72dc-126">Com a biblioteca .NET do Lote, defina a propriedade [CloudPool.MaxTasksPerComputeNode][maxtasks_net] quando criar um pool.</span><span class="sxs-lookup"><span data-stu-id="c72dc-126">With the Batch .NET library, set the [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property when you create a pool.</span></span> <span data-ttu-id="c72dc-127">Se você estiver usando a API REST do Lote, defina o elemento [maxTasksPerNode][rest_addpool] no corpo da solicitação durante a criação do pool.</span><span class="sxs-lookup"><span data-stu-id="c72dc-127">If you are using the Batch REST API, set the [maxTasksPerNode][rest_addpool] element in the request body during pool creation.</span></span>

<span data-ttu-id="c72dc-128">O Lote do Azure permite que você configure o número máximo de tarefas por nó até quatro vezes (4x) o número de núcleos de nó.</span><span class="sxs-lookup"><span data-stu-id="c72dc-128">Azure Batch allows you to set maximum tasks per node up to four times (4x) the number of node cores.</span></span> <span data-ttu-id="c72dc-129">Por exemplo, se o pool estiver configurado com nós de tamanho "Grande" (quatro núcleos), será possível definir `maxTasksPerNode` como 16.</span><span class="sxs-lookup"><span data-stu-id="c72dc-129">For example, if the pool is configured with nodes of size "Large" (four cores), then `maxTasksPerNode` may be set to 16.</span></span> <span data-ttu-id="c72dc-130">Para obter detalhes sobre o número de núcleos para cada um dos tamanhos de nó, confira [Tamanhos para Serviços de Nuvem](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="c72dc-130">For details on the number of cores for each of the node sizes, see [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span> <span data-ttu-id="c72dc-131">Para saber mais sobre limites de serviço, confira [Cotas e limites para o serviço de Lote do Azure](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="c72dc-131">For more information on service limits, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span>

> [!TIP]
> <span data-ttu-id="c72dc-132">Leve em consideração o valor de `maxTasksPerNode` ao criar uma [fórmula de dimensionamento automático][enable_autoscaling] para o seu pool.</span><span class="sxs-lookup"><span data-stu-id="c72dc-132">Be sure to take into account the `maxTasksPerNode` value when you construct an [autoscale formula][enable_autoscaling] for your pool.</span></span> <span data-ttu-id="c72dc-133">Por exemplo, uma fórmula que avalia `$RunningTasks` poderia ser drasticamente afetada por um aumento nas tarefas por nó.</span><span class="sxs-lookup"><span data-stu-id="c72dc-133">For example, a formula that evaluates `$RunningTasks` could be dramatically affected by an increase in tasks per node.</span></span> <span data-ttu-id="c72dc-134">Consulte [Dimensionar automaticamente nós de computação em um pool do Lote do Azure](batch-automatic-scaling.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="c72dc-134">See [Automatically scale compute nodes in an Azure Batch pool](batch-automatic-scaling.md) for more information.</span></span>
>
>

## <a name="distribution-of-tasks"></a><span data-ttu-id="c72dc-135">Distribuição de tarefas</span><span class="sxs-lookup"><span data-stu-id="c72dc-135">Distribution of tasks</span></span>
<span data-ttu-id="c72dc-136">Quando os nós de computação em um pool puderem executar as tarefas simultaneamente, será importante especificar como você deseja distribuir suas tarefas nos nós no pool.</span><span class="sxs-lookup"><span data-stu-id="c72dc-136">When the compute nodes in a pool can execute tasks concurrently, it's important to specify how you want the tasks to be distributed across the nodes in the pool.</span></span>

<span data-ttu-id="c72dc-137">Ao usar a propriedade [CloudPool.TaskSchedulingPolicy][task_schedule], você pode especificar que as tarefas devam ser atribuídas uniformemente em todos os nós no pool ("difusão").</span><span class="sxs-lookup"><span data-stu-id="c72dc-137">By using the [CloudPool.TaskSchedulingPolicy][task_schedule] property, you can specify that tasks should be assigned evenly across all nodes in the pool ("spreading").</span></span> <span data-ttu-id="c72dc-138">Ou você pode especificar que o máximo possível de tarefas deve ser atribuído a cada nó antes de as tarefas serem atribuídas a outro nó no pool ("remessa").</span><span class="sxs-lookup"><span data-stu-id="c72dc-138">Or you can specify that as many tasks as possible should be assigned to each node before tasks are assigned to another node in the pool ("packing").</span></span>

<span data-ttu-id="c72dc-139">Como um exemplo de como esse recurso é útil, considere o pool de nós [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) (no exemplo acima) configurado com um valor de 16 para [CloudPool.MaxTasksPerComputeNode][maxtasks_net].</span><span class="sxs-lookup"><span data-stu-id="c72dc-139">As an example of how this feature is valuable, consider the pool of [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes (in the example above) that is configured with a [CloudPool.MaxTasksPerComputeNode][maxtasks_net] value of 16.</span></span> <span data-ttu-id="c72dc-140">Se [CloudPool.TaskSchedulingPolicy][task_schedule] for configurada com um [ComputeNodeFillType][fill_type] igual a *Pack*, ela maximizaria o uso de todos os 16 núcleos de cada nó e permitiria que um [pool de dimensionamento automático](batch-automatic-scaling.md) removesse os nós não utilizados do pool (nós sem nenhuma tarefa atribuída).</span><span class="sxs-lookup"><span data-stu-id="c72dc-140">If the [CloudPool.TaskSchedulingPolicy][task_schedule] is configured with a [ComputeNodeFillType][fill_type] of *Pack*, it would maximize usage of all 16 cores of each node and allow an [autoscaling pool](batch-automatic-scaling.md) to prune unused nodes from the pool (nodes without any tasks assigned).</span></span> <span data-ttu-id="c72dc-141">Isso minimiza o uso de recursos e economizando dinheiro.</span><span class="sxs-lookup"><span data-stu-id="c72dc-141">This minimizes resource usage and saves money.</span></span>

## <a name="batch-net-example"></a><span data-ttu-id="c72dc-142">Exemplo de .NET do Lote</span><span class="sxs-lookup"><span data-stu-id="c72dc-142">Batch .NET example</span></span>
<span data-ttu-id="c72dc-143">Esse trecho de código da API [.NET do Lote][api_net] mostra uma solicitação para criar um pool com quatro nós grandes, com um máximo de quatro tarefas por nó.</span><span class="sxs-lookup"><span data-stu-id="c72dc-143">This [Batch .NET][api_net] API code snippet shows a request to create a pool that contains four large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="c72dc-144">Isso especifica uma política de agendamento de tarefas que preencherá cada nó com tarefas antes de atribuir tarefas a outro nó no pool.</span><span class="sxs-lookup"><span data-stu-id="c72dc-144">It specifies a task scheduling policy that will fill each node with tasks prior to assigning tasks to another node in the pool.</span></span> <span data-ttu-id="c72dc-145">Para saber mais sobre como adicionar pools usando a API .NET do Lote, confira [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span><span class="sxs-lookup"><span data-stu-id="c72dc-145">For more information on adding pools by using the Batch .NET API, see [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span></span>

```csharp
CloudPool pool =
    batchClient.PoolOperations.CreatePool(
        poolId: "mypool",
        targetDedicatedComputeNodes: 4
        virtualMachineSize: "large",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

pool.MaxTasksPerComputeNode = 4;
pool.TaskSchedulingPolicy = new TaskSchedulingPolicy(ComputeNodeFillType.Pack);
pool.Commit();
```

## <a name="batch-rest-example"></a><span data-ttu-id="c72dc-146">Exemplo REST do Lote</span><span class="sxs-lookup"><span data-stu-id="c72dc-146">Batch REST example</span></span>
<span data-ttu-id="c72dc-147">Esse trecho da API [REST do Lote][api_rest] mostra uma solicitação para criar um pool com dois nós grandes, com um máximo de quatro tarefas por nó.</span><span class="sxs-lookup"><span data-stu-id="c72dc-147">This [Batch REST][api_rest] API snippet shows a request to create a pool that contains two large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="c72dc-148">Para obter mais informações sobre como adicionar pools usando a API REST, consulte [Adicionar um pool a uma conta][rest_addpool].</span><span class="sxs-lookup"><span data-stu-id="c72dc-148">For more information on adding pools by using the REST API, see [Add a pool to an account][rest_addpool].</span></span>

```json
{
  "odata.metadata":"https://myaccount.myregion.batch.azure.com/$metadata#pools/@Element",
  "id":"mypool",
  "vmSize":"large",
  "cloudServiceConfiguration": {
    "osFamily":"4",
    "targetOSVersion":"*",
  }
  "targetDedicatedComputeNodes":2,
  "maxTasksPerNode":4,
  "enableInterNodeCommunication":true,
}
```

> [!NOTE]
> <span data-ttu-id="c72dc-149">Você pode definir o elemento `maxTasksPerNode` e a propriedade [MaxTasksPerComputeNode][maxtasks_net] apenas no momento da criação do pool.</span><span class="sxs-lookup"><span data-stu-id="c72dc-149">You can set the `maxTasksPerNode` element and [MaxTasksPerComputeNode][maxtasks_net] property only at pool creation time.</span></span> <span data-ttu-id="c72dc-150">Eles não poderão ser modificados após a criação do pool.</span><span class="sxs-lookup"><span data-stu-id="c72dc-150">They cannot be modified after a pool has already been created.</span></span>
>
>

## <a name="code-sample"></a><span data-ttu-id="c72dc-151">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="c72dc-151">Code sample</span></span>
<span data-ttu-id="c72dc-152">O projeto [ParallelNodeTasks][parallel_tasks_sample] no GitHub ilustra o uso da propriedade [CloudPool.MaxTasksPerComputeNode][maxtasks_net].</span><span class="sxs-lookup"><span data-stu-id="c72dc-152">The [ParallelNodeTasks][parallel_tasks_sample] project on GitHub illustrates the use of the [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property.</span></span>

<span data-ttu-id="c72dc-153">Este aplicativo de console C# usa a biblioteca [.NET do Lote][api_net] para criar um pool com um ou mais nós de computação.</span><span class="sxs-lookup"><span data-stu-id="c72dc-153">This C# console application uses the [Batch .NET][api_net] library to create a pool with one or more compute nodes.</span></span> <span data-ttu-id="c72dc-154">Ele executa um número configurável de tarefas nesses nós para simular uma carga variável.</span><span class="sxs-lookup"><span data-stu-id="c72dc-154">It executes a configurable number of tasks on those nodes to simulate variable load.</span></span> <span data-ttu-id="c72dc-155">A saída do aplicativo especifica os nós executados em cada tarefa.</span><span class="sxs-lookup"><span data-stu-id="c72dc-155">Output from the application specifies which nodes executed each task.</span></span> <span data-ttu-id="c72dc-156">O aplicativo também fornece um resumo dos parâmetros do trabalho e a duração.</span><span class="sxs-lookup"><span data-stu-id="c72dc-156">The application also provides a summary of the job parameters and duration.</span></span> <span data-ttu-id="c72dc-157">A parte de resumo da saída de duas execuções diferentes do aplicativo de exemplo é exibida abaixo.</span><span class="sxs-lookup"><span data-stu-id="c72dc-157">The summary portion of the output from two different runs of the sample application appears below.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

<span data-ttu-id="c72dc-158">A primeira execução do aplicativo de exemplo mostra que com um único nó no pool, e a configuração padrão de uma tarefa por nó, a duração do trabalho será superior a 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="c72dc-158">The first execution of the sample application shows that with a single node in the pool and the default setting of one task per node, the job duration is over 30 minutes.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

<span data-ttu-id="c72dc-159">A segunda execução do exemplo mostra uma redução significativa na duração do trabalho.</span><span class="sxs-lookup"><span data-stu-id="c72dc-159">The second run of the sample shows a significant decrease in job duration.</span></span> <span data-ttu-id="c72dc-160">Isso ocorre porque o pool foi configurado com quatro tarefas por nó, o que permite que a execução paralela de tarefas conclua o trabalho em aproximadamente um quarto do tempo.</span><span class="sxs-lookup"><span data-stu-id="c72dc-160">This is because the pool was configured with four tasks per node, which allows for parallel task execution to complete the job in nearly a quarter of the time.</span></span>

> [!NOTE]
> <span data-ttu-id="c72dc-161">As durações de trabalho nos resumos acima não incluem o tempo de criação do pool.</span><span class="sxs-lookup"><span data-stu-id="c72dc-161">The job durations in the summaries above do not include pool creation time.</span></span> <span data-ttu-id="c72dc-162">Cada um dos trabalhos acima foi enviado para pools criados anteriormente e cujos nós de computação estavam no estado *Ocioso* na hora do envio.</span><span class="sxs-lookup"><span data-stu-id="c72dc-162">Each of the jobs above was submitted to previously created pools whose compute nodes were in the *Idle* state at submission time.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="c72dc-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c72dc-163">Next steps</span></span>
### <a name="batch-explorer-heat-map"></a><span data-ttu-id="c72dc-164">Mapa de Calor do Explorador do Lote</span><span class="sxs-lookup"><span data-stu-id="c72dc-164">Batch Explorer Heat Map</span></span>
<span data-ttu-id="c72dc-165">O [Gerenciador de Lotes do Azure][batch_explorer], um dos [aplicativos de exemplo][github_samples] do Lote do Azure, contém um recurso *Mapa de Calor*, que fornece a visualização da execução da tarefa.</span><span class="sxs-lookup"><span data-stu-id="c72dc-165">The [Azure Batch Explorer][batch_explorer], one of the Azure Batch [sample applications][github_samples], contains a *Heat Map* feature that provides visualization of task execution.</span></span> <span data-ttu-id="c72dc-166">Ao executar o aplicativo de exemplo [ParallelTasks][parallel_tasks_sample], você pode usar o recurso Mapa de Calor para visualizar facilmente a execução das tarefas paralelas em cada nó.</span><span class="sxs-lookup"><span data-stu-id="c72dc-166">When you're executing the [ParallelTasks][parallel_tasks_sample] sample application, you can use the Heat Map feature to easily visualize the execution of parallel tasks on each node.</span></span>

![Mapa de Calor do Explorador do Lote][1]

<span data-ttu-id="c72dc-168">*Mapa de Calor do Gerenciador de Lotes que mostra um pool de quatro nós, com cada nó atualmente executando quatro tarefas*</span><span class="sxs-lookup"><span data-stu-id="c72dc-168">*Batch Explorer Heat Map showing a pool of four nodes, with each node currently executing four tasks*</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[enable_autoscaling]: https://msdn.microsoft.com/library/azure/dn820173.aspx
[fill_type]: https://msdn.microsoft.com/library/microsoft.azure.batch.common.computenodefilltype.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[maxtasks_net]: http://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.maxtaskspercomputenode.aspx
[rest_addpool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[parallel_tasks_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/ParallelTasks
[poolcreate_net]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[task_schedule]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudpool.taskschedulingpolicy.aspx

[1]: ./media/batch-parallel-node-tasks\heat_map.png
