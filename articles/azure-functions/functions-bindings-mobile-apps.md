---
title: "Associações de Aplicativos Móveis do Azure Functions | Microsoft Docs"
description: "Entenda como usar associações dos Aplicativos Móveis do Azure no Azure Functions."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "azure functions, funções, processamento de eventos, computação dinâmica, arquitetura sem servidor"
ms.assetid: faad1263-0fa5-41a9-964f-aecbc0be706a
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/31/2016
ms.author: glenga
ms.openlocfilehash: c5e1c02984f9773b263c0bee7685c7d5ff62e658
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a><span data-ttu-id="d00a3-104">Associações de Aplicativos Móveis do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="d00a3-104">Azure Functions Mobile Apps bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="d00a3-105">Este artigo explica como configurar e codificar associações dos [Aplicativos Móveis do Azure](../app-service-mobile/app-service-mobile-value-prop.md) no Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="d00a3-105">This article explains how to configure and code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions.</span></span> <span data-ttu-id="d00a3-106">O Azure Functions dá suporte a associações de entrada e saída para os Aplicativos Móveis.</span><span class="sxs-lookup"><span data-stu-id="d00a3-106">Azure Functions supports input and output bindings for Mobile Apps.</span></span>

<span data-ttu-id="d00a3-107">As associações de entrada e saída para os Aplicativos Móveis permitem [ler e gravar em tabelas de dados](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) em seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="d00a3-107">The Mobile Apps input and output bindings let you [read from and write to data tables](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in your mobile app.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a><span data-ttu-id="d00a3-108">Associação de entrada dos Aplicativos Móveis</span><span class="sxs-lookup"><span data-stu-id="d00a3-108">Mobile Apps input binding</span></span>
<span data-ttu-id="d00a3-109">A associação de entrada dos Aplicativos Móveis carrega um registro de um ponto de extremidade de tabela móvel e o passa para a função.</span><span class="sxs-lookup"><span data-stu-id="d00a3-109">The Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function.</span></span> <span data-ttu-id="d00a3-110">Em uma função do C# ou do F#, todas as alterações feitas no registro são enviadas novamente de forma automática para a tabela quando a função é fechada com êxito.</span><span class="sxs-lookup"><span data-stu-id="d00a3-110">In a C# and F# functions, any changes made to the record are automatically sent back to the table when the function exits successfully.</span></span>

<span data-ttu-id="d00a3-111">A entrada dos Aplicativos Móveis de uma função usa o seguinte objeto JSON na matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="d00a3-111">The Mobile Apps input to a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of the record to retrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

<span data-ttu-id="d00a3-112">Observe o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d00a3-112">Note the following:</span></span>

* <span data-ttu-id="d00a3-113">`id` pode ser estático ou se basear no gatilho que invoca a função.</span><span class="sxs-lookup"><span data-stu-id="d00a3-113">`id` can be static, or it can be based on the trigger that invokes the function.</span></span> <span data-ttu-id="d00a3-114">Por exemplo, se você usar um [gatilho da fila]() para sua função, o `"id": "{queueTrigger}"` usará o valor de cadeia de caracteres da mensagem da fila como a ID de registro a ser recuperada.</span><span class="sxs-lookup"><span data-stu-id="d00a3-114">For example, if you use a [queue trigger]() for your function, then `"id": "{queueTrigger}"` uses the string value of the queue message as the record ID to retrieve.</span></span>
* <span data-ttu-id="d00a3-115">`connection` deve conter o nome de uma configuração de aplicativo no aplicativo de funções que, por sua vez, contém a URL do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="d00a3-115">`connection` should contain the name of an app setting in your function app, which in turn contains the URL of your mobile app.</span></span> <span data-ttu-id="d00a3-116">A função usa essa URL para construir as operações REST necessárias no aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="d00a3-116">The function uses this URL to construct the required REST operations against your mobile app.</span></span> <span data-ttu-id="d00a3-117">Você [cria uma configuração de aplicativo no aplicativo de funções]() que contém a URL do aplicativo móvel (que se parece com `http://<appname>.azurewebsites.net`) e especifica o nome da configuração do aplicativo na propriedade `connection` na associação de entrada.</span><span class="sxs-lookup"><span data-stu-id="d00a3-117">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify the name of the app setting in the `connection` property in your input binding.</span></span> 
* <span data-ttu-id="d00a3-118">Você precisará especificar `apiKey` se [implementar uma chave de API no back-end do aplicativo móvel do Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key) ou se [implementar uma chave de API no back-end do aplicativo móvel do .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="d00a3-118">You need to specify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="d00a3-119">Para fazer isso, você [cria uma configuração de aplicativo no aplicativo de funções]() que contém a chave de API e adiciona a propriedade `apiKey` na associação de entrada ao nome da configuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d00a3-119">To do this, you [create an app setting in your function app]() that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="d00a3-120">Essa chave de API não deve ser compartilhada com seus clientes de aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="d00a3-120">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="d00a3-121">Ela só deve ser distribuída com segurança aos clientes do lado do serviço, como o Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="d00a3-121">It should only be distributed securely to service-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="d00a3-122">O Azure Functions armazena suas informações de conexão e as chaves de API como configurações de aplicativo, para que elas não sejam inseridas no repositório de controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="d00a3-122">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="d00a3-123">Isso protege as informações confidenciais.</span><span class="sxs-lookup"><span data-stu-id="d00a3-123">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="d00a3-124">Uso de entrada</span><span class="sxs-lookup"><span data-stu-id="d00a3-124">Input usage</span></span>
<span data-ttu-id="d00a3-125">Esta seção mostra como usar a associação de entrada dos Aplicativos Móveis no código da função.</span><span class="sxs-lookup"><span data-stu-id="d00a3-125">This section shows you how to use your Mobile Apps input binding in your function code.</span></span> 

<span data-ttu-id="d00a3-126">Quando o registro com a tabela e a ID de registro especificadas é encontrado, ele é passado para o parâmetro [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) nomeado (ou, no Node.js, ele é passado para o objeto `context.bindings.<name>`).</span><span class="sxs-lookup"><span data-stu-id="d00a3-126">When the record with the specified table and record ID is found, it is passed into the named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (or, in Node.js, it is passed into the `context.bindings.<name>` object).</span></span> <span data-ttu-id="d00a3-127">Quando o registro não é encontrado, o parâmetro é `null`.</span><span class="sxs-lookup"><span data-stu-id="d00a3-127">When the record is not found, the parameter is `null`.</span></span> 

<span data-ttu-id="d00a3-128">Nas funções do C# ou do F#, todas as alterações feitas no registro de entrada (parâmetro de entrada) são enviadas novamente de forma automática para os Aplicativos Móveis quando a função é fechada com êxito.</span><span class="sxs-lookup"><span data-stu-id="d00a3-128">In C# and F# functions, any changes you make to the input record (input parameter) is automatically sent back to the Mobile Apps table when the function exits successfully.</span></span> <span data-ttu-id="d00a3-129">Nas funções do Node.js, use `context.bindings.<name>` para acessar o registro de entrada.</span><span class="sxs-lookup"><span data-stu-id="d00a3-129">In Node.js functions, use `context.bindings.<name>` to access the input record.</span></span> <span data-ttu-id="d00a3-130">Não é possível modificar um registro no Node.js.</span><span class="sxs-lookup"><span data-stu-id="d00a3-130">You cannot modify a record in Node.js.</span></span>

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="d00a3-131">Amostra de entrada</span><span class="sxs-lookup"><span data-stu-id="d00a3-131">Input sample</span></span>
<span data-ttu-id="d00a3-132">Suponha que você tem o seguinte function.json, que recupera um registro de tabela do Aplicativo Móvel com a ID da mensagem do gatilho da fila:</span><span class="sxs-lookup"><span data-stu-id="d00a3-132">Suppose you have the following function.json, that retrieves a Mobile App table record with the id of the queue trigger message:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
        "name": "record",
        "type": "mobileTable",
        "tableName": "MyTable",
        "id" : "{queueTrigger}",
        "connection": "My_MobileApp_Url",
        "apiKey": "My_MobileApp_Key",
        "direction": "in"
    }
],
"disabled": false
}
```

<span data-ttu-id="d00a3-133">Consulte a amostra específica da linguagem que usa o registro de entrada da associação.</span><span class="sxs-lookup"><span data-stu-id="d00a3-133">See the language-specific sample that uses the input record from the binding.</span></span> <span data-ttu-id="d00a3-134">As amostras do C# e do F# também modificam a propriedade `text` do registro.</span><span class="sxs-lookup"><span data-stu-id="d00a3-134">The C# and F# samples also modify the record's `text` property.</span></span>

* [<span data-ttu-id="d00a3-135">C#</span><span class="sxs-lookup"><span data-stu-id="d00a3-135">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="d00a3-136">Node.js</span><span class="sxs-lookup"><span data-stu-id="d00a3-136">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="d00a3-137">Exemplo de entrada em C#</span><span class="sxs-lookup"><span data-stu-id="d00a3-137">Input sample in C#</span></span> #

```cs
#r "Newtonsoft.Json"    
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, JObject record)
{
    if (record != null)
    {
        record["Text"] = "This has changed.";
    }    
}
```

<!--
<a name="inputfsharp"></a>
### Input sample in F# ## 

```fsharp
#r "Newtonsoft.Json"    
open Newtonsoft.Json.Linq
let Run(myQueueItem: string, record: JObject) =
  inputDocument?text <- "This has changed."
```
-->

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="d00a3-138">Amostra de entrada no Node.js</span><span class="sxs-lookup"><span data-stu-id="d00a3-138">Input sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a><span data-ttu-id="d00a3-139">Associação de saída dos Aplicativos Móveis</span><span class="sxs-lookup"><span data-stu-id="d00a3-139">Mobile Apps output binding</span></span>
<span data-ttu-id="d00a3-140">Use a associação de saída dos Aplicativos Móveis para gravar um novo registro em um ponto de extremidade de tabela dos Aplicativos Móveis.</span><span class="sxs-lookup"><span data-stu-id="d00a3-140">Use the Mobile Apps output binding to write a new record to a Mobile Apps table endpoint.</span></span>  

<span data-ttu-id="d00a3-141">A saída dos Aplicativos Móveis para uma função usa o seguinte objeto JSON na matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="d00a3-141">The Mobile Apps output for a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of output parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "out"
}
```

<span data-ttu-id="d00a3-142">Observe o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d00a3-142">Note the following:</span></span>

* <span data-ttu-id="d00a3-143">`connection` deve conter o nome de uma configuração de aplicativo no aplicativo de funções que, por sua vez, contém a URL do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="d00a3-143">`connection` should contain the name of an app setting in your function app, which in turn contains the URL of your mobile app.</span></span> <span data-ttu-id="d00a3-144">A função usa essa URL para construir as operações REST necessárias no aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="d00a3-144">The function uses this URL to construct the required REST operations against your mobile app.</span></span> <span data-ttu-id="d00a3-145">Você [cria uma configuração de aplicativo no aplicativo de funções]() que contém a URL do aplicativo móvel (que se parece com `http://<appname>.azurewebsites.net`) e especifica o nome da configuração do aplicativo na propriedade `connection` na associação de entrada.</span><span class="sxs-lookup"><span data-stu-id="d00a3-145">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify the name of the app setting in the `connection` property in your input binding.</span></span> 
* <span data-ttu-id="d00a3-146">Você precisará especificar `apiKey` se [implementar uma chave de API no back-end do aplicativo móvel do Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key) ou se [implementar uma chave de API no back-end do aplicativo móvel do .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="d00a3-146">You need to specify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="d00a3-147">Para fazer isso, você [cria uma configuração de aplicativo no aplicativo de funções]() que contém a chave de API e adiciona a propriedade `apiKey` na associação de entrada ao nome da configuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d00a3-147">To do this, you [create an app setting in your function app]() that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="d00a3-148">Essa chave de API não deve ser compartilhada com seus clientes de aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="d00a3-148">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="d00a3-149">Ela só deve ser distribuída com segurança aos clientes do lado do serviço, como o Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="d00a3-149">It should only be distributed securely to service-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="d00a3-150">O Azure Functions armazena suas informações de conexão e as chaves de API como configurações de aplicativo, para que elas não sejam inseridas no repositório de controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="d00a3-150">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="d00a3-151">Isso protege as informações confidenciais.</span><span class="sxs-lookup"><span data-stu-id="d00a3-151">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="d00a3-152">Uso de saída</span><span class="sxs-lookup"><span data-stu-id="d00a3-152">Output usage</span></span>
<span data-ttu-id="d00a3-153">Esta seção mostra como usar a associação de saída dos Aplicativos Móveis no código da função.</span><span class="sxs-lookup"><span data-stu-id="d00a3-153">This section shows you how to use your Mobile Apps output binding in your function code.</span></span> 

<span data-ttu-id="d00a3-154">Nas funções do C#, use um parâmetro de saída nomeado do tipo `out object` para acessar o registro de saída.</span><span class="sxs-lookup"><span data-stu-id="d00a3-154">In C# functions, use a named output parameter of type `out object` to access the output record.</span></span> <span data-ttu-id="d00a3-155">Nas funções do Node.js, use `context.bindings.<name>` para acessar o registro de saída.</span><span class="sxs-lookup"><span data-stu-id="d00a3-155">In Node.js functions, use `context.bindings.<name>` to access the output record.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="d00a3-156">Amostra de saída</span><span class="sxs-lookup"><span data-stu-id="d00a3-156">Output sample</span></span>
<span data-ttu-id="d00a3-157">Suponha que você tem o seguinte function.json, que define um gatilho da fila e uma saída dos Aplicativos Móveis:</span><span class="sxs-lookup"><span data-stu-id="d00a3-157">Suppose you have the following function.json, that defines a queue trigger and a Mobile Apps output:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
    "name": "record",
    "type": "mobileTable",
    "tableName": "MyTable",
    "connection": "My_MobileApp_Url",
    "apiKey": "My_MobileApp_Key",
    "direction": "out"
    }
],
"disabled": false
}
```

<span data-ttu-id="d00a3-158">Consulte a amostra específica da linguagem que cria um registro no ponto de extremidade de tabela dos Aplicativos Móveis com o conteúdo da mensagem da fila.</span><span class="sxs-lookup"><span data-stu-id="d00a3-158">See the language-specific sample that creates a record in the Mobile Apps table endpoint with the content of the queue message.</span></span>

* [<span data-ttu-id="d00a3-159">C#</span><span class="sxs-lookup"><span data-stu-id="d00a3-159">C#</span></span>](#outcsharp)
* [<span data-ttu-id="d00a3-160">Node.js</span><span class="sxs-lookup"><span data-stu-id="d00a3-160">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="d00a3-161">Amostra de saída em C#</span><span class="sxs-lookup"><span data-stu-id="d00a3-161">Output sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, out object record)
{
    record = new {
        Text = $"I'm running in a C# function! {myQueueItem}"
    };
}
```

<!--
<a name="outfsharp"></a>
### Output sample in F# ## 
```fsharp

```
-->
<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="d00a3-162">Amostra de saída no Node.js</span><span class="sxs-lookup"><span data-stu-id="d00a3-162">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="d00a3-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d00a3-163">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

