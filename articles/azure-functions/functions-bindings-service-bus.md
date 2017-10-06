---
title: "aaaAzure barramento de serviço de funções de gatilhos e associações | Microsoft Docs"
description: "Entenda como dispara toouse Azure Service Bus e associações em funções do Azure."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, funções, processamento de eventos, computação dinâmica, arquitetura sem servidor"
ms.assetid: daedacf0-6546-4355-a65c-50873e74f66b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/01/2017
ms.author: glenga
ms.openlocfilehash: dff9e89bd3840b8c11f91cae41e13502afc7aa60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-service-bus-bindings"></a>Associações do Barramento de Serviço do Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artigo explica como tooconfigure e trabalhar com associações do barramento de serviço do Azure em funções do Azure. 

O Azure Functions dá suporte a gatilhos e a associações de saída para filas e tópicos do Barramento de Serviço.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a>Gatilho do Barramento de Serviço
Use Olá barramento de serviço gatilho toorespond toomessages de uma fila do barramento de serviço ou um tópico. 

Olá gatilhos de filas e tópicos do barramento de serviço são definidos por Olá seguintes objetos JSON em Olá `bindings` matriz de function.json:

* Gatilho de *fila*:

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

* Gatilho de *tópico*:

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

Observe o seguinte hello:

* Para `connection`, [criar uma configuração de aplicativo em seu aplicativo de função](functions-how-to-use-azure-function-app-settings.md) que contém o namespace de barramento de serviço do hello conexão cadeia de caracteres tooyour, em seguida, especifique o nome de saudação de configuração do aplicativo hello em Olá `connection` propriedade em seu gatilho. Obter cadeia de caracteres de conexão Olá seguindo as etapas Olá mostradas no [obter credenciais de gerenciamento Olá](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).
  cadeia de caracteres de conexão Olá deve ser para um namespace, fila específica tooa não limitado ou tópico do barramento de serviço.
  Se você deixar `connection` vazio, gatilho Olá pressupõe que uma cadeia de caracteres de conexão de barramento de serviço padrão é especificada em um aplicativo de configuração nomeada `AzureWebJobsServiceBus`.
* Para `accessRights`, os valores disponíveis são `manage` e `listen`. saudação padrão é `manage`, que indica que Olá `connection` tem Olá **gerenciar** permissão. Se você usar uma cadeia de caracteres de conexão que não tenha Olá **gerenciar** conjunto de permissões, `accessRights` muito`listen`. Caso contrário, Olá tempo de execução de funções podem falhar tentar toodo as operações que exigem gerenciar direitos.

## <a name="trigger-behavior"></a>Comportamento do gatilho
* **Threading único** - por padrão, os processos de tempo de execução de funções hello várias mensagens simultaneamente. toodirect Olá runtime tooprocess apenas uma única fila ou tópico de mensagem por vez, defina `serviceBus.maxConcurrentCalls` too1 na *host.json*. 
  Para obter informações sobre o *host.json*, consulte [Estrutura da pasta](functions-reference.md#folder-structure) e [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).
* **Manipulação de mensagens suspeitas** - o Barramento de Serviço faz seu próprio tratamento de mensagens suspeitas que não pode ser controlado ou definido na configuração ou código do Azure Functions. 
* **Comportamento de PeekLock** -tempo de execução de funções hello recebe uma mensagem em [ `PeekLock` modo](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) e chamadas de `Complete` na mensagem de saudação quando função hello concluído com êxito, ou chamadas `Abandon` se hello função falhará. 
  Se a função hello executada por mais de saudação `PeekLock` tempo limite de bloqueio de saudação é renovada automaticamente.

<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Uso de gatilho
Esta seção mostra como toouse o barramento de serviço do disparador no seu código de função. 

Em c# e F #, mensagem de saudação do gatilho de barramento de serviço pode ser desserializado tooany de saudação tipos de entrada a seguir:

* `string` - útil para mensagens de cadeia de caracteres
* `byte[]` - útil para dados binários
* Qualquer [Objeto](https://msdn.microsoft.com/library/system.object.aspx) - útil para dados JSON serializados.
  Se você declarar um tipo de entrada personalizado, como `CustomType`, funções do Azure tenta dados do toodeserialize Olá JSON para o tipo especificado.
* `BrokeredMessage`-permite que você Olá desserializado mensagem de saudação [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) método.

No Node. js, mensagem de saudação do gatilho de barramento de serviço é passada para a função hello como uma cadeia de caracteres ou um objeto JSON.

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Exemplo de gatilho
Suponha que você tenha Olá function.json a seguir:

```json
{
"bindings": [
    {
    "queueName": "testqueue",
    "connection": "MyServiceBusConnection",
    "name": "myQueueItem",
    "type": "serviceBusTrigger",
    "direction": "in"
    }
],
"disabled": false
}
```

Consulte exemplo específico do idioma hello que processa uma mensagem da fila de barramento de serviço.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Exemplo de gatilho em C# #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a>Exemplo de gatilho em F# #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Exemplo de gatilho em Node.js

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a>Associação de saída do Barramento de Serviço
Olá saída de filas e tópicos do barramento de serviço para uma função usar Olá seguintes objetos JSON em Olá `bindings` matriz de function.json:

* Saída da *fila*:

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```
* Saída do *tópico*:

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```

Observe o seguinte hello:

* Para `connection`, [criar uma configuração de aplicativo em seu aplicativo de função](functions-how-to-use-azure-function-app-settings.md) que contém o namespace de barramento de serviço do hello conexão cadeia de caracteres tooyour, em seguida, especifique o nome de saudação de configuração do aplicativo hello em Olá `connection` propriedade na saída associação. Obter cadeia de caracteres de conexão Olá seguindo as etapas Olá mostradas no [obter credenciais de gerenciamento Olá](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).
  cadeia de caracteres de conexão Olá deve ser para um namespace, fila específica tooa não limitado ou tópico do barramento de serviço.
  Se você deixar `connection` vazio, hello associação de saída pressupõe que uma cadeia de caracteres de conexão de barramento de serviço padrão é especificada em um aplicativo de configuração nomeada `AzureWebJobsServiceBus`.
* Para `accessRights`, os valores disponíveis são `manage` e `listen`. saudação padrão é `manage`, que indica que Olá `connection` tem Olá **gerenciar** permissão. Se você usar uma cadeia de caracteres de conexão que não tenha Olá **gerenciar** conjunto de permissões, `accessRights` muito`listen`. Caso contrário, Olá tempo de execução de funções podem falhar tentar toodo as operações que exigem gerenciar direitos.

<a name="outputusage"></a>

## <a name="output-usage"></a>Uso de saída
Em c# e F #, funções do Azure pode criar uma mensagem de fila do barramento de serviço de qualquer um dos seguintes tipos de saudação:

* Qualquer [Objeto](https://msdn.microsoft.com/library/system.object.aspx) - A definição do parâmetro se parece com `out T paramName` (C#).
  Funções desserializa o objeto Olá em uma mensagem JSON. Se o valor de saída de saudação é nulo quando Olá função for encerrada, funções cria a mensagem de saudação com um objeto nulo.
* `string` - A definição de parâmetro se parece com `out string paraName` (C#). Se o valor do parâmetro hello for não nulo quando Olá função for encerrada, funções cria uma mensagem.
* `byte[]` - A definição de parâmetro se parece com `out byte[] paraName` (C#). Se o valor do parâmetro hello for não nulo quando Olá função for encerrada, funções cria uma mensagem.
* `BrokeredMessage` A definição de parâmetro se parece com `out BrokeredMessage paraName` (C#). Se o valor do parâmetro hello for não nulo quando Olá função for encerrada, funções cria uma mensagem.

Para criar várias mensagens em uma função C#, você pode usar `ICollector<T>` ou `IAsyncCollector<T>`. Uma mensagem é criada quando você chamar hello `Add` método.

Node. js, você pode atribuir uma cadeia de caracteres, uma matriz de bytes ou um objeto de Javascript (desserializado em JSON) muito`context.binding.<paramName>`.

<a name="outputsample"></a>

## <a name="output-sample"></a>Amostra de saída
Suponha que você tenha Olá function.json, que define uma saída de fila do barramento de serviço a seguir:

```json
{
    "bindings": [
        {
            "schedule": "0/15 * * * * *",
            "name": "myTimer",
            "runsOnStartup": true,
            "type": "timerTrigger",
            "direction": "in"
        },
        {
            "name": "outputSbQueue",
            "type": "serviceBus",
            "queueName": "testqueue",
            "connection": "MyServiceBusConnection",
            "direction": "out"
        }
    ],
    "disabled": false
}
```

Consulte Olá específico do idioma exemplo envia uma fila de mensagem toohello service bus.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Amostra de saída em C# #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

Ou, toocreate várias mensagens:

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, ICollector<string> outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue.Add("1 " + message);
    outputSbQueue.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a>Amostra de saída em F# #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a>Amostra de saída no Node.js

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

Ou, toocreate várias mensagens:

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = [];
    context.bindings.outputSbQueueMsg.push("1 " + message);
    context.bindings.outputSbQueueMsg.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

