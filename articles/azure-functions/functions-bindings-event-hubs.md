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
# <a name="azure-functions-event-hubs-bindings"></a><span data-ttu-id="87a1a-104">Associações dos Hubs de Eventos do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="87a1a-104">Azure Functions Event Hubs bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="87a1a-105">Este artigo explica como tooconfigure e usar [Hubs de eventos do Azure](../event-hubs/event-hubs-what-is-event-hubs.md) associações para funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="87a1a-105">This article explains how tooconfigure and use [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) bindings for Azure Functions.</span></span>
<span data-ttu-id="87a1a-106">O Azure Functions dá suporte a associações de gatilho e de saída para os Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="87a1a-106">Azure Functions supports trigger and output bindings for Event Hubs.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="87a1a-107">Se você for novo tooAzure os Hubs de eventos, consulte Olá [visão geral de Hubs de evento](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="87a1a-107">If you are new tooAzure Event Hubs, see hello [Event Hubs overview](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

<a name="trigger"></a>

## <a name="event-hub-trigger"></a><span data-ttu-id="87a1a-108">Gatilho do hub de eventos</span><span class="sxs-lookup"><span data-stu-id="87a1a-108">Event hub trigger</span></span>
<span data-ttu-id="87a1a-109">Hubs de eventos do uso Olá disparar toorespond tooan eventos enviados tooan fluxo de evento de hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="87a1a-109">Use hello Event Hubs trigger toorespond tooan event sent tooan event hub event stream.</span></span> <span data-ttu-id="87a1a-110">Você deve ter acesso de leitura toohello evento hub tooset o gatilho de saudação.</span><span class="sxs-lookup"><span data-stu-id="87a1a-110">You must have read access toohello event hub tooset up hello trigger.</span></span>

<span data-ttu-id="87a1a-111">gatilho de função de Hubs de eventos de saudação usa Olá seguinte objeto JSON na Olá `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="87a1a-111">hello Event Hubs function trigger uses hello following JSON object in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="87a1a-112">`consumerGroup`é uma saudação de tooset propriedade opcional usada [grupo de consumidores](../event-hubs/event-hubs-features.md#event-consumers) usado toosubscribe tooevents no hub de saudação.</span><span class="sxs-lookup"><span data-stu-id="87a1a-112">`consumerGroup` is an optional property used tooset hello [consumer group](../event-hubs/event-hubs-features.md#event-consumers) used toosubscribe tooevents in hello hub.</span></span> <span data-ttu-id="87a1a-113">Se omitido, Olá `$Default` grupo de consumidores é usado.</span><span class="sxs-lookup"><span data-stu-id="87a1a-113">If omitted, hello `$Default` consumer group is used.</span></span>  
<span data-ttu-id="87a1a-114">`connection`deve ser o nome de saudação de uma configuração de aplicativo que contém o namespace do hub de eventos toohello string hello conexão.</span><span class="sxs-lookup"><span data-stu-id="87a1a-114">`connection` must be hello name of an app setting that contains hello connection string toohello event hub's namespace.</span></span>
<span data-ttu-id="87a1a-115">Copie essa cadeia de caracteres de conexão clicando Olá **informações de Conexão** botão para Olá *namespace*, não hub de eventos Olá em si.</span><span class="sxs-lookup"><span data-stu-id="87a1a-115">Copy this connection string by clicking hello **Connection Information** button for hello *namespace*, not hello event hub itself.</span></span> <span data-ttu-id="87a1a-116">Essa cadeia de caracteres de conexão deve ter pelo menos leitura gatilho de saudação tooactivate permissões.</span><span class="sxs-lookup"><span data-stu-id="87a1a-116">This connection string must have at least read permissions tooactivate hello trigger.</span></span>

<span data-ttu-id="87a1a-117">[Configurações adicionais](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) pode ser fornecido um host.json arquivo toofurther bem ajusta os gatilhos de Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="87a1a-117">[Additional settings](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) can be provided in a host.json file toofurther fine tune Event Hubs triggers.</span></span>  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="87a1a-118">Uso de gatilho</span><span class="sxs-lookup"><span data-stu-id="87a1a-118">Trigger usage</span></span>
<span data-ttu-id="87a1a-119">Quando uma função de gatilho de Hubs de evento é disparada, mensagem de saudação do que o aciona é passada para função hello como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="87a1a-119">When an Event Hubs trigger function is triggered, hello message that triggers it is passed into hello function as a string.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="87a1a-120">Exemplo de gatilho</span><span class="sxs-lookup"><span data-stu-id="87a1a-120">Trigger sample</span></span>
<span data-ttu-id="87a1a-121">Suponha que você tenha Olá seguintes Hubs de evento de gatilho Olá `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="87a1a-121">Suppose you have hello following Event Hubs trigger in hello `bindings` array of function.json:</span></span>

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

<span data-ttu-id="87a1a-122">Consulte Olá específico do idioma exemplo registra o corpo da mensagem de saudação do disparador de hub de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="87a1a-122">See hello language-specific sample that logs hello message body of hello event hub trigger.</span></span>

* [<span data-ttu-id="87a1a-123">C#</span><span class="sxs-lookup"><span data-stu-id="87a1a-123">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="87a1a-124">F#</span><span class="sxs-lookup"><span data-stu-id="87a1a-124">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="87a1a-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="87a1a-125">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="87a1a-126">Exemplo de gatilho em C#</span><span class="sxs-lookup"><span data-stu-id="87a1a-126">Trigger sample in C#</span></span> #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="87a1a-127">Você também pode receber o evento hello como um [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) objeto, que dá a você acessar metadados de evento toohello.</span><span class="sxs-lookup"><span data-stu-id="87a1a-127">You can also receive hello event as an [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) object, which gives you access toohello event metadata.</span></span>

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

<span data-ttu-id="87a1a-128">tooreceive eventos em um lote, alterar a assinatura do método hello muito`string[]` ou `EventData[]`.</span><span class="sxs-lookup"><span data-stu-id="87a1a-128">tooreceive events in a batch, change hello method signature too`string[]` or `EventData[]`.</span></span>

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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="87a1a-129">Exemplo de gatilho em F#</span><span class="sxs-lookup"><span data-stu-id="87a1a-129">Trigger sample in F#</span></span> #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="87a1a-130">Exemplo de gatilho em Node.js</span><span class="sxs-lookup"><span data-stu-id="87a1a-130">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a><span data-ttu-id="87a1a-131">Associação de saída dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="87a1a-131">Event Hubs output binding</span></span>
<span data-ttu-id="87a1a-132">Olá usar Hubs de eventos de saída fluxo de evento hub de eventos tooan de eventos toowrite de associação.</span><span class="sxs-lookup"><span data-stu-id="87a1a-132">Use hello Event Hubs output binding toowrite events tooan event hub event stream.</span></span> <span data-ttu-id="87a1a-133">Você deve ter o envio permissão tooan evento hub toowrite eventos tooit.</span><span class="sxs-lookup"><span data-stu-id="87a1a-133">You must have send permission tooan event hub toowrite events tooit.</span></span>

<span data-ttu-id="87a1a-134">associação de saída Hello usa Olá seguinte objeto JSON na Olá `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="87a1a-134">hello output binding uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

<span data-ttu-id="87a1a-135">`connection`deve ser o nome de saudação de uma configuração de aplicativo que contém o namespace do hub de eventos toohello string hello conexão.</span><span class="sxs-lookup"><span data-stu-id="87a1a-135">`connection` must be hello name of an app setting that contains hello connection string toohello event hub's namespace.</span></span>
<span data-ttu-id="87a1a-136">Copie essa cadeia de caracteres de conexão clicando Olá **informações de Conexão** botão para Olá *namespace*, não hub de eventos Olá em si.</span><span class="sxs-lookup"><span data-stu-id="87a1a-136">Copy this connection string by clicking hello **Connection Information** button for hello *namespace*, not hello event hub itself.</span></span> <span data-ttu-id="87a1a-137">Essa cadeia de caracteres de conexão deve ter um fluxo de eventos do envio permissões toosend Olá mensagem toohello.</span><span class="sxs-lookup"><span data-stu-id="87a1a-137">This connection string must have send permissions toosend hello message toohello event stream.</span></span>

## <a name="output-usage"></a><span data-ttu-id="87a1a-138">Uso de saída</span><span class="sxs-lookup"><span data-stu-id="87a1a-138">Output usage</span></span>
<span data-ttu-id="87a1a-139">Esta seção mostra como toouse seus Hubs de eventos de saída de associação no seu código de função.</span><span class="sxs-lookup"><span data-stu-id="87a1a-139">This section shows you how toouse your Event Hubs output binding in your function code.</span></span>

<span data-ttu-id="87a1a-140">Você pode dar saída hub de eventos mensagens toohello configurado com hello tipos de parâmetro a seguir:</span><span class="sxs-lookup"><span data-stu-id="87a1a-140">You can output messages toohello configured event hub with hello following parameter types:</span></span>

* `out string`
* <span data-ttu-id="87a1a-141">`ICollector<string>`(toooutput várias mensagens)</span><span class="sxs-lookup"><span data-stu-id="87a1a-141">`ICollector<string>` (toooutput multiple messages)</span></span>
* <span data-ttu-id="87a1a-142">`IAsyncCollector<string>` (versão assíncrona de `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="87a1a-142">`IAsyncCollector<string>` (async version of `ICollector<T>`)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="87a1a-143">Amostra de saída</span><span class="sxs-lookup"><span data-stu-id="87a1a-143">Output sample</span></span>
<span data-ttu-id="87a1a-144">Suponha que você tenha a seguinte Olá Hubs de eventos de saída associação em Olá `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="87a1a-144">Suppose you have hello following Event Hubs output binding in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

<span data-ttu-id="87a1a-145">Consulte Olá específico do idioma exemplo grava um fluxo até mesmo de toohello de eventos.</span><span class="sxs-lookup"><span data-stu-id="87a1a-145">See hello language-specific sample that writes an event toohello even stream.</span></span>

* [<span data-ttu-id="87a1a-146">C#</span><span class="sxs-lookup"><span data-stu-id="87a1a-146">C#</span></span>](#outcsharp)
* [<span data-ttu-id="87a1a-147">F#</span><span class="sxs-lookup"><span data-stu-id="87a1a-147">F#</span></span>](#outfsharp)
* [<span data-ttu-id="87a1a-148">Node.js</span><span class="sxs-lookup"><span data-stu-id="87a1a-148">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="87a1a-149">Amostra de saída em C#</span><span class="sxs-lookup"><span data-stu-id="87a1a-149">Output sample in C#</span></span> #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

<span data-ttu-id="87a1a-150">Ou, toocreate várias mensagens:</span><span class="sxs-lookup"><span data-stu-id="87a1a-150">Or, toocreate multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="87a1a-151">Amostra de saída em F#</span><span class="sxs-lookup"><span data-stu-id="87a1a-151">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a><span data-ttu-id="87a1a-152">Exemplo de saída em Node.js</span><span class="sxs-lookup"><span data-stu-id="87a1a-152">Output sample for Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

<span data-ttu-id="87a1a-153">Ou, toosend várias mensagens,</span><span class="sxs-lookup"><span data-stu-id="87a1a-153">Or, toosend multiple messages,</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="87a1a-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="87a1a-154">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
