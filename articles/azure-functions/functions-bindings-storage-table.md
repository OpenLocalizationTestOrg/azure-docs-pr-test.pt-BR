---
title: "Associações de tabela de armazenamento do Azure Functions | Microsoft Docs"
description: "Entenda como usar as associações do Armazenamento do Azure no Azure Functions."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, funções, processamento de eventos, computação dinâmica, arquitetura sem servidor"
ms.assetid: 65b3437e-2571-4d3f-a996-61a74b50a1c2
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/28/2016
ms.author: chrande
ms.openlocfilehash: bb01be3ee044f60376e0c9c2de7b3dd34f3b7aca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-storage-table-bindings"></a><span data-ttu-id="a0862-104">Associações de tabela de armazenamento do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="a0862-104">Azure Functions Storage table bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="a0862-105">Esse artigo explica como configurar e codificar associações de tabela do Armazenamento do Azure no Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="a0862-105">This article explains how to configure and code Azure Storage table bindings in Azure Functions.</span></span> <span data-ttu-id="a0862-106">O Azure Functions dá suporte a associações de entrada e saída para tabelas do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0862-106">Azure Functions supports input and output bindings for Azure Storage tables.</span></span>

<span data-ttu-id="a0862-107">A associação da tabela de Armazenamento dá suporte aos seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="a0862-107">The Storage table binding supports the following scenarios:</span></span>

* <span data-ttu-id="a0862-108">**Ler uma única linha em uma função do C# ou do Node.js** – Defina `partitionKey` e `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="a0862-108">**Read a single row in a C# or Node.js function** - Set `partitionKey` and `rowKey`.</span></span> <span data-ttu-id="a0862-109">As propriedades `filter` e `take` não são usadas neste cenário.</span><span class="sxs-lookup"><span data-stu-id="a0862-109">The `filter` and `take` properties are not used in this scenario.</span></span>
* <span data-ttu-id="a0862-110">**Ler várias linhas em uma função do C#** – O tempo de execução do Functions fornece um objeto `IQueryable<T>` associado à tabela.</span><span class="sxs-lookup"><span data-stu-id="a0862-110">**Read multiple rows in a C# function** - The Functions runtime provides an `IQueryable<T>` object bound to the table.</span></span> <span data-ttu-id="a0862-111">O tipo `T` deve derivar de `TableEntity` ou implementar `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="a0862-111">Type `T` must derive from `TableEntity` or implement `ITableEntity`.</span></span> <span data-ttu-id="a0862-112">As propriedades `partitionKey`, `rowKey`, `filter` e `take` não são usadas neste cenário; você pode usar o objeto `IQueryable` para fazer qualquer filtragem necessária.</span><span class="sxs-lookup"><span data-stu-id="a0862-112">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario; you can use the `IQueryable` object to do any filtering required.</span></span> 
* <span data-ttu-id="a0862-113">**Ler várias linhas em uma função do Node** – Defina as propriedades `filter` e `take`.</span><span class="sxs-lookup"><span data-stu-id="a0862-113">**Read multiple rows in a Node function** - Set the `filter` and `take` properties.</span></span> <span data-ttu-id="a0862-114">Não definir `partitionKey` ou `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="a0862-114">Don't set `partitionKey` or `rowKey`.</span></span>
* <span data-ttu-id="a0862-115">**Escrever uma ou mais linhas em uma função do C#** – O tempo de execução do Functions oferece uma associação `ICollector<T>` ou `IAsyncCollector<T>` à tabela, em que `T` especifica o esquema das entidades que você deseja adicionar.</span><span class="sxs-lookup"><span data-stu-id="a0862-115">**Write one or more rows in a C# function** - The Functions runtime provides an `ICollector<T>` or `IAsyncCollector<T>` bound to the table, where `T` specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="a0862-116">Geralmente, o tipo `T` deriva de `TableEntity` ou implementa `ITableEntity`, mas isso não é obrigatório.</span><span class="sxs-lookup"><span data-stu-id="a0862-116">Typically, type `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="a0862-117">As propriedades `partitionKey`, `rowKey`, `filter` e `take` não são usadas neste cenário.</span><span class="sxs-lookup"><span data-stu-id="a0862-117">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a><span data-ttu-id="a0862-118">Associação de entrada da tabela de armazenamento</span><span class="sxs-lookup"><span data-stu-id="a0862-118">Storage table input binding</span></span>
<span data-ttu-id="a0862-119">A associação de entrada da tabela de Armazenamento do Azure permite usar uma tabela de armazenamento na função.</span><span class="sxs-lookup"><span data-stu-id="a0862-119">The Azure Storage table input binding enables you to use a storage table in your function.</span></span> 

<span data-ttu-id="a0862-120">A entrada da tabela de Armazenamento de uma função usa os seguintes objetos JSON na matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="a0862-120">The Storage table input to a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "in",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity to read - see below>",
    "rowKey": "<RowKey of table entity to read - see below>",
    "take": "<Maximum number of entities to read in Node.js - optional>",
    "filter": "<OData filter expression for table input in Node.js - optional>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="a0862-121">Observe o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a0862-121">Note the following:</span></span> 

* <span data-ttu-id="a0862-122">Use `partitionKey` e `rowKey` juntos para ler uma única entidade.</span><span class="sxs-lookup"><span data-stu-id="a0862-122">Use `partitionKey` and `rowKey` together to read a single entity.</span></span> <span data-ttu-id="a0862-123">Essas propriedades são opcionais.</span><span class="sxs-lookup"><span data-stu-id="a0862-123">These properties are optional.</span></span> 
* <span data-ttu-id="a0862-124">`connection` deve conter o nome de uma configuração de aplicativo que contém uma cadeia de conexão de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a0862-124">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="a0862-125">No portal do Azure, o editor padrão da guia **Integrar** define essa configuração de aplicativo para você quando você cria uma conta de Armazenamento ou seleciona uma conta existente.</span><span class="sxs-lookup"><span data-stu-id="a0862-125">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="a0862-126">Você também pode [definir a configuração deste aplicativo manualmente](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="a0862-126">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>  

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="a0862-127">Uso de entrada</span><span class="sxs-lookup"><span data-stu-id="a0862-127">Input usage</span></span>
<span data-ttu-id="a0862-128">Em funções do C#, você associa à entidade (ou entidades) de tabela de entrada usando um parâmetro nomeado na assinatura da função, como `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="a0862-128">In C# functions, you bind to the input table entity (or entities) by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="a0862-129">Em que `T` é o tipo de dados no qual você deseja desserializar os dados e `paramName` é o nome especificado na [associação de entrada](#input).</span><span class="sxs-lookup"><span data-stu-id="a0862-129">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span></span> <span data-ttu-id="a0862-130">Em funções do Node.js, você acessa a entidade (ou entidades) de tabela de entrada usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="a0862-130">In Node.js functions, you access the input table entity (or entities) using `context.bindings.<name>`.</span></span>

<span data-ttu-id="a0862-131">Os dados de entrada podem ser desserializados em funções do Node.js ou do C#.</span><span class="sxs-lookup"><span data-stu-id="a0862-131">The input data can be deserialized in Node.js or C# functions.</span></span> <span data-ttu-id="a0862-132">Os objetos desserializados têm propriedades `RowKey` e `PartitionKey`.</span><span class="sxs-lookup"><span data-stu-id="a0862-132">The deserialized objects have `RowKey` and `PartitionKey` properties.</span></span>

<span data-ttu-id="a0862-133">Em funções do C#, você também pode associar a qualquer um dos seguintes tipos, e o tempo de execução do Functions tentará desserializar os dados da tabela usando esse tipo:</span><span class="sxs-lookup"><span data-stu-id="a0862-133">In C# functions, you can also bind to any of the following types, and the Functions runtime will attempt to deserialize the table data using that type:</span></span>

* <span data-ttu-id="a0862-134">Qualquer tipo que implementa `ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="a0862-134">Any type that implements `ITableEntity`</span></span>
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="a0862-135">Amostra de entrada</span><span class="sxs-lookup"><span data-stu-id="a0862-135">Input sample</span></span>
<span data-ttu-id="a0862-136">Suponha que você tem o function.json a seguir, que usa um gatilho da fila para ler uma única linha da tabela.</span><span class="sxs-lookup"><span data-stu-id="a0862-136">Supposed you have the following function.json, which uses a queue trigger to read a single table row.</span></span> <span data-ttu-id="a0862-137">O JSON especifica `PartitionKey` 
`RowKey`.</span><span class="sxs-lookup"><span data-stu-id="a0862-137">The JSON specifies `PartitionKey` 
`RowKey`.</span></span> <span data-ttu-id="a0862-138">`"rowKey": "{queueTrigger}"` indica que a chave de linha foi obtida da cadeia de caracteres da mensagem da fila.</span><span class="sxs-lookup"><span data-stu-id="a0862-138">`"rowKey": "{queueTrigger}"` indicates that the row key comes from the queue message string.</span></span>

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "personEntity",
      "type": "table",
      "tableName": "Person",
      "partitionKey": "Test",
      "rowKey": "{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="a0862-139">Consulte a amostra específica da linguagem que lê uma única entidade de tabela.</span><span class="sxs-lookup"><span data-stu-id="a0862-139">See the language-specific sample that reads a single table entity.</span></span>

* [<span data-ttu-id="a0862-140">C#</span><span class="sxs-lookup"><span data-stu-id="a0862-140">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="a0862-141">F#</span><span class="sxs-lookup"><span data-stu-id="a0862-141">F#</span></span>](#inputfsharp)
* [<span data-ttu-id="a0862-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="a0862-142">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="a0862-143">Exemplo de entrada em C#</span><span class="sxs-lookup"><span data-stu-id="a0862-143">Input sample in C#</span></span> #
```csharp
public static void Run(string myQueueItem, Person personEntity, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    log.Info($"Name in Person entity: {personEntity.Name}");
}

public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
}
```

<a name="inputfsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="a0862-144">Exemplo de entrada em F#</span><span class="sxs-lookup"><span data-stu-id="a0862-144">Input sample in F#</span></span> #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(myQueueItem: string, personEntity: Person) =
    log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
    log.Info(sprintf "Name in Person entity: %s" personEntity.Name)
```

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="a0862-145">Amostra de entrada no Node.js</span><span class="sxs-lookup"><span data-stu-id="a0862-145">Input sample in Node.js</span></span>
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a><span data-ttu-id="a0862-146">Associação de saída da tabela de armazenamento</span><span class="sxs-lookup"><span data-stu-id="a0862-146">Storage table output binding</span></span>
<span data-ttu-id="a0862-147">A associação de saída da tabela de Armazenamento do Azure permite gravar entidades em uma tabela de Armazenamento na função.</span><span class="sxs-lookup"><span data-stu-id="a0862-147">The Azure Storage table output binding enables you to write entities to a Storage table in your function.</span></span> 

<span data-ttu-id="a0862-148">A saída da tabela de Armazenamento de uma função usa os seguintes objetos JSON na matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="a0862-148">The Storage table output for a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "out",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity to write - see below>",
    "rowKey": "<RowKey of table entity to write - see below>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="a0862-149">Observe o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a0862-149">Note the following:</span></span> 

* <span data-ttu-id="a0862-150">Use `partitionKey` e `rowKey` juntos para gravar uma única entidade.</span><span class="sxs-lookup"><span data-stu-id="a0862-150">Use `partitionKey` and `rowKey` together to write a single entity.</span></span> <span data-ttu-id="a0862-151">Essas propriedades são opcionais.</span><span class="sxs-lookup"><span data-stu-id="a0862-151">These properties are optional.</span></span> <span data-ttu-id="a0862-152">Também especifique `PartitionKey` e `RowKey` ao criar os objetos de entidade no código da função.</span><span class="sxs-lookup"><span data-stu-id="a0862-152">You can also specify `PartitionKey` and `RowKey` when you create the entity objects in your function code.</span></span>
* <span data-ttu-id="a0862-153">`connection` deve conter o nome de uma configuração de aplicativo que contém uma cadeia de conexão de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a0862-153">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="a0862-154">No portal do Azure, o editor padrão da guia **Integrar** define essa configuração de aplicativo para você quando você cria uma conta de Armazenamento ou seleciona uma conta existente.</span><span class="sxs-lookup"><span data-stu-id="a0862-154">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="a0862-155">Você também pode [definir a configuração deste aplicativo manualmente](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="a0862-155">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span> 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="a0862-156">Uso de saída</span><span class="sxs-lookup"><span data-stu-id="a0862-156">Output usage</span></span>
<span data-ttu-id="a0862-157">Em funções do C#, você associa à saída de tabela usando o parâmetro `out` nomeado na assinatura da função, como `out <T> <name>`, em que `T` é o tipo de dados no qual você deseja serializar os dados, e `paramName` é o nome especificado na [associação de saída](#output).</span><span class="sxs-lookup"><span data-stu-id="a0862-157">In C# functions, you bind to the table output by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span></span> <span data-ttu-id="a0862-158">Em funções do Node.js, você acessa a tabela de saída usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="a0862-158">In Node.js functions, you access the table output using `context.bindings.<name>`.</span></span>

<span data-ttu-id="a0862-159">Serialize objetos em funções do Node.js ou do C#.</span><span class="sxs-lookup"><span data-stu-id="a0862-159">You can serialize objects in Node.js or C# functions.</span></span> <span data-ttu-id="a0862-160">Em funções do C#, também é possível associar aos seguintes tipos:</span><span class="sxs-lookup"><span data-stu-id="a0862-160">In C# functions, you can also bind to the following types:</span></span>

* <span data-ttu-id="a0862-161">Qualquer tipo que implementa `ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="a0862-161">Any type that implements `ITableEntity`</span></span>
* <span data-ttu-id="a0862-162">`ICollector<T>` (para gerar várias entidades.</span><span class="sxs-lookup"><span data-stu-id="a0862-162">`ICollector<T>` (to output multiple entities.</span></span> <span data-ttu-id="a0862-163">Consulte a [amostra](#outcsharp).)</span><span class="sxs-lookup"><span data-stu-id="a0862-163">See [sample](#outcsharp).)</span></span>
* <span data-ttu-id="a0862-164">`IAsyncCollector<T>` (versão assíncrona de `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="a0862-164">`IAsyncCollector<T>` (async version of `ICollector<T>`)</span></span>
* <span data-ttu-id="a0862-165">`CloudTable` (usando o SDK do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0862-165">`CloudTable` (using the Azure Storage SDK.</span></span> <span data-ttu-id="a0862-166">Consulte a [amostra](#readmulti).)</span><span class="sxs-lookup"><span data-stu-id="a0862-166">See [sample](#readmulti).)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="a0862-167">Amostra de saída</span><span class="sxs-lookup"><span data-stu-id="a0862-167">Output sample</span></span>
<span data-ttu-id="a0862-168">O exemplo de *function.json* e *run.csx* a seguir mostra como gravar várias entidades de tabela.</span><span class="sxs-lookup"><span data-stu-id="a0862-168">The following *function.json* and *run.csx* example shows how to write multiple table entities.</span></span>

```json
{
  "bindings": [
    {
      "name": "input",
      "type": "manualTrigger",
      "direction": "in"
    },
    {
      "tableName": "Person",
      "connection": "MyStorageConnection",
      "name": "tableBinding",
      "type": "table",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="a0862-169">Consulte a amostra específica da linguagem que cria várias entidades de tabela.</span><span class="sxs-lookup"><span data-stu-id="a0862-169">See the language-specific sample that creates multiple table entities.</span></span>

* [<span data-ttu-id="a0862-170">C#</span><span class="sxs-lookup"><span data-stu-id="a0862-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="a0862-171">F#</span><span class="sxs-lookup"><span data-stu-id="a0862-171">F#</span></span>](#outfsharp)
* [<span data-ttu-id="a0862-172">Node.js</span><span class="sxs-lookup"><span data-stu-id="a0862-172">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="a0862-173">Amostra de saída em C#</span><span class="sxs-lookup"><span data-stu-id="a0862-173">Output sample in C#</span></span> #
```csharp
public static void Run(string input, ICollector<Person> tableBinding, TraceWriter log)
{
    for (int i = 1; i < 10; i++)
        {
            log.Info($"Adding Person entity {i}");
            tableBinding.Add(
                new Person() { 
                    PartitionKey = "Test", 
                    RowKey = i.ToString(), 
                    Name = "Name" + i.ToString() }
                );
        }

}

public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
}

```
<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="a0862-174">Amostra de saída em F#</span><span class="sxs-lookup"><span data-stu-id="a0862-174">Output sample in F#</span></span> #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(input: string, tableBinding: ICollector<Person>, log: TraceWriter) =
    for i = 1 to 10 do
        log.Info(sprintf "Adding Person entity %d" i)
        tableBinding.Add(
            { PartitionKey = "Test"
              RowKey = i.ToString()
              Name = "Name" + i.ToString() })
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="a0862-175">Amostra de saída no Node.js</span><span class="sxs-lookup"><span data-stu-id="a0862-175">Output sample in Node.js</span></span>
```javascript
module.exports = function (context) {

    context.bindings.tableBinding = [];

    for (var i = 1; i < 10; i++) {
        context.bindings.tableBinding.push({
            PartitionKey: "Test",
            RowKey: i.toString(),
            Name: "Name " + i
        });
    }
    
    context.done();
};
```

<a name="readmulti"></a>

## <a name="sample-read-multiple-table-entities-in-c"></a><span data-ttu-id="a0862-176">Amostra: ler várias entidades de tabela em C#</span><span class="sxs-lookup"><span data-stu-id="a0862-176">Sample: Read multiple table entities in C#</span></span>  #
<span data-ttu-id="a0862-177">O exemplo de código *function.json* e C# a seguir lê entidades para uma chave de partição especificada na mensagem de fila.</span><span class="sxs-lookup"><span data-stu-id="a0862-177">The following *function.json* and C# code example reads entities for a partition key that is specified in the queue message.</span></span>

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "tableBinding",
      "type": "table",
      "connection": "MyStorageConnection",
      "tableName": "Person",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="a0862-178">O código C# adiciona uma referência ao SDK de Armazenamento do Azure para que o tipo de entidade possa derivar de `TableEntity`.</span><span class="sxs-lookup"><span data-stu-id="a0862-178">The C# code adds a reference to the Azure Storage SDK so that the entity type can derive from `TableEntity`.</span></span>

```csharp
#r "Microsoft.WindowsAzure.Storage"
using Microsoft.WindowsAzure.Storage.Table;

public static void Run(string myQueueItem, IQueryable<Person> tableBinding, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    foreach (Person person in tableBinding.Where(p => p.PartitionKey == myQueueItem).ToList())
    {
        log.Info($"Name: {person.Name}");
    }
}

public class Person : TableEntity
{
    public string Name { get; set; }
}
```

## <a name="next-steps"></a><span data-ttu-id="a0862-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a0862-179">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

