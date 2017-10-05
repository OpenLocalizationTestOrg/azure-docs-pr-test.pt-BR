---
title: "Gatilhos e associações do Barramento de Serviço do Azure Functions | Microsoft Docs"
description: "Entenda como usar gatilhos e associações do Barramento de Serviço do Azure no Azure Functions."
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
ms.openlocfilehash: b3ee306cd37ebf88dc9369ccc2dc6c670557fd5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-service-bus-bindings"></a><span data-ttu-id="bb1b3-104">Associações do Barramento de Serviço do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="bb1b3-104">Azure Functions Service Bus bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="bb1b3-105">Este artigo explica como configurar e trabalhar com associações do Barramento de Serviço do Azure no Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-105">This article explains how to configure and work with Azure Service Bus bindings in Azure Functions.</span></span> 

<span data-ttu-id="bb1b3-106">O Azure Functions dá suporte a gatilhos e a associações de saída para filas e tópicos do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-106">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a><span data-ttu-id="bb1b3-107">Gatilho do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="bb1b3-107">Service Bus trigger</span></span>
<span data-ttu-id="bb1b3-108">Use o gatilho do Barramento de Serviço para responder às mensagens de uma fila ou tópico do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-108">Use the Service Bus trigger to respond to messages from a Service Bus queue or topic.</span></span> 

<span data-ttu-id="bb1b3-109">Os gatilhos de fila e de tópico do Barramento de Serviço são definidos pelos seguintes objetos JSON na matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="bb1b3-109">The Service Bus queue and topic triggers are defined by the following JSON objects in the `bindings` array of function.json:</span></span>

* <span data-ttu-id="bb1b3-110">Gatilho de *fila*:</span><span class="sxs-lookup"><span data-stu-id="bb1b3-110">*queue* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "queueName" : "<Name of the queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

* <span data-ttu-id="bb1b3-111">Gatilho de *tópico*:</span><span class="sxs-lookup"><span data-stu-id="bb1b3-111">*topic* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "topicName" : "<Name of the topic>",
        "subscriptionName" : "<Name of the subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

<span data-ttu-id="bb1b3-112">Observe o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bb1b3-112">Note the following:</span></span>

* <span data-ttu-id="bb1b3-113">Para `connection`, [crie uma configuração de aplicativo em seu aplicativo de função](functions-how-to-use-azure-function-app-settings.md) que contenha a cadeia de conexão até o namespace de seu Barramento de Serviço, depois especifique o nome da configuração de aplicativo na propriedade `connection` em seu gatilho.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-113">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains the connection string to your Service Bus namespace, then specify the name of the app setting in the `connection` property in your trigger.</span></span> <span data-ttu-id="bb1b3-114">Obtenha a cadeia de conexão, seguindo as etapas mostradas em [Obter as credenciais de gerenciamento](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="bb1b3-114">You obtain the connection string by following the steps shown at [Obtain the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="bb1b3-115">A cadeia de conexão deve ser voltada para um namespace do Barramento de Serviço, não limitada a uma fila ou tópico específico.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-115">The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.</span></span>
  <span data-ttu-id="bb1b3-116">Se você deixar `connection` vazio, o gatilho assumirá que uma cadeia de conexão do Barramento de Serviço padrão foi especificada em uma configuração de aplicativo chamada `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-116">If you leave `connection` empty, the trigger assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="bb1b3-117">Para `accessRights`, os valores disponíveis são `manage` e `listen`.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-117">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="bb1b3-118">O padrão é `manage`, que indica que o `connection` tem a permissão **Gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-118">The default is `manage`, which indicates that the `connection` has the **Manage** permission.</span></span> <span data-ttu-id="bb1b3-119">Se você usar uma cadeia de conexão que não tenha a permissão **Gerenciar**, defina `accessRights` como `listen`.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-119">If you use a connection string that does not have the **Manage** permission, set `accessRights` to `listen`.</span></span> <span data-ttu-id="bb1b3-120">Caso contrário, o tempo de execução do Functions talvez falhe ao tentar executar operações que exigem o gerenciamento de direitos.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-120">Otherwise, the Functions runtime might fail trying to do operations that require manage rights.</span></span>

## <a name="trigger-behavior"></a><span data-ttu-id="bb1b3-121">Comportamento do gatilho</span><span class="sxs-lookup"><span data-stu-id="bb1b3-121">Trigger behavior</span></span>
* <span data-ttu-id="bb1b3-122">**Threading simples** - por padrão, o tempo de execução do Functions processa várias mensagens simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-122">**Single-threading** - By default, the Functions runtime processes multiple messages concurrently.</span></span> <span data-ttu-id="bb1b3-123">Para direcionar o tempo de execução para processar uma única fila ou mensagem de tópico de cada vez, defina `serviceBus.maxConcurrentCalls` como 1 em *host.json* .</span><span class="sxs-lookup"><span data-stu-id="bb1b3-123">To direct the runtime to process only a single queue or topic message at a time, set `serviceBus.maxConcurrentCalls` to 1 in *host.json*.</span></span> 
  <span data-ttu-id="bb1b3-124">Para obter informações sobre o *host.json*, consulte [Estrutura da pasta](functions-reference.md#folder-structure) e [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="bb1b3-124">For information about *host.json*, see [Folder Structure](functions-reference.md#folder-structure) and [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>
* <span data-ttu-id="bb1b3-125">**Manipulação de mensagens suspeitas** - o Barramento de Serviço faz seu próprio tratamento de mensagens suspeitas que não pode ser controlado ou definido na configuração ou código do Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-125">**Poison message handling** - Service Bus does its own poison message handling, which can't be controlled or configured in Azure Functions configuration or code.</span></span> 
* <span data-ttu-id="bb1b3-126">**Comportamento PeekLock** - o tempo de execução do Functions recebe uma mensagem no modo [`PeekLock` ](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) e chama `Complete` na mensagem se a função for concluída com êxito, ou chama `Abandon` se a função falhar.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-126">**PeekLock behavior** - The Functions runtime receives a message in [`PeekLock` mode](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) and calls `Complete` on the message if the function finishes successfully, or calls `Abandon` if the function fails.</span></span> 
  <span data-ttu-id="bb1b3-127">Se a função for executada por mais tempo que o limite `PeekLock` , o bloqueio é renovado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-127">If the function runs longer than the `PeekLock` timeout, the lock is automatically renewed.</span></span>

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="bb1b3-128">Uso de gatilho</span><span class="sxs-lookup"><span data-stu-id="bb1b3-128">Trigger usage</span></span>
<span data-ttu-id="bb1b3-129">Esta seção mostra como usar o gatilho do Barramento de Serviço no código de sua função.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-129">This section shows you how to use your Service Bus trigger in your function code.</span></span> 

<span data-ttu-id="bb1b3-130">Em C# e F#, a mensagem do gatilho do Barramento de Serviço pode ser desserializada para qualquer um destes tipos de entrada:</span><span class="sxs-lookup"><span data-stu-id="bb1b3-130">In C# and F#, the Service Bus trigger message can be deserialized to any of the following input types:</span></span>

* <span data-ttu-id="bb1b3-131">`string` - útil para mensagens de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="bb1b3-131">`string` - useful for string messages</span></span>
* <span data-ttu-id="bb1b3-132">`byte[]` - útil para dados binários</span><span class="sxs-lookup"><span data-stu-id="bb1b3-132">`byte[]` - useful for binary data</span></span>
* <span data-ttu-id="bb1b3-133">Qualquer [Objeto](https://msdn.microsoft.com/library/system.object.aspx) - útil para dados JSON serializados.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-133">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized data.</span></span>
  <span data-ttu-id="bb1b3-134">Se você declarar um tipo de entrada personalizado, por exemplo, `CustomType`, o Azure Functions tentará desserializar os dados JSON para o tipo especificado.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-134">If you declare a custom input type, such as `CustomType`, Azure Functions tries to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="bb1b3-135">`BrokeredMessage` -fornece a você a mensagem desserializada com o método [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx).</span><span class="sxs-lookup"><span data-stu-id="bb1b3-135">`BrokeredMessage` - gives you the deserialized message with the [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) method.</span></span>

<span data-ttu-id="bb1b3-136">No Node.js, a mensagem de gatilho do Barramento de Serviço é passada em uma função como uma cadeia de caracteres ou um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-136">In Node.js, the Service Bus trigger message is passed into the function as either a string or JSON object.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="bb1b3-137">Exemplo de gatilho</span><span class="sxs-lookup"><span data-stu-id="bb1b3-137">Trigger sample</span></span>
<span data-ttu-id="bb1b3-138">Vamos supor que você tenha o seguinte function.json:</span><span class="sxs-lookup"><span data-stu-id="bb1b3-138">Suppose you have the following function.json:</span></span>

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

<span data-ttu-id="bb1b3-139">Veja o exemplo específico à linguagem que processa uma mensagem de fila do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-139">See the language-specific sample that processes a Service Bus queue message.</span></span>

* [<span data-ttu-id="bb1b3-140">C#</span><span class="sxs-lookup"><span data-stu-id="bb1b3-140">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="bb1b3-141">F#</span><span class="sxs-lookup"><span data-stu-id="bb1b3-141">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="bb1b3-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="bb1b3-142">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="bb1b3-143">Exemplo de gatilho em C#</span><span class="sxs-lookup"><span data-stu-id="bb1b3-143">Trigger sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="bb1b3-144">Exemplo de gatilho em F#</span><span class="sxs-lookup"><span data-stu-id="bb1b3-144">Trigger sample in F#</span></span> #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="bb1b3-145">Exemplo de gatilho em Node.js</span><span class="sxs-lookup"><span data-stu-id="bb1b3-145">Trigger sample in Node.js</span></span>

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a><span data-ttu-id="bb1b3-146">Associação de saída do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="bb1b3-146">Service Bus output binding</span></span>
<span data-ttu-id="bb1b3-147">A saída da fila e do tópico do Barramento de Serviço para uma função usa os seguintes objetos JSON na matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="bb1b3-147">The Service Bus queue and topic output for a function use the following JSON objects in the `bindings` array of function.json:</span></span>

* <span data-ttu-id="bb1b3-148">Saída da *fila*:</span><span class="sxs-lookup"><span data-stu-id="bb1b3-148">*queue* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "queueName" : "<Name of the queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```
* <span data-ttu-id="bb1b3-149">Saída do *tópico*:</span><span class="sxs-lookup"><span data-stu-id="bb1b3-149">*topic* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "topicName" : "<Name of the topic>",
        "subscriptionName" : "<Name of the subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```

<span data-ttu-id="bb1b3-150">Observe o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bb1b3-150">Note the following:</span></span>

* <span data-ttu-id="bb1b3-151">Para `connection`, [crie uma configuração de aplicativo em seu aplicativo de função](functions-how-to-use-azure-function-app-settings.md) que contenha a cadeia de conexão até o namespace de seu Barramento de Serviço, depois especifique o nome da configuração de aplicativo na propriedade `connection` em sua associação de saída.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-151">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains the connection string to your Service Bus namespace, then specify the name of the app setting in the `connection` property in your output binding.</span></span> <span data-ttu-id="bb1b3-152">Obtenha a cadeia de conexão, seguindo as etapas mostradas em [Obter as credenciais de gerenciamento](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="bb1b3-152">You obtain the connection string by following the steps shown at [Obtain the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="bb1b3-153">A cadeia de conexão deve ser voltada para um namespace do Barramento de Serviço, não limitada a uma fila ou tópico específico.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-153">The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.</span></span>
  <span data-ttu-id="bb1b3-154">Se você deixar `connection` vazio, a associação da saída assumirá que uma cadeia de conexão do Barramento de Serviço padrão foi especificada em uma configuração de aplicativo chamada `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-154">If you leave `connection` empty, the output binding assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="bb1b3-155">Para `accessRights`, os valores disponíveis são `manage` e `listen`.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-155">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="bb1b3-156">O padrão é `manage`, que indica que o `connection` tem a permissão **Gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-156">The default is `manage`, which indicates that the `connection` has the **Manage** permission.</span></span> <span data-ttu-id="bb1b3-157">Se você usar uma cadeia de conexão que não tenha a permissão **Gerenciar**, defina `accessRights` como `listen`.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-157">If you use a connection string that does not have the **Manage** permission, set `accessRights` to `listen`.</span></span> <span data-ttu-id="bb1b3-158">Caso contrário, o tempo de execução do Functions talvez falhe ao tentar executar operações que exigem o gerenciamento de direitos.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-158">Otherwise, the Functions runtime might fail trying to do operations that require manage rights.</span></span>

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="bb1b3-159">Uso de saída</span><span class="sxs-lookup"><span data-stu-id="bb1b3-159">Output usage</span></span>
<span data-ttu-id="bb1b3-160">Em C# e F#, o Azure Functions pode criar uma mensagem de fila do Barramento de Serviço a partir de qualquer um dos tipos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bb1b3-160">In C# and F#, Azure Functions can create a Service Bus queue message from any of the following types:</span></span>

* <span data-ttu-id="bb1b3-161">Qualquer [Objeto](https://msdn.microsoft.com/library/system.object.aspx) - A definição do parâmetro se parece com `out T paramName` (C#).</span><span class="sxs-lookup"><span data-stu-id="bb1b3-161">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - Parameter definition looks like `out T paramName` (C#).</span></span>
  <span data-ttu-id="bb1b3-162">O Functions desserializa o objeto em uma mensagem JSON.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-162">Functions deserializes the object into a JSON message.</span></span> <span data-ttu-id="bb1b3-163">Se o valor de saída for nulo quando a função existir, o Functions cria a mensagem com um objeto nulo.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-163">If the output value is null when the function exits, Functions creates the message with a null object.</span></span>
* <span data-ttu-id="bb1b3-164">`string` - A definição de parâmetro se parece com `out string paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="bb1b3-164">`string` - Parameter definition looks like `out string paraName` (C#).</span></span> <span data-ttu-id="bb1b3-165">Se o valor de parâmetro não for nulo quando a função existir, o Functions criará uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-165">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>
* <span data-ttu-id="bb1b3-166">`byte[]` - A definição de parâmetro se parece com `out byte[] paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="bb1b3-166">`byte[]` - Parameter definition looks like `out byte[] paraName` (C#).</span></span> <span data-ttu-id="bb1b3-167">Se o valor de parâmetro não for nulo quando a função existir, o Functions criará uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-167">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>
* <span data-ttu-id="bb1b3-168">`BrokeredMessage` A definição de parâmetro se parece com `out BrokeredMessage paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="bb1b3-168">`BrokeredMessage` Parameter definition looks like `out BrokeredMessage paraName` (C#).</span></span> <span data-ttu-id="bb1b3-169">Se o valor de parâmetro não for nulo quando a função existir, o Functions criará uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-169">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>

<span data-ttu-id="bb1b3-170">Para criar várias mensagens em uma função C#, você pode usar `ICollector<T>` ou `IAsyncCollector<T>`.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-170">For creating multiple messages in a C# function, you can use `ICollector<T>` or `IAsyncCollector<T>`.</span></span> <span data-ttu-id="bb1b3-171">Uma mensagem é criada quando você chama o método `Add` .</span><span class="sxs-lookup"><span data-stu-id="bb1b3-171">A message is created when you call the `Add` method.</span></span>

<span data-ttu-id="bb1b3-172">No Node.js, você pode atribuir uma cadeia de caracteres, uma matriz de bytes ou um objeto Javascript (desserializado em JSON) para `context.binding.<paramName>`.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-172">In Node.js, you can assign a string, a byte array, or a Javascript object (deserialized into JSON) to `context.binding.<paramName>`.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="bb1b3-173">Amostra de saída</span><span class="sxs-lookup"><span data-stu-id="bb1b3-173">Output sample</span></span>
<span data-ttu-id="bb1b3-174">Vamos supor que você tenha o seguinte function.json, que define uma saída de fila do Barramento de Serviço:</span><span class="sxs-lookup"><span data-stu-id="bb1b3-174">Suppose you have the following function.json, that defines a Service Bus queue output:</span></span>

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

<span data-ttu-id="bb1b3-175">Veja o exemplo específico à linguagem que envia uma mensagem à fila do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="bb1b3-175">See the language-specific sample that sends a message to the service bus queue.</span></span>

* [<span data-ttu-id="bb1b3-176">C#</span><span class="sxs-lookup"><span data-stu-id="bb1b3-176">C#</span></span>](#outcsharp)
* [<span data-ttu-id="bb1b3-177">F#</span><span class="sxs-lookup"><span data-stu-id="bb1b3-177">F#</span></span>](#outfsharp)
* [<span data-ttu-id="bb1b3-178">Node.js</span><span class="sxs-lookup"><span data-stu-id="bb1b3-178">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="bb1b3-179">Amostra de saída em C#</span><span class="sxs-lookup"><span data-stu-id="bb1b3-179">Output sample in C#</span></span> #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

<span data-ttu-id="bb1b3-180">Ou, para criar várias mensagens:</span><span class="sxs-lookup"><span data-stu-id="bb1b3-180">Or, to create multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="bb1b3-181">Amostra de saída em F#</span><span class="sxs-lookup"><span data-stu-id="bb1b3-181">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="bb1b3-182">Amostra de saída no Node.js</span><span class="sxs-lookup"><span data-stu-id="bb1b3-182">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

<span data-ttu-id="bb1b3-183">Ou, para criar várias mensagens:</span><span class="sxs-lookup"><span data-stu-id="bb1b3-183">Or, to create multiple messages:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="bb1b3-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bb1b3-184">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

