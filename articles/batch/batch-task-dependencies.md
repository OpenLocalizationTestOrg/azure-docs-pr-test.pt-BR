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
# <a name="create-task-dependencies-toorun-tasks-that-depend-on-other-tasks"></a>Criar dependências toorun tarefas que dependem de outras tarefas

Você pode definir tarefa dependências toorun uma tarefa ou um conjunto de tarefas somente depois que uma tarefa pai foi concluída. Alguns cenários em que as dependências entre tarefas são úteis incluem:

* Cargas de trabalho de estilo de MapReduce na nuvem hello.
* Trabalhos cujas tarefas de processamento de dados podem ser expressas como um DAG (gráfico acíclico dirigido).
* Processos de renderização pré e pós-processamento, onde cada tarefa deve concluir antes de começar a próxima tarefa de saudação.
* Qualquer outro trabalho que tarefas de downstream dependem saída Olá das tarefas de upstream.

Dependências de tarefa em lotes, você pode criar tarefas que estão agendadas para execução em nós de computação após a conclusão de saudação de uma ou mais tarefas de pai. Por exemplo, você pode criar um trabalho que processa cada quadro de um filme 3D com tarefas paralelas separadas. tarefa final do Hello – hello "tarefa de mesclagem –" hello renderizado quadros em filme completo Olá somente depois que todos os quadros de mesclagens tenham sido com êxito gerados.

Por padrão, tarefas dependentes agendadas para execução após a tarefa pai de saudação foi concluída com êxito. Você pode especificar um comportamento padrão da dependência ação toooverride hello e executar tarefas quando ocorre falha na tarefa pai de saudação. Consulte Olá [ações de dependência](#dependency-actions) seção para obter detalhes.  

Você pode criar tarefas que dependem de outras tarefas em uma relação um para um ou um para muitos. Você também pode criar uma dependência de intervalo em que uma tarefa depende de conclusão de saudação de um grupo de tarefas dentro de um intervalo especificado de IDs de tarefas. Você pode combinar essas relações de muitos-para-muitos três cenários básicos toocreate.

## <a name="task-dependencies-with-batch-net"></a>Dependências de tarefas com o .NET do Lote
Neste artigo, discutiremos como dependências tooconfigure usando Olá [Batch .NET] [ net_msdn] biblioteca. Primeiro mostraremos como muito[ativar a dependência de tarefa](#enable-task-dependencies) em seus trabalhos e, em seguida, demonstre como muito[configurar uma tarefa com dependências](#create-dependent-tasks). Podemos também descrevem como toospecify uma dependência ação toorun tarefas dependentes se pai Olá falhar. Por fim, discutiremos Olá [situações de dependência](#dependency-scenarios) que dá suporte ao lote.

## <a name="enable-task-dependencies"></a>Habilitar dependências de tarefas
dependências de tarefa toouse em seu aplicativo de lote, você deve primeiro configurar Olá trabalho toouse dependências. No .NET em lotes, habilitá-lo no seu [CloudJob] [ net_cloudjob] definindo seu [UsesTaskDependencies] [ net_usestaskdependencies] propriedade muito`true`:

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

Olá precede o trecho de código, "batchClient" é uma instância de saudação [BatchClient] [ net_batchclient] classe.

## <a name="create-dependent-tasks"></a>Criar tarefas dependentes
toocreate uma tarefa que depende de conclusão de saudação de uma ou mais tarefas de pai, você pode especificar que Olá tarefa "depende" Olá, outras tarefas. No .NET de lote configurar Olá [CloudTask][net_cloudtask].[ DependsOn] [ net_dependson] propriedade com uma instância do hello [TaskDependencies] [ net_taskdependencies] classe:

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

Este trecho de código cria uma tarefa dependente com a identificação da tarefa “Flowers”. Olá tarefa "Flores" depende das tarefas "Chuva" e "Sun". A tarefa "Flores" será toorun agendado em um nó de computação somente após tarefas "Chuva" e "Sun" foram concluídos com êxito.

> [!NOTE]
> Uma tarefa é considerada toobe foi concluída com êxito quando ele está em Olá **concluída** estado e seu **código de saída** é `0`. No .NET em lotes, isso significa um [CloudTask][net_cloudtask].[ Estado] [ net_taskstate] valor da propriedade `Completed` e Olá do CloudTask [TaskExecutionInformation][net_taskexecutioninformation].[ ExitCode] [ net_exitcode] é o valor da propriedade `0`.
> 
> 

## <a name="dependency-scenarios"></a>Cenários de dependência
Há três cenários de dependência de tarefas básicos que você pode usar no Lote do Azure: um-para-um, um-para-muitos e dependência de intervalo de IDs de tarefas. Eles podem ser combinados tooprovide um quarto cenário, muitos-para-muitos.

| Cenário&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Exemplo |  |
|:---:| --- | --- |
|  [Um-para-um](#one-to-one) |*tarefaB* depende de *tarefaA* <p/> A *tarefaB* não será agendada para execução até que a *tarefaA* seja concluída com êxito |![Diagrama: dependência de tarefa de um para um][1] |
|  [Um-para-muitos](#one-to-many) |A *tarefaC* depende da *tarefaA* e da *tarefaB* <p/> A *tarefaC* não será agendada para execução até que a *tarefaA* e a *tarefaB* sejam concluídas com êxito |![Diagrama: dependência de tarefa de um para muitos][2] |
|  [Intervalo de IDs de tarefa](#task-id-range) |A *taskD* depende de diversas tarefas <p/> *taskD* não será agendado para execução até que as tarefas de saudação com IDs *1* por meio de *10* foram concluídos com êxito |![Diagrama: dependência de intervalo de ids de tarefas][3] |

> [!TIP]
> Você pode criar **muitos-para-muitos** relações, como onde tarefas C, D, E e F cada dependem das tarefas A e B. Isso é útil, por exemplo, em cenários de pré-processamento em paralelo, em que as tarefas de downstream dependem de saída Olá de várias tarefas de upstream.
> 
> Olá exemplos nesta seção, uma tarefa dependente é executada somente depois que tarefas de pai Olá concluída com êxito. Esse comportamento é o comportamento padrão de saudação para uma tarefa dependente. Depois que uma tarefa pai falha, especificando um comportamento padrão da dependência ação toooverride hello, você pode executar uma tarefa dependente. Consulte Olá [ações de dependência](#dependency-actions) seção para obter detalhes.

### <a name="one-to-one"></a>Um-para-um
Em uma relação um para um, uma tarefa depende após a conclusão bem-sucedida da tarefa pai de uma saudação. toocreate Olá dependência, forneça um toohello de ID única tarefa [TaskDependencies][net_taskdependencies].[ OnId] [ net_onid] método estático ao preencher Olá [DependsOn] [ net_dependson] propriedade [CloudTask] [ net_cloudtask].

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a>Um-para-muitos
Em uma relação um-para-muitos, uma tarefa depende da conclusão de saudação de várias tarefas de pai. toocreate Olá dependência, fornecer um conjunto de tarefas IDs toohello [TaskDependencies][net_taskdependencies].[ OnIds] [ net_onids] método estático ao preencher Olá [DependsOn] [ net_dependson] propriedade [CloudTask] [ net_cloudtask].

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

### <a name="task-id-range"></a>Intervalo de IDs de tarefa
Em uma dependência em uma variedade de tarefas de pai, uma tarefa depende da conclusão de Olá Olá cujos IDs residem dentro de um intervalo de tarefas.
dependência de saudação toocreate, forneça Olá primeiro e última tarefa IDs no hello intervalo toohello [TaskDependencies][net_taskdependencies].[ OnIdRange] [ net_onidrange] método estático ao preencher Olá [DependsOn] [ net_dependson] propriedade [CloudTask] [net_cloudtask].

> [!IMPORTANT]
> Quando você usa os intervalos de ID de tarefa para as suas dependências, Olá IDs de tarefa no intervalo de saudação *deve* ser representações de cadeia de caracteres de valores inteiros.
> 
> Todas as tarefas no intervalo de saudação devem satisfazer a dependência hello, concluindo com êxito ou executando com uma falha de ação de dependência tooa mapeado definida muito**satisfação**. Consulte Olá [ações de dependência](#dependency-actions) seção para obter detalhes.
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

## <a name="dependency-actions"></a>Ações de dependência

Por padrão, uma tarefa dependente ou um conjunto de tarefas é executado somente após a conclusão bem-sucedida de uma tarefa pai. Em alguns cenários, convém tarefas dependentes toorun mesmo se a tarefa pai de saudação falha. Você pode substituir o comportamento padrão de saudação especificando uma ação de dependência. Uma ação de dependência Especifica se uma tarefa dependente toorun qualificado, com base no sucesso de saudação ou a falha da tarefa pai de saudação. 

Por exemplo, suponha que uma tarefa dependente está aguardando a data de conclusão de saudação da tarefa de upstream hello. Se a tarefa de upstream Olá falhar, tarefa dependente Olá ainda pode ser capaz de toorun usando os dados mais antigos. Nesse caso, uma ação de dependência pode especificar a que tarefa dependente Olá é elegível toorun apesar da falha de saudação da tarefa pai de saudação.

Uma ação de dependência baseia-se em uma condição de saída para a tarefa pai de saudação. Você pode especificar uma ação de dependência para qualquer Olá seguintes condições de saída; para .NET, consulte Olá [ExitConditions] [ net_exitconditions] classe para obter detalhes:

- Quando ocorre um erro de pré-processamento.
- Quando ocorre um erro de carregamento de arquivo. Se a tarefa de saudação for encerrada com um código de saída foi especificado por meio de **exitCodes** ou **exitCodeRanges**e, em seguida, encontra um erro de carregamento de arquivo, a ação de saudação especificado pelo Olá saída código terá precedência.
- Quando a tarefa de saudação encerrada com um código de saída definido pelo Olá **ExitCodes** propriedade.
- Quando a tarefa de saudação encerrada com um código de saída que está em um intervalo especificado por Olá **ExitCodeRanges** propriedade.
- Olá caso padrão, se Olá tarefa é encerrada com um código de saída não está definido por **ExitCodes** ou **ExitCodeRanges**, ou se Olá tarefa é encerrada com um erro de pré-processamento e Olá **PreProcessingError**  propriedade não está definida ou se hello falha de tarefa com um arquivo carregar erro e hello **FileUploadError** propriedade não está definida. 

toospecify uma ação de dependência no .NET, Olá conjunto [ExitOptions][net_exitoptions].[ DependencyAction] [ net_dependencyaction] propriedade para a condição de saída de hello. Olá **DependencyAction** propriedade tem um dos dois valores:

- Saudação de configuração **DependencyAction** propriedade muito**satisfação** indica que tarefas dependentes estão qualificado toorun se a tarefa pai de saudação for encerrada com um erro especificado.
- Saudação de configuração **DependencyAction** propriedade muito**bloco** indica que as tarefas dependentes não são qualificado toorun.

Olá a configuração padrão para Olá **DependencyAction** é de propriedade **satisfação** para o código de saída 0, e **bloco** para todas as outras condições de saída.

trecho de código a seguir Hello define Olá **DependencyAction** propriedade para uma tarefa pai. Se tarefa pai de saudação for encerrada com um erro de pré-processamento, ou com Olá Olá dependentes a códigos de erro especificada, a tarefa é bloqueada. Se a tarefa pai de saudação for encerrada com qualquer outro erro diferente de zero, tarefa dependente Olá é toorun qualificado.

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

## <a name="code-sample"></a>Exemplo de código
Olá [TaskDependencies] [ github_taskdependencies] projeto de exemplo é uma saudação [exemplos de código do Azure Batch] [ github_samples] no GitHub. Esta solução do Visual Studio demonstra:

- Como tooenable dependência em um trabalho de tarefas
- Como toocreate tarefas que dependem de outras tarefas
- Como tooexecute as tarefas em um conjunto de nós de computação.

## <a name="next-steps"></a>Próximas etapas
### <a name="application-deployment"></a>Implantação do aplicativo
Olá [pacotes de aplicativos](batch-application-packages.md) recurso de lote fornece um modo fácil de implantar tooboth e versão aplicativos Olá as tarefas executadas em nós de computação.

### <a name="installing-applications-and-staging-data"></a>Instalação de aplicativos e preparação de dados
Consulte [nós de computação de instalação de aplicativos e dados em lotes de preparo] [ forum_post] no Fórum do lote do Azure Olá para uma visão geral dos métodos para preparar seus nós toorun tarefas. Gravado por um dos membros da equipe do Azure Batch Olá, que esta postagem é um bom primer em aplicativos de toocopy de maneiras diferentes de hello, dados de entrada de tarefa e outros arquivos tooyour nós de computação.

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
