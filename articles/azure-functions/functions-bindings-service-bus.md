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
# <a name="azure-functions-service-bus-bindings"></a><span data-ttu-id="0d75b-104">Associações do Barramento de Serviço do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="0d75b-104">Azure Functions Service Bus bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="0d75b-105">Este artigo explica como tooconfigure e trabalhar com associações do barramento de serviço do Azure em funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d75b-105">This article explains how tooconfigure and work with Azure Service Bus bindings in Azure Functions.</span></span> 

<span data-ttu-id="0d75b-106">O Azure Functions dá suporte a gatilhos e a associações de saída para filas e tópicos do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="0d75b-106">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a><span data-ttu-id="0d75b-107">Gatilho do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="0d75b-107">Service Bus trigger</span></span>
<span data-ttu-id="0d75b-108">Use Olá barramento de serviço gatilho toorespond toomessages de uma fila do barramento de serviço ou um tópico.</span><span class="sxs-lookup"><span data-stu-id="0d75b-108">Use hello Service Bus trigger toorespond toomessages from a Service Bus queue or topic.</span></span> 

<span data-ttu-id="0d75b-109">Olá gatilhos de filas e tópicos do barramento de serviço são definidos por Olá seguintes objetos JSON em Olá `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="0d75b-109">hello Service Bus queue and topic triggers are defined by hello following JSON objects in hello `bindings` array of function.json:</span></span>

* <span data-ttu-id="0d75b-110">Gatilho de *fila*:</span><span class="sxs-lookup"><span data-stu-id="0d75b-110">*queue* trigger:</span></span>

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

* <span data-ttu-id="0d75b-111">Gatilho de *tópico*:</span><span class="sxs-lookup"><span data-stu-id="0d75b-111">*topic* trigger:</span></span>

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

<span data-ttu-id="0d75b-112">Observe o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="0d75b-112">Note hello following:</span></span>

* <span data-ttu-id="0d75b-113">Para `connection`, [criar uma configuração de aplicativo em seu aplicativo de função](functions-how-to-use-azure-function-app-settings.md) que contém o namespace de barramento de serviço do hello conexão cadeia de caracteres tooyour, em seguida, especifique o nome de saudação de configuração do aplicativo hello em Olá `connection` propriedade em seu gatilho.</span><span class="sxs-lookup"><span data-stu-id="0d75b-113">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains hello connection string tooyour Service Bus namespace, then specify hello name of hello app setting in hello `connection` property in your trigger.</span></span> <span data-ttu-id="0d75b-114">Obter cadeia de caracteres de conexão Olá seguindo as etapas Olá mostradas no [obter credenciais de gerenciamento Olá](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="0d75b-114">You obtain hello connection string by following hello steps shown at [Obtain hello management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="0d75b-115">cadeia de caracteres de conexão Olá deve ser para um namespace, fila específica tooa não limitado ou tópico do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="0d75b-115">hello connection string must be for a Service Bus namespace, not limited tooa specific queue or topic.</span></span>
  <span data-ttu-id="0d75b-116">Se você deixar `connection` vazio, gatilho Olá pressupõe que uma cadeia de caracteres de conexão de barramento de serviço padrão é especificada em um aplicativo de configuração nomeada `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="0d75b-116">If you leave `connection` empty, hello trigger assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="0d75b-117">Para `accessRights`, os valores disponíveis são `manage` e `listen`.</span><span class="sxs-lookup"><span data-stu-id="0d75b-117">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="0d75b-118">saudação padrão é `manage`, que indica que Olá `connection` tem Olá **gerenciar** permissão.</span><span class="sxs-lookup"><span data-stu-id="0d75b-118">hello default is `manage`, which indicates that hello `connection` has hello **Manage** permission.</span></span> <span data-ttu-id="0d75b-119">Se você usar uma cadeia de caracteres de conexão que não tenha Olá **gerenciar** conjunto de permissões, `accessRights` muito`listen`.</span><span class="sxs-lookup"><span data-stu-id="0d75b-119">If you use a connection string that does not have hello **Manage** permission, set `accessRights` too`listen`.</span></span> <span data-ttu-id="0d75b-120">Caso contrário, Olá tempo de execução de funções podem falhar tentar toodo as operações que exigem gerenciar direitos.</span><span class="sxs-lookup"><span data-stu-id="0d75b-120">Otherwise, hello Functions runtime might fail trying toodo operations that require manage rights.</span></span>

## <a name="trigger-behavior"></a><span data-ttu-id="0d75b-121">Comportamento do gatilho</span><span class="sxs-lookup"><span data-stu-id="0d75b-121">Trigger behavior</span></span>
* <span data-ttu-id="0d75b-122">**Threading único** - por padrão, os processos de tempo de execução de funções hello várias mensagens simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="0d75b-122">**Single-threading** - By default, hello Functions runtime processes multiple messages concurrently.</span></span> <span data-ttu-id="0d75b-123">toodirect Olá runtime tooprocess apenas uma única fila ou tópico de mensagem por vez, defina `serviceBus.maxConcurrentCalls` too1 na *host.json*.</span><span class="sxs-lookup"><span data-stu-id="0d75b-123">toodirect hello runtime tooprocess only a single queue or topic message at a time, set `serviceBus.maxConcurrentCalls` too1 in *host.json*.</span></span> 
  <span data-ttu-id="0d75b-124">Para obter informações sobre o *host.json*, consulte [Estrutura da pasta](functions-reference.md#folder-structure) e [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="0d75b-124">For information about *host.json*, see [Folder Structure](functions-reference.md#folder-structure) and [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>
* <span data-ttu-id="0d75b-125">**Manipulação de mensagens suspeitas** - o Barramento de Serviço faz seu próprio tratamento de mensagens suspeitas que não pode ser controlado ou definido na configuração ou código do Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="0d75b-125">**Poison message handling** - Service Bus does its own poison message handling, which can't be controlled or configured in Azure Functions configuration or code.</span></span> 
* <span data-ttu-id="0d75b-126">**Comportamento de PeekLock** -tempo de execução de funções hello recebe uma mensagem em [ `PeekLock` modo](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) e chamadas de `Complete` na mensagem de saudação quando função hello concluído com êxito, ou chamadas `Abandon` se hello função falhará.</span><span class="sxs-lookup"><span data-stu-id="0d75b-126">**PeekLock behavior** - hello Functions runtime receives a message in [`PeekLock` mode](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) and calls `Complete` on hello message if hello function finishes successfully, or calls `Abandon` if hello function fails.</span></span> 
  <span data-ttu-id="0d75b-127">Se a função hello executada por mais de saudação `PeekLock` tempo limite de bloqueio de saudação é renovada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0d75b-127">If hello function runs longer than hello `PeekLock` timeout, hello lock is automatically renewed.</span></span>

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="0d75b-128">Uso de gatilho</span><span class="sxs-lookup"><span data-stu-id="0d75b-128">Trigger usage</span></span>
<span data-ttu-id="0d75b-129">Esta seção mostra como toouse o barramento de serviço do disparador no seu código de função.</span><span class="sxs-lookup"><span data-stu-id="0d75b-129">This section shows you how toouse your Service Bus trigger in your function code.</span></span> 

<span data-ttu-id="0d75b-130">Em c# e F #, mensagem de saudação do gatilho de barramento de serviço pode ser desserializado tooany de saudação tipos de entrada a seguir:</span><span class="sxs-lookup"><span data-stu-id="0d75b-130">In C# and F#, hello Service Bus trigger message can be deserialized tooany of hello following input types:</span></span>

* <span data-ttu-id="0d75b-131">`string` - útil para mensagens de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0d75b-131">`string` - useful for string messages</span></span>
* <span data-ttu-id="0d75b-132">`byte[]` - útil para dados binários</span><span class="sxs-lookup"><span data-stu-id="0d75b-132">`byte[]` - useful for binary data</span></span>
* <span data-ttu-id="0d75b-133">Qualquer [Objeto](https://msdn.microsoft.com/library/system.object.aspx) - útil para dados JSON serializados.</span><span class="sxs-lookup"><span data-stu-id="0d75b-133">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized data.</span></span>
  <span data-ttu-id="0d75b-134">Se você declarar um tipo de entrada personalizado, como `CustomType`, funções do Azure tenta dados do toodeserialize Olá JSON para o tipo especificado.</span><span class="sxs-lookup"><span data-stu-id="0d75b-134">If you declare a custom input type, such as `CustomType`, Azure Functions tries toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="0d75b-135">`BrokeredMessage`-permite que você Olá desserializado mensagem de saudação [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) método.</span><span class="sxs-lookup"><span data-stu-id="0d75b-135">`BrokeredMessage` - gives you hello deserialized message with hello [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) method.</span></span>

<span data-ttu-id="0d75b-136">No Node. js, mensagem de saudação do gatilho de barramento de serviço é passada para a função hello como uma cadeia de caracteres ou um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="0d75b-136">In Node.js, hello Service Bus trigger message is passed into hello function as either a string or JSON object.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="0d75b-137">Exemplo de gatilho</span><span class="sxs-lookup"><span data-stu-id="0d75b-137">Trigger sample</span></span>
<span data-ttu-id="0d75b-138">Suponha que você tenha Olá function.json a seguir:</span><span class="sxs-lookup"><span data-stu-id="0d75b-138">Suppose you have hello following function.json:</span></span>

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

<span data-ttu-id="0d75b-139">Consulte exemplo específico do idioma hello que processa uma mensagem da fila de barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="0d75b-139">See hello language-specific sample that processes a Service Bus queue message.</span></span>

* [<span data-ttu-id="0d75b-140">C#</span><span class="sxs-lookup"><span data-stu-id="0d75b-140">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="0d75b-141">F#</span><span class="sxs-lookup"><span data-stu-id="0d75b-141">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="0d75b-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="0d75b-142">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="0d75b-143">Exemplo de gatilho em C#</span><span class="sxs-lookup"><span data-stu-id="0d75b-143">Trigger sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="0d75b-144">Exemplo de gatilho em F#</span><span class="sxs-lookup"><span data-stu-id="0d75b-144">Trigger sample in F#</span></span> #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="0d75b-145">Exemplo de gatilho em Node.js</span><span class="sxs-lookup"><span data-stu-id="0d75b-145">Trigger sample in Node.js</span></span>

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a><span data-ttu-id="0d75b-146">Associação de saída do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="0d75b-146">Service Bus output binding</span></span>
<span data-ttu-id="0d75b-147">Olá saída de filas e tópicos do barramento de serviço para uma função usar Olá seguintes objetos JSON em Olá `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="0d75b-147">hello Service Bus queue and topic output for a function use hello following JSON objects in hello `bindings` array of function.json:</span></span>

* <span data-ttu-id="0d75b-148">Saída da *fila*:</span><span class="sxs-lookup"><span data-stu-id="0d75b-148">*queue* output:</span></span>

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
* <span data-ttu-id="0d75b-149">Saída do *tópico*:</span><span class="sxs-lookup"><span data-stu-id="0d75b-149">*topic* output:</span></span>

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

<span data-ttu-id="0d75b-150">Observe o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="0d75b-150">Note hello following:</span></span>

* <span data-ttu-id="0d75b-151">Para `connection`, [criar uma configuração de aplicativo em seu aplicativo de função](functions-how-to-use-azure-function-app-settings.md) que contém o namespace de barramento de serviço do hello conexão cadeia de caracteres tooyour, em seguida, especifique o nome de saudação de configuração do aplicativo hello em Olá `connection` propriedade na saída associação.</span><span class="sxs-lookup"><span data-stu-id="0d75b-151">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains hello connection string tooyour Service Bus namespace, then specify hello name of hello app setting in hello `connection` property in your output binding.</span></span> <span data-ttu-id="0d75b-152">Obter cadeia de caracteres de conexão Olá seguindo as etapas Olá mostradas no [obter credenciais de gerenciamento Olá](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="0d75b-152">You obtain hello connection string by following hello steps shown at [Obtain hello management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="0d75b-153">cadeia de caracteres de conexão Olá deve ser para um namespace, fila específica tooa não limitado ou tópico do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="0d75b-153">hello connection string must be for a Service Bus namespace, not limited tooa specific queue or topic.</span></span>
  <span data-ttu-id="0d75b-154">Se você deixar `connection` vazio, hello associação de saída pressupõe que uma cadeia de caracteres de conexão de barramento de serviço padrão é especificada em um aplicativo de configuração nomeada `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="0d75b-154">If you leave `connection` empty, hello output binding assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="0d75b-155">Para `accessRights`, os valores disponíveis são `manage` e `listen`.</span><span class="sxs-lookup"><span data-stu-id="0d75b-155">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="0d75b-156">saudação padrão é `manage`, que indica que Olá `connection` tem Olá **gerenciar** permissão.</span><span class="sxs-lookup"><span data-stu-id="0d75b-156">hello default is `manage`, which indicates that hello `connection` has hello **Manage** permission.</span></span> <span data-ttu-id="0d75b-157">Se você usar uma cadeia de caracteres de conexão que não tenha Olá **gerenciar** conjunto de permissões, `accessRights` muito`listen`.</span><span class="sxs-lookup"><span data-stu-id="0d75b-157">If you use a connection string that does not have hello **Manage** permission, set `accessRights` too`listen`.</span></span> <span data-ttu-id="0d75b-158">Caso contrário, Olá tempo de execução de funções podem falhar tentar toodo as operações que exigem gerenciar direitos.</span><span class="sxs-lookup"><span data-stu-id="0d75b-158">Otherwise, hello Functions runtime might fail trying toodo operations that require manage rights.</span></span>

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="0d75b-159">Uso de saída</span><span class="sxs-lookup"><span data-stu-id="0d75b-159">Output usage</span></span>
<span data-ttu-id="0d75b-160">Em c# e F #, funções do Azure pode criar uma mensagem de fila do barramento de serviço de qualquer um dos seguintes tipos de saudação:</span><span class="sxs-lookup"><span data-stu-id="0d75b-160">In C# and F#, Azure Functions can create a Service Bus queue message from any of hello following types:</span></span>

* <span data-ttu-id="0d75b-161">Qualquer [Objeto](https://msdn.microsoft.com/library/system.object.aspx) - A definição do parâmetro se parece com `out T paramName` (C#).</span><span class="sxs-lookup"><span data-stu-id="0d75b-161">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - Parameter definition looks like `out T paramName` (C#).</span></span>
  <span data-ttu-id="0d75b-162">Funções desserializa o objeto Olá em uma mensagem JSON.</span><span class="sxs-lookup"><span data-stu-id="0d75b-162">Functions deserializes hello object into a JSON message.</span></span> <span data-ttu-id="0d75b-163">Se o valor de saída de saudação é nulo quando Olá função for encerrada, funções cria a mensagem de saudação com um objeto nulo.</span><span class="sxs-lookup"><span data-stu-id="0d75b-163">If hello output value is null when hello function exits, Functions creates hello message with a null object.</span></span>
* <span data-ttu-id="0d75b-164">`string` - A definição de parâmetro se parece com `out string paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="0d75b-164">`string` - Parameter definition looks like `out string paraName` (C#).</span></span> <span data-ttu-id="0d75b-165">Se o valor do parâmetro hello for não nulo quando Olá função for encerrada, funções cria uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="0d75b-165">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>
* <span data-ttu-id="0d75b-166">`byte[]` - A definição de parâmetro se parece com `out byte[] paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="0d75b-166">`byte[]` - Parameter definition looks like `out byte[] paraName` (C#).</span></span> <span data-ttu-id="0d75b-167">Se o valor do parâmetro hello for não nulo quando Olá função for encerrada, funções cria uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="0d75b-167">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>
* <span data-ttu-id="0d75b-168">`BrokeredMessage` A definição de parâmetro se parece com `out BrokeredMessage paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="0d75b-168">`BrokeredMessage` Parameter definition looks like `out BrokeredMessage paraName` (C#).</span></span> <span data-ttu-id="0d75b-169">Se o valor do parâmetro hello for não nulo quando Olá função for encerrada, funções cria uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="0d75b-169">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>

<span data-ttu-id="0d75b-170">Para criar várias mensagens em uma função C#, você pode usar `ICollector<T>` ou `IAsyncCollector<T>`.</span><span class="sxs-lookup"><span data-stu-id="0d75b-170">For creating multiple messages in a C# function, you can use `ICollector<T>` or `IAsyncCollector<T>`.</span></span> <span data-ttu-id="0d75b-171">Uma mensagem é criada quando você chamar hello `Add` método.</span><span class="sxs-lookup"><span data-stu-id="0d75b-171">A message is created when you call hello `Add` method.</span></span>

<span data-ttu-id="0d75b-172">Node. js, você pode atribuir uma cadeia de caracteres, uma matriz de bytes ou um objeto de Javascript (desserializado em JSON) muito`context.binding.<paramName>`.</span><span class="sxs-lookup"><span data-stu-id="0d75b-172">In Node.js, you can assign a string, a byte array, or a Javascript object (deserialized into JSON) too`context.binding.<paramName>`.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="0d75b-173">Amostra de saída</span><span class="sxs-lookup"><span data-stu-id="0d75b-173">Output sample</span></span>
<span data-ttu-id="0d75b-174">Suponha que você tenha Olá function.json, que define uma saída de fila do barramento de serviço a seguir:</span><span class="sxs-lookup"><span data-stu-id="0d75b-174">Suppose you have hello following function.json, that defines a Service Bus queue output:</span></span>

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

<span data-ttu-id="0d75b-175">Consulte Olá específico do idioma exemplo envia uma fila de mensagem toohello service bus.</span><span class="sxs-lookup"><span data-stu-id="0d75b-175">See hello language-specific sample that sends a message toohello service bus queue.</span></span>

* [<span data-ttu-id="0d75b-176">C#</span><span class="sxs-lookup"><span data-stu-id="0d75b-176">C#</span></span>](#outcsharp)
* [<span data-ttu-id="0d75b-177">F#</span><span class="sxs-lookup"><span data-stu-id="0d75b-177">F#</span></span>](#outfsharp)
* [<span data-ttu-id="0d75b-178">Node.js</span><span class="sxs-lookup"><span data-stu-id="0d75b-178">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="0d75b-179">Amostra de saída em C#</span><span class="sxs-lookup"><span data-stu-id="0d75b-179">Output sample in C#</span></span> #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

<span data-ttu-id="0d75b-180">Ou, toocreate várias mensagens:</span><span class="sxs-lookup"><span data-stu-id="0d75b-180">Or, toocreate multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="0d75b-181">Amostra de saída em F#</span><span class="sxs-lookup"><span data-stu-id="0d75b-181">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="0d75b-182">Amostra de saída no Node.js</span><span class="sxs-lookup"><span data-stu-id="0d75b-182">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

<span data-ttu-id="0d75b-183">Ou, toocreate várias mensagens:</span><span class="sxs-lookup"><span data-stu-id="0d75b-183">Or, toocreate multiple messages:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0d75b-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0d75b-184">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

