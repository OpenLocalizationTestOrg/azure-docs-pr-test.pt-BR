---
title: "Associações de armazenamento de filas do Azure Functions | Microsoft Docs"
description: "Entenda como usar gatilhos e associações do Armazenamento do Azure em Azure Functions."
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
ms.openlocfilehash: e007acd75a2210d54f512e2c6698c90919f0fcd2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-queue-storage-bindings"></a><span data-ttu-id="ff981-104">Associações de Armazenamento de Filas do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="ff981-104">Azure Functions Queue Storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="ff981-105">Esse artigo descreve como configurar e codificar associações de armazenamento de filas do Azure no Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ff981-105">This article describes how to configure and code Azure Queue storage bindings in Azure Functions.</span></span> <span data-ttu-id="ff981-106">O Azure Functions dá suporte a associações de gatilho e de saída para filas do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff981-106">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="ff981-107">Para os recursos que estão disponíveis em todas as associações, veja [Gatilhos e conceitos de associações do Azure Functions](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="ff981-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a><span data-ttu-id="ff981-108">Gatilho de armazenamento de filas</span><span class="sxs-lookup"><span data-stu-id="ff981-108">Queue storage trigger</span></span>
<span data-ttu-id="ff981-109">O gatilho do armazenamento de filas do Azure permite que você monitore um armazenamento de fila para novas mensagens e responda a elas.</span><span class="sxs-lookup"><span data-stu-id="ff981-109">The Azure Queue storage trigger enables you to monitor a queue storage for new messages and react to them.</span></span> 

<span data-ttu-id="ff981-110">Defina um gatilho de fila usando a guia **Integrar** no portal do Functions.</span><span class="sxs-lookup"><span data-stu-id="ff981-110">Define a queue trigger using the **Integrate** tab in the Functions portal.</span></span> <span data-ttu-id="ff981-111">O portal cria a seguinte definição na seção **Ligações** de *function.json*:</span><span class="sxs-lookup"><span data-stu-id="ff981-111">The portal creates the following definition in the  **bindings** section of *function.json*:</span></span>

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<The name used to identify the trigger data in your code>",
    "queueName": "<Name of queue to poll>",
    "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="ff981-112">A propriedade `connection` deve conter o nome de uma configuração de aplicativo que contenha uma cadeia de conexão de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ff981-112">The `connection` property must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="ff981-113">No Portal do Azure, o editor padrão na guia **Integrar** define essa configuração de aplicativo para você ao selecionar uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ff981-113">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<span data-ttu-id="ff981-114">[Configurações adicionais](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) podem ser fornecidas em um arquivo host.json para ajustar ainda mais gatilhos de armazenamento de filas.</span><span class="sxs-lookup"><span data-stu-id="ff981-114">Additional settings can be provided in a [host.json file](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) to further fine-tune queue storage triggers.</span></span> <span data-ttu-id="ff981-115">Por exemplo, você pode alterar o intervalo de sondagem de fila no host.json.</span><span class="sxs-lookup"><span data-stu-id="ff981-115">For example, you can change the queue polling interval in host.json.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a><span data-ttu-id="ff981-116">Usando um gatilho de fila</span><span class="sxs-lookup"><span data-stu-id="ff981-116">Using a queue trigger</span></span>
<span data-ttu-id="ff981-117">Em funções do Node.js, acesse os dados da fila usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="ff981-117">In Node.js functions, access the queue data using `context.bindings.<name>`.</span></span>


<span data-ttu-id="ff981-118">Nas funções do .NET, acesse o conteúdo da fila usando um parâmetro de método, como `CloudQueueMessage paramName`.</span><span class="sxs-lookup"><span data-stu-id="ff981-118">In .NET functions, access the queue payload using a method parameter such as `CloudQueueMessage paramName`.</span></span> <span data-ttu-id="ff981-119">Aqui, `paramName` é o valor especificado na [configuração do gatilho](#trigger).</span><span class="sxs-lookup"><span data-stu-id="ff981-119">Here, `paramName` is the value you specified in the [trigger configuration](#trigger).</span></span> <span data-ttu-id="ff981-120">A mensagem da fila pode ser desserializada para qualquer um destes tipos:</span><span class="sxs-lookup"><span data-stu-id="ff981-120">The queue message can be deserialized to any of the following types:</span></span>

* <span data-ttu-id="ff981-121">Objeto POCO.</span><span class="sxs-lookup"><span data-stu-id="ff981-121">POCO object.</span></span> <span data-ttu-id="ff981-122">Use se o conteúdo da fila for um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="ff981-122">Use if the queue payload is a JSON object.</span></span> <span data-ttu-id="ff981-123">O tempo de execução do Functions desserializa o conteúdo no objeto POCO.</span><span class="sxs-lookup"><span data-stu-id="ff981-123">The Functions runtime deserializes the payload into the POCO object.</span></span> 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a><span data-ttu-id="ff981-124">Metadados de gatilho de fila</span><span class="sxs-lookup"><span data-stu-id="ff981-124">Queue trigger metadata</span></span>
<span data-ttu-id="ff981-125">O gatilho de fila fornece várias propriedades de metadados.</span><span class="sxs-lookup"><span data-stu-id="ff981-125">The queue trigger provides several metadata properties.</span></span> <span data-ttu-id="ff981-126">Essas propriedades podem ser usadas como parte de expressões de associação em outras associações ou como parâmetros em seu código.</span><span class="sxs-lookup"><span data-stu-id="ff981-126">These properties can be used as part of binding expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="ff981-127">Os valores têm a mesma semântica que [`CloudQueueMessage`].</span><span class="sxs-lookup"><span data-stu-id="ff981-127">The values have the same semantics as [`CloudQueueMessage`].</span></span>

* <span data-ttu-id="ff981-128">**QueueTrigger** – conteúdo da fila (se for uma cadeia de caracteres válida)</span><span class="sxs-lookup"><span data-stu-id="ff981-128">**QueueTrigger** - queue payload (if a valid string)</span></span>
* <span data-ttu-id="ff981-129">**DequeueCount** – Tipo `int`.</span><span class="sxs-lookup"><span data-stu-id="ff981-129">**DequeueCount** - Type `int`.</span></span> <span data-ttu-id="ff981-130">O número de vezes que essa mensagem foi removida da fila.</span><span class="sxs-lookup"><span data-stu-id="ff981-130">The number of times this message has been dequeued.</span></span>
* <span data-ttu-id="ff981-131">**ExpirationTime** – Tipo `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="ff981-131">**ExpirationTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="ff981-132">A hora em que a mensagem expira.</span><span class="sxs-lookup"><span data-stu-id="ff981-132">The time that the message expires.</span></span>
* <span data-ttu-id="ff981-133">**Id** – Tipo `string`.</span><span class="sxs-lookup"><span data-stu-id="ff981-133">**Id** - Type `string`.</span></span> <span data-ttu-id="ff981-134">ID da mensagem da fila.</span><span class="sxs-lookup"><span data-stu-id="ff981-134">Queue message ID.</span></span>
* <span data-ttu-id="ff981-135">**InsertionTime** – Tipo `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="ff981-135">**InsertionTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="ff981-136">A hora em que a mensagem foi adicionada à fila.</span><span class="sxs-lookup"><span data-stu-id="ff981-136">The time that the message was added to the queue.</span></span>
* <span data-ttu-id="ff981-137">**NextVisibleTime** – Tipo `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="ff981-137">**NextVisibleTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="ff981-138">A hora em que a mensagem estará visível.</span><span class="sxs-lookup"><span data-stu-id="ff981-138">The time that the message will next be visible.</span></span>
* <span data-ttu-id="ff981-139">**PopReceipt** – Tipo `string`.</span><span class="sxs-lookup"><span data-stu-id="ff981-139">**PopReceipt** - Type `string`.</span></span> <span data-ttu-id="ff981-140">Recebimento pop da mensagem.</span><span class="sxs-lookup"><span data-stu-id="ff981-140">The message's pop receipt.</span></span>

<span data-ttu-id="ff981-141">Confira como usar os metadados de fila no [Exemplo de gatilho](#triggersample).</span><span class="sxs-lookup"><span data-stu-id="ff981-141">See how to use the queue metadata in [Trigger sample](#triggersample).</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="ff981-142">Exemplo de gatilho</span><span class="sxs-lookup"><span data-stu-id="ff981-142">Trigger sample</span></span>
<span data-ttu-id="ff981-143">Suponha que você tem o seguinte function.json, que define um gatilho da fila:</span><span class="sxs-lookup"><span data-stu-id="ff981-143">Suppose you have the following function.json that defines a queue trigger:</span></span>

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

<span data-ttu-id="ff981-144">Confira o exemplo específico a um idioma que recupera e registra os metadados da fila.</span><span class="sxs-lookup"><span data-stu-id="ff981-144">See the language-specific sample that retrieves and logs queue metadata.</span></span>

* [<span data-ttu-id="ff981-145">C#</span><span class="sxs-lookup"><span data-stu-id="ff981-145">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="ff981-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="ff981-146">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="ff981-147">Exemplo de gatilho em C#</span><span class="sxs-lookup"><span data-stu-id="ff981-147">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="ff981-148">Exemplo de gatilho em Node.js</span><span class="sxs-lookup"><span data-stu-id="ff981-148">Trigger sample in Node.js</span></span>

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

### <a name="handling-poison-queue-messages"></a><span data-ttu-id="ff981-149">Tratamento de mensagens suspeitas na fila</span><span class="sxs-lookup"><span data-stu-id="ff981-149">Handling poison queue messages</span></span>
<span data-ttu-id="ff981-150">Quando uma função do gatilho de fila falhar, o Azure Functions repetirá essa função até cinco vezes para uma determinada mensagem da fila, incluindo a primeira tentativa.</span><span class="sxs-lookup"><span data-stu-id="ff981-150">When a queue trigger function fails, Azure Functions retries that function up to five times for a given queue message, including the first try.</span></span> <span data-ttu-id="ff981-151">Se todas as cinco tentativas falharem, o tempo de execução das funções adicionará uma mensagem em um armazenamento de filas chamada *&lt;originalqueuename>-poison*.</span><span class="sxs-lookup"><span data-stu-id="ff981-151">If all five attempts fail, the functions runtime adds a message to a queue storage named *&lt;originalqueuename>-poison*.</span></span> <span data-ttu-id="ff981-152">Você pode gravar uma função para processar as mensagens da fila de mensagens suspeitas registrando-as ou enviando uma notificação de que a atenção manual é necessária.</span><span class="sxs-lookup"><span data-stu-id="ff981-152">You can write a function to process messages from the poison queue by logging them or sending a  notification that manual attention is needed.</span></span> 

<span data-ttu-id="ff981-153">Para tratar mensagens suspeitas manualmente, verifique o `dequeueCount` da mensagem da fila (veja [Metadados de gatilho de fila](#meta)).</span><span class="sxs-lookup"><span data-stu-id="ff981-153">To handle poison messages manually, check the `dequeueCount` of the queue message (see [Queue trigger metadata](#meta)).</span></span>

<a name="output"></a>

## <a name="queue-storage-output-binding"></a><span data-ttu-id="ff981-154">Associação de saída de armazenamento de filas</span><span class="sxs-lookup"><span data-stu-id="ff981-154">Queue storage output binding</span></span>
<span data-ttu-id="ff981-155">A associação de saída do armazenamento de filas do Azure permite que você escreva mensagens em uma fila.</span><span class="sxs-lookup"><span data-stu-id="ff981-155">The Azure queue storage output binding enables you to write messages to a queue.</span></span> 

<span data-ttu-id="ff981-156">Defina uma associação de saída de fila usando a guia **Integrar** no portal do Functions.</span><span class="sxs-lookup"><span data-stu-id="ff981-156">Define a queue output binding using the **Integrate** tab in the Functions portal.</span></span> <span data-ttu-id="ff981-157">O portal cria a seguinte definição na seção **Ligações** de *function.json*:</span><span class="sxs-lookup"><span data-stu-id="ff981-157">The portal creates the following definition in the  **bindings** section of *function.json*:</span></span>

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<The name used to identify the trigger data in your code>",
   "queueName": "<Name of queue to write to>",
   "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="ff981-158">A propriedade `connection` deve conter o nome de uma configuração de aplicativo que contenha uma cadeia de conexão de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ff981-158">The `connection` property must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="ff981-159">No Portal do Azure, o editor padrão na guia **Integrar** define essa configuração de aplicativo para você ao selecionar uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ff981-159">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a><span data-ttu-id="ff981-160">Usando uma associação de saída da fila</span><span class="sxs-lookup"><span data-stu-id="ff981-160">Using a queue output binding</span></span>
<span data-ttu-id="ff981-161">Nas funções do Node.js, você acessa a fila de saída usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="ff981-161">In Node.js functions, you access the output queue using `context.bindings.<name>`.</span></span>

<span data-ttu-id="ff981-162">Em funções do .NET, é possível executar a saída para qualquer um dos seguintes tipos.</span><span class="sxs-lookup"><span data-stu-id="ff981-162">In .NET functions, you can output to any of the following types.</span></span> <span data-ttu-id="ff981-163">Quando há um parâmetro de tipo `T`, o `T` deve ser um dos tipos de saída com suporte, como `string` ou um POCO.</span><span class="sxs-lookup"><span data-stu-id="ff981-163">When there is a type parameter `T`, `T` must be one of the supported output types, such as `string` or a POCO.</span></span>

* <span data-ttu-id="ff981-164">`out T` (serializado como JSON)</span><span class="sxs-lookup"><span data-stu-id="ff981-164">`out T` (serialized as JSON)</span></span>
* `out string`
* `out byte[]`
* <span data-ttu-id="ff981-165">`out` [`CloudQueueMessage`]</span><span class="sxs-lookup"><span data-stu-id="ff981-165">`out` [`CloudQueueMessage`]</span></span> 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

<span data-ttu-id="ff981-166">Você também pode usar o tipo de retorno do método como a associação de saída.</span><span class="sxs-lookup"><span data-stu-id="ff981-166">You can also use the method return type as the output binding.</span></span>

<a name="outputsample"></a>

## <a name="queue-output-sample"></a><span data-ttu-id="ff981-167">Amostra de saída da fila</span><span class="sxs-lookup"><span data-stu-id="ff981-167">Queue output sample</span></span>
<span data-ttu-id="ff981-168">O *function.json* a seguir define um gatilho de HTTP com uma associação de saída de fila:</span><span class="sxs-lookup"><span data-stu-id="ff981-168">The following *function.json* defines an HTTP trigger with a queue output binding:</span></span>

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

<span data-ttu-id="ff981-169">Veja a amostra específica do idioma que gera uma mensagem da fila com o conteúdo de HTTP de entrada.</span><span class="sxs-lookup"><span data-stu-id="ff981-169">See the language-specific sample that outputs a queue message with the incoming HTTP payload.</span></span>

* [<span data-ttu-id="ff981-170">C#</span><span class="sxs-lookup"><span data-stu-id="ff981-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="ff981-171">Node.js</span><span class="sxs-lookup"><span data-stu-id="ff981-171">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a><span data-ttu-id="ff981-172">Amostra de saída da fila em C#</span><span class="sxs-lookup"><span data-stu-id="ff981-172">Queue output sample in C#</span></span> #

```cs
// C# example of HTTP trigger binding to a custom POCO, with a queue output binding
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

<span data-ttu-id="ff981-173">Para enviar várias mensagens, use um `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="ff981-173">To send multiple messages, use an `ICollector`:</span></span>

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a><span data-ttu-id="ff981-174">Amostra de saída de fila em Node.js</span><span class="sxs-lookup"><span data-stu-id="ff981-174">Queue output sample in Node.js</span></span>

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

<span data-ttu-id="ff981-175">Ou, para enviar várias mensagens,</span><span class="sxs-lookup"><span data-stu-id="ff981-175">Or, to send multiple messages,</span></span>

```javascript
module.exports = function(context) {
    // Define a message array for the myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="ff981-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ff981-176">Next steps</span></span>

<span data-ttu-id="ff981-177">Para obter um exemplo de uma função que usa gatilhos de armazenamento de fila e associações, veja [Criar um Azure Function conectado a um serviço do Azure](functions-create-an-azure-connected-function.md).</span><span class="sxs-lookup"><span data-stu-id="ff981-177">For an example of a function that uses queue storage triggers and bindings, see [Create an Azure Function connected to an Azure service](functions-create-an-azure-connected-function.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

[`CloudQueueMessage`]: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
