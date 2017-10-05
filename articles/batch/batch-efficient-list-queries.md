---
title: Projetar consultas de lista eficientes - Lote do Azure | Microsoft Docs
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
ms.openlocfilehash: a80b207f591bd888d4749287527013c5e554fb6e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-queries-to-list-batch-resources-efficiently"></a><span data-ttu-id="6c713-103">Criar consultas para listar recursos do Lote com eficiência</span><span class="sxs-lookup"><span data-stu-id="6c713-103">Create queries to list Batch resources efficiently</span></span>

<span data-ttu-id="6c713-104">Aqui, você aprenderá a melhorar o desempenho do aplicativo do Lote do Azure reduzindo a quantidade de dados retornados pelo serviço quando consulta trabalhos, tarefas e nós de computação com a biblioteca [.NET do Lote][api_net].</span><span class="sxs-lookup"><span data-stu-id="6c713-104">Here you'll learn how to increase your Azure Batch application's performance by reducing the amount of data that is returned by the service when you query jobs, tasks, and compute nodes with the [Batch .NET][api_net] library.</span></span>

<span data-ttu-id="6c713-105">Quase todos os aplicativos do Lote precisam executar algum tipo de monitoramento ou outra operação que consulta o serviço de Lote, geralmente em intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="6c713-105">Nearly all Batch applications need to perform some type of monitoring or other operation that queries the Batch service, often at regular intervals.</span></span> <span data-ttu-id="6c713-106">Por exemplo, para determinar se há qualquer tarefa em fila restante em um trabalho, você deve obter dados sobre cada tarefa no trabalho.</span><span class="sxs-lookup"><span data-stu-id="6c713-106">For example, to determine whether there are any queued tasks remaining in a job, you must get data on every task in the job.</span></span> <span data-ttu-id="6c713-107">Para determinar o status de nós em seu pool, você deve obter os dados em cada nó no pool.</span><span class="sxs-lookup"><span data-stu-id="6c713-107">To determine the status of nodes in your pool, you must get data on every node in the pool.</span></span> <span data-ttu-id="6c713-108">Este artigo explica como executar essas consultas da forma mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="6c713-108">This article explains how to execute such queries in the most efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="6c713-109">O serviço de Lote fornece suporte de API especial para o cenário comum de tarefas de contagem em um trabalho.</span><span class="sxs-lookup"><span data-stu-id="6c713-109">The Batch service provides special API support for the common scenario of counting tasks in a job.</span></span> <span data-ttu-id="6c713-110">Em vez de usar uma consulta de lista para elas, você pode chamar a operação [Obter Contagens de Tarefas][rest_get_task_counts].</span><span class="sxs-lookup"><span data-stu-id="6c713-110">Instead of using a list query for these, you can call the [Get Task Counts][rest_get_task_counts] operation.</span></span> <span data-ttu-id="6c713-111">Obter Contagens de Tarefas indica quantas tarefas estão pendentes, em execução ou concluídas e quantas tarefas tiveram êxito ou falharam.</span><span class="sxs-lookup"><span data-stu-id="6c713-111">Get Task Counts indicates how many tasks are pending, running or complete, and how many tasks have succeeded or failed.</span></span> <span data-ttu-id="6c713-112">Obter Contagens de Tarefas é mais eficiente do que uma consulta de lista.</span><span class="sxs-lookup"><span data-stu-id="6c713-112">Get Task Counts is more efficient than a list query.</span></span> <span data-ttu-id="6c713-113">Para obter mais informações, consulte [Contar tarefas para um trabalho por estado (versão prévia)](batch-get-task-counts.md).</span><span class="sxs-lookup"><span data-stu-id="6c713-113">For more information, see [Count tasks for a job by state (Preview)](batch-get-task-counts.md).</span></span> 
>
> <span data-ttu-id="6c713-114">A operação obter contagens de tarefa não está disponível em versões do serviço de Lote anteriores a 2017-06-01.5.1.</span><span class="sxs-lookup"><span data-stu-id="6c713-114">The Get Task Counts operation is not available in Batch service versions earlier than 2017-06-01.5.1.</span></span> <span data-ttu-id="6c713-115">Se você estiver usando uma versão mais antiga do serviço, use uma consulta de lista para contar tarefas em um trabalho em vez disso.</span><span class="sxs-lookup"><span data-stu-id="6c713-115">If you are using an older version of the service, then use a list query to count tasks in a job instead.</span></span>
>
> 

## <a name="meet-the-detaillevel"></a><span data-ttu-id="6c713-116">Atender DetailLevel</span><span class="sxs-lookup"><span data-stu-id="6c713-116">Meet the DetailLevel</span></span>
<span data-ttu-id="6c713-117">Em um aplicativo do Lote de produção, as entidades, como trabalhos, tarefas e nós de computação, podem chegar a milhares.</span><span class="sxs-lookup"><span data-stu-id="6c713-117">In a production Batch application, entities like jobs, tasks, and compute nodes can number in the thousands.</span></span> <span data-ttu-id="6c713-118">Quando você solicita informações sobre esses recursos, uma quantidade de dados potencialmente grande deve "cruzar a transmissão" do serviço do Lote para seu aplicativo em cada consulta.</span><span class="sxs-lookup"><span data-stu-id="6c713-118">When you request information on these resources, a potentially large amount of data must "cross the wire" from the Batch service to your application on each query.</span></span> <span data-ttu-id="6c713-119">Limitando o número de itens e o tipo de informação retornada por uma consulta, você pode aumentar a velocidade de suas consultas e, portanto, o desempenho de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6c713-119">By limiting the number of items and type of information that is returned by a query, you can increase the speed of your queries, and therefore the performance of your application.</span></span>

<span data-ttu-id="6c713-120">Esse trecho de código da API do [.NET do Lote][api_net] lista *todas* as tarefas associadas a um trabalho, bem como *todas* as propriedades de cada tarefa:</span><span class="sxs-lookup"><span data-stu-id="6c713-120">This [Batch .NET][api_net] API code snippet lists *every* task that is associated with a job, along with *all* of the properties of each task:</span></span>

```csharp
// Get a collection of all of the tasks and all of their properties for job-001
IPagedEnumerable<CloudTask> allTasks =
    batchClient.JobOperations.ListTasks("job-001");
```

<span data-ttu-id="6c713-121">Porém, você pode executar uma consulta de lista muito mais eficiente aplicando um "nível de detalhe" à sua consulta.</span><span class="sxs-lookup"><span data-stu-id="6c713-121">You can perform a much more efficient list query, however, by applying a "detail level" to your query.</span></span> <span data-ttu-id="6c713-122">Você faz isso fornecendo um objeto [ODATADetailLevel][odata] ao método [JobOperations.ListTasks][net_list_tasks].</span><span class="sxs-lookup"><span data-stu-id="6c713-122">You do this by supplying an [ODATADetailLevel][odata] object to the [JobOperations.ListTasks][net_list_tasks] method.</span></span> <span data-ttu-id="6c713-123">Este trecho de código retorna apenas a ID, a linha de comando e as propriedades de informações do nó de computação das tarefas concluídas:</span><span class="sxs-lookup"><span data-stu-id="6c713-123">This snippet returns only the ID, command line, and compute node information properties of completed tasks:</span></span>

```csharp
// Configure an ODATADetailLevel specifying a subset of tasks and
// their properties to return
ODATADetailLevel detailLevel = new ODATADetailLevel();
detailLevel.FilterClause = "state eq 'completed'";
detailLevel.SelectClause = "id,commandLine,nodeInfo";

// Supply the ODATADetailLevel to the ListTasks method
IPagedEnumerable<CloudTask> completedTasks =
    batchClient.JobOperations.ListTasks("job-001", detailLevel);
```

<span data-ttu-id="6c713-124">Neste cenário do exemplo, se houver milhares de tarefas no trabalho, os resultados da segunda consulta serão retornados normalmente muito mais rapidamente do que os da primeira.</span><span class="sxs-lookup"><span data-stu-id="6c713-124">In this example scenario, if there are thousands of tasks in the job, the results from the second query will typically be returned much quicker than the first.</span></span> <span data-ttu-id="6c713-125">Mais informações sobre como usar o ODATADetailLevel ao listar os itens com a API do Lote .NET são incluídas [abaixo](#efficient-querying-in-batch-net).</span><span class="sxs-lookup"><span data-stu-id="6c713-125">More information about using ODATADetailLevel when you list items with the Batch .NET API is included [below](#efficient-querying-in-batch-net).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c713-126">Recomendamos que você *sempre* forneça um objeto ODATADetailLevel para as chamadas de lista da API .NET para garantir a máxima eficiência e desempenho de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6c713-126">We highly recommend that you *always* supply an ODATADetailLevel object to your .NET API list calls to ensure maximum efficiency and performance of your application.</span></span> <span data-ttu-id="6c713-127">Ao especificar um nível de detalhe, você ajuda a reduzir os tempos de resposta do serviço Lote, a melhorar a utilização da rede e a minimizar o uso da memória por aplicativos clientes.</span><span class="sxs-lookup"><span data-stu-id="6c713-127">By specifying a detail level, you can help to lower Batch service response times, improve network utilization, and minimize memory usage by client applications.</span></span>
> 
> 

## <a name="filter-select-and-expand"></a><span data-ttu-id="6c713-128">Filtrar, selecionar e expandir</span><span class="sxs-lookup"><span data-stu-id="6c713-128">Filter, select, and expand</span></span>
<span data-ttu-id="6c713-129">As APIs [.NET do Lote][api_net] e [REST do Lote][api_rest] permitem reduzir o número de itens retornados em uma lista e a quantidade de informações retornadas para cada um.</span><span class="sxs-lookup"><span data-stu-id="6c713-129">The [Batch .NET][api_net] and [Batch REST][api_rest] APIs provide the ability to reduce both the number of items that are returned in a list, as well as the amount of information that is returned for each.</span></span> <span data-ttu-id="6c713-130">Você faz isso especificando **filter**, **select** e **expand strings** ao executar as consultas da lista.</span><span class="sxs-lookup"><span data-stu-id="6c713-130">You do so by specifying **filter**, **select**, and **expand strings** when performing list queries.</span></span>

### <a name="filter"></a><span data-ttu-id="6c713-131">Filter</span><span class="sxs-lookup"><span data-stu-id="6c713-131">Filter</span></span>
<span data-ttu-id="6c713-132">A cadeia de caracteres filter é uma expressão que reduz o número de itens retornados.</span><span class="sxs-lookup"><span data-stu-id="6c713-132">The filter string is an expression that reduces the number of items that are returned.</span></span> <span data-ttu-id="6c713-133">Por exemplo, liste somente as tarefas em execução para um trabalho, ou liste apenas nós de computação que estejam prontos para executar tarefas.</span><span class="sxs-lookup"><span data-stu-id="6c713-133">For example, list only the running tasks for a job, or list only compute nodes that are ready to run tasks.</span></span>

* <span data-ttu-id="6c713-134">A cadeia de caracteres filter consiste em uma ou mais expressões, em que uma expressão consiste em um nome de propriedade, um operador e um valor.</span><span class="sxs-lookup"><span data-stu-id="6c713-134">The filter string consists of one or more expressions, with an expression that consists of a property name, operator, and value.</span></span> <span data-ttu-id="6c713-135">As propriedades que podem ser especificadas são específicas a cada tipo de entidade consultado, assim como os operadores com suporte para cada propriedade.</span><span class="sxs-lookup"><span data-stu-id="6c713-135">The properties that can be specified are specific to each entity type that you query, as are the operators that are supported for each property.</span></span>
* <span data-ttu-id="6c713-136">Várias expressões podem ser combinadas usando os operadores lógicos `and` e `or`.</span><span class="sxs-lookup"><span data-stu-id="6c713-136">Multiple expressions can be combined by using the logical operators `and` and `or`.</span></span>
* <span data-ttu-id="6c713-137">Esta cadeia de caracteres filter de exemplo lista apenas as tarefas de “renderização” em execução: `(state eq 'running') and startswith(id, 'renderTask')`.</span><span class="sxs-lookup"><span data-stu-id="6c713-137">This example filter string lists only the running "render" tasks: `(state eq 'running') and startswith(id, 'renderTask')`.</span></span>

### <a name="select"></a><span data-ttu-id="6c713-138">Selecionar</span><span class="sxs-lookup"><span data-stu-id="6c713-138">Select</span></span>
<span data-ttu-id="6c713-139">A cadeia de caracteres select limita os valores de propriedade retornados para cada item.</span><span class="sxs-lookup"><span data-stu-id="6c713-139">The select string limits the property values that are returned for each item.</span></span> <span data-ttu-id="6c713-140">Especifique uma lista de nomes de propriedade e apenas os valores dessas propriedades retornarão para os itens nos resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="6c713-140">You specify a list of property names, and only those property values are returned for the items in the query results.</span></span>

* <span data-ttu-id="6c713-141">A cadeia de caracteres de seleção consiste em uma lista separada por vírgulas de nomes de propriedade.</span><span class="sxs-lookup"><span data-stu-id="6c713-141">The select string consists of a comma-separated list of property names.</span></span> <span data-ttu-id="6c713-142">Você pode especificar qualquer uma das propriedades para o tipo de entidade que você está consultando.</span><span class="sxs-lookup"><span data-stu-id="6c713-142">You can specify any of the properties for the entity type you are querying.</span></span>
* <span data-ttu-id="6c713-143">Esta cadeia de caracteres select de exemplo especifica que apenas três valores da propriedade devem ser retornados para cada tarefa: `id, state, stateTransitionTime`.</span><span class="sxs-lookup"><span data-stu-id="6c713-143">This example select string specifies that only three property values should be returned for each task: `id, state, stateTransitionTime`.</span></span>

### <a name="expand"></a><span data-ttu-id="6c713-144">Expanda</span><span class="sxs-lookup"><span data-stu-id="6c713-144">Expand</span></span>
<span data-ttu-id="6c713-145">A cadeia de caracteres expand reduz o número de chamadas de API necessárias para obter determinadas informações.</span><span class="sxs-lookup"><span data-stu-id="6c713-145">The expand string reduces the number of API calls that are required to obtain certain information.</span></span> <span data-ttu-id="6c713-146">Quando você usa uma cadeia de caracteres expand, é possível obter mais informações sobre cada item com uma única chamada de API.</span><span class="sxs-lookup"><span data-stu-id="6c713-146">When you use an expand string, more information about each item can be obtained with a single API call.</span></span> <span data-ttu-id="6c713-147">Em vez de obter primeiro a lista de entidades para depois solicitar informações para cada item na lista, você pode usar uma cadeia de caracteres expand para obter as mesmas informações em uma única chamada de API.</span><span class="sxs-lookup"><span data-stu-id="6c713-147">Rather than first obtaining the list of entities, then requesting information for each item in the list, you use an expand string to obtain the same information in a single API call.</span></span> <span data-ttu-id="6c713-148">Menos chamadas de API significam um desempenho melhor.</span><span class="sxs-lookup"><span data-stu-id="6c713-148">Less API calls means better performance.</span></span>

* <span data-ttu-id="6c713-149">Assim como a cadeia de caracteres de seleção, a cadeia de caracteres de expansão controla se determinados dados são incluídos nos resultados da consulta de lista.</span><span class="sxs-lookup"><span data-stu-id="6c713-149">Similar to the select string, the expand string controls whether certain data is included in list query results.</span></span>
* <span data-ttu-id="6c713-150">A cadeia de caracteres de expansão tem suporte apenas quando ela é usada na listagem de trabalhos, agendas de trabalho, tarefas e pools.</span><span class="sxs-lookup"><span data-stu-id="6c713-150">The expand string is only supported when it is used in listing jobs, job schedules, tasks, and pools.</span></span> <span data-ttu-id="6c713-151">Atualmente, dá suporte apenas a informações de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="6c713-151">Currently, it only supports statistics information.</span></span>
* <span data-ttu-id="6c713-152">Quando todas as propriedades forem necessárias e nenhuma cadeia de seleção tiver sido especificada, a cadeia de expansão *terá* que ser usada para obter informações estatísticas.</span><span class="sxs-lookup"><span data-stu-id="6c713-152">When all properties are required and no select string is specified, the expand string *must* be used to get statistics information.</span></span> <span data-ttu-id="6c713-153">Se uma cadeia de caracteres select for usada para obter um subconjunto de propriedades, `stats` poderá ser especificado na cadeia select e a cadeia de caracteres expand não precisará ser especificada.</span><span class="sxs-lookup"><span data-stu-id="6c713-153">If a select string is used to obtain a subset of properties, then `stats` can be specified in the select string, and the expand string does not need to be specified.</span></span>
* <span data-ttu-id="6c713-154">Esta cadeia de caracteres expand de exemplo especifica que as informações de estatística devem ser retornadas para cada item na lista: `stats`.</span><span class="sxs-lookup"><span data-stu-id="6c713-154">This example expand string specifies that statistics information should be returned for each item in the list: `stats`.</span></span>

> [!NOTE]
> <span data-ttu-id="6c713-155">Ao criar qualquer um dos três tipos de cadeias de caracteres de consulta (filter, select e expand), você deve garantir que os nomes de propriedade e caso correspondam aos seus equivalentes de elemento da API REST.</span><span class="sxs-lookup"><span data-stu-id="6c713-155">When constructing any of the three query string types (filter, select, and expand), you must ensure that the property names and case match that of their REST API element counterparts.</span></span> <span data-ttu-id="6c713-156">Por exemplo, ao trabalhar com a classe [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) do .NET, você deve especificar **state** em vez de **State**, mesmo que a propriedade .NET seja [CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state).</span><span class="sxs-lookup"><span data-stu-id="6c713-156">For example, when working with the .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) class, you must specify **state** instead of **State**, even though the .NET property is [CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state).</span></span> <span data-ttu-id="6c713-157">Consulte as tabelas abaixo para ver mapeamentos de propriedade entre o .NET e APIs REST.</span><span class="sxs-lookup"><span data-stu-id="6c713-157">See the tables below for property mappings between the .NET and REST APIs.</span></span>
> 
> 

### <a name="rules-for-filter-select-and-expand-strings"></a><span data-ttu-id="6c713-158">Especificações das cadeias de caracteres filter, select e expand</span><span class="sxs-lookup"><span data-stu-id="6c713-158">Rules for filter, select, and expand strings</span></span>
* <span data-ttu-id="6c713-159">Os nomes das propriedades nas cadeias de caracteres filter, select e expand devem aparecer como na API [REST do Lote][api_rest] – mesmo quando você usa o [.NET do Lote][api_net] ou um dos outros SDKs do Lote.</span><span class="sxs-lookup"><span data-stu-id="6c713-159">Properties names in filter, select, and expand strings should appear as they do in the [Batch REST][api_rest] API--even when you use [Batch .NET][api_net] or one of the other Batch SDKs.</span></span>
* <span data-ttu-id="6c713-160">Todos os nomes de propriedade diferenciam maiúsculas de minúsculas, mas valores de propriedade não diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="6c713-160">All property names are case-sensitive, but property values are case insensitive.</span></span>
* <span data-ttu-id="6c713-161">As cadeias de caracteres de data/hora podem ter um dos dois formatos e devem ser precedidas por `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="6c713-161">Date/time strings can be one of two formats, and must be preceded with `DateTime`.</span></span>
  
  * <span data-ttu-id="6c713-162">Exemplo de formato W3C-DTF: `creationTime gt DateTime'2011-05-08T08:49:37Z'`</span><span class="sxs-lookup"><span data-stu-id="6c713-162">W3C-DTF format example: `creationTime gt DateTime'2011-05-08T08:49:37Z'`</span></span>
  * <span data-ttu-id="6c713-163">Exemplo de formato RFC 1123: `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span><span class="sxs-lookup"><span data-stu-id="6c713-163">RFC 1123 format example: `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span></span>
* <span data-ttu-id="6c713-164">As cadeias de caracteres boolianas são `true` ou `false`.</span><span class="sxs-lookup"><span data-stu-id="6c713-164">Boolean strings are either `true` or `false`.</span></span>
* <span data-ttu-id="6c713-165">Se uma propriedade ou operador inválido for especificado, o resultado será um erro `400 (Bad Request)` .</span><span class="sxs-lookup"><span data-stu-id="6c713-165">If an invalid property or operator is specified, a `400 (Bad Request)` error will result.</span></span>

## <a name="efficient-querying-in-batch-net"></a><span data-ttu-id="6c713-166">Consulta eficiente no .NET de Lote</span><span class="sxs-lookup"><span data-stu-id="6c713-166">Efficient querying in Batch .NET</span></span>
<span data-ttu-id="6c713-167">Na API [.NET do Lote][api_net], a classe [ODATADetailLevel][odata] é usada para fornecimento de cadeias de caracteres filter, select e expand para operações de lista.</span><span class="sxs-lookup"><span data-stu-id="6c713-167">Within the [Batch .NET][api_net] API, the [ODATADetailLevel][odata] class is used for supplying filter, select, and expand strings to list operations.</span></span> <span data-ttu-id="6c713-168">A classe ODataDetailLevel tem três propriedades de cadeia de caracteres públicas que podem ser especificadas no construtor ou definidas diretamente.</span><span class="sxs-lookup"><span data-stu-id="6c713-168">The ODataDetailLevel class has three public string properties that can be specified in the constructor, or set directly on the object.</span></span> <span data-ttu-id="6c713-169">Em seguida, você passa o objeto ODataDetailLevel como um parâmetro para as várias operações da lista, como [ListPools][net_list_pools], [ListJobs][net_list_jobs] e [ListTasks][net_list_tasks].</span><span class="sxs-lookup"><span data-stu-id="6c713-169">You then pass the ODataDetailLevel object as a parameter to the various list operations such as [ListPools][net_list_pools], [ListJobs][net_list_jobs], and [ListTasks][net_list_tasks].</span></span>

* <span data-ttu-id="6c713-170">[ODATADetailLevel][odata].[FilterClause][odata_filter]: limitar o número de itens retornados.</span><span class="sxs-lookup"><span data-stu-id="6c713-170">[ODATADetailLevel][odata].[FilterClause][odata_filter]: Limit the number of items that are returned.</span></span>
* <span data-ttu-id="6c713-171">[ODATADetailLevel][odata].[SelectClause][odata_select]: especificar quais valores da propriedade são retornados com cada item.</span><span class="sxs-lookup"><span data-stu-id="6c713-171">[ODATADetailLevel][odata].[SelectClause][odata_select]: Specify which property values are returned with each item.</span></span>
* <span data-ttu-id="6c713-172">[ODATADetailLevel][odata].[ExpandClause][odata_expand]: recuperar dados de todos os itens em uma única chamada à API, em vez de chamadas separadas para cada item.</span><span class="sxs-lookup"><span data-stu-id="6c713-172">[ODATADetailLevel][odata].[ExpandClause][odata_expand]: Retrieve data for all items in a single API call instead of separate calls for each item.</span></span>

<span data-ttu-id="6c713-173">O trecho de código abaixo usa a API de Lote .NET para consultar o serviço de Lote com eficiência a fim de obter as estatísticas de um conjunto específico de pools.</span><span class="sxs-lookup"><span data-stu-id="6c713-173">The following code snippet uses the Batch .NET API to efficiently query the Batch service for the statistics of a specific set of pools.</span></span> <span data-ttu-id="6c713-174">Nesse cenário, o usuário de Lote tem grupos de teste e de produção.</span><span class="sxs-lookup"><span data-stu-id="6c713-174">In this scenario, the Batch user has both test and production pools.</span></span> <span data-ttu-id="6c713-175">As IDs do pool de teste são prefixadas com "test", e as IDs do grupo de produção são prefixadas com "prod".</span><span class="sxs-lookup"><span data-stu-id="6c713-175">The test pool IDs are prefixed with "test", and the production pool IDs are prefixed with "prod".</span></span> <span data-ttu-id="6c713-176">No trecho de código, *myBatchClient* é uma instância devidamente inicializada da classe [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) .</span><span class="sxs-lookup"><span data-stu-id="6c713-176">In the snippet, *myBatchClient* is a properly initialized instance of the [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) class.</span></span>

```csharp
// First we need an ODATADetailLevel instance on which to set the filter, select,
// and expand clause strings
ODATADetailLevel detailLevel = new ODATADetailLevel();

// We want to pull only the "test" pools, so we limit the number of items returned
// by using a FilterClause and specifying that the pool IDs must start with "test"
detailLevel.FilterClause = "startswith(id, 'test')";

// To further limit the data that crosses the wire, configure the SelectClause to
// limit the properties that are returned on each CloudPool object to only
// CloudPool.Id and CloudPool.Statistics
detailLevel.SelectClause = "id, stats";

// Specify the ExpandClause so that the .NET API pulls the statistics for the
// CloudPools in a single underlying REST API call. Note that we use the pool's
// REST API element name "stats" here as opposed to "Statistics" as it appears in
// the .NET API (CloudPool.Statistics)
detailLevel.ExpandClause = "stats";

// Now get our collection of pools, minimizing the amount of data that is returned
// by specifying the detail level that we configured above
List<CloudPool> testPools =
    await myBatchClient.PoolOperations.ListPools(detailLevel).ToListAsync();
```

> [!TIP]
> <span data-ttu-id="6c713-177">Uma instância de [ODATADetailLevel][odata] configurada com as cláusulas Select e Expand também pode ser passada para os devidos métodos Get, como [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx), para limitar a quantidade de dados retornados.</span><span class="sxs-lookup"><span data-stu-id="6c713-177">An instance of [ODATADetailLevel][odata] that is configured with Select and Expand clauses can also be passed to appropriate Get methods, such as [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx), to limit the amount of data that is returned.</span></span>
> 
> 

## <a name="batch-rest-to-net-api-mappings"></a><span data-ttu-id="6c713-178">Mapeamentos REST Batch para API .NET</span><span class="sxs-lookup"><span data-stu-id="6c713-178">Batch REST to .NET API mappings</span></span>
<span data-ttu-id="6c713-179">Os nomes de propriedade nas cadeias de caracteres de filtro, seleção e expansão *devem* refletir os seus equivalentes da API REST, no nome e no caso.</span><span class="sxs-lookup"><span data-stu-id="6c713-179">Property names in filter, select, and expand strings *must* reflect their REST API counterparts, both in name and case.</span></span> <span data-ttu-id="6c713-180">As tabelas a seguir fornecem os mapeamentos entre os equivalentes API .NET e REST.</span><span class="sxs-lookup"><span data-stu-id="6c713-180">The tables below provide mappings between the .NET and REST API counterparts.</span></span>

### <a name="mappings-for-filter-strings"></a><span data-ttu-id="6c713-181">Mapeamentos para cadeias de caracteres de filtro</span><span class="sxs-lookup"><span data-stu-id="6c713-181">Mappings for filter strings</span></span>
* <span data-ttu-id="6c713-182">**Métodos da lista .NET**: cada um dos métodos da API .NET nesta coluna aceita um objeto [ODATADetailLevel][odata] como parâmetro.</span><span class="sxs-lookup"><span data-stu-id="6c713-182">**.NET list methods**: Each of the .NET API methods in this column accepts an [ODATADetailLevel][odata] object as a parameter.</span></span>
* <span data-ttu-id="6c713-183">**Solicitações da lista REST**: cada página da API REST associada a essa coluna contém uma tabela especificando as propriedades e as operações permitidas nas cadeias de caracteres *filter* .</span><span class="sxs-lookup"><span data-stu-id="6c713-183">**REST list requests**: Each REST API page linked to in this column contains a table that specifies the properties and operations that are allowed in *filter* strings.</span></span> <span data-ttu-id="6c713-184">Você usará esses nomes de propriedade e operações ao construir uma cadeia de caracteres [ODATADetailLevel.FilterClause][odata_filter].</span><span class="sxs-lookup"><span data-stu-id="6c713-184">You will use these property names and operations when you construct an [ODATADetailLevel.FilterClause][odata_filter] string.</span></span>

| <span data-ttu-id="6c713-185">Métodos da lista .NET</span><span class="sxs-lookup"><span data-stu-id="6c713-185">.NET list methods</span></span> | <span data-ttu-id="6c713-186">Solicitações da lista REST</span><span class="sxs-lookup"><span data-stu-id="6c713-186">REST list requests</span></span> |
| --- | --- |
| <span data-ttu-id="6c713-187">[CertificateOperations.ListCertificates][net_list_certs]</span><span class="sxs-lookup"><span data-stu-id="6c713-187">[CertificateOperations.ListCertificates][net_list_certs]</span></span> |<span data-ttu-id="6c713-188">[Listar os certificados de uma conta][rest_list_certs]</span><span class="sxs-lookup"><span data-stu-id="6c713-188">[List the certificates in an account][rest_list_certs]</span></span> |
| <span data-ttu-id="6c713-189">[CloudTask.ListNodeFiles][net_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="6c713-189">[CloudTask.ListNodeFiles][net_list_task_files]</span></span> |<span data-ttu-id="6c713-190">[Listar os arquivos associados a uma tarefa][rest_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="6c713-190">[List the files associated with a task][rest_list_task_files]</span></span> |
| <span data-ttu-id="6c713-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="6c713-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span></span> |<span data-ttu-id="6c713-192">[Listar o status das tarefas de preparação e liberação de trabalho para um determinado trabalho][rest_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="6c713-192">[List the status of the job preparation and job release tasks for a job][rest_list_jobprep_status]</span></span> |
| <span data-ttu-id="6c713-193">[JobOperations.ListJobs][net_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="6c713-193">[JobOperations.ListJobs][net_list_jobs]</span></span> |<span data-ttu-id="6c713-194">[Listar os trabalhos em uma conta][rest_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="6c713-194">[List the jobs in an account][rest_list_jobs]</span></span> |
| <span data-ttu-id="6c713-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="6c713-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span></span> |<span data-ttu-id="6c713-196">[Listar os arquivos em um nó][rest_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="6c713-196">[List the files on a node][rest_list_nodefiles]</span></span> |
| <span data-ttu-id="6c713-197">[JobOperations.ListTasks][net_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="6c713-197">[JobOperations.ListTasks][net_list_tasks]</span></span> |<span data-ttu-id="6c713-198">[Listar as tarefas associadas a um trabalho][rest_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="6c713-198">[List the tasks associated with a job][rest_list_tasks]</span></span> |
| <span data-ttu-id="6c713-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="6c713-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span></span> |<span data-ttu-id="6c713-200">[Listar os cronogramas de trabalho em uma conta][rest_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="6c713-200">[List the job schedules in an account][rest_list_job_schedules]</span></span> |
| <span data-ttu-id="6c713-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="6c713-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span></span> |<span data-ttu-id="6c713-202">[Listar os trabalhos associados a um cronograma de trabalho][rest_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="6c713-202">[List the jobs associated with a job schedule][rest_list_schedule_jobs]</span></span> |
| <span data-ttu-id="6c713-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="6c713-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span></span> |<span data-ttu-id="6c713-204">[Listar os nós de computação em um pool][rest_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="6c713-204">[List the compute nodes in a pool][rest_list_compute_nodes]</span></span> |
| <span data-ttu-id="6c713-205">[PoolOperations.ListPools][net_list_pools]</span><span class="sxs-lookup"><span data-stu-id="6c713-205">[PoolOperations.ListPools][net_list_pools]</span></span> |<span data-ttu-id="6c713-206">[Listar os pools em uma conta][rest_list_pools]</span><span class="sxs-lookup"><span data-stu-id="6c713-206">[List the pools in an account][rest_list_pools]</span></span> |

### <a name="mappings-for-select-strings"></a><span data-ttu-id="6c713-207">Mapeamentos para cadeias de caracteres de seleção</span><span class="sxs-lookup"><span data-stu-id="6c713-207">Mappings for select strings</span></span>
* <span data-ttu-id="6c713-208">**Tipos de Lote .NET**: tipos de API do Lote .NET.</span><span class="sxs-lookup"><span data-stu-id="6c713-208">**Batch .NET types**: Batch .NET API types.</span></span>
* <span data-ttu-id="6c713-209">**Entidades da API REST**: cada página nesta coluna contém uma ou mais tabelas que listam os nomes de propriedade da API REST para o tipo.</span><span class="sxs-lookup"><span data-stu-id="6c713-209">**REST API entities**: Each page in this column contains one or more tables that list the REST API property names for the type.</span></span> <span data-ttu-id="6c713-210">Esses nomes de propriedade são usados ao construir as cadeias de caracteres *select* .</span><span class="sxs-lookup"><span data-stu-id="6c713-210">These property names are used when you construct *select* strings.</span></span> <span data-ttu-id="6c713-211">Você usará esses mesmos nomes de propriedade ao construir uma cadeia de caracteres [ODATADetailLevel.SelectClause][odata_select].</span><span class="sxs-lookup"><span data-stu-id="6c713-211">You will use these same property names when you construct an [ODATADetailLevel.SelectClause][odata_select] string.</span></span>

| <span data-ttu-id="6c713-212">Tipos de Lote .NET</span><span class="sxs-lookup"><span data-stu-id="6c713-212">Batch .NET types</span></span> | <span data-ttu-id="6c713-213">Entidades da API REST</span><span class="sxs-lookup"><span data-stu-id="6c713-213">REST API entities</span></span> |
| --- | --- |
| <span data-ttu-id="6c713-214">[Certificate][net_cert]</span><span class="sxs-lookup"><span data-stu-id="6c713-214">[Certificate][net_cert]</span></span> |<span data-ttu-id="6c713-215">[Obter informações sobre um certificado][rest_get_cert]</span><span class="sxs-lookup"><span data-stu-id="6c713-215">[Get information about a certificate][rest_get_cert]</span></span> |
| <span data-ttu-id="6c713-216">[CloudJob][net_job]</span><span class="sxs-lookup"><span data-stu-id="6c713-216">[CloudJob][net_job]</span></span> |<span data-ttu-id="6c713-217">[Obter informações sobre um trabalho][rest_get_job]</span><span class="sxs-lookup"><span data-stu-id="6c713-217">[Get information about a job][rest_get_job]</span></span> |
| <span data-ttu-id="6c713-218">[CloudJobSchedule][net_schedule]</span><span class="sxs-lookup"><span data-stu-id="6c713-218">[CloudJobSchedule][net_schedule]</span></span> |<span data-ttu-id="6c713-219">[Obter informações sobre um cronograma de trabalho][rest_get_schedule]</span><span class="sxs-lookup"><span data-stu-id="6c713-219">[Get information about a job schedule][rest_get_schedule]</span></span> |
| <span data-ttu-id="6c713-220">[ComputeNode][net_node]</span><span class="sxs-lookup"><span data-stu-id="6c713-220">[ComputeNode][net_node]</span></span> |<span data-ttu-id="6c713-221">[Obter informações sobre um nó][rest_get_node]</span><span class="sxs-lookup"><span data-stu-id="6c713-221">[Get information about a node][rest_get_node]</span></span> |
| <span data-ttu-id="6c713-222">[CloudPool][net_pool]</span><span class="sxs-lookup"><span data-stu-id="6c713-222">[CloudPool][net_pool]</span></span> |<span data-ttu-id="6c713-223">[Obter informações sobre um pool][rest_get_pool]</span><span class="sxs-lookup"><span data-stu-id="6c713-223">[Get information about a pool][rest_get_pool]</span></span> |
| <span data-ttu-id="6c713-224">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="6c713-224">[CloudTask][net_task]</span></span> |<span data-ttu-id="6c713-225">[Obter informações sobre uma tarefa][rest_get_task]</span><span class="sxs-lookup"><span data-stu-id="6c713-225">[Get information about a task][rest_get_task]</span></span> |

## <a name="example-construct-a-filter-string"></a><span data-ttu-id="6c713-226">Exemplo: construir uma cadeia de caracteres filter</span><span class="sxs-lookup"><span data-stu-id="6c713-226">Example: construct a filter string</span></span>
<span data-ttu-id="6c713-227">Ao construir uma cadeia de caracteres filter para [ODATADetailLevel.FilterClause][odata_filter], consulte a tabela acima em “Mapeamentos para cadeias de caracteres filter” para localizar a página da documentação da API REST correspondente à operação de lista que você deseja executar.</span><span class="sxs-lookup"><span data-stu-id="6c713-227">When you construct a filter string for [ODATADetailLevel.FilterClause][odata_filter], consult the table above under "Mappings for filter strings" to find the REST API documentation page that corresponds to the list operation that you wish to perform.</span></span> <span data-ttu-id="6c713-228">Você encontrará as propriedades e os operadores com suporte na primeira tabela com várias linhas nessa página.</span><span class="sxs-lookup"><span data-stu-id="6c713-228">You will find the filterable properties and their supported operators in the first multirow table on that page.</span></span> <span data-ttu-id="6c713-229">Se quiser recuperar todas as tarefas cujo código de saída era diferente de zero, por exemplo, essa linha em [Listar as tarefas associadas a um trabalho][rest_list_tasks] especificará a cadeia de caracteres da propriedade aplicável e os operadores permitidos:</span><span class="sxs-lookup"><span data-stu-id="6c713-229">If you wish to retrieve all tasks whose exit code was nonzero, for example, this row on [List the tasks associated with a job][rest_list_tasks] specifies the applicable property string and allowable operators:</span></span>

| <span data-ttu-id="6c713-230">Propriedade</span><span class="sxs-lookup"><span data-stu-id="6c713-230">Property</span></span> | <span data-ttu-id="6c713-231">Operações permitidas</span><span class="sxs-lookup"><span data-stu-id="6c713-231">Operations allowed</span></span> | <span data-ttu-id="6c713-232">Tipo</span><span class="sxs-lookup"><span data-stu-id="6c713-232">Type</span></span> |
|:--- |:--- |:--- |
| `executionInfo/exitCode` |`eq, ge, gt, le , lt` |`Int` |

<span data-ttu-id="6c713-233">Assim, a cadeia de caracteres de filtro para listar todas as tarefas com um código de saída diferente de zero deve ser:</span><span class="sxs-lookup"><span data-stu-id="6c713-233">Thus, the filter string for listing all tasks with a nonzero exit code would be:</span></span>

`(executionInfo/exitCode lt 0) or (executionInfo/exitCode gt 0)`

## <a name="example-construct-a-select-string"></a><span data-ttu-id="6c713-234">Exemplo: construir uma cadeia de caracteres select</span><span class="sxs-lookup"><span data-stu-id="6c713-234">Example: construct a select string</span></span>
<span data-ttu-id="6c713-235">Para construir um [ODATADetailLevel.SelectClause][odata_select], consulte a tabela acima em “Mapeamentos para as cadeias de caracteres select” e navegue até a página da API REST correspondente ao tipo de entidade listada.</span><span class="sxs-lookup"><span data-stu-id="6c713-235">To construct [ODATADetailLevel.SelectClause][odata_select], consult the table above under "Mappings for select strings" and navigate to the REST API page that corresponds to the type of entity that you are listing.</span></span> <span data-ttu-id="6c713-236">Você encontrará as propriedades selecionáveis e os operadores com suporte na primeira tabela de várias linha nessa página.</span><span class="sxs-lookup"><span data-stu-id="6c713-236">You will find the selectable properties and their supported operators in the first multirow table on that page.</span></span> <span data-ttu-id="6c713-237">Se quiser recuperar apenas a ID e a linha de comando de cada tarefa em uma lista, por exemplo, você encontrará essas linhas na tabela aplicável em [Obter informações sobre uma tarefa][rest_get_task]:</span><span class="sxs-lookup"><span data-stu-id="6c713-237">If you wish to retrieve only the ID and command line for each task in a list, for example, you will find these rows in the applicable table on [Get information about a task][rest_get_task]:</span></span>

| <span data-ttu-id="6c713-238">Propriedade</span><span class="sxs-lookup"><span data-stu-id="6c713-238">Property</span></span> | <span data-ttu-id="6c713-239">Tipo</span><span class="sxs-lookup"><span data-stu-id="6c713-239">Type</span></span> | <span data-ttu-id="6c713-240">Observações</span><span class="sxs-lookup"><span data-stu-id="6c713-240">Notes</span></span> |
|:--- |:--- |:--- |
| `id` |`String` |`The ID of the task.` |
| `commandLine` |`String` |`The command line of the task.` |

<span data-ttu-id="6c713-241">A cadeia de caracteres de seleção para incluir somente a ID e a linha de comando com cada tarefa listada seria:</span><span class="sxs-lookup"><span data-stu-id="6c713-241">The select string for including only the ID and command line with each listed task would then be:</span></span>

`id, commandLine`

## <a name="code-samples"></a><span data-ttu-id="6c713-242">Exemplos de código</span><span class="sxs-lookup"><span data-stu-id="6c713-242">Code samples</span></span>
### <a name="efficient-list-queries-code-sample"></a><span data-ttu-id="6c713-243">Exemplo de código de consultas de lista eficientes</span><span class="sxs-lookup"><span data-stu-id="6c713-243">Efficient list queries code sample</span></span>
<span data-ttu-id="6c713-244">Confira o projeto de exemplo [EfficientListQueries][efficient_query_sample] no GitHub para ver como uma consulta de lista eficaz pode afetar o desempenho de um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6c713-244">Check out the [EfficientListQueries][efficient_query_sample] sample project on GitHub to see how efficient list querying can affect performance in an application.</span></span> <span data-ttu-id="6c713-245">Esse aplicativo de console em C# cria e adiciona um grande número de tarefas a um trabalho.</span><span class="sxs-lookup"><span data-stu-id="6c713-245">This C# console application creates and adds a large number of tasks to a job.</span></span> <span data-ttu-id="6c713-246">Em seguida, ele faz várias chamadas para o método [JobOperations.ListTasks][net_list_tasks] e passa objetos [ODATADetailLevel][odata] que são configurados com valores de propriedade diferentes para variar a quantidade de dados a serem retornados.</span><span class="sxs-lookup"><span data-stu-id="6c713-246">Then, it makes multiple calls to the [JobOperations.ListTasks][net_list_tasks] method and passes [ODATADetailLevel][odata] objects that are configured with different property values to vary the amount of data to be returned.</span></span> <span data-ttu-id="6c713-247">Ele produz uma saída semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="6c713-247">It produces output similar to the following:</span></span>

```
Adding 5000 tasks to job jobEffQuery...
5000 tasks added in 00:00:47.3467587, hit ENTER to query tasks...

4943 tasks retrieved in 00:00:04.3408081 (ExpandClause:  | FilterClause: state eq 'active' | SelectClause: id,state)
0 tasks retrieved in 00:00:00.2662920 (ExpandClause:  | FilterClause: state eq 'running' | SelectClause: id,state)
59 tasks retrieved in 00:00:00.3337760 (ExpandClause:  | FilterClause: state eq 'completed' | SelectClause: id,state)
5000 tasks retrieved in 00:00:04.1429881 (ExpandClause:  | FilterClause:  | SelectClause: id,state)
5000 tasks retrieved in 00:00:15.1016127 (ExpandClause:  | FilterClause:  | SelectClause: id,state,environmentSettings)
5000 tasks retrieved in 00:00:17.0548145 (ExpandClause: stats | FilterClause:  | SelectClause: )

Sample complete, hit ENTER to continue...
```

<span data-ttu-id="6c713-248">Como mostrado nos tempos transcorridos, você pode diminuir muito os tempos de resposta da consulta limitando as propriedades e o número de itens retornados.</span><span class="sxs-lookup"><span data-stu-id="6c713-248">As shown in the elapsed times, you can greatly lower query response times by limiting the properties and the number of items that are returned.</span></span> <span data-ttu-id="6c713-249">Você pode encontrar esse e outros exemplos de projetos no repositório [azure-batch-samples][github_samples] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="6c713-249">You can find this and other sample projects in the [azure-batch-samples][github_samples] repository on GitHub.</span></span>

### <a name="batchmetrics-library-and-code-sample"></a><span data-ttu-id="6c713-250">Biblioteca BatchMetrics e exemplo de código</span><span class="sxs-lookup"><span data-stu-id="6c713-250">BatchMetrics library and code sample</span></span>
<span data-ttu-id="6c713-251">Além do exemplo de código EfficientListQueries acima, você pode encontrar o projeto [BatchMetrics][batch_metrics] no repositório GitHub [azure-batch-samples][github_samples].</span><span class="sxs-lookup"><span data-stu-id="6c713-251">In addition to the EfficientListQueries code sample above, you can find the [BatchMetrics][batch_metrics] project in the [azure-batch-samples][github_samples] GitHub repository.</span></span> <span data-ttu-id="6c713-252">O projeto de exemplo BatchMetrics demonstra como monitorar com eficiência o andamento do trabalho de Lote do Azure usando a API do Lote.</span><span class="sxs-lookup"><span data-stu-id="6c713-252">The BatchMetrics sample project demonstrates how to efficiently monitor Azure Batch job progress using the Batch API.</span></span>

<span data-ttu-id="6c713-253">O exemplo [BatchMetrics][batch_metrics] inclui um projeto da biblioteca de classes .NET que você pode incorporar a seus próprios projetos e um programa de linha de comando simples para treinar e demonstrar o uso da biblioteca.</span><span class="sxs-lookup"><span data-stu-id="6c713-253">The [BatchMetrics][batch_metrics] sample includes a .NET class library project which you can incorporate into your own projects, and a simple command-line program to exercise and demonstrate the use of the library.</span></span>

<span data-ttu-id="6c713-254">O aplicativo de exemplo no projeto demonstra as seguintes operações:</span><span class="sxs-lookup"><span data-stu-id="6c713-254">The sample application within the project demonstrates the following operations:</span></span>

1. <span data-ttu-id="6c713-255">Selecionando atributos específicos para baixar somente as propriedades necessárias</span><span class="sxs-lookup"><span data-stu-id="6c713-255">Selecting specific attributes in order to download only the properties you need</span></span>
2. <span data-ttu-id="6c713-256">Filtrando os tempos de transição do estado para baixar somente as alterações desde a última consulta</span><span class="sxs-lookup"><span data-stu-id="6c713-256">Filtering on state transition times in order to download only changes since the last query</span></span>

<span data-ttu-id="6c713-257">Por exemplo, o método a seguir aparece na biblioteca BatchMetrics.</span><span class="sxs-lookup"><span data-stu-id="6c713-257">For example, the following method appears in the BatchMetrics library.</span></span> <span data-ttu-id="6c713-258">Ele retorna um ODATADetailLevel que especifica que somente as propriedades `id` e `state` devem ser obtidas para as entidades consultadas.</span><span class="sxs-lookup"><span data-stu-id="6c713-258">It returns an ODATADetailLevel that specifies that only the `id` and `state` properties should be obtained for the entities that are queried.</span></span> <span data-ttu-id="6c713-259">Também especifica que apenas as entidades cujo estado foi alterado desde o parâmetro `DateTime` especificado devem ser retornadas.</span><span class="sxs-lookup"><span data-stu-id="6c713-259">It also specifies that only entities whose state has changed since the specified `DateTime` parameter should be returned.</span></span>

```csharp
internal static ODATADetailLevel OnlyChangedAfter(DateTime time)
{
    return new ODATADetailLevel(
        selectClause: "id, state",
        filterClause: string.Format("stateTransitionTime gt DateTime'{0:o}'", time)
    );
}
```

## <a name="next-steps"></a><span data-ttu-id="6c713-260">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6c713-260">Next steps</span></span>
### <a name="parallel-node-tasks"></a><span data-ttu-id="6c713-261">Tarefas paralelas do nó</span><span class="sxs-lookup"><span data-stu-id="6c713-261">Parallel node tasks</span></span>
<span data-ttu-id="6c713-262">[Maximizar o uso de recursos de computação do Lote do Azure com tarefas de nó simultâneas](batch-parallel-node-tasks.md) é outro artigo relacionado ao desempenho de aplicativos do Lote.</span><span class="sxs-lookup"><span data-stu-id="6c713-262">[Maximize Azure Batch compute resource usage with concurrent node tasks](batch-parallel-node-tasks.md) is another article related to Batch application performance.</span></span> <span data-ttu-id="6c713-263">Alguns tipos de cargas de trabalho podem aproveitar a execução de tarefas paralelas nos nós de computação maiores, porém em menor número.</span><span class="sxs-lookup"><span data-stu-id="6c713-263">Some types of workloads can benefit from executing parallel tasks on larger--but fewer--compute nodes.</span></span> <span data-ttu-id="6c713-264">Consulte o [cenário de exemplo](batch-parallel-node-tasks.md#example-scenario) no artigo para obter detalhes sobre esse cenário.</span><span class="sxs-lookup"><span data-stu-id="6c713-264">Check out the [example scenario](batch-parallel-node-tasks.md#example-scenario) in the article for details on such a scenario.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="6c713-265">Fórum do Lote</span><span class="sxs-lookup"><span data-stu-id="6c713-265">Batch Forum</span></span>
<span data-ttu-id="6c713-266">O [Fórum do Lote do Azure][forum] no MSDN é um ótimo lugar para discutir sobre o Lote e fazer perguntas sobre o serviço.</span><span class="sxs-lookup"><span data-stu-id="6c713-266">The [Azure Batch Forum][forum] on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="6c713-267">Acesse diretamente as postagens “fixas” úteis e poste suas dúvidas conforme elas surgirem enquanto você cria suas soluções do Lote.</span><span class="sxs-lookup"><span data-stu-id="6c713-267">Head on over for helpful "sticky" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

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