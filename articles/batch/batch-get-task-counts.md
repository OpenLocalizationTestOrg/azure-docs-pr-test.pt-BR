---
title: aaaMonitor andamento do trabalho pela contagem de tarefas por estado - lote do Azure | Microsoft Docs
description: "Monitorar o progresso de saudação de um trabalho chamando a operação de obter contagens de tarefa de saudação toocount tarefas para um trabalho. Você pode obter uma contagem de tarefas ativas, em execução e concluídas e das tarefas que tiveram êxito ou falharam."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: article
ms.date: 08/02/2017
ms.author: tamram
ms.openlocfilehash: 03957d8a3d678bf44587f3bc7f988a76885c2af0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="count-tasks-by-state-toomonitor-a-jobs-progress-preview"></a>Contagem de tarefas por estado toomonitor andamento do trabalho (visualização)

Lote do Azure fornece o andamento de Olá de toomonitor uma maneira eficiente de um trabalho que ele execute suas tarefas. Você pode chamar hello [obter contagens de tarefa] [ rest_get_task_counts] toofind operação quantas tarefas estão em um estado ativo, em execução ou concluído e quantos têm êxito ou falhou. Contando o número de saudação de tarefas em cada estado, você pode mais facilmente exibir usuário de tooa de andamento do trabalho hello, ou detectar atrasos inesperados ou falhas que podem afetar o trabalho de saudação.

> [!IMPORTANT]
> Olá operação obter contagens de tarefa está atualmente em visualização e ainda não está disponível no Azure Government do Azure na China e Azure Alemanha. 
>
>

## <a name="how-tasks-are-counted"></a>Como as tarefas são contadas

Olá operação obter contagens de tarefa contagens de tarefas por estado, da seguinte maneira:

- Uma tarefa é contabilizada como **active** quando ele é toorun em fila e é capaz de, mas não esteja atualmente atribuído tooa do nó de computação. Uma tarefa também é contada como **ativa** se depende de uma tarefa pai que ainda não foi concluída. Para obter mais informações sobre dependências de tarefas, consulte [criar dependências toorun tarefas que dependem de outras tarefas](batch-task-dependencies.md). 
- Uma tarefa é contabilizada como **executando** quando ele foi atribuído tooa do nó de computação, mas ainda não foi concluído. Uma tarefa é contabilizada como **executando** quando seu estado é `preparing` ou `running`, conforme indicado pelo Olá [obter informações sobre uma tarefa] [ rest_get_task] operação.
- Uma tarefa é contabilizada como **concluída** quando ele não está mais qualificado toorun. Uma tarefa contabilizada como **concluída** normalmente foi concluída com êxito ou foi concluída sem êxito e também esgotou o seu limite de repetições. 

Olá operação obter contagens de tarefa também informa quantas tarefas tem êxito ou falhou. Lote determina se uma tarefa teve êxito ou falha, verificando Olá **resultados** propriedade Olá [executionInfo] [https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task#executionInfo] propriedade:

    - Uma tarefa é contabilizada como **bem-sucedida** se Olá resultado da execução da tarefa é `success`.
    - Uma tarefa é contabilizada como **falha** se Olá resultado da execução da tarefa é `failure`.

Para obter mais informações sobre estados de tarefa, consulte [Obter informações sobre uma tarefa][rest_get_task].

Olá .NET exemplo de código mostra como contagens de tarefa tooretrieve por estado: 

```csharp
var taskCounts = await batchClient.JobOperations.GetTaskCountsAsync("job-1");

Console.WriteLine("Task count in active state: {0}", taskCounts.Active);
Console.WriteLine("Task count in preparing or running state: {0}", taskCounts.Running);
Console.WriteLine("Task count in completed state: {0}", taskCounts.Completed);
Console.WriteLine("Succeeded task count: {0}", taskCounts.Succeeded);
Console.WriteLine("Failed task count: {0}", taskCounts.Failed);
Console.WriteLine("ValidationStatus: {0}", taskCounts.ValidationStatus);
```

> [!NOTE]
> Você pode usar um padrão similar para REST e outras linguagens com suporte tooget tarefa contagens de um trabalho. 
> 
> 

## <a name="consistency-checking-for-task-counts"></a>Verificação de consistência para contagens de tarefas

serviço de lote Olá agrega as contagens de tarefa ao coletar dados de várias partes de um sistema distribuído assíncrono. tooensure que a tarefa contagens estão corretas, o lote fornece validação adicional para contagens de estado executando verificações de consistência em vários componentes do sistema de saudação. Lote executa essas verificações de consistência, como há menos de 200.000 tarefas no trabalho de saudação. Olá improvável que a verificação de consistência de saudação encontra erros, lote corrige o resultado de saudação da operação obter contagens de tarefas de saudação com base nos resultados de Olá Olá de verificação de consistência. Olá, verificação de consistência é uma tooensure extra de medida que os clientes que utilizam Olá operação obter contagens de tarefa obtém informações de direito Olá que eles precisam para sua solução.

Olá **validationStatus** propriedade em resposta Olá indica se o lote executou a verificação de consistência de saudação. Se o lote não foi capaz de toocheck contagens de estado contra estados real de saudação mantidos no sistema de saudação, Olá **validationStatus** propriedade for definida muito`unvalidated`. Por motivos de desempenho, lote não executará verificação de consistência Olá se Olá trabalho inclui mais de 200.000 tarefas, portanto Olá **validationStatus** propriedade pode ser definida muito`unvalidated` nesse caso. No entanto, contagem de tarefas de saudação não é necessariamente errada nesse caso, como até mesmo uma perda de dados muito limitada é muito improvável. 

Quando uma tarefa muda de estado, o pipeline de agregação Olá processa Olá alteração dentro de alguns segundos. Olá operação obter contagens de tarefa reflete as contagens de tarefa Olá atualizada dentro desse período. No entanto, se uma alteração em um estado de tarefa de erros de pipeline de agregação Olá, em seguida, alteração não é registrado até a próxima passagem de validação hello. Durante esse tempo, as contagens de tarefa podem ser ligeiramente imprecisas vencimento evento ausentes toohello, mas corrigidos na próxima fase de validação hello.

## <a name="best-practices-for-counting-a-jobs-tasks"></a>Melhores práticas para contagem de tarefas de um trabalho

É chamar a operação obter contagens de tarefa de saudação tooreturn de maneira mais eficiente de saudação uma contagem básica das tarefas de um trabalho por estado. Se você estiver usando a versão do serviço de lote de 2017-06-01.5.1, é recomendável escrever ou atualizar seu toouse código obter contagens de tarefa.

Olá operação obter contagens de tarefa não está disponível em versões de serviço de lote anterior ao 2017-06-01.5.1. Se você estiver usando uma versão mais antiga do serviço hello, em seguida, use uma lista de tarefas de toocount de consulta em um trabalho. Para obter mais informações, consulte [criar consultas de recursos de lote toolist com eficiência](batch-efficient-list-queries.md).

## <a name="next-steps"></a>Próximas etapas

* Consulte Olá [visão geral do recurso de lote](batch-api-basics.md) toolearn mais sobre recursos e conceitos do serviço de lote. Olá artigo aborda os principais recursos de lote hello, como pools, nós de computação, trabalhos e tarefas e fornece uma visão geral dos recursos do serviço de saudação.
* Conheça os fundamentos de saudação do desenvolvimento de um aplicativo habilitado para lote usando Olá [biblioteca cliente .NET do lote](batch-dotnet-get-started.md) ou [Python](batch-python-tutorial.md). Esses artigos introdutórios guiá-lo por meio de um aplicativo de trabalho que usa tooexecute de serviço de lote Olá uma carga de trabalho em vários nós de computação.


[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job
[rest_get_task]: https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task
[rest_list_tasks]: https://docs.microsoft.com/rest/api/batchservice/list-the-tasks-associated-with-a-job
