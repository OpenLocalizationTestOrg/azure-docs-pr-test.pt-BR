---
title: consultas de lista eficiente aaaDesign - lote do Azure | Microsoft Docs
description: "Aumente o desempenho filtrando suas consultas ao solicitar informações sobre os recursos do Lote, como pools, trabalhos, tarefas e nós de computação."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 031fefeb-248e-4d5a-9bc2-f07e46ddd30d
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 08/02/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b7e554119ec9d0e9e8007ccfb1ca80fe142a5e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-queries-toolist-batch-resources-efficiently"></a>Criar consultas de recursos de lote toolist com eficiência

Aqui você aprenderá como tooincrease desempenho do seu aplicativo do Azure Batch reduzindo Olá quantidade de dados que são retornados pelo serviço de hello quando você consulta trabalhos, tarefas e nós de computação com hello [Batch .NET] [ api_net] biblioteca.

Quase todos os aplicativos de lote necessário tooperform algum tipo de monitoramento ou outra operação que consulta o serviço de lote hello, geralmente em intervalos regulares. Por exemplo, toodetermine se houver qualquer tarefa em fila restantes em um trabalho, você deve obter dados em todas as tarefas no trabalho de saudação. status de saudação toodetermine de nós em seu pool, você deve obter dados em cada nó no pool de saudação. Este artigo explica como tooexecute como as consultas em Olá modo mais eficiente.

> [!NOTE]
> Olá serviço de lote fornece suporte de API especial para o cenário comum de saudação de contagem de tarefas em um trabalho. Em vez de usar uma consulta de lista para eles, você pode chamar hello [obter contagens de tarefa] [ rest_get_task_counts] operação. Obter Contagens de Tarefas indica quantas tarefas estão pendentes, em execução ou concluídas e quantas tarefas tiveram êxito ou falharam. Obter Contagens de Tarefas é mais eficiente do que uma consulta de lista. Para obter mais informações, consulte [Contar tarefas para um trabalho por estado (versão prévia)](batch-get-task-counts.md). 
>
> Olá operação obter contagens de tarefa não está disponível em versões de serviço de lote anterior ao 2017-06-01.5.1. Se você estiver usando uma versão mais antiga do serviço hello, em seguida, use uma lista de tarefas de toocount de consulta em um trabalho.
>
> 

## <a name="meet-hello-detaillevel"></a>Atender Olá DetailLevel
Em um aplicativo de lote de produção, podem número de entidades, como trabalhos, tarefas e os nós de computação em Olá milhares. Quando você solicita informações sobre esses recursos, uma potencialmente grande quantidade de dados deve "ocupar durante a transmissão hello" do aplicativo de tooyour de serviço de lote hello em cada consulta. Limitando o número de saudação de itens e o tipo de informações retornadas por uma consulta, você pode aumentar a velocidade de saudação de suas consultas e hello, portanto, o desempenho de seu aplicativo.

Isso [.NET em lotes] [ api_net] listas de trecho de código API *cada* tarefa que está associada com um trabalho, juntamente com *todas as* das propriedades de saudação de cada tarefa:

```csharp
// Get a collection of all of hello tasks and all of their properties for job-001
IPagedEnumerable<CloudTask> allTasks =
    batchClient.JobOperations.ListTasks("job-001");
```

Você pode executar uma consulta de lista muito mais eficiente, no entanto, ao aplicar uma consulta de tooyour "nível de detalhe". Isso é feito fornecendo uma [ODATADetailLevel] [ odata] objeto toohello [JobOperations.ListTasks] [ net_list_tasks] método. Este trecho de código retorna apenas ID hello, linha de comando e propriedades de informações de nó de computação de tarefas concluídas:

```csharp
// Configure an ODATADetailLevel specifying a subset of tasks and
// their properties tooreturn
ODATADetailLevel detailLevel = new ODATADetailLevel();
detailLevel.FilterClause = "state eq 'completed'";
detailLevel.SelectClause = "id,commandLine,nodeInfo";

// Supply hello ODATADetailLevel toohello ListTasks method
IPagedEnumerable<CloudTask> completedTasks =
    batchClient.JobOperations.ListTasks("job-001", detailLevel);
```

Nesse cenário de exemplo, se houver milhares de tarefas no trabalho hello, Olá resultados da consulta segundo Olá normalmente serão muito mais rápido do que Olá retornado pela primeira vez. Há mais informações sobre como usar ODATADetailLevel, quando você lista itens com hello lote .NET API [abaixo](#efficient-querying-in-batch-net).

> [!IMPORTANT]
> É altamente recomendável que você *sempre* forneça uma lista de .NET API ODATADetailLevel objeto tooyour chama tooensure máxima eficiência e o desempenho do seu aplicativo. Ao especificar um nível de detalhe, você pode ajudar a toolower tempos de resposta do serviço de lote, melhorar a utilização de rede e minimizar o uso de memória por aplicativos cliente.
> 
> 

## <a name="filter-select-and-expand"></a>Filtrar, selecionar e expandir
Olá [Batch .NET] [ api_net] e [restante do lote] [ api_rest] APIs fornecem Olá capacidade tooreduce ambos de número de itens que são retornados em uma lista, Olá Assim como Olá a quantidade de informações que são retornadas para cada um. Você faz isso especificando **filter**, **select** e **expand strings** ao executar as consultas da lista.

### <a name="filter"></a>Filter
cadeia de caracteres de filtro de saudação é uma expressão que reduz o número de saudação de itens que são retornados. Por exemplo, lista apenas hello tarefas para um trabalho ou lista somente nós de computação que estão prontos toorun tarefas em execução.

* cadeia de caracteres de filtro de saudação consiste em uma ou mais expressões, com uma expressão que consiste em um nome de propriedade, um operador e um valor. Propriedades de saudação que podem ser especificadas são tipo de entidade tooeach específico que você consulta, assim como operadores Olá que têm suporte para cada propriedade.
* Várias expressões podem ser combinadas usando operadores lógicos Olá `and` e `or`.
* Este exemplo filtrar listas de cadeia de caracteres somente tarefas Olá executando "renderizar": `(state eq 'running') and startswith(id, 'renderTask')`.

### <a name="select"></a>Selecionar
cadeia de caracteres selecione Olá limita os valores de propriedade Olá são retornados para cada item. Especificar uma lista de nomes de propriedade e apenas os valores de propriedade são retornados para itens de Olá Olá resultados da consulta.

* cadeia de caracteres selecione Olá consiste em uma lista separada por vírgulas de nomes de propriedade. Você pode especificar qualquer uma das propriedades Olá Olá tipo de entidade que está sendo consultada.
* Esta cadeia de caracteres select de exemplo especifica que apenas três valores da propriedade devem ser retornados para cada tarefa: `id, state, stateTransitionTime`.

### <a name="expand"></a>Expanda
Olá expanda cadeia de caracteres reduz o número de saudação de chamadas de API que são necessária tooobtain certas informações. Quando você usa uma cadeia de caracteres expand, é possível obter mais informações sobre cada item com uma única chamada de API. Em vez de primeira lista Olá obtenção de entidades, solicitação de informações para cada item na lista de saudação, você use uma cadeia de caracteres de expansão tooobtain Olá mesmas informações em uma única chamada de API. Menos chamadas de API significam um desempenho melhor.

* Toohello selecione cadeia de caracteres semelhante, Olá expandir os controles de cadeia de caracteres se determinados dados são incluídos nos resultados da consulta de lista.
* Olá expanda cadeia de caracteres é suportado apenas quando ele é usado na lista de trabalhos, agendas de trabalho, tarefas e pools. Atualmente, dá suporte apenas a informações de estatísticas.
* Quando todas as propriedades são necessárias e selecione nenhuma cadeia de caracteres for especificada, Olá expanda cadeia de caracteres *deve* ser tooget usadas as informações de estatísticas. Se uma cadeia de select é tooobtain usado um subconjunto de propriedades, em seguida, `stats` pode ser especificada na cadeia de caracteres selecione hello e Olá expanda cadeia de caracteres não precisa toobe especificado.
* Este exemplo expanda cadeia de caracteres Especifica que as informações de estatísticas devem ser retornadas para cada item na lista de saudação: `stats`.

> [!NOTE]
> Ao construir qualquer Olá três tipos de cadeia de caracteres de consulta (filtrar, selecione e expanda), você deve garantir que os nomes de propriedade hello e case correspondem ao que suas contrapartes de elemento da API REST. Por exemplo, ao trabalhar com hello .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) classe, você deve especificar **estado** em vez de **estado**, embora Olá propriedade .NET é [ CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state). Consulte as tabelas de saudação abaixo para mapeamentos de propriedade entre Olá .NET e APIs REST.
> 
> 

### <a name="rules-for-filter-select-and-expand-strings"></a>Especificações das cadeias de caracteres filter, select e expand
* Nomes de propriedades no filtro, selecione e expanda cadeias de caracteres deve aparecer como fazem em Olá [restante do lote] [ api_rest] API – mesmo quando você usa [Batch .NET] [ api_net] ou um dos Olá outros SDKs do lote.
* Todos os nomes de propriedade diferenciam maiúsculas de minúsculas, mas valores de propriedade não diferenciam maiúsculas de minúsculas.
* As cadeias de caracteres de data/hora podem ter um dos dois formatos e devem ser precedidas por `DateTime`.
  
  * Exemplo de formato W3C-DTF: `creationTime gt DateTime'2011-05-08T08:49:37Z'`
  * Exemplo de formato RFC 1123: `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`
* As cadeias de caracteres boolianas são `true` ou `false`.
* Se uma propriedade ou operador inválido for especificado, o resultado será um erro `400 (Bad Request)` .

## <a name="efficient-querying-in-batch-net"></a>Consulta eficiente no .NET de Lote
Dentro de saudação [Batch .NET] [ api_net] API, Olá [ODATADetailLevel] [ odata] classe é usada para fornecimento de filtro, selecione e expanda cadeias de caracteres operações de toolist. Olá ODataDetailLevel classe tem três propriedades de cadeia de caracteres pública que podem ser especificadas no construtor de saudação ou definidas diretamente no objeto de saudação. Você, em seguida, passa Olá ODataDetailLevel objeto como um parâmetro toohello várias operações de lista como [ListPools][net_list_pools], [ListJobs][net_list_jobs], e [ListTasks][net_list_tasks].

* [ODATADetailLevel][odata].[ FilterClause][odata_filter]: limitar o número de saudação de itens que são retornados.
* [ODATADetailLevel][odata].[SelectClause][odata_select]: especificar quais valores da propriedade são retornados com cada item.
* [ODATADetailLevel][odata].[ExpandClause][odata_expand]: recuperar dados de todos os itens em uma única chamada à API, em vez de chamadas separadas para cada item.

Hello trecho de código a seguir usa Olá lote .NET API tooefficiently consulta Olá serviço de lote para estatísticas de saudação de um conjunto específico de pools de. Nesse cenário, o usuário de lote de saudação tem pools de teste e produção. pool de teste Olá IDs são prefixados com "test" e o grupo de produção de hello IDs são prefixados com "produção". No trecho hello, *myBatchClient* é uma instância inicializada corretamente do hello [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) classe.

```csharp
// First we need an ODATADetailLevel instance on which tooset hello filter, select,
// and expand clause strings
ODATADetailLevel detailLevel = new ODATADetailLevel();

// We want toopull only hello "test" pools, so we limit hello number of items returned
// by using a FilterClause and specifying that hello pool IDs must start with "test"
detailLevel.FilterClause = "startswith(id, 'test')";

// toofurther limit hello data that crosses hello wire, configure hello SelectClause to
// limit hello properties that are returned on each CloudPool object tooonly
// CloudPool.Id and CloudPool.Statistics
detailLevel.SelectClause = "id, stats";

// Specify hello ExpandClause so that hello .NET API pulls hello statistics for the
// CloudPools in a single underlying REST API call. Note that we use hello pool's
// REST API element name "stats" here as opposed too"Statistics" as it appears in
// hello .NET API (CloudPool.Statistics)
detailLevel.ExpandClause = "stats";

// Now get our collection of pools, minimizing hello amount of data that is returned
// by specifying hello detail level that we configured above
List<CloudPool> testPools =
    await myBatchClient.PoolOperations.ListPools(detailLevel).ToListAsync();
```

> [!TIP]
> Uma instância de [ODATADetailLevel] [ odata] configurado com Select e cláusulas de expansão também podem ser passadas tooappropriate Get métodos, como [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx) , quantidade de saudação toolimit de dados que é retornado.
> 
> 

## <a name="batch-rest-toonet-api-mappings"></a>Mapeamentos REST too.NET API de lote
Os nomes de propriedade nas cadeias de caracteres de filtro, seleção e expansão *devem* refletir os seus equivalentes da API REST, no nome e no caso. tabelas de saudação abaixo fornecem mapeamentos entre hello .NET e contrapartes da API REST.

### <a name="mappings-for-filter-strings"></a>Mapeamentos para cadeias de caracteres de filtro
* **Métodos de lista do .NET**: cada um dos métodos de API .NET Olá nesta coluna aceita um [ODATADetailLevel] [ odata] objeto como um parâmetro.
* **Solicitações REST de lista**: API de REST de cada página vinculada tooin esta coluna contém uma tabela que especifica propriedades hello e operações que é permitido em *filtro* cadeias de caracteres. Você usará esses nomes de propriedade e operações ao construir uma cadeia de caracteres [ODATADetailLevel.FilterClause][odata_filter].

| Métodos da lista .NET | Solicitações da lista REST |
| --- | --- |
| [CertificateOperations.ListCertificates][net_list_certs] |[Listar certificados de saudação em uma conta][rest_list_certs] |
| [CloudTask.ListNodeFiles][net_list_task_files] |[Listar arquivos de saudação associados à tarefa][rest_list_task_files] |
| [JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status] |[Lista o status de saudação de preparação de trabalho hello e tarefas de versão para um trabalho][rest_list_jobprep_status] |
| [JobOperations.ListJobs][net_list_jobs] |[Listar trabalhos de saudação em uma conta][rest_list_jobs] |
| [JobOperations.ListNodeFiles][net_list_nodefiles] |[Lista Olá arquivos em um nó][rest_list_nodefiles] |
| [JobOperations.ListTasks][net_list_tasks] |[Lista de tarefas Olá associada a um trabalho][rest_list_tasks] |
| [JobScheduleOperations.ListJobSchedules][net_list_job_schedules] |[Lista Olá agendas de trabalho em uma conta][rest_list_job_schedules] |
| [JobScheduleOperations.ListJobs][net_list_schedule_jobs] |[Listar trabalhos de saudação associados com uma agenda de trabalho][rest_list_schedule_jobs] |
| [PoolOperations.ListComputeNodes][net_list_compute_nodes] |[Olá lista nós de computação em um pool][rest_list_compute_nodes] |
| [PoolOperations.ListPools][net_list_pools] |[Listar pools de saudação em uma conta][rest_list_pools] |

### <a name="mappings-for-select-strings"></a>Mapeamentos para cadeias de caracteres de seleção
* **Tipos de Lote .NET**: tipos de API do Lote .NET.
* **Entidades da API REST**: cada página nesta coluna contém uma ou mais tabelas que listam os nomes de propriedade Olá API REST para o tipo de saudação. Esses nomes de propriedade são usados ao construir as cadeias de caracteres *select* . Você usará esses mesmos nomes de propriedade ao construir uma cadeia de caracteres [ODATADetailLevel.SelectClause][odata_select].

| Tipos de Lote .NET | Entidades da API REST |
| --- | --- |
| [Certificate][net_cert] |[Obter informações sobre um certificado][rest_get_cert] |
| [CloudJob][net_job] |[Obter informações sobre um trabalho][rest_get_job] |
| [CloudJobSchedule][net_schedule] |[Obter informações sobre um cronograma de trabalho][rest_get_schedule] |
| [ComputeNode][net_node] |[Obter informações sobre um nó][rest_get_node] |
| [CloudPool][net_pool] |[Obter informações sobre um pool][rest_get_pool] |
| [CloudTask][net_task] |[Obter informações sobre uma tarefa][rest_get_task] |

## <a name="example-construct-a-filter-string"></a>Exemplo: construir uma cadeia de caracteres filter
Quando você cria uma cadeia de caracteres de filtro para [ODATADetailLevel.FilterClause][odata_filter], consulte a tabela Olá acima em "Mapeamentos para cadeias de caracteres de filtro" toofind Olá API REST documentação página correspondente operação de lista de toohello que você deseja tooperform. Você encontrará as propriedades de saudação e os operadores com suporte na primeira tabela multilinha Olá nessa página. Se você desejar tooretrieve todas as tarefas cujo código de saída era diferente de zero, por exemplo, essa linha no [lista Olá as tarefas associadas a um trabalho] [ rest_list_tasks] Especifica a cadeia de caracteres de propriedade aplicável hello e operadores permitidos:

| Propriedade | Operações permitidas | Tipo |
|:--- |:--- |:--- |
| `executionInfo/exitCode` |`eq, ge, gt, le , lt` |`Int` |

Assim, a cadeia de caracteres de filtro de saudação para listar todas as tarefas com um código de saída diferente de zero seria:

`(executionInfo/exitCode lt 0) or (executionInfo/exitCode gt 0)`

## <a name="example-construct-a-select-string"></a>Exemplo: construir uma cadeia de caracteres select
tooconstruct [ODATADetailLevel.SelectClause][odata_select], consulte a tabela Olá acima em "Mapeamentos para cadeias de caracteres selecionados" e navegue toohello página de API REST que corresponde a toohello tipo de entidade que você Listar. Você encontrará propriedades selecionável hello e os operadores com suporte na primeira tabela multilinha Olá nessa página. Se você deseja tooretrieve somente Olá ID e a linha de comando para cada tarefa em uma lista, por exemplo, você encontrará essas linhas na tabela aplicável Olá em [obter informações sobre uma tarefa][rest_get_task]:

| Propriedade | Tipo | Observações |
|:--- |:--- |:--- |
| `id` |`String` |`hello ID of hello task.` |
| `commandLine` |`String` |`hello command line of hello task.` |

cadeia de caracteres Selecione para incluir somente Olá ID e a linha de comando com cada tarefa listada Olá seria:

`id, commandLine`

## <a name="code-samples"></a>Exemplos de código
### <a name="efficient-list-queries-code-sample"></a>Exemplo de código de consultas de lista eficientes
Check-out Olá [EfficientListQueries] [ efficient_query_sample] projeto de exemplo no GitHub toosee como eficiente consulta lista pode afetar o desempenho em um aplicativo. Este aplicativo de console c# cria e adiciona um grande número de tarefas tooa trabalho. Em seguida, faz várias toohello de chamadas [JobOperations.ListTasks] [ net_list_tasks] método e passa [ODATADetailLevel] [ odata] objetos configurado com propriedades diferentes valores toovary Olá total toobe dados retornado. Ele produz o seguinte de toohello semelhante de saída:

```
Adding 5000 tasks toojob jobEffQuery...
5000 tasks added in 00:00:47.3467587, hit ENTER tooquery tasks...

4943 tasks retrieved in 00:00:04.3408081 (ExpandClause:  | FilterClause: state eq 'active' | SelectClause: id,state)
0 tasks retrieved in 00:00:00.2662920 (ExpandClause:  | FilterClause: state eq 'running' | SelectClause: id,state)
59 tasks retrieved in 00:00:00.3337760 (ExpandClause:  | FilterClause: state eq 'completed' | SelectClause: id,state)
5000 tasks retrieved in 00:00:04.1429881 (ExpandClause:  | FilterClause:  | SelectClause: id,state)
5000 tasks retrieved in 00:00:15.1016127 (ExpandClause:  | FilterClause:  | SelectClause: id,state,environmentSettings)
5000 tasks retrieved in 00:00:17.0548145 (ExpandClause: stats | FilterClause:  | SelectClause: )

Sample complete, hit ENTER toocontinue...
```

Conforme mostrado no tempo de saudação, você pode diminuir significativamente tempos de resposta de consulta limitando propriedades hello e número de saudação de itens retornados. Você pode encontrar esse e outros projetos de exemplo no hello [exemplos de lote do azure] [ github_samples] repositório no GitHub.

### <a name="batchmetrics-library-and-code-sample"></a>Biblioteca BatchMetrics e exemplo de código
Além disso toohello EfficientListQueries código de exemplo acima, você pode encontrar hello [BatchMetrics] [ batch_metrics] projeto no hello [exemplos de lote do azure] [ github_samples] Repositório do GitHub. projeto de exemplo Hello BatchMetrics demonstra como tooefficiently monitorar o andamento do trabalho de lote do Azure usando a API de lote de saudação.

Olá [BatchMetrics] [ batch_metrics] exemplo inclui um projeto de biblioteca de classes .NET que você pode incorporar em seus próprios projetos e um simples de linha de comando tooexercise de programa e demonstrar o uso de saudação do hello biblioteca.

aplicativo de exemplo Hello dentro do projeto Olá demonstra Olá operações a seguir:

1. Selecionar atributos específicos nas propriedades de saudação ordem toodownload somente é necessário
2. Filtrando em tempos de transição de estado no toodownload ordem somente alterações desde a última consulta de saudação

Por exemplo, Olá método a seguir aparece no hello BatchMetrics biblioteca. Ele retorna um ODATADetailLevel que especifica que somente Olá `id` e `state` propriedades devem ser obtidas para entidades de saudação que são consultadas. Ela também especifica que apenas as entidades cujo estado foi alterado desde a saudação especificada `DateTime` parâmetro deve ser retornado.

```csharp
internal static ODATADetailLevel OnlyChangedAfter(DateTime time)
{
    return new ODATADetailLevel(
        selectClause: "id, state",
        filterClause: string.Format("stateTransitionTime gt DateTime'{0:o}'", time)
    );
}
```

## <a name="next-steps"></a>Próximas etapas
### <a name="parallel-node-tasks"></a>Tarefas paralelas do nó
[Maximizar o uso de recursos de computação do Azure Batch com tarefas simultâneas do nó](batch-parallel-node-tasks.md) é outro artigo relacionados ao desempenho do aplicativo tooBatch. Alguns tipos de cargas de trabalho podem aproveitar a execução de tarefas paralelas nos nós de computação maiores, porém em menor número. Check-out Olá [cenário de exemplo](batch-parallel-node-tasks.md#example-scenario) artigo Olá para obter detalhes sobre esse cenário.

### <a name="batch-forum"></a>Fórum do Lote
Olá [Fórum do lote do Azure] [ forum] no MSDN é um ótimo colocar toodiscuss em lotes e fazer perguntas sobre o serviço de saudação. Acesse diretamente as postagens “fixas” úteis e poste suas dúvidas conforme elas surgirem enquanto você cria suas soluções do Lote.

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_metrics]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchMetrics
[efficient_query_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/EfficientListQueries
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_samples]: https://github.com/Azure/azure-batch-samples
[odata]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[odata_ctor]: https://msdn.microsoft.com/library/azure/dn866178.aspx
[odata_expand]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.expandclause.aspx
[odata_filter]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.filterclause.aspx
[odata_select]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.selectclause.aspx

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

[rest_list_certs]: https://msdn.microsoft.com/library/azure/dn820154.aspx
[rest_list_compute_nodes]: https://msdn.microsoft.com/library/azure/dn820159.aspx
[rest_list_job_schedules]: https://msdn.microsoft.com/library/azure/mt282174.aspx
[rest_list_jobprep_status]: https://msdn.microsoft.com/library/azure/mt282170.aspx
[rest_list_jobs]: https://msdn.microsoft.com/library/azure/dn820117.aspx
[rest_list_nodefiles]: https://msdn.microsoft.com/library/azure/dn820151.aspx
[rest_list_pools]: https://msdn.microsoft.com/library/azure/dn820101.aspx
[rest_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/mt282169.aspx
[rest_list_task_files]: https://msdn.microsoft.com/library/azure/dn820142.aspx
[rest_list_tasks]: https://msdn.microsoft.com/library/azure/dn820187.aspx

[rest_get_cert]: https://msdn.microsoft.com/library/azure/dn820176.aspx
[rest_get_job]: https://msdn.microsoft.com/library/azure/dn820106.aspx
[rest_get_node]: https://msdn.microsoft.com/library/azure/dn820168.aspx
[rest_get_pool]: https://msdn.microsoft.com/library/azure/dn820165.aspx
[rest_get_schedule]: https://msdn.microsoft.com/library/azure/mt282171.aspx
[rest_get_task]: https://msdn.microsoft.com/library/azure/dn820133.aspx

[net_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificate.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_schedule]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjobschedule.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx

[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job