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
# <a name="run-tasks-concurrently-toomaximize-usage-of-batch-compute-nodes"></a>Executar tarefas simultaneamente toomaximize uso de nós de computação do lote 

Ao executar mais de uma tarefa simultaneamente em cada nó de computação no pool de lote do Azure, você pode maximizar o uso de recursos em um número menor de nós no pool de saudação. Para algumas cargas de trabalho, isso pode resultar em tempos mais curtos de trabalho e reduzir os custos.

Enquanto alguns cenários beneficiam dedicar todos tarefa única de tooa de recursos de um nó, várias situações beneficiam permitindo tooshare de várias tarefas esses recursos:

* **Minimizar a transferência de dados** quando as tarefas estão tooshare capaz de dados. Nesse cenário, você pode reduzir consideravelmente os encargos de transferência de dados por meio de cópia de dados compartilhados tooa menor número de nós e executar tarefas em paralelo em cada nó. Isso se aplica especialmente se o nó de tooeach copiado Olá dados toobe deve ser transferido entre regiões geográficas.
* **Maximização do uso de memória** quando as tarefas exigirem uma grande quantidade de memória, mas somente durante curtos períodos de tempo, e em momentos variáveis durante a execução. Você pode empregar menos, mas maiores, nós com tooefficiently de memória mais tratar esses picos de computação. Esses nós teria várias tarefas em execução em paralelo em cada nó, mas cada tarefa seria tirar proveito de memória bastante de nós de saudação em momentos diferentes.
* **Redução dos limites do número de nós** quando a comunicação entre nós for necessária em um pool. Atualmente, pools configurados para comunicação entre nós são nós de computação too50 limitado. Se cada nó em um pool tal tooexecute capaz de tarefas em paralelo, um número maior de tarefas pode ser executado simultaneamente.
* **Replicação de um cluster de computação local**, por exemplo, quando você move um tooAzure do ambiente de computação primeiro. Se sua solução no local atual executa várias tarefas por nó de computação, você pode aumentar o número máximo de saudação de tarefas de nó toomore refletem com maior exatidão essa configuração.

## <a name="example-scenario"></a>Cenário de exemplo
Como um exemplo tooillustrate Olá benefícios da execução de tarefas paralelas, digamos que seu aplicativo de tarefa tem requisitos de CPU e memória, de modo que [padrão\_D1](../cloud-services/cloud-services-sizes-specs.md) nós são suficientes. Mas, em ordem toofinish Olá trabalho em tempo de saudação necessário 1.000 de nós são necessários.

Em vez de usar os nós Standard\_D1, que têm um núcleo de CPU, você poderia utilizar os nós [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) com 16 núcleos cada e permitir a execução de tarefas paralelas. Portanto, *16 vezes menos nós* poderiam ser usados; em vez de 1.000 nós, somente 63 seriam necessários. Além disso, se os arquivos de aplicativo grande ou dados de referência são necessários para cada nó, eficiência e a duração do trabalho são novamente aprimorados como dados de saudação são copiado tooonly 16 nós.

## <a name="enable-parallel-task-execution"></a>Habilitar a execução de tarefas paralelas
Você pode configurar nós de computação para execução de tarefas paralelas no nível do pool de saudação. A biblioteca do .NET em lotes hello, definir Olá [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] propriedade quando você cria um pool. Se você estiver usando Olá API REST do lote, defina Olá [maxTasksPerNode] [ rest_addpool] elemento no corpo da solicitação Olá durante a criação do pool.

Lote do Azure permite que você tooset máximo de tarefas por nó toofour vezes (4 x) Olá número de núcleos de nó. Por exemplo, se hello pool está configurado conosco de tamanho "Grande" (quatro núcleos), em seguida, `maxTasksPerNode` too16 pode ser definido. Para obter detalhes sobre o número de saudação de cores para cada um dos tamanhos de nó Olá, consulte [tamanhos para serviços de nuvem](../cloud-services/cloud-services-sizes-specs.md). Para obter mais informações sobre limites de serviço, consulte [cotas e limites de saudação do serviço Azure Batch](batch-quota-limit.md).

> [!TIP]
> Ser tootake-se em Olá conta `maxTasksPerNode` valor quando você construir um [fórmula de dimensionamento automático] [ enable_autoscaling] para o pool. Por exemplo, uma fórmula que avalia `$RunningTasks` poderia ser drasticamente afetada por um aumento nas tarefas por nó. Consulte [Dimensionar automaticamente nós de computação em um pool do Lote do Azure](batch-automatic-scaling.md) para saber mais.
>
>

## <a name="distribution-of-tasks"></a>Distribuição de tarefas
Quando nós de computação Olá em um pool podem executar tarefas simultaneamente, é importante toospecify como você deseja Olá tarefas toobe distribuída entre os nós de saudação no pool de saudação.

Usando Olá [CloudPool.TaskSchedulingPolicy] [ task_schedule] propriedade, você pode especificar que as tarefas devem ser atribuídas uniformemente em todos os nós no pool de saudação ("difusão"). Ou você pode especificar que máximo possível de tarefas devem ser atribuídas o nó tooeach antes de tarefas atribuídas nó tooanother no pool de saudação ("remessa").

Como um exemplo de como esse recurso é útil, considere o pool de saudação do [padrão\_D14](../cloud-services/cloud-services-sizes-specs.md) nós (por exemplo hello acima) que é configurado com um [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] valor de 16. Se hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] é configurado com um [ComputeNodeFillType] [ fill_type] de *pacote*, ele seria maximizar o uso de todos os 16 núcleos de cada nó e permitir uma [pool de dimensionamento automático](batch-automatic-scaling.md) tooprune nós não utilizados do pool de saudação (nós sem quaisquer tarefas atribuídas). Isso minimiza o uso de recursos e economizando dinheiro.

## <a name="batch-net-example"></a>Exemplo de .NET do Lote
Isso [Batch .NET] [ api_net] trecho de código da API mostra uma solicitação toocreate um pool que contém quatro nós grande com um máximo de quatro tarefas por nó. Especifica uma política que preencher cada nó com o nó do tarefas anteriores tooassigning tarefas tooanother no pool de saudação de agendamento de tarefas. Para obter mais informações sobre como adicionar pools usando Olá lote .NET API, consulte [BatchClient.PoolOperations.CreatePool][poolcreate_net].

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

## <a name="batch-rest-example"></a>Exemplo REST do Lote
Isso [restante do lote] [ api_rest] trecho API mostra uma solicitação toocreate um pool que contém dois nós grandes com um máximo de quatro tarefas por nó. Para obter mais informações sobre como adicionar pools usando Olá API REST, consulte [adicionar uma conta do pool de tooan][rest_addpool].

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
> Você pode definir Olá `maxTasksPerNode` elemento e [MaxTasksPerComputeNode] [ maxtasks_net] propriedade apenas no momento da criação de pool. Eles não poderão ser modificados após a criação do pool.
>
>

## <a name="code-sample"></a>Exemplo de código
Olá [ParallelNodeTasks] [ parallel_tasks_sample] projeto no GitHub ilustra o uso de saudação do hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] propriedade.

Este aplicativo de console c# usa Olá [Batch .NET] [ api_net] biblioteca toocreate um pool com um ou mais nós de computação. Ele executa um número configurável de tarefas nesses nós de carga de variável de toosimulate. Saída do aplicativo hello Especifica quais nós executado cada tarefa. aplicativo Hello também fornece um resumo dos parâmetros do trabalho hello e duração. parte de saída de saudação de duas execuções diferentes do aplicativo de exemplo hello resumo Olá é exibida abaixo.

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

a primeira execução Olá Olá do aplicativo de exemplo mostra que com um único nó no pool de saudação e a configuração padrão de saudação de uma tarefa por nó, a duração do trabalho Olá é em 30 minutos.

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

Olá segundo execute de saudação exemplo mostra uma redução significativa na duração do trabalho. Isso ocorre porque o pool de saudação foi configurado com quatro tarefas por nó, o que permite que o trabalho de saudação do toocomplete de execução de tarefas paralelas em aproximadamente um quarto de tempo de saudação.

> [!NOTE]
> durações de trabalho Olá em resumos de saudação acima não incluem o tempo de criação de pool. Cada um dos trabalhos de saudação acima foi enviado toopreviously criado pools cujos nós de computação estavam em hello *ocioso* estado na hora de envio.
>
>

## <a name="next-steps"></a>Próximas etapas
### <a name="batch-explorer-heat-map"></a>Mapa de Calor do Explorador do Lote
Olá [Gerenciador de lote do Azure][batch_explorer], uma saudação do Azure Batch [aplicativos de exemplo][github_samples], contém um *mapa de calor* recurso que fornece visualização da execução da tarefa. Quando você estiver executando Olá [ParallelTasks] [ parallel_tasks_sample] aplicativo de exemplo, você pode usar tooeasily de recurso de mapa de calor Olá visualizar execução Olá de tarefas paralelas em cada nó.

![Mapa de Calor do Explorador do Lote][1]

*Mapa de Calor do Gerenciador de Lotes que mostra um pool de quatro nós, com cada nó atualmente executando quatro tarefas*

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
