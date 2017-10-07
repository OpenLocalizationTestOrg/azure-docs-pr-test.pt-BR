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
# <a name="azure-functions-queue-storage-bindings"></a><span data-ttu-id="8b8af-104">Associações de Armazenamento de Filas do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="8b8af-104">Azure Functions Queue Storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="8b8af-105">Este artigo descreve como tooconfigure e o código de associações de armazenamento de fila do Azure em funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b8af-105">This article describes how tooconfigure and code Azure Queue storage bindings in Azure Functions.</span></span> <span data-ttu-id="8b8af-106">O Azure Functions dá suporte a associações de gatilho e de saída para filas do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b8af-106">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="8b8af-107">Para os recursos que estão disponíveis em todas as associações, veja [Gatilhos e conceitos de associações do Azure Functions](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="8b8af-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a><span data-ttu-id="8b8af-108">Gatilho de armazenamento de filas</span><span class="sxs-lookup"><span data-stu-id="8b8af-108">Queue storage trigger</span></span>
<span data-ttu-id="8b8af-109">gatilho de armazenamento de fila do Azure Olá permite toomonitor um armazenamento de fila para novas mensagens e reage toothem.</span><span class="sxs-lookup"><span data-stu-id="8b8af-109">hello Azure Queue storage trigger enables you toomonitor a queue storage for new messages and react toothem.</span></span> 

<span data-ttu-id="8b8af-110">Definir um gatilho de fila usando Olá **integrar** no portal de funções hello.</span><span class="sxs-lookup"><span data-stu-id="8b8af-110">Define a queue trigger using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="8b8af-111">Olá, portal cria Olá após a definição no hello **associações** seção *function.json*:</span><span class="sxs-lookup"><span data-stu-id="8b8af-111">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "queueName": "<Name of queue toopoll>",
    "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="8b8af-112">Olá `connection` propriedade deve conter o nome de saudação de uma configuração de aplicativo que contém uma cadeia de caracteres de conexão de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8b8af-112">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="8b8af-113">No portal do Azure de Olá, Olá editor padrão no hello **integrar** guia configura essa definição de aplicativo para você quando você seleciona uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8b8af-113">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<span data-ttu-id="8b8af-114">Configurações adicionais podem ser fornecidas em um [host.json arquivo](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther ajustar gatilhos de armazenamento de fila.</span><span class="sxs-lookup"><span data-stu-id="8b8af-114">Additional settings can be provided in a [host.json file](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther fine-tune queue storage triggers.</span></span> <span data-ttu-id="8b8af-115">Por exemplo, você pode alterar o intervalo de sondagem de fila de saudação em host.json.</span><span class="sxs-lookup"><span data-stu-id="8b8af-115">For example, you can change hello queue polling interval in host.json.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a><span data-ttu-id="8b8af-116">Usando um gatilho de fila</span><span class="sxs-lookup"><span data-stu-id="8b8af-116">Using a queue trigger</span></span>
<span data-ttu-id="8b8af-117">Em funções do Node. js, acessar Olá fila dados usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="8b8af-117">In Node.js functions, access hello queue data using `context.bindings.<name>`.</span></span>


<span data-ttu-id="8b8af-118">Em funções do .NET, acessar a carga de fila hello usando um parâmetro de método como `CloudQueueMessage paramName`.</span><span class="sxs-lookup"><span data-stu-id="8b8af-118">In .NET functions, access hello queue payload using a method parameter such as `CloudQueueMessage paramName`.</span></span> <span data-ttu-id="8b8af-119">Aqui, `paramName` é Olá valor especificado em Olá [configuração do disparador](#trigger).</span><span class="sxs-lookup"><span data-stu-id="8b8af-119">Here, `paramName` is hello value you specified in hello [trigger configuration](#trigger).</span></span> <span data-ttu-id="8b8af-120">mensagem de saudação do fila pode ser desserializado tooany dos seguintes tipos de saudação:</span><span class="sxs-lookup"><span data-stu-id="8b8af-120">hello queue message can be deserialized tooany of hello following types:</span></span>

* <span data-ttu-id="8b8af-121">Objeto POCO.</span><span class="sxs-lookup"><span data-stu-id="8b8af-121">POCO object.</span></span> <span data-ttu-id="8b8af-122">Use se a carga de fila de saudação é um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="8b8af-122">Use if hello queue payload is a JSON object.</span></span> <span data-ttu-id="8b8af-123">tempo de execução de funções Hello desserializa carga Olá no objeto POCO hello.</span><span class="sxs-lookup"><span data-stu-id="8b8af-123">hello Functions runtime deserializes hello payload into hello POCO object.</span></span> 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a><span data-ttu-id="8b8af-124">Metadados de gatilho de fila</span><span class="sxs-lookup"><span data-stu-id="8b8af-124">Queue trigger metadata</span></span>
<span data-ttu-id="8b8af-125">gatilho de fila Olá fornece várias propriedades de metadados.</span><span class="sxs-lookup"><span data-stu-id="8b8af-125">hello queue trigger provides several metadata properties.</span></span> <span data-ttu-id="8b8af-126">Essas propriedades podem ser usadas como parte de expressões de associação em outras associações ou como parâmetros em seu código.</span><span class="sxs-lookup"><span data-stu-id="8b8af-126">These properties can be used as part of binding expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="8b8af-127">valores de saudação têm Olá mesma semântica [ `CloudQueueMessage` ].</span><span class="sxs-lookup"><span data-stu-id="8b8af-127">hello values have hello same semantics as [`CloudQueueMessage`].</span></span>

* <span data-ttu-id="8b8af-128">**QueueTrigger** – conteúdo da fila (se for uma cadeia de caracteres válida)</span><span class="sxs-lookup"><span data-stu-id="8b8af-128">**QueueTrigger** - queue payload (if a valid string)</span></span>
* <span data-ttu-id="8b8af-129">**DequeueCount** – Tipo `int`.</span><span class="sxs-lookup"><span data-stu-id="8b8af-129">**DequeueCount** - Type `int`.</span></span> <span data-ttu-id="8b8af-130">Olá o número de vezes que esta mensagem foi removida da fila.</span><span class="sxs-lookup"><span data-stu-id="8b8af-130">hello number of times this message has been dequeued.</span></span>
* <span data-ttu-id="8b8af-131">**ExpirationTime** – Tipo `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="8b8af-131">**ExpirationTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="8b8af-132">tempo de saudação essa mensagem de saudação expira.</span><span class="sxs-lookup"><span data-stu-id="8b8af-132">hello time that hello message expires.</span></span>
* <span data-ttu-id="8b8af-133">**Id** – Tipo `string`.</span><span class="sxs-lookup"><span data-stu-id="8b8af-133">**Id** - Type `string`.</span></span> <span data-ttu-id="8b8af-134">ID da mensagem da fila.</span><span class="sxs-lookup"><span data-stu-id="8b8af-134">Queue message ID.</span></span>
* <span data-ttu-id="8b8af-135">**InsertionTime** – Tipo `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="8b8af-135">**InsertionTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="8b8af-136">tempo de saudação essa mensagem de saudação foi adicionada toohello fila.</span><span class="sxs-lookup"><span data-stu-id="8b8af-136">hello time that hello message was added toohello queue.</span></span>
* <span data-ttu-id="8b8af-137">**NextVisibleTime** – Tipo `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="8b8af-137">**NextVisibleTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="8b8af-138">tempo de saudação essa mensagem de saudação estará visível.</span><span class="sxs-lookup"><span data-stu-id="8b8af-138">hello time that hello message will next be visible.</span></span>
* <span data-ttu-id="8b8af-139">**PopReceipt** – Tipo `string`.</span><span class="sxs-lookup"><span data-stu-id="8b8af-139">**PopReceipt** - Type `string`.</span></span> <span data-ttu-id="8b8af-140">recebimento de mensagem de saudação pop.</span><span class="sxs-lookup"><span data-stu-id="8b8af-140">hello message's pop receipt.</span></span>

<span data-ttu-id="8b8af-141">Consulte como toouse Olá metadados de fila no [exemplo de gatilho](#triggersample).</span><span class="sxs-lookup"><span data-stu-id="8b8af-141">See how toouse hello queue metadata in [Trigger sample](#triggersample).</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="8b8af-142">Exemplo de gatilho</span><span class="sxs-lookup"><span data-stu-id="8b8af-142">Trigger sample</span></span>
<span data-ttu-id="8b8af-143">Suponha que você tenha Olá function.json que define um gatilho de fila a seguir:</span><span class="sxs-lookup"><span data-stu-id="8b8af-143">Suppose you have hello following function.json that defines a queue trigger:</span></span>

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

<span data-ttu-id="8b8af-144">Consulte Olá específico do idioma exemplo que recupera e metadados de fila de logs.</span><span class="sxs-lookup"><span data-stu-id="8b8af-144">See hello language-specific sample that retrieves and logs queue metadata.</span></span>

* [<span data-ttu-id="8b8af-145">C#</span><span class="sxs-lookup"><span data-stu-id="8b8af-145">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="8b8af-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="8b8af-146">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="8b8af-147">Exemplo de gatilho em C#</span><span class="sxs-lookup"><span data-stu-id="8b8af-147">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="8b8af-148">Exemplo de gatilho em Node.js</span><span class="sxs-lookup"><span data-stu-id="8b8af-148">Trigger sample in Node.js</span></span>

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

### <a name="handling-poison-queue-messages"></a><span data-ttu-id="8b8af-149">Tratamento de mensagens suspeitas na fila</span><span class="sxs-lookup"><span data-stu-id="8b8af-149">Handling poison queue messages</span></span>
<span data-ttu-id="8b8af-150">Quando uma função de gatilho de fila falha, funções do Azure repete essa função backup toofive vezes para uma mensagem de determinada fila, incluindo Olá primeiro tente.</span><span class="sxs-lookup"><span data-stu-id="8b8af-150">When a queue trigger function fails, Azure Functions retries that function up toofive times for a given queue message, including hello first try.</span></span> <span data-ttu-id="8b8af-151">Se todas as cinco tentativas falharem, tempo de execução de funções hello adiciona uma mensagem tooa fila de armazenamento denominado  *&lt;originalqueuename >-suspeitas*.</span><span class="sxs-lookup"><span data-stu-id="8b8af-151">If all five attempts fail, hello functions runtime adds a message tooa queue storage named *&lt;originalqueuename>-poison*.</span></span> <span data-ttu-id="8b8af-152">Você pode escrever uma função tooprocess mensagens da fila de suspeitas Olá registrá-los ou enviar uma notificação que atenção manual é necessária.</span><span class="sxs-lookup"><span data-stu-id="8b8af-152">You can write a function tooprocess messages from hello poison queue by logging them or sending a  notification that manual attention is needed.</span></span> 

<span data-ttu-id="8b8af-153">mensagens suspeitas toohandle verificar manualmente, Olá `dequeueCount` de mensagem da fila de saudação (consulte [metadados de gatilho de fila](#meta)).</span><span class="sxs-lookup"><span data-stu-id="8b8af-153">toohandle poison messages manually, check hello `dequeueCount` of hello queue message (see [Queue trigger metadata](#meta)).</span></span>

<a name="output"></a>

## <a name="queue-storage-output-binding"></a><span data-ttu-id="8b8af-154">Associação de saída de armazenamento de filas</span><span class="sxs-lookup"><span data-stu-id="8b8af-154">Queue storage output binding</span></span>
<span data-ttu-id="8b8af-155">Olá armazenamento de fila do Azure associação permite que a fila tooa toowrite mensagens de saída.</span><span class="sxs-lookup"><span data-stu-id="8b8af-155">hello Azure queue storage output binding enables you toowrite messages tooa queue.</span></span> 

<span data-ttu-id="8b8af-156">Definir uma fila de associação de saída usando Olá **integrar** no portal de funções hello.</span><span class="sxs-lookup"><span data-stu-id="8b8af-156">Define a queue output binding using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="8b8af-157">Olá, portal cria Olá após a definição no hello **associações** seção *function.json*:</span><span class="sxs-lookup"><span data-stu-id="8b8af-157">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<hello name used tooidentify hello trigger data in your code>",
   "queueName": "<Name of queue toowrite to>",
   "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="8b8af-158">Olá `connection` propriedade deve conter o nome de saudação de uma configuração de aplicativo que contém uma cadeia de caracteres de conexão de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8b8af-158">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="8b8af-159">No portal do Azure de Olá, Olá editor padrão no hello **integrar** guia configura essa definição de aplicativo para você quando você seleciona uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8b8af-159">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a><span data-ttu-id="8b8af-160">Usando uma associação de saída da fila</span><span class="sxs-lookup"><span data-stu-id="8b8af-160">Using a queue output binding</span></span>
<span data-ttu-id="8b8af-161">Em funções do Node. js, você acessar a fila de saída de hello usando `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="8b8af-161">In Node.js functions, you access hello output queue using `context.bindings.<name>`.</span></span>

<span data-ttu-id="8b8af-162">Em funções do .NET, você pode dar saída tooany de saudação tipos a seguir.</span><span class="sxs-lookup"><span data-stu-id="8b8af-162">In .NET functions, you can output tooany of hello following types.</span></span> <span data-ttu-id="8b8af-163">Quando há um parâmetro de tipo `T`, `T` deve ser um dos tipos de saída de hello com suporte, como `string` ou um POCO.</span><span class="sxs-lookup"><span data-stu-id="8b8af-163">When there is a type parameter `T`, `T` must be one of hello supported output types, such as `string` or a POCO.</span></span>

* <span data-ttu-id="8b8af-164">`out T` (serializado como JSON)</span><span class="sxs-lookup"><span data-stu-id="8b8af-164">`out T` (serialized as JSON)</span></span>
* `out string`
* `out byte[]`
* <span data-ttu-id="8b8af-165">`out` [`CloudQueueMessage`]</span><span class="sxs-lookup"><span data-stu-id="8b8af-165">`out` [`CloudQueueMessage`]</span></span> 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

<span data-ttu-id="8b8af-166">Você também pode usar o tipo de retorno do método hello como Olá associação de saída.</span><span class="sxs-lookup"><span data-stu-id="8b8af-166">You can also use hello method return type as hello output binding.</span></span>

<a name="outputsample"></a>

## <a name="queue-output-sample"></a><span data-ttu-id="8b8af-167">Amostra de saída da fila</span><span class="sxs-lookup"><span data-stu-id="8b8af-167">Queue output sample</span></span>
<span data-ttu-id="8b8af-168">a seguir Olá *function.json* define um gatilho HTTP com uma fila de associação de saída:</span><span class="sxs-lookup"><span data-stu-id="8b8af-168">hello following *function.json* defines an HTTP trigger with a queue output binding:</span></span>

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

<span data-ttu-id="8b8af-169">Consulte o exemplo de específico do idioma de saudação que gera uma mensagem da fila com carga de HTTP de entrada de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b8af-169">See hello language-specific sample that outputs a queue message with hello incoming HTTP payload.</span></span>

* [<span data-ttu-id="8b8af-170">C#</span><span class="sxs-lookup"><span data-stu-id="8b8af-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="8b8af-171">Node.js</span><span class="sxs-lookup"><span data-stu-id="8b8af-171">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a><span data-ttu-id="8b8af-172">Amostra de saída da fila em C#</span><span class="sxs-lookup"><span data-stu-id="8b8af-172">Queue output sample in C#</span></span> #

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

<span data-ttu-id="8b8af-173">toosend várias mensagens, use uma `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="8b8af-173">toosend multiple messages, use an `ICollector`:</span></span>

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a><span data-ttu-id="8b8af-174">Amostra de saída de fila em Node.js</span><span class="sxs-lookup"><span data-stu-id="8b8af-174">Queue output sample in Node.js</span></span>

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

<span data-ttu-id="8b8af-175">Ou, toosend várias mensagens,</span><span class="sxs-lookup"><span data-stu-id="8b8af-175">Or, toosend multiple messages,</span></span>

```javascript
module.exports = function(context) {
    // Define a message array for hello myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="8b8af-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8b8af-176">Next steps</span></span>

<span data-ttu-id="8b8af-177">Para obter um exemplo de uma função que usa gatilhos de armazenamento de fila e associações, consulte [criar tooan uma função do Azure conectados do serviço do Azure](functions-create-an-azure-connected-function.md).</span><span class="sxs-lookup"><span data-stu-id="8b8af-177">For an example of a function that uses queue storage triggers and bindings, see [Create an Azure Function connected tooan Azure service](functions-create-an-azure-connected-function.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

[`CloudQueueMessage`]: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
