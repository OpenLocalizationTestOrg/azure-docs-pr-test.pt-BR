---
title: "Associações dos Hubs de Eventos do Azure Functions | Microsoft Docs"
description: "Entenda como usar associações dos Hubs de Eventos do Azure no Azure Functions."
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
ms.openlocfilehash: 19021bef8b7156b3049f43b0275c0ed0c6b22514
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-event-hubs-bindings"></a><span data-ttu-id="766d5-104">Associações dos Hubs de Eventos do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="766d5-104">Azure Functions Event Hubs bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="766d5-105">Este artigo explica como configurar e usar associações dos [Hubs de Eventos do Azure](../event-hubs/event-hubs-what-is-event-hubs.md) no Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="766d5-105">This article explains how to configure and use [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) bindings for Azure Functions.</span></span>
<span data-ttu-id="766d5-106">O Azure Functions dá suporte a associações de gatilho e de saída para os Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="766d5-106">Azure Functions supports trigger and output bindings for Event Hubs.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="766d5-107">Se você for novo nos Hubs de Evento do Azure, consulte a [Visão geral dos Hubs de Eventos](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="766d5-107">If you are new to Azure Event Hubs, see the [Event Hubs overview](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

<a name="trigger"></a>

## <a name="event-hub-trigger"></a><span data-ttu-id="766d5-108">Gatilho do hub de eventos</span><span class="sxs-lookup"><span data-stu-id="766d5-108">Event hub trigger</span></span>
<span data-ttu-id="766d5-109">Use o gatilho dos Hubs de Eventos do Azure para responder a um evento enviado para uma transmissão de evento do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="766d5-109">Use the Event Hubs trigger to respond to an event sent to an event hub event stream.</span></span> <span data-ttu-id="766d5-110">É necessário ter acesso de leitura ao hub de eventos para configurar o gatilho.</span><span class="sxs-lookup"><span data-stu-id="766d5-110">You must have read access to the event hub to set up the trigger.</span></span>

<span data-ttu-id="766d5-111">O gatilho da função Hubs de Eventos usa o seguinte objeto JSON na matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="766d5-111">The Event Hubs function trigger uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHubTrigger",
    "name": "<Name of trigger parameter in function signature>",
    "direction": "in",
    "path": "<Name of the event hub>",
    "consumerGroup": "Consumer group to use - see below",
    "connection": "<Name of app setting with connection string - see below>"
}
```

<span data-ttu-id="766d5-112">`consumerGroup` é uma propriedade opcional usada para definir o [grupo de consumidores](../event-hubs/event-hubs-features.md#event-consumers) usado para assinar eventos no hub.</span><span class="sxs-lookup"><span data-stu-id="766d5-112">`consumerGroup` is an optional property used to set the [consumer group](../event-hubs/event-hubs-features.md#event-consumers) used to subscribe to events in the hub.</span></span> <span data-ttu-id="766d5-113">Se omitido, o grupo de consumidores `$Default` será usado.</span><span class="sxs-lookup"><span data-stu-id="766d5-113">If omitted, the `$Default` consumer group is used.</span></span>  
<span data-ttu-id="766d5-114">`connection` deve ser o nome de uma configuração de aplicativo que contém a cadeia de conexão para o namespace do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="766d5-114">`connection` must be the name of an app setting that contains the connection string to the event hub's namespace.</span></span>
<span data-ttu-id="766d5-115">Copie essa cadeia de conexão clicando no botão **Informações de Conexão** do *namespace*, não no próprio hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="766d5-115">Copy this connection string by clicking the **Connection Information** button for the *namespace*, not the event hub itself.</span></span> <span data-ttu-id="766d5-116">Essa cadeia de conexão deve ter, pelo menos, permissões de leitura para ativar o gatilho.</span><span class="sxs-lookup"><span data-stu-id="766d5-116">This connection string must have at least read permissions to activate the trigger.</span></span>

<span data-ttu-id="766d5-117">[Configurações adicionais](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) podem ser fornecidas em um arquivo host.json para ajustar ainda mais gatilhos dos Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="766d5-117">[Additional settings](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) can be provided in a host.json file to further fine tune Event Hubs triggers.</span></span>  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="766d5-118">Uso de gatilho</span><span class="sxs-lookup"><span data-stu-id="766d5-118">Trigger usage</span></span>
<span data-ttu-id="766d5-119">Quando uma função de gatilho dos Hubs de Eventos é disparada, a mensagem que a dispara é passada para a função como cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="766d5-119">When an Event Hubs trigger function is triggered, the message that triggers it is passed into the function as a string.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="766d5-120">Exemplo de gatilho</span><span class="sxs-lookup"><span data-stu-id="766d5-120">Trigger sample</span></span>
<span data-ttu-id="766d5-121">Suponha que você tenha o seguinte gatilho dos Hubs de Eventos na matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="766d5-121">Suppose you have the following Event Hubs trigger in the `bindings` array of function.json:</span></span>

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

<span data-ttu-id="766d5-122">Consulte o exemplo específico a um idioma de registro do corpo da mensagem do gatilho do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="766d5-122">See the language-specific sample that logs the message body of the event hub trigger.</span></span>

* [<span data-ttu-id="766d5-123">C#</span><span class="sxs-lookup"><span data-stu-id="766d5-123">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="766d5-124">F#</span><span class="sxs-lookup"><span data-stu-id="766d5-124">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="766d5-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="766d5-125">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="766d5-126">Exemplo de gatilho em C#</span><span class="sxs-lookup"><span data-stu-id="766d5-126">Trigger sample in C#</span></span> #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="766d5-127">Você também pode receber o evento como um objeto [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata), que fornece acesso aos metadados do evento.</span><span class="sxs-lookup"><span data-stu-id="766d5-127">You can also receive the event as an [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) object, which gives you access to the event metadata.</span></span>

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

<span data-ttu-id="766d5-128">Para receber eventos em um lote, altere o método de assinatura para `string[]` ou `EventData[]`.</span><span class="sxs-lookup"><span data-stu-id="766d5-128">To receive events in a batch, change the method signature to `string[]` or `EventData[]`.</span></span>

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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="766d5-129">Exemplo de gatilho em F#</span><span class="sxs-lookup"><span data-stu-id="766d5-129">Trigger sample in F#</span></span> #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="766d5-130">Exemplo de gatilho em Node.js</span><span class="sxs-lookup"><span data-stu-id="766d5-130">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a><span data-ttu-id="766d5-131">Associação de saída dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="766d5-131">Event Hubs output binding</span></span>
<span data-ttu-id="766d5-132">Use a associação de saída dos Hubs de Eventos para gravar eventos em uma transmissão de evento do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="766d5-132">Use the Event Hubs output binding to write events to an event hub event stream.</span></span> <span data-ttu-id="766d5-133">É necessário ter permissão de envio para um hub de eventos a fim de gravar eventos nele.</span><span class="sxs-lookup"><span data-stu-id="766d5-133">You must have send permission to an event hub to write events to it.</span></span>

<span data-ttu-id="766d5-134">A associação de saída usa o seguinte objeto JSON na matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="766d5-134">The output binding uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

<span data-ttu-id="766d5-135">`connection` deve ser o nome de uma configuração de aplicativo que contém a cadeia de conexão para o namespace do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="766d5-135">`connection` must be the name of an app setting that contains the connection string to the event hub's namespace.</span></span>
<span data-ttu-id="766d5-136">Copie essa cadeia de conexão clicando no botão **Informações de Conexão** do *namespace*, não no próprio hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="766d5-136">Copy this connection string by clicking the **Connection Information** button for the *namespace*, not the event hub itself.</span></span> <span data-ttu-id="766d5-137">Essa cadeia de conexão deve ter permissões de envio para enviar a mensagem à transmissão do evento.</span><span class="sxs-lookup"><span data-stu-id="766d5-137">This connection string must have send permissions to send the message to the event stream.</span></span>

## <a name="output-usage"></a><span data-ttu-id="766d5-138">Uso de saída</span><span class="sxs-lookup"><span data-stu-id="766d5-138">Output usage</span></span>
<span data-ttu-id="766d5-139">Esta seção mostra como usar a associação de saída dos Hubs de Eventos no seu código de função.</span><span class="sxs-lookup"><span data-stu-id="766d5-139">This section shows you how to use your Event Hubs output binding in your function code.</span></span>

<span data-ttu-id="766d5-140">Você pode gerar mensagens de saída para o hub de eventos configurado com os seguintes tipos de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="766d5-140">You can output messages to the configured event hub with the following parameter types:</span></span>

* `out string`
* <span data-ttu-id="766d5-141">`ICollector<string>` (para gerar várias mensagens)</span><span class="sxs-lookup"><span data-stu-id="766d5-141">`ICollector<string>` (to output multiple messages)</span></span>
* <span data-ttu-id="766d5-142">`IAsyncCollector<string>` (versão assíncrona de `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="766d5-142">`IAsyncCollector<string>` (async version of `ICollector<T>`)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="766d5-143">Amostra de saída</span><span class="sxs-lookup"><span data-stu-id="766d5-143">Output sample</span></span>
<span data-ttu-id="766d5-144">Suponha que você tenha a seguinte associação de saída dos Hubs de Eventos na matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="766d5-144">Suppose you have the following Event Hubs output binding in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

<span data-ttu-id="766d5-145">Consulte o exemplo específico a um idioma de gravação de evento na mesma transmissão.</span><span class="sxs-lookup"><span data-stu-id="766d5-145">See the language-specific sample that writes an event to the even stream.</span></span>

* [<span data-ttu-id="766d5-146">C#</span><span class="sxs-lookup"><span data-stu-id="766d5-146">C#</span></span>](#outcsharp)
* [<span data-ttu-id="766d5-147">F#</span><span class="sxs-lookup"><span data-stu-id="766d5-147">F#</span></span>](#outfsharp)
* [<span data-ttu-id="766d5-148">Node.js</span><span class="sxs-lookup"><span data-stu-id="766d5-148">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="766d5-149">Amostra de saída em C#</span><span class="sxs-lookup"><span data-stu-id="766d5-149">Output sample in C#</span></span> #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

<span data-ttu-id="766d5-150">Ou, para criar várias mensagens:</span><span class="sxs-lookup"><span data-stu-id="766d5-150">Or, to create multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="766d5-151">Amostra de saída em F#</span><span class="sxs-lookup"><span data-stu-id="766d5-151">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a><span data-ttu-id="766d5-152">Exemplo de saída em Node.js</span><span class="sxs-lookup"><span data-stu-id="766d5-152">Output sample for Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

<span data-ttu-id="766d5-153">Ou, para enviar várias mensagens,</span><span class="sxs-lookup"><span data-stu-id="766d5-153">Or, to send multiple messages,</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="766d5-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="766d5-154">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
