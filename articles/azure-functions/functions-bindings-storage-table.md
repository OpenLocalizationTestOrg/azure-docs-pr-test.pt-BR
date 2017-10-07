---
title: "associações de tabela de armazenamento de funções aaaAzure | Microsoft Docs"
description: "Entender como toouse associações de armazenamento do Azure em funções do Azure."
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
ms.openlocfilehash: 90c2a73329139d4ab3504bc0e2c90370133158bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-storage-table-bindings"></a><span data-ttu-id="32440-104">Associações de tabela de armazenamento do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="32440-104">Azure Functions Storage table bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="32440-105">Este artigo explica como tooconfigure e o código de armazenamento do Azure tabela associações em funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="32440-105">This article explains how tooconfigure and code Azure Storage table bindings in Azure Functions.</span></span> <span data-ttu-id="32440-106">O Azure Functions dá suporte a associações de entrada e saída para tabelas do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="32440-106">Azure Functions supports input and output bindings for Azure Storage tables.</span></span>

<span data-ttu-id="32440-107">associação de tabela de armazenamento Olá dá suporte a saudação os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="32440-107">hello Storage table binding supports hello following scenarios:</span></span>

* <span data-ttu-id="32440-108">**Ler uma única linha em uma função do C# ou do Node.js** – Defina `partitionKey` e `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="32440-108">**Read a single row in a C# or Node.js function** - Set `partitionKey` and `rowKey`.</span></span> <span data-ttu-id="32440-109">Olá `filter` e `take` propriedades não são usadas neste cenário.</span><span class="sxs-lookup"><span data-stu-id="32440-109">hello `filter` and `take` properties are not used in this scenario.</span></span>
* <span data-ttu-id="32440-110">**Ler várias linhas em uma função c#** -tempo de execução de funções hello fornece um `IQueryable<T>` toohello tabela do objeto associado.</span><span class="sxs-lookup"><span data-stu-id="32440-110">**Read multiple rows in a C# function** - hello Functions runtime provides an `IQueryable<T>` object bound toohello table.</span></span> <span data-ttu-id="32440-111">O tipo `T` deve derivar de `TableEntity` ou implementar `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="32440-111">Type `T` must derive from `TableEntity` or implement `ITableEntity`.</span></span> <span data-ttu-id="32440-112">Olá `partitionKey`, `rowKey`, `filter`, e `take` propriedades não são usadas neste cenário; você pode usar o hello `IQueryable` toodo do objeto de filtragem necessário.</span><span class="sxs-lookup"><span data-stu-id="32440-112">hello `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario; you can use hello `IQueryable` object toodo any filtering required.</span></span> 
* <span data-ttu-id="32440-113">**Ler várias linhas em uma função de nó** - defina hello `filter` e `take` propriedades.</span><span class="sxs-lookup"><span data-stu-id="32440-113">**Read multiple rows in a Node function** - Set hello `filter` and `take` properties.</span></span> <span data-ttu-id="32440-114">Não definir `partitionKey` ou `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="32440-114">Don't set `partitionKey` or `rowKey`.</span></span>
* <span data-ttu-id="32440-115">**Gravar uma ou mais linhas em uma função c#** -tempo de execução de funções hello fornece um `ICollector<T>` ou `IAsyncCollector<T>` toohello associado de tabela, onde `T` Especifica o esquema de saudação de entidades Olá deseja tooadd.</span><span class="sxs-lookup"><span data-stu-id="32440-115">**Write one or more rows in a C# function** - hello Functions runtime provides an `ICollector<T>` or `IAsyncCollector<T>` bound toohello table, where `T` specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="32440-116">Geralmente, o tipo `T` deriva de `TableEntity` ou implementa `ITableEntity`, mas isso não é obrigatório.</span><span class="sxs-lookup"><span data-stu-id="32440-116">Typically, type `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="32440-117">Olá `partitionKey`, `rowKey`, `filter`, e `take` propriedades não são usadas neste cenário.</span><span class="sxs-lookup"><span data-stu-id="32440-117">hello `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a><span data-ttu-id="32440-118">Associação de entrada da tabela de armazenamento</span><span class="sxs-lookup"><span data-stu-id="32440-118">Storage table input binding</span></span>
<span data-ttu-id="32440-119">Olá associação de entrada de tabela de armazenamento do Azure permite que você toouse uma tabela de armazenamento na sua função.</span><span class="sxs-lookup"><span data-stu-id="32440-119">hello Azure Storage table input binding enables you toouse a storage table in your function.</span></span> 

<span data-ttu-id="32440-120">Olá função do armazenamento de tabela tooa entrada usa Olá seguintes objetos JSON em Olá `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="32440-120">hello Storage table input tooa function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "in",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity tooread - see below>",
    "rowKey": "<RowKey of table entity tooread - see below>",
    "take": "<Maximum number of entities tooread in Node.js - optional>",
    "filter": "<OData filter expression for table input in Node.js - optional>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="32440-121">Observe o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="32440-121">Note hello following:</span></span> 

* <span data-ttu-id="32440-122">Use `partitionKey` e `rowKey` tooread junto uma única entidade.</span><span class="sxs-lookup"><span data-stu-id="32440-122">Use `partitionKey` and `rowKey` together tooread a single entity.</span></span> <span data-ttu-id="32440-123">Essas propriedades são opcionais.</span><span class="sxs-lookup"><span data-stu-id="32440-123">These properties are optional.</span></span> 
* <span data-ttu-id="32440-124">`connection`deve conter o nome de saudação de uma configuração de aplicativo que contém uma cadeia de caracteres de conexão de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="32440-124">`connection` must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="32440-125">No portal do Azure de Olá, Olá editor padrão no hello **integrar** guia configura essa definição de aplicativo para você quando você criar um armazenamento de conta ou seleciona um existente.</span><span class="sxs-lookup"><span data-stu-id="32440-125">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="32440-126">Você também pode [definir a configuração deste aplicativo manualmente](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="32440-126">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>  

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="32440-127">Uso de entrada</span><span class="sxs-lookup"><span data-stu-id="32440-127">Input usage</span></span>
<span data-ttu-id="32440-128">Funções de C#, você associar toohello entrada tabela (ou mais entidades) usando um parâmetro nomeado na sua assinatura de função, como `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="32440-128">In C# functions, you bind toohello input table entity (or entities) by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="32440-129">Onde `T` é o tipo de dados de saudação que você deseja toodeserialize Olá dados, e `paramName` é Olá nome especificado no hello [associação de entrada](#input).</span><span class="sxs-lookup"><span data-stu-id="32440-129">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in hello [input binding](#input).</span></span> <span data-ttu-id="32440-130">Funções do Node. js, você acessa Olá entrada tabela (ou mais entidades) usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="32440-130">In Node.js functions, you access hello input table entity (or entities) using `context.bindings.<name>`.</span></span>

<span data-ttu-id="32440-131">dados de entrada Hello podem ser desserializados em funções Node. js ou c#.</span><span class="sxs-lookup"><span data-stu-id="32440-131">hello input data can be deserialized in Node.js or C# functions.</span></span> <span data-ttu-id="32440-132">Olá desserializar objetos têm `RowKey` e `PartitionKey` propriedades.</span><span class="sxs-lookup"><span data-stu-id="32440-132">hello deserialized objects have `RowKey` and `PartitionKey` properties.</span></span>

<span data-ttu-id="32440-133">Em c# funções, você também pode associar tooany dos seguintes tipos de saudação e funções hello tentará o tempo de execução muito desserializar usando esse tipo de dados da tabela de saudação:</span><span class="sxs-lookup"><span data-stu-id="32440-133">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime will attempt too deserialize hello table data using that type:</span></span>

* <span data-ttu-id="32440-134">Qualquer tipo que implementa `ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="32440-134">Any type that implements `ITableEntity`</span></span>
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="32440-135">Amostra de entrada</span><span class="sxs-lookup"><span data-stu-id="32440-135">Input sample</span></span>
<span data-ttu-id="32440-136">Suponha que você tenha Olá function.json, que usa um gatilho de fila tooread uma linha da tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="32440-136">Supposed you have hello following function.json, which uses a queue trigger tooread a single table row.</span></span> <span data-ttu-id="32440-137">Olá JSON especifica `PartitionKey`  
 `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="32440-137">hello JSON specifies `PartitionKey` 
`RowKey`.</span></span> <span data-ttu-id="32440-138">`"rowKey": "{queueTrigger}"`Indica se que essa chave de linha de saudação vem da cadeia de caracteres de mensagem de fila hello.</span><span class="sxs-lookup"><span data-stu-id="32440-138">`"rowKey": "{queueTrigger}"` indicates that hello row key comes from hello queue message string.</span></span>

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

<span data-ttu-id="32440-139">Consulte exemplo específico do idioma hello que lê uma entidade de tabela única.</span><span class="sxs-lookup"><span data-stu-id="32440-139">See hello language-specific sample that reads a single table entity.</span></span>

* [<span data-ttu-id="32440-140">C#</span><span class="sxs-lookup"><span data-stu-id="32440-140">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="32440-141">F#</span><span class="sxs-lookup"><span data-stu-id="32440-141">F#</span></span>](#inputfsharp)
* [<span data-ttu-id="32440-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="32440-142">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="32440-143">Exemplo de entrada em C#</span><span class="sxs-lookup"><span data-stu-id="32440-143">Input sample in C#</span></span> #
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

### <a name="input-sample-in-f"></a><span data-ttu-id="32440-144">Exemplo de entrada em F#</span><span class="sxs-lookup"><span data-stu-id="32440-144">Input sample in F#</span></span> #
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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="32440-145">Amostra de entrada no Node.js</span><span class="sxs-lookup"><span data-stu-id="32440-145">Input sample in Node.js</span></span>
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a><span data-ttu-id="32440-146">Associação de saída da tabela de armazenamento</span><span class="sxs-lookup"><span data-stu-id="32440-146">Storage table output binding</span></span>
<span data-ttu-id="32440-147">Olá tabela de armazenamento do Azure saída vinculação permite tabela de armazenamento de tooa toowrite entidades em sua função.</span><span class="sxs-lookup"><span data-stu-id="32440-147">hello Azure Storage table output binding enables you toowrite entities tooa Storage table in your function.</span></span> 

<span data-ttu-id="32440-148">Olá a saída da tabela de armazenamento para uma função usa Olá seguintes objetos JSON em Olá `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="32440-148">hello Storage table output for a function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "out",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity toowrite - see below>",
    "rowKey": "<RowKey of table entity toowrite - see below>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="32440-149">Observe o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="32440-149">Note hello following:</span></span> 

* <span data-ttu-id="32440-150">Use `partitionKey` e `rowKey` toowrite junto uma única entidade.</span><span class="sxs-lookup"><span data-stu-id="32440-150">Use `partitionKey` and `rowKey` together toowrite a single entity.</span></span> <span data-ttu-id="32440-151">Essas propriedades são opcionais.</span><span class="sxs-lookup"><span data-stu-id="32440-151">These properties are optional.</span></span> <span data-ttu-id="32440-152">Você também pode especificar `PartitionKey` e `RowKey` quando você cria Olá objetos de entidade em seu código de função.</span><span class="sxs-lookup"><span data-stu-id="32440-152">You can also specify `PartitionKey` and `RowKey` when you create hello entity objects in your function code.</span></span>
* <span data-ttu-id="32440-153">`connection`deve conter o nome de saudação de uma configuração de aplicativo que contém uma cadeia de caracteres de conexão de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="32440-153">`connection` must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="32440-154">No portal do Azure de Olá, Olá editor padrão no hello **integrar** guia configura essa definição de aplicativo para você quando você criar um armazenamento de conta ou seleciona um existente.</span><span class="sxs-lookup"><span data-stu-id="32440-154">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="32440-155">Você também pode [definir a configuração deste aplicativo manualmente](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="32440-155">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span> 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="32440-156">Uso de saída</span><span class="sxs-lookup"><span data-stu-id="32440-156">Output usage</span></span>
<span data-ttu-id="32440-157">Em c# funções, você deve associar toohello saída da tabela usando Olá denominado `out` parâmetro em sua assinatura de função, como `out <T> <name>`, onde `T` é o tipo de dados de saudação que você deseja tooserialize Olá dados, e `paramName` é Olá nome especificado em Olá [associação de saída](#output).</span><span class="sxs-lookup"><span data-stu-id="32440-157">In C# functions, you bind toohello table output by using hello named `out` parameter in your function signature, like `out <T> <name>`, where `T` is hello data type that you want tooserialize hello data into, and `paramName` is hello name you specified in hello [output binding](#output).</span></span> <span data-ttu-id="32440-158">Funções do Node. js, você acessa tabela Olá saída usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="32440-158">In Node.js functions, you access hello table output using `context.bindings.<name>`.</span></span>

<span data-ttu-id="32440-159">Serialize objetos em funções do Node.js ou do C#.</span><span class="sxs-lookup"><span data-stu-id="32440-159">You can serialize objects in Node.js or C# functions.</span></span> <span data-ttu-id="32440-160">Em c# funções, você também pode associar toohello tipos a seguir:</span><span class="sxs-lookup"><span data-stu-id="32440-160">In C# functions, you can also bind toohello following types:</span></span>

* <span data-ttu-id="32440-161">Qualquer tipo que implementa `ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="32440-161">Any type that implements `ITableEntity`</span></span>
* <span data-ttu-id="32440-162">`ICollector<T>`(toooutput várias entidades.</span><span class="sxs-lookup"><span data-stu-id="32440-162">`ICollector<T>` (toooutput multiple entities.</span></span> <span data-ttu-id="32440-163">Consulte a [amostra](#outcsharp).)</span><span class="sxs-lookup"><span data-stu-id="32440-163">See [sample](#outcsharp).)</span></span>
* <span data-ttu-id="32440-164">`IAsyncCollector<T>` (versão assíncrona de `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="32440-164">`IAsyncCollector<T>` (async version of `ICollector<T>`)</span></span>
* <span data-ttu-id="32440-165">`CloudTable`(usando Olá SDK de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="32440-165">`CloudTable` (using hello Azure Storage SDK.</span></span> <span data-ttu-id="32440-166">Consulte a [amostra](#readmulti).)</span><span class="sxs-lookup"><span data-stu-id="32440-166">See [sample](#readmulti).)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="32440-167">Amostra de saída</span><span class="sxs-lookup"><span data-stu-id="32440-167">Output sample</span></span>
<span data-ttu-id="32440-168">a seguir Olá *function.json* e *run.csx* exemplo mostra como toowrite várias entidades de tabela.</span><span class="sxs-lookup"><span data-stu-id="32440-168">hello following *function.json* and *run.csx* example shows how toowrite multiple table entities.</span></span>

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

<span data-ttu-id="32440-169">Consulte Olá específico do idioma exemplo que cria várias entidades de tabela.</span><span class="sxs-lookup"><span data-stu-id="32440-169">See hello language-specific sample that creates multiple table entities.</span></span>

* [<span data-ttu-id="32440-170">C#</span><span class="sxs-lookup"><span data-stu-id="32440-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="32440-171">F#</span><span class="sxs-lookup"><span data-stu-id="32440-171">F#</span></span>](#outfsharp)
* [<span data-ttu-id="32440-172">Node.js</span><span class="sxs-lookup"><span data-stu-id="32440-172">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="32440-173">Amostra de saída em C#</span><span class="sxs-lookup"><span data-stu-id="32440-173">Output sample in C#</span></span> #
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

### <a name="output-sample-in-f"></a><span data-ttu-id="32440-174">Amostra de saída em F#</span><span class="sxs-lookup"><span data-stu-id="32440-174">Output sample in F#</span></span> #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(input: string, tableBinding: ICollector<Person>, log: TraceWriter) =
    for i = 1 too10 do
        log.Info(sprintf "Adding Person entity %d" i)
        tableBinding.Add(
            { PartitionKey = "Test"
              RowKey = i.ToString()
              Name = "Name" + i.ToString() })
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="32440-175">Amostra de saída no Node.js</span><span class="sxs-lookup"><span data-stu-id="32440-175">Output sample in Node.js</span></span>
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

## <a name="sample-read-multiple-table-entities-in-c"></a><span data-ttu-id="32440-176">Amostra: ler várias entidades de tabela em C#</span><span class="sxs-lookup"><span data-stu-id="32440-176">Sample: Read multiple table entities in C#</span></span>  #
<span data-ttu-id="32440-177">a seguir Olá *function.json* e exemplo de código c# lê entidades para uma chave de partição que é especificado na mensagem da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="32440-177">hello following *function.json* and C# code example reads entities for a partition key that is specified in hello queue message.</span></span>

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

<span data-ttu-id="32440-178">Olá código c# adiciona um toohello Referência SDK de armazenamento do Azure para que o tipo de entidade Olá pode derivar de `TableEntity`.</span><span class="sxs-lookup"><span data-stu-id="32440-178">hello C# code adds a reference toohello Azure Storage SDK so that hello entity type can derive from `TableEntity`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="32440-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="32440-179">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

