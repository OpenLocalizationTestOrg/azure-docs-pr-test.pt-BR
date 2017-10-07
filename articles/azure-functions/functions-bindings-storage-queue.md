---
title: "associações de armazenamento de fila de funções aaaAzure | Microsoft Docs"
description: "Entenda como dispara toouse armazenamento do Azure e associações em funções do Azure."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, funções, processamento de eventos, computação dinâmica, arquitetura sem servidor"
ms.assetid: 4e6a837d-e64f-45a0-87b7-aa02688a75f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: glenga
ms.openlocfilehash: 438b4f63e823149072c86fdefa7e15bfd2a2c4df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-queue-storage-bindings"></a>Associações de Armazenamento de Filas do Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artigo descreve como tooconfigure e o código de associações de armazenamento de fila do Azure em funções do Azure. O Azure Functions dá suporte a associações de gatilho e de saída para filas do Azure. Para os recursos que estão disponíveis em todas as associações, veja [Gatilhos e conceitos de associações do Azure Functions](functions-triggers-bindings.md).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a>Gatilho de armazenamento de filas
gatilho de armazenamento de fila do Azure Olá permite toomonitor um armazenamento de fila para novas mensagens e reage toothem. 

Definir um gatilho de fila usando Olá **integrar** no portal de funções hello. Olá, portal cria Olá após a definição no hello **associações** seção *function.json*:

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "queueName": "<Name of queue toopoll>",
    "connection":"<Name of app setting - see below>"
}
```

* Olá `connection` propriedade deve conter o nome de saudação de uma configuração de aplicativo que contém uma cadeia de caracteres de conexão de armazenamento. No portal do Azure de Olá, Olá editor padrão no hello **integrar** guia configura essa definição de aplicativo para você quando você seleciona uma conta de armazenamento.

Configurações adicionais podem ser fornecidas em um [host.json arquivo](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther ajustar gatilhos de armazenamento de fila. Por exemplo, você pode alterar o intervalo de sondagem de fila de saudação em host.json.

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a>Usando um gatilho de fila
Em funções do Node. js, acessar Olá fila dados usando `context.bindings.<name>`.


Em funções do .NET, acessar a carga de fila hello usando um parâmetro de método como `CloudQueueMessage paramName`. Aqui, `paramName` é Olá valor especificado em Olá [configuração do disparador](#trigger). mensagem de saudação do fila pode ser desserializado tooany dos seguintes tipos de saudação:

* Objeto POCO. Use se a carga de fila de saudação é um objeto JSON. tempo de execução de funções Hello desserializa carga Olá no objeto POCO hello. 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a>Metadados de gatilho de fila
gatilho de fila Olá fornece várias propriedades de metadados. Essas propriedades podem ser usadas como parte de expressões de associação em outras associações ou como parâmetros em seu código. valores de saudação têm Olá mesma semântica [ `CloudQueueMessage` ].

* **QueueTrigger** – conteúdo da fila (se for uma cadeia de caracteres válida)
* **DequeueCount** – Tipo `int`. Olá o número de vezes que esta mensagem foi removida da fila.
* **ExpirationTime** – Tipo `DateTimeOffset?`. tempo de saudação essa mensagem de saudação expira.
* **Id** – Tipo `string`. ID da mensagem da fila.
* **InsertionTime** – Tipo `DateTimeOffset?`. tempo de saudação essa mensagem de saudação foi adicionada toohello fila.
* **NextVisibleTime** – Tipo `DateTimeOffset?`. tempo de saudação essa mensagem de saudação estará visível.
* **PopReceipt** – Tipo `string`. recebimento de mensagem de saudação pop.

Consulte como toouse Olá metadados de fila no [exemplo de gatilho](#triggersample).

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Exemplo de gatilho
Suponha que você tenha Olá function.json que define um gatilho de fila a seguir:

```json
{
    "disabled": false,
    "bindings": [
        {
            "type": "queueTrigger",
            "direction": "in",
            "name": "myQueueItem",
            "queueName": "myqueue-items",
            "connection":"MyStorageConnectionString"
        }
    ]
}
```

Consulte Olá específico do idioma exemplo que recupera e metadados de fila de logs.

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Exemplo de gatilho em C# #
```csharp
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Queue;
using System;

public static void Run(CloudQueueMessage myQueueItem, 
    DateTimeOffset expirationTime, 
    DateTimeOffset insertionTime, 
    DateTimeOffset nextVisibleTime,
    string queueTrigger,
    string id,
    string popReceipt,
    int dequeueCount,
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem.AsString}\n" +
        $"queueTrigger={queueTrigger}\n" +
        $"expirationTime={expirationTime}\n" +
        $"insertionTime={insertionTime}\n" +
        $"nextVisibleTime={nextVisibleTime}\n" +
        $"id={id}\n" +
        $"popReceipt={popReceipt}\n" + 
        $"dequeueCount={dequeueCount}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger sample in F# ## 
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Exemplo de gatilho em Node.js

```javascript
module.exports = function (context) {
    context.log('Node.js queue trigger function processed work item', context.bindings.myQueueItem);
    context.log('queueTrigger =', context.bindingData.queueTrigger);
    context.log('expirationTime =', context.bindingData.expirationTime);
    context.log('insertionTime =', context.bindingData.insertionTime);
    context.log('nextVisibleTime =', context.bindingData.nextVisibleTime);
    context.log('id=', context.bindingData.id);
    context.log('popReceipt =', context.bindingData.popReceipt);
    context.log('dequeueCount =', context.bindingData.dequeueCount);
    context.done();
};
```

### <a name="handling-poison-queue-messages"></a>Tratamento de mensagens suspeitas na fila
Quando uma função de gatilho de fila falha, funções do Azure repete essa função backup toofive vezes para uma mensagem de determinada fila, incluindo Olá primeiro tente. Se todas as cinco tentativas falharem, tempo de execução de funções hello adiciona uma mensagem tooa fila de armazenamento denominado  *&lt;originalqueuename >-suspeitas*. Você pode escrever uma função tooprocess mensagens da fila de suspeitas Olá registrá-los ou enviar uma notificação que atenção manual é necessária. 

mensagens suspeitas toohandle verificar manualmente, Olá `dequeueCount` de mensagem da fila de saudação (consulte [metadados de gatilho de fila](#meta)).

<a name="output"></a>

## <a name="queue-storage-output-binding"></a>Associação de saída de armazenamento de filas
Olá armazenamento de fila do Azure associação permite que a fila tooa toowrite mensagens de saída. 

Definir uma fila de associação de saída usando Olá **integrar** no portal de funções hello. Olá, portal cria Olá após a definição no hello **associações** seção *function.json*:

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<hello name used tooidentify hello trigger data in your code>",
   "queueName": "<Name of queue toowrite to>",
   "connection":"<Name of app setting - see below>"
}
```

* Olá `connection` propriedade deve conter o nome de saudação de uma configuração de aplicativo que contém uma cadeia de caracteres de conexão de armazenamento. No portal do Azure de Olá, Olá editor padrão no hello **integrar** guia configura essa definição de aplicativo para você quando você seleciona uma conta de armazenamento.

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a>Usando uma associação de saída da fila
Em funções do Node. js, você acessar a fila de saída de hello usando `context.bindings.<name>`.

Em funções do .NET, você pode dar saída tooany de saudação tipos a seguir. Quando há um parâmetro de tipo `T`, `T` deve ser um dos tipos de saída de hello com suporte, como `string` ou um POCO.

* `out T` (serializado como JSON)
* `out string`
* `out byte[]`
* `out` [`CloudQueueMessage`] 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

Você também pode usar o tipo de retorno do método hello como Olá associação de saída.

<a name="outputsample"></a>

## <a name="queue-output-sample"></a>Amostra de saída da fila
a seguir Olá *function.json* define um gatilho HTTP com uma fila de associação de saída:

```json
{
  "bindings": [
    {
      "type": "httpTrigger",
      "direction": "in",
      "authLevel": "function",
      "name": "input"
    },
    {
      "type": "http",
      "direction": "out",
      "name": "return"
    },
    {
      "type": "queue",
      "direction": "out",
      "name": "$return",
      "queueName": "outqueue",
      "connection": "MyStorageConnectionString",
    }
  ]
}
``` 

Consulte o exemplo de específico do idioma de saudação que gera uma mensagem da fila com carga de HTTP de entrada de saudação.

* [C#](#outcsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a>Amostra de saída da fila em C# #

```cs
// C# example of HTTP trigger binding tooa custom POCO, with a queue output binding
public class CustomQueueMessage
{
    public string PersonName { get; set; }
    public string Title { get; set; }
}

public static CustomQueueMessage Run(CustomQueueMessage input, TraceWriter log)
{
    return input;
}
```

toosend várias mensagens, use uma `ICollector`:

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a>Amostra de saída de fila em Node.js

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

Ou, toosend várias mensagens,

```javascript
module.exports = function(context) {
    // Define a message array for hello myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a>Próximas etapas

Para obter um exemplo de uma função que usa gatilhos de armazenamento de fila e associações, consulte [criar tooan uma função do Azure conectados do serviço do Azure](functions-create-an-azure-connected-function.md).

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

[`CloudQueueMessage`]: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
