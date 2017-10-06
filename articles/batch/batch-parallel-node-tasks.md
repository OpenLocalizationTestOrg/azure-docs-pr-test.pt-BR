---
title: "aaaRun tarefas em paralelo toouse recursos de computação com eficiência - lote do Azure | Microsoft Docs"
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
ms.openlocfilehash: 05df4b7d8e0bc595168a97faa231b7c90fe81980
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-concurrently-toomaximize-usage-of-batch-compute-nodes"></a><span data-ttu-id="5a52f-103">Executar tarefas simultaneamente toomaximize uso de nós de computação do lote</span><span class="sxs-lookup"><span data-stu-id="5a52f-103">Run tasks concurrently toomaximize usage of Batch compute nodes</span></span> 

<span data-ttu-id="5a52f-104">Ao executar mais de uma tarefa simultaneamente em cada nó de computação no pool de lote do Azure, você pode maximizar o uso de recursos em um número menor de nós no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a52f-104">By running more than one task simultaneously on each compute node in your Azure Batch pool, you can maximize resource usage on a smaller number of nodes in hello pool.</span></span> <span data-ttu-id="5a52f-105">Para algumas cargas de trabalho, isso pode resultar em tempos mais curtos de trabalho e reduzir os custos.</span><span class="sxs-lookup"><span data-stu-id="5a52f-105">For some workloads, this can result in shorter job times and lower cost.</span></span>

<span data-ttu-id="5a52f-106">Enquanto alguns cenários beneficiam dedicar todos tarefa única de tooa de recursos de um nó, várias situações beneficiam permitindo tooshare de várias tarefas esses recursos:</span><span class="sxs-lookup"><span data-stu-id="5a52f-106">While some scenarios benefit from dedicating all of a node's resources tooa single task, several situations benefit from allowing multiple tasks tooshare those resources:</span></span>

* <span data-ttu-id="5a52f-107">**Minimizar a transferência de dados** quando as tarefas estão tooshare capaz de dados.</span><span class="sxs-lookup"><span data-stu-id="5a52f-107">**Minimizing data transfer** when tasks are able tooshare data.</span></span> <span data-ttu-id="5a52f-108">Nesse cenário, você pode reduzir consideravelmente os encargos de transferência de dados por meio de cópia de dados compartilhados tooa menor número de nós e executar tarefas em paralelo em cada nó.</span><span class="sxs-lookup"><span data-stu-id="5a52f-108">In this scenario, you can dramatically reduce data transfer charges by copying shared data tooa smaller number of nodes and executing tasks in parallel on each node.</span></span> <span data-ttu-id="5a52f-109">Isso se aplica especialmente se o nó de tooeach copiado Olá dados toobe deve ser transferido entre regiões geográficas.</span><span class="sxs-lookup"><span data-stu-id="5a52f-109">This especially applies if hello data toobe copied tooeach node must be transferred between geographic regions.</span></span>
* <span data-ttu-id="5a52f-110">**Maximização do uso de memória** quando as tarefas exigirem uma grande quantidade de memória, mas somente durante curtos períodos de tempo, e em momentos variáveis durante a execução.</span><span class="sxs-lookup"><span data-stu-id="5a52f-110">**Maximizing memory usage** when tasks require a large amount of memory, but only during short periods of time, and at variable times during execution.</span></span> <span data-ttu-id="5a52f-111">Você pode empregar menos, mas maiores, nós com tooefficiently de memória mais tratar esses picos de computação.</span><span class="sxs-lookup"><span data-stu-id="5a52f-111">You can employ fewer, but larger, compute nodes with more memory tooefficiently handle such spikes.</span></span> <span data-ttu-id="5a52f-112">Esses nós teria várias tarefas em execução em paralelo em cada nó, mas cada tarefa seria tirar proveito de memória bastante de nós de saudação em momentos diferentes.</span><span class="sxs-lookup"><span data-stu-id="5a52f-112">These nodes would have multiple tasks running in parallel on each node, but each task would take advantage of hello nodes' plentiful memory at different times.</span></span>
* <span data-ttu-id="5a52f-113">**Redução dos limites do número de nós** quando a comunicação entre nós for necessária em um pool.</span><span class="sxs-lookup"><span data-stu-id="5a52f-113">**Mitigating node number limits** when inter-node communication is required within a pool.</span></span> <span data-ttu-id="5a52f-114">Atualmente, pools configurados para comunicação entre nós são nós de computação too50 limitado.</span><span class="sxs-lookup"><span data-stu-id="5a52f-114">Currently, pools configured for inter-node communication are limited too50 compute nodes.</span></span> <span data-ttu-id="5a52f-115">Se cada nó em um pool tal tooexecute capaz de tarefas em paralelo, um número maior de tarefas pode ser executado simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="5a52f-115">If each node in such a pool is able tooexecute tasks in parallel, a greater number of tasks can be executed simultaneously.</span></span>
* <span data-ttu-id="5a52f-116">**Replicação de um cluster de computação local**, por exemplo, quando você move um tooAzure do ambiente de computação primeiro.</span><span class="sxs-lookup"><span data-stu-id="5a52f-116">**Replicating an on-premises compute cluster**, such as when you first move a compute environment tooAzure.</span></span> <span data-ttu-id="5a52f-117">Se sua solução no local atual executa várias tarefas por nó de computação, você pode aumentar o número máximo de saudação de tarefas de nó toomore refletem com maior exatidão essa configuração.</span><span class="sxs-lookup"><span data-stu-id="5a52f-117">If your current on-premises solution executes multiple tasks per compute node, you can increase hello maximum number of node tasks toomore closely mirror that configuration.</span></span>

## <a name="example-scenario"></a><span data-ttu-id="5a52f-118">Cenário de exemplo</span><span class="sxs-lookup"><span data-stu-id="5a52f-118">Example scenario</span></span>
<span data-ttu-id="5a52f-119">Como um exemplo tooillustrate Olá benefícios da execução de tarefas paralelas, digamos que seu aplicativo de tarefa tem requisitos de CPU e memória, de modo que [padrão\_D1](../cloud-services/cloud-services-sizes-specs.md) nós são suficientes.</span><span class="sxs-lookup"><span data-stu-id="5a52f-119">As an example tooillustrate hello benefits of parallel task execution, let's say that your task application has CPU and memory requirements such that [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nodes are sufficient.</span></span> <span data-ttu-id="5a52f-120">Mas, em ordem toofinish Olá trabalho em tempo de saudação necessário 1.000 de nós são necessários.</span><span class="sxs-lookup"><span data-stu-id="5a52f-120">But, in order toofinish hello job in hello required time, 1,000 of these nodes are needed.</span></span>

<span data-ttu-id="5a52f-121">Em vez de usar os nós Standard\_D1, que têm um núcleo de CPU, você poderia utilizar os nós [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) com 16 núcleos cada e permitir a execução de tarefas paralelas.</span><span class="sxs-lookup"><span data-stu-id="5a52f-121">Instead of using Standard\_D1 nodes that have 1 CPU core, you could use [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes that have 16 cores each, and enable parallel task execution.</span></span> <span data-ttu-id="5a52f-122">Portanto, *16 vezes menos nós* poderiam ser usados; em vez de 1.000 nós, somente 63 seriam necessários.</span><span class="sxs-lookup"><span data-stu-id="5a52f-122">Therefore, *16 times fewer nodes* could be used--instead of 1,000 nodes, only 63 would be required.</span></span> <span data-ttu-id="5a52f-123">Além disso, se os arquivos de aplicativo grande ou dados de referência são necessários para cada nó, eficiência e a duração do trabalho são novamente aprimorados como dados de saudação são copiado tooonly 16 nós.</span><span class="sxs-lookup"><span data-stu-id="5a52f-123">Additionally, if large application files or reference data are required for each node, job duration and efficiency are again improved since hello data is copied tooonly 16 nodes.</span></span>

## <a name="enable-parallel-task-execution"></a><span data-ttu-id="5a52f-124">Habilitar a execução de tarefas paralelas</span><span class="sxs-lookup"><span data-stu-id="5a52f-124">Enable parallel task execution</span></span>
<span data-ttu-id="5a52f-125">Você pode configurar nós de computação para execução de tarefas paralelas no nível do pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a52f-125">You configure compute nodes for parallel task execution at hello pool level.</span></span> <span data-ttu-id="5a52f-126">A biblioteca do .NET em lotes hello, definir Olá [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] propriedade quando você cria um pool.</span><span class="sxs-lookup"><span data-stu-id="5a52f-126">With hello Batch .NET library, set hello [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property when you create a pool.</span></span> <span data-ttu-id="5a52f-127">Se você estiver usando Olá API REST do lote, defina Olá [maxTasksPerNode] [ rest_addpool] elemento no corpo da solicitação Olá durante a criação do pool.</span><span class="sxs-lookup"><span data-stu-id="5a52f-127">If you are using hello Batch REST API, set hello [maxTasksPerNode][rest_addpool] element in hello request body during pool creation.</span></span>

<span data-ttu-id="5a52f-128">Lote do Azure permite que você tooset máximo de tarefas por nó toofour vezes (4 x) Olá número de núcleos de nó.</span><span class="sxs-lookup"><span data-stu-id="5a52f-128">Azure Batch allows you tooset maximum tasks per node up toofour times (4x) hello number of node cores.</span></span> <span data-ttu-id="5a52f-129">Por exemplo, se hello pool está configurado conosco de tamanho "Grande" (quatro núcleos), em seguida, `maxTasksPerNode` too16 pode ser definido.</span><span class="sxs-lookup"><span data-stu-id="5a52f-129">For example, if hello pool is configured with nodes of size "Large" (four cores), then `maxTasksPerNode` may be set too16.</span></span> <span data-ttu-id="5a52f-130">Para obter detalhes sobre o número de saudação de cores para cada um dos tamanhos de nó Olá, consulte [tamanhos para serviços de nuvem](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="5a52f-130">For details on hello number of cores for each of hello node sizes, see [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span> <span data-ttu-id="5a52f-131">Para obter mais informações sobre limites de serviço, consulte [cotas e limites de saudação do serviço Azure Batch](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="5a52f-131">For more information on service limits, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span>

> [!TIP]
> <span data-ttu-id="5a52f-132">Ser tootake-se em Olá conta `maxTasksPerNode` valor quando você construir um [fórmula de dimensionamento automático] [ enable_autoscaling] para o pool.</span><span class="sxs-lookup"><span data-stu-id="5a52f-132">Be sure tootake into account hello `maxTasksPerNode` value when you construct an [autoscale formula][enable_autoscaling] for your pool.</span></span> <span data-ttu-id="5a52f-133">Por exemplo, uma fórmula que avalia `$RunningTasks` poderia ser drasticamente afetada por um aumento nas tarefas por nó.</span><span class="sxs-lookup"><span data-stu-id="5a52f-133">For example, a formula that evaluates `$RunningTasks` could be dramatically affected by an increase in tasks per node.</span></span> <span data-ttu-id="5a52f-134">Consulte [Dimensionar automaticamente nós de computação em um pool do Lote do Azure](batch-automatic-scaling.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="5a52f-134">See [Automatically scale compute nodes in an Azure Batch pool](batch-automatic-scaling.md) for more information.</span></span>
>
>

## <a name="distribution-of-tasks"></a><span data-ttu-id="5a52f-135">Distribuição de tarefas</span><span class="sxs-lookup"><span data-stu-id="5a52f-135">Distribution of tasks</span></span>
<span data-ttu-id="5a52f-136">Quando nós de computação Olá em um pool podem executar tarefas simultaneamente, é importante toospecify como você deseja Olá tarefas toobe distribuída entre os nós de saudação no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a52f-136">When hello compute nodes in a pool can execute tasks concurrently, it's important toospecify how you want hello tasks toobe distributed across hello nodes in hello pool.</span></span>

<span data-ttu-id="5a52f-137">Usando Olá [CloudPool.TaskSchedulingPolicy] [ task_schedule] propriedade, você pode especificar que as tarefas devem ser atribuídas uniformemente em todos os nós no pool de saudação ("difusão").</span><span class="sxs-lookup"><span data-stu-id="5a52f-137">By using hello [CloudPool.TaskSchedulingPolicy][task_schedule] property, you can specify that tasks should be assigned evenly across all nodes in hello pool ("spreading").</span></span> <span data-ttu-id="5a52f-138">Ou você pode especificar que máximo possível de tarefas devem ser atribuídas o nó tooeach antes de tarefas atribuídas nó tooanother no pool de saudação ("remessa").</span><span class="sxs-lookup"><span data-stu-id="5a52f-138">Or you can specify that as many tasks as possible should be assigned tooeach node before tasks are assigned tooanother node in hello pool ("packing").</span></span>

<span data-ttu-id="5a52f-139">Como um exemplo de como esse recurso é útil, considere o pool de saudação do [padrão\_D14](../cloud-services/cloud-services-sizes-specs.md) nós (por exemplo hello acima) que é configurado com um [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] valor de 16.</span><span class="sxs-lookup"><span data-stu-id="5a52f-139">As an example of how this feature is valuable, consider hello pool of [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes (in hello example above) that is configured with a [CloudPool.MaxTasksPerComputeNode][maxtasks_net] value of 16.</span></span> <span data-ttu-id="5a52f-140">Se hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] é configurado com um [ComputeNodeFillType] [ fill_type] de *pacote*, ele seria maximizar o uso de todos os 16 núcleos de cada nó e permitir uma [pool de dimensionamento automático](batch-automatic-scaling.md) tooprune nós não utilizados do pool de saudação (nós sem quaisquer tarefas atribuídas).</span><span class="sxs-lookup"><span data-stu-id="5a52f-140">If hello [CloudPool.TaskSchedulingPolicy][task_schedule] is configured with a [ComputeNodeFillType][fill_type] of *Pack*, it would maximize usage of all 16 cores of each node and allow an [autoscaling pool](batch-automatic-scaling.md) tooprune unused nodes from hello pool (nodes without any tasks assigned).</span></span> <span data-ttu-id="5a52f-141">Isso minimiza o uso de recursos e economizando dinheiro.</span><span class="sxs-lookup"><span data-stu-id="5a52f-141">This minimizes resource usage and saves money.</span></span>

## <a name="batch-net-example"></a><span data-ttu-id="5a52f-142">Exemplo de .NET do Lote</span><span class="sxs-lookup"><span data-stu-id="5a52f-142">Batch .NET example</span></span>
<span data-ttu-id="5a52f-143">Isso [Batch .NET] [ api_net] trecho de código da API mostra uma solicitação toocreate um pool que contém quatro nós grande com um máximo de quatro tarefas por nó.</span><span class="sxs-lookup"><span data-stu-id="5a52f-143">This [Batch .NET][api_net] API code snippet shows a request toocreate a pool that contains four large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="5a52f-144">Especifica uma política que preencher cada nó com o nó do tarefas anteriores tooassigning tarefas tooanother no pool de saudação de agendamento de tarefas.</span><span class="sxs-lookup"><span data-stu-id="5a52f-144">It specifies a task scheduling policy that will fill each node with tasks prior tooassigning tasks tooanother node in hello pool.</span></span> <span data-ttu-id="5a52f-145">Para obter mais informações sobre como adicionar pools usando Olá lote .NET API, consulte [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span><span class="sxs-lookup"><span data-stu-id="5a52f-145">For more information on adding pools by using hello Batch .NET API, see [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span></span>

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

## <a name="batch-rest-example"></a><span data-ttu-id="5a52f-146">Exemplo REST do Lote</span><span class="sxs-lookup"><span data-stu-id="5a52f-146">Batch REST example</span></span>
<span data-ttu-id="5a52f-147">Isso [restante do lote] [ api_rest] trecho API mostra uma solicitação toocreate um pool que contém dois nós grandes com um máximo de quatro tarefas por nó.</span><span class="sxs-lookup"><span data-stu-id="5a52f-147">This [Batch REST][api_rest] API snippet shows a request toocreate a pool that contains two large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="5a52f-148">Para obter mais informações sobre como adicionar pools usando Olá API REST, consulte [adicionar uma conta do pool de tooan][rest_addpool].</span><span class="sxs-lookup"><span data-stu-id="5a52f-148">For more information on adding pools by using hello REST API, see [Add a pool tooan account][rest_addpool].</span></span>

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
> <span data-ttu-id="5a52f-149">Você pode definir Olá `maxTasksPerNode` elemento e [MaxTasksPerComputeNode] [ maxtasks_net] propriedade apenas no momento da criação de pool.</span><span class="sxs-lookup"><span data-stu-id="5a52f-149">You can set hello `maxTasksPerNode` element and [MaxTasksPerComputeNode][maxtasks_net] property only at pool creation time.</span></span> <span data-ttu-id="5a52f-150">Eles não poderão ser modificados após a criação do pool.</span><span class="sxs-lookup"><span data-stu-id="5a52f-150">They cannot be modified after a pool has already been created.</span></span>
>
>

## <a name="code-sample"></a><span data-ttu-id="5a52f-151">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="5a52f-151">Code sample</span></span>
<span data-ttu-id="5a52f-152">Olá [ParallelNodeTasks] [ parallel_tasks_sample] projeto no GitHub ilustra o uso de saudação do hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] propriedade.</span><span class="sxs-lookup"><span data-stu-id="5a52f-152">hello [ParallelNodeTasks][parallel_tasks_sample] project on GitHub illustrates hello use of hello [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property.</span></span>

<span data-ttu-id="5a52f-153">Este aplicativo de console c# usa Olá [Batch .NET] [ api_net] biblioteca toocreate um pool com um ou mais nós de computação.</span><span class="sxs-lookup"><span data-stu-id="5a52f-153">This C# console application uses hello [Batch .NET][api_net] library toocreate a pool with one or more compute nodes.</span></span> <span data-ttu-id="5a52f-154">Ele executa um número configurável de tarefas nesses nós de carga de variável de toosimulate.</span><span class="sxs-lookup"><span data-stu-id="5a52f-154">It executes a configurable number of tasks on those nodes toosimulate variable load.</span></span> <span data-ttu-id="5a52f-155">Saída do aplicativo hello Especifica quais nós executado cada tarefa.</span><span class="sxs-lookup"><span data-stu-id="5a52f-155">Output from hello application specifies which nodes executed each task.</span></span> <span data-ttu-id="5a52f-156">aplicativo Hello também fornece um resumo dos parâmetros do trabalho hello e duração.</span><span class="sxs-lookup"><span data-stu-id="5a52f-156">hello application also provides a summary of hello job parameters and duration.</span></span> <span data-ttu-id="5a52f-157">parte de saída de saudação de duas execuções diferentes do aplicativo de exemplo hello resumo Olá é exibida abaixo.</span><span class="sxs-lookup"><span data-stu-id="5a52f-157">hello summary portion of hello output from two different runs of hello sample application appears below.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

<span data-ttu-id="5a52f-158">a primeira execução Olá Olá do aplicativo de exemplo mostra que com um único nó no pool de saudação e a configuração padrão de saudação de uma tarefa por nó, a duração do trabalho Olá é em 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="5a52f-158">hello first execution of hello sample application shows that with a single node in hello pool and hello default setting of one task per node, hello job duration is over 30 minutes.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

<span data-ttu-id="5a52f-159">Olá segundo execute de saudação exemplo mostra uma redução significativa na duração do trabalho.</span><span class="sxs-lookup"><span data-stu-id="5a52f-159">hello second run of hello sample shows a significant decrease in job duration.</span></span> <span data-ttu-id="5a52f-160">Isso ocorre porque o pool de saudação foi configurado com quatro tarefas por nó, o que permite que o trabalho de saudação do toocomplete de execução de tarefas paralelas em aproximadamente um quarto de tempo de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a52f-160">This is because hello pool was configured with four tasks per node, which allows for parallel task execution toocomplete hello job in nearly a quarter of hello time.</span></span>

> [!NOTE]
> <span data-ttu-id="5a52f-161">durações de trabalho Olá em resumos de saudação acima não incluem o tempo de criação de pool.</span><span class="sxs-lookup"><span data-stu-id="5a52f-161">hello job durations in hello summaries above do not include pool creation time.</span></span> <span data-ttu-id="5a52f-162">Cada um dos trabalhos de saudação acima foi enviado toopreviously criado pools cujos nós de computação estavam em hello *ocioso* estado na hora de envio.</span><span class="sxs-lookup"><span data-stu-id="5a52f-162">Each of hello jobs above was submitted toopreviously created pools whose compute nodes were in hello *Idle* state at submission time.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="5a52f-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5a52f-163">Next steps</span></span>
### <a name="batch-explorer-heat-map"></a><span data-ttu-id="5a52f-164">Mapa de Calor do Explorador do Lote</span><span class="sxs-lookup"><span data-stu-id="5a52f-164">Batch Explorer Heat Map</span></span>
<span data-ttu-id="5a52f-165">Olá [Gerenciador de lote do Azure][batch_explorer], uma saudação do Azure Batch [aplicativos de exemplo][github_samples], contém um *mapa de calor* recurso que fornece visualização da execução da tarefa.</span><span class="sxs-lookup"><span data-stu-id="5a52f-165">hello [Azure Batch Explorer][batch_explorer], one of hello Azure Batch [sample applications][github_samples], contains a *Heat Map* feature that provides visualization of task execution.</span></span> <span data-ttu-id="5a52f-166">Quando você estiver executando Olá [ParallelTasks] [ parallel_tasks_sample] aplicativo de exemplo, você pode usar tooeasily de recurso de mapa de calor Olá visualizar execução Olá de tarefas paralelas em cada nó.</span><span class="sxs-lookup"><span data-stu-id="5a52f-166">When you're executing hello [ParallelTasks][parallel_tasks_sample] sample application, you can use hello Heat Map feature tooeasily visualize hello execution of parallel tasks on each node.</span></span>

![Mapa de Calor do Explorador do Lote][1]

<span data-ttu-id="5a52f-168">*Mapa de Calor do Gerenciador de Lotes que mostra um pool de quatro nós, com cada nó atualmente executando quatro tarefas*</span><span class="sxs-lookup"><span data-stu-id="5a52f-168">*Batch Explorer Heat Map showing a pool of four nodes, with each node currently executing four tasks*</span></span>

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
