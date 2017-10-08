---
title: "associações de Hubs de eventos de funções aaaAzure | Microsoft Docs"
description: "Entender como toouse associações de Hubs de eventos do Azure em funções do Azure."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, funções, processamento de eventos, computação dinâmica, arquitetura sem servidor"
ms.assetid: daf81798-7acc-419a-bc32-b5a41c6db56b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/20/2017
ms.author: wesmc
ms.openlocfilehash: e864f032ad5ac58d318c9843c3844b5642733a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-event-hubs-bindings"></a>Associações dos Hubs de Eventos do Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artigo explica como tooconfigure e usar [Hubs de eventos do Azure](../event-hubs/event-hubs-what-is-event-hubs.md) associações para funções do Azure.
O Azure Functions dá suporte a associações de gatilho e de saída para os Hubs de Eventos.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Se você for novo tooAzure os Hubs de eventos, consulte Olá [visão geral de Hubs de evento](../event-hubs/event-hubs-what-is-event-hubs.md).

<a name="trigger"></a>

## <a name="event-hub-trigger"></a>Gatilho do hub de eventos
Hubs de eventos do uso Olá disparar toorespond tooan eventos enviados tooan fluxo de evento de hub de eventos. Você deve ter acesso de leitura toohello evento hub tooset o gatilho de saudação.

gatilho de função de Hubs de eventos de saudação usa Olá seguinte objeto JSON na Olá `bindings` matriz de function.json:

```json
{
    "type": "eventHubTrigger",
    "name": "<Name of trigger parameter in function signature>",
    "direction": "in",
    "path": "<Name of hello event hub>",
    "consumerGroup": "Consumer group toouse - see below",
    "connection": "<Name of app setting with connection string - see below>"
}
```

`consumerGroup`é uma saudação de tooset propriedade opcional usada [grupo de consumidores](../event-hubs/event-hubs-features.md#event-consumers) usado toosubscribe tooevents no hub de saudação. Se omitido, Olá `$Default` grupo de consumidores é usado.  
`connection`deve ser o nome de saudação de uma configuração de aplicativo que contém o namespace do hub de eventos toohello string hello conexão.
Copie essa cadeia de caracteres de conexão clicando Olá **informações de Conexão** botão para Olá *namespace*, não hub de eventos Olá em si. Essa cadeia de caracteres de conexão deve ter pelo menos leitura gatilho de saudação tooactivate permissões.

[Configurações adicionais](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) pode ser fornecido um host.json arquivo toofurther bem ajusta os gatilhos de Hubs de eventos.  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Uso de gatilho
Quando uma função de gatilho de Hubs de evento é disparada, mensagem de saudação do que o aciona é passada para função hello como uma cadeia de caracteres.

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Exemplo de gatilho
Suponha que você tenha Olá seguintes Hubs de evento de gatilho Olá `bindings` matriz de function.json:

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

Consulte Olá específico do idioma exemplo registra o corpo da mensagem de saudação do disparador de hub de eventos de saudação.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Exemplo de gatilho em C# #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

Você também pode receber o evento hello como um [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) objeto, que dá a você acessar metadados de evento toohello.

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

tooreceive eventos em um lote, alterar a assinatura do método hello muito`string[]` ou `EventData[]`.

```cs
public static void Run(string[] eventHubMessages, TraceWriter log)
{
    foreach (var message in eventHubMessages)
    {
        log.Info($"C# Event Hub trigger function processed a message: {message}");
    }
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a>Exemplo de gatilho em F# #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Exemplo de gatilho em Node.js

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a>Associação de saída dos Hubs de Eventos
Olá usar Hubs de eventos de saída fluxo de evento hub de eventos tooan de eventos toowrite de associação. Você deve ter o envio permissão tooan evento hub toowrite eventos tooit.

associação de saída Hello usa Olá seguinte objeto JSON na Olá `bindings` matriz de function.json:

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

`connection`deve ser o nome de saudação de uma configuração de aplicativo que contém o namespace do hub de eventos toohello string hello conexão.
Copie essa cadeia de caracteres de conexão clicando Olá **informações de Conexão** botão para Olá *namespace*, não hub de eventos Olá em si. Essa cadeia de caracteres de conexão deve ter um fluxo de eventos do envio permissões toosend Olá mensagem toohello.

## <a name="output-usage"></a>Uso de saída
Esta seção mostra como toouse seus Hubs de eventos de saída de associação no seu código de função.

Você pode dar saída hub de eventos mensagens toohello configurado com hello tipos de parâmetro a seguir:

* `out string`
* `ICollector<string>`(toooutput várias mensagens)
* `IAsyncCollector<string>` (versão assíncrona de `ICollector<T>`)

<a name="outputsample"></a>

## <a name="output-sample"></a>Amostra de saída
Suponha que você tenha a seguinte Olá Hubs de eventos de saída associação em Olá `bindings` matriz de function.json:

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

Consulte Olá específico do idioma exemplo grava um fluxo até mesmo de toohello de eventos.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Amostra de saída em C# #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

Ou, toocreate várias mensagens:

```cs
public static void Run(TimerInfo myTimer, ICollector<string> outputEventHubMessage, TraceWriter log)
{
    string message = $"Event Hub message created at: {DateTime.Now}";
    log.Info(message);
    outputEventHubMessage.Add("1 " + message);
    outputEventHubMessage.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a>Amostra de saída em F# #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a>Exemplo de saída em Node.js

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

Ou, toosend várias mensagens,

```javascript
module.exports = function(context) {
    var timeStamp = new Date().toISOString();
    var message = 'Event Hub message created at: ' + timeStamp;

    context.bindings.outputEventHubMessage = [];

    context.bindings.outputEventHubMessage.push("1 " + message);
    context.bindings.outputEventHubMessage.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
