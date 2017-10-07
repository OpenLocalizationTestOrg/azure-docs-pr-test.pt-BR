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
# <a name="azure-functions-storage-table-bindings"></a>Associações de tabela de armazenamento do Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artigo explica como tooconfigure e o código de armazenamento do Azure tabela associações em funções do Azure. O Azure Functions dá suporte a associações de entrada e saída para tabelas do Armazenamento do Azure.

associação de tabela de armazenamento Olá dá suporte a saudação os seguintes cenários:

* **Ler uma única linha em uma função do C# ou do Node.js** – Defina `partitionKey` e `rowKey`. Olá `filter` e `take` propriedades não são usadas neste cenário.
* **Ler várias linhas em uma função c#** -tempo de execução de funções hello fornece um `IQueryable<T>` toohello tabela do objeto associado. O tipo `T` deve derivar de `TableEntity` ou implementar `ITableEntity`. Olá `partitionKey`, `rowKey`, `filter`, e `take` propriedades não são usadas neste cenário; você pode usar o hello `IQueryable` toodo do objeto de filtragem necessário. 
* **Ler várias linhas em uma função de nó** - defina hello `filter` e `take` propriedades. Não definir `partitionKey` ou `rowKey`.
* **Gravar uma ou mais linhas em uma função c#** -tempo de execução de funções hello fornece um `ICollector<T>` ou `IAsyncCollector<T>` toohello associado de tabela, onde `T` Especifica o esquema de saudação de entidades Olá deseja tooadd. Geralmente, o tipo `T` deriva de `TableEntity` ou implementa `ITableEntity`, mas isso não é obrigatório. Olá `partitionKey`, `rowKey`, `filter`, e `take` propriedades não são usadas neste cenário.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a>Associação de entrada da tabela de armazenamento
Olá associação de entrada de tabela de armazenamento do Azure permite que você toouse uma tabela de armazenamento na sua função. 

Olá função do armazenamento de tabela tooa entrada usa Olá seguintes objetos JSON em Olá `bindings` matriz de function.json:

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

Observe o seguinte hello: 

* Use `partitionKey` e `rowKey` tooread junto uma única entidade. Essas propriedades são opcionais. 
* `connection`deve conter o nome de saudação de uma configuração de aplicativo que contém uma cadeia de caracteres de conexão de armazenamento. No portal do Azure de Olá, Olá editor padrão no hello **integrar** guia configura essa definição de aplicativo para você quando você criar um armazenamento de conta ou seleciona um existente. Você também pode [definir a configuração deste aplicativo manualmente](functions-how-to-use-azure-function-app-settings.md#settings).  

<a name="inputusage"></a>

## <a name="input-usage"></a>Uso de entrada
Funções de C#, você associar toohello entrada tabela (ou mais entidades) usando um parâmetro nomeado na sua assinatura de função, como `<T> <name>`.
Onde `T` é o tipo de dados de saudação que você deseja toodeserialize Olá dados, e `paramName` é Olá nome especificado no hello [associação de entrada](#input). Funções do Node. js, você acessa Olá entrada tabela (ou mais entidades) usando `context.bindings.<name>`.

dados de entrada Hello podem ser desserializados em funções Node. js ou c#. Olá desserializar objetos têm `RowKey` e `PartitionKey` propriedades.

Em c# funções, você também pode associar tooany dos seguintes tipos de saudação e funções hello tentará o tempo de execução muito desserializar usando esse tipo de dados da tabela de saudação:

* Qualquer tipo que implementa `ITableEntity`
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a>Amostra de entrada
Suponha que você tenha Olá function.json, que usa um gatilho de fila tooread uma linha da tabela a seguir. Olá JSON especifica `PartitionKey`  
 `RowKey`. `"rowKey": "{queueTrigger}"`Indica se que essa chave de linha de saudação vem da cadeia de caracteres de mensagem de fila hello.

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

Consulte exemplo específico do idioma hello que lê uma entidade de tabela única.

* [C#](#inputcsharp)
* [F#](#inputfsharp)
* [Node.js](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a>Exemplo de entrada em C# #
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

### <a name="input-sample-in-f"></a>Exemplo de entrada em F# #
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

### <a name="input-sample-in-nodejs"></a>Amostra de entrada no Node.js
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a>Associação de saída da tabela de armazenamento
Olá tabela de armazenamento do Azure saída vinculação permite tabela de armazenamento de tooa toowrite entidades em sua função. 

Olá a saída da tabela de armazenamento para uma função usa Olá seguintes objetos JSON em Olá `bindings` matriz de function.json:

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

Observe o seguinte hello: 

* Use `partitionKey` e `rowKey` toowrite junto uma única entidade. Essas propriedades são opcionais. Você também pode especificar `PartitionKey` e `RowKey` quando você cria Olá objetos de entidade em seu código de função.
* `connection`deve conter o nome de saudação de uma configuração de aplicativo que contém uma cadeia de caracteres de conexão de armazenamento. No portal do Azure de Olá, Olá editor padrão no hello **integrar** guia configura essa definição de aplicativo para você quando você criar um armazenamento de conta ou seleciona um existente. Você também pode [definir a configuração deste aplicativo manualmente](functions-how-to-use-azure-function-app-settings.md#settings). 

<a name="outputusage"></a>

## <a name="output-usage"></a>Uso de saída
Em c# funções, você deve associar toohello saída da tabela usando Olá denominado `out` parâmetro em sua assinatura de função, como `out <T> <name>`, onde `T` é o tipo de dados de saudação que você deseja tooserialize Olá dados, e `paramName` é Olá nome especificado em Olá [associação de saída](#output). Funções do Node. js, você acessa tabela Olá saída usando `context.bindings.<name>`.

Serialize objetos em funções do Node.js ou do C#. Em c# funções, você também pode associar toohello tipos a seguir:

* Qualquer tipo que implementa `ITableEntity`
* `ICollector<T>`(toooutput várias entidades. Consulte a [amostra](#outcsharp).)
* `IAsyncCollector<T>` (versão assíncrona de `ICollector<T>`)
* `CloudTable`(usando Olá SDK de armazenamento do Azure. Consulte a [amostra](#readmulti).)

<a name="outputsample"></a>

## <a name="output-sample"></a>Amostra de saída
a seguir Olá *function.json* e *run.csx* exemplo mostra como toowrite várias entidades de tabela.

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

Consulte Olá específico do idioma exemplo que cria várias entidades de tabela.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Amostra de saída em C# #
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

### <a name="output-sample-in-f"></a>Amostra de saída em F# #
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

### <a name="output-sample-in-nodejs"></a>Amostra de saída no Node.js
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

## <a name="sample-read-multiple-table-entities-in-c"></a>Amostra: ler várias entidades de tabela em C#  #
a seguir Olá *function.json* e exemplo de código c# lê entidades para uma chave de partição que é especificado na mensagem da fila de saudação.

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

Olá código c# adiciona um toohello Referência SDK de armazenamento do Azure para que o tipo de entidade Olá pode derivar de `TableEntity`.

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

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

