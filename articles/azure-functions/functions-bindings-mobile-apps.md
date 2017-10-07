---
title: "associações de aplicativos móveis de funções aaaAzure | Microsoft Docs"
description: "Entender como associações de aplicativos do Azure Mobile toouse em funções do Azure."
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
ms.openlocfilehash: d3679a5d5c66705b32e422ec17e3a1e6d6ac063c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a><span data-ttu-id="1d5ba-104">Associações de Aplicativos Móveis do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="1d5ba-104">Azure Functions Mobile Apps bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="1d5ba-105">Este artigo explica como tooconfigure e código [aplicativos móveis do Azure](../app-service-mobile/app-service-mobile-value-prop.md) associações em funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-105">This article explains how tooconfigure and code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions.</span></span> <span data-ttu-id="1d5ba-106">O Azure Functions dá suporte a associações de entrada e saída para os Aplicativos Móveis.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-106">Azure Functions supports input and output bindings for Mobile Apps.</span></span>

<span data-ttu-id="1d5ba-107">Hello aplicativos móveis de entrada e saída associações permitem [de leitura e gravação tabelas toodata](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) em seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-107">hello Mobile Apps input and output bindings let you [read from and write toodata tables](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in your mobile app.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a><span data-ttu-id="1d5ba-108">Associação de entrada dos Aplicativos Móveis</span><span class="sxs-lookup"><span data-stu-id="1d5ba-108">Mobile Apps input binding</span></span>
<span data-ttu-id="1d5ba-109">Olá associação de entrada de aplicativos móveis carrega um registro de um ponto de extremidade móvel de tabela e o transmite para sua função.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-109">hello Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function.</span></span> <span data-ttu-id="1d5ba-110">Em c# e F # funções, qualquer registro de toohello as alterações feitas serão enviados automaticamente toohello back tabela quando a função hello encerrada com êxito.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-110">In a C# and F# functions, any changes made toohello record are automatically sent back toohello table when hello function exits successfully.</span></span>

<span data-ttu-id="1d5ba-111">função tooa usa Olá seguinte objeto JSON na saudação de entrada Hello aplicativos móveis `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="1d5ba-111">hello Mobile Apps input tooa function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of hello record tooretrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

<span data-ttu-id="1d5ba-112">Observe o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="1d5ba-112">Note hello following:</span></span>

* <span data-ttu-id="1d5ba-113">`id`pode ser estático, ou ele pode ser baseado em gatilho Olá que invoca a função hello.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-113">`id` can be static, or it can be based on hello trigger that invokes hello function.</span></span> <span data-ttu-id="1d5ba-114">Por exemplo, se você usar um [gatilho fila]() para sua função, em seguida, `"id": "{queueTrigger}"` usa Olá valor de cadeia de caracteres de mensagem da fila de saudação como Olá tooretrieve de ID de registro.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-114">For example, if you use a [queue trigger]() for your function, then `"id": "{queueTrigger}"` uses hello string value of hello queue message as hello record ID tooretrieve.</span></span>
* <span data-ttu-id="1d5ba-115">`connection`deve conter o nome de saudação de uma configuração de aplicativo em seu aplicativo de função, que por sua vez, contém Olá URL do seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-115">`connection` should contain hello name of an app setting in your function app, which in turn contains hello URL of your mobile app.</span></span> <span data-ttu-id="1d5ba-116">função Hello usa operações REST URL tooconstruct Olá necessárias em relação a seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-116">hello function uses this URL tooconstruct hello required REST operations against your mobile app.</span></span> <span data-ttu-id="1d5ba-117">Você [criar uma configuração de aplicativo em seu aplicativo de função]() que contém a URL do seu aplicativo móvel (que se parece com `http://<appname>.azurewebsites.net`), em seguida, especifique o nome de saudação de configuração do aplicativo hello no hello `connection` propriedade na associação de entrada.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-117">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify hello name of hello app setting in hello `connection` property in your input binding.</span></span> 
* <span data-ttu-id="1d5ba-118">Você precisa toospecify `apiKey` se você [implementar uma chave de API em seu back-end de aplicativo móvel Node. js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), ou [implementar uma chave de API em seu back-end de aplicativo móvel .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="1d5ba-118">You need toospecify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="1d5ba-119">toodo isso, você [criar uma configuração de aplicativo em seu aplicativo de função]() que contém a chave de API de saudação, em seguida, adicione Olá `apiKey` propriedade em sua associação de entrada com o nome da saudação de configuração do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-119">toodo this, you [create an app setting in your function app]() that contains hello API key, then add hello `apiKey` property in your input binding with hello name of hello app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="1d5ba-120">Essa chave de API não deve ser compartilhada com seus clientes de aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-120">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="1d5ba-121">Ele deve ser apenas clientes distribuídos do lado do tooservice com segurança, como funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-121">It should only be distributed securely tooservice-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="1d5ba-122">O Azure Functions armazena suas informações de conexão e as chaves de API como configurações de aplicativo, para que elas não sejam inseridas no repositório de controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-122">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="1d5ba-123">Isso protege as informações confidenciais.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-123">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="1d5ba-124">Uso de entrada</span><span class="sxs-lookup"><span data-stu-id="1d5ba-124">Input usage</span></span>
<span data-ttu-id="1d5ba-125">Esta seção mostra como toouse seus aplicativos móveis de entrada em seu código de função de associação.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-125">This section shows you how toouse your Mobile Apps input binding in your function code.</span></span> 

<span data-ttu-id="1d5ba-126">Quando registro Olá com hello especificado ID de tabela e o registro for encontrado, ele é passado para Olá denominado [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parâmetro (ou, no Node. js, que é transmitido Olá `context.bindings.<name>` objeto).</span><span class="sxs-lookup"><span data-stu-id="1d5ba-126">When hello record with hello specified table and record ID is found, it is passed into hello named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (or, in Node.js, it is passed into hello `context.bindings.<name>` object).</span></span> <span data-ttu-id="1d5ba-127">Quando o registro de saudação não for encontrado, parâmetro hello é `null`.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-127">When hello record is not found, hello parameter is `null`.</span></span> 

<span data-ttu-id="1d5ba-128">Em c# e F # funções, as alterações feitas toohello entrada do registro (parâmetro de entrada) é enviado automaticamente back toohello tabela de aplicativos móveis quando a função hello encerrada com êxito.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-128">In C# and F# functions, any changes you make toohello input record (input parameter) is automatically sent back toohello Mobile Apps table when hello function exits successfully.</span></span> <span data-ttu-id="1d5ba-129">Em funções do Node. js, use `context.bindings.<name>` tooaccess Olá registro de entrada.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-129">In Node.js functions, use `context.bindings.<name>` tooaccess hello input record.</span></span> <span data-ttu-id="1d5ba-130">Não é possível modificar um registro no Node.js.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-130">You cannot modify a record in Node.js.</span></span>

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="1d5ba-131">Amostra de entrada</span><span class="sxs-lookup"><span data-stu-id="1d5ba-131">Input sample</span></span>
<span data-ttu-id="1d5ba-132">Suponha que você tenha Olá function.json a seguir, que recupera um registro da tabela de aplicativos móveis com a id de saudação da mensagem de saudação do gatilho de fila:</span><span class="sxs-lookup"><span data-stu-id="1d5ba-132">Suppose you have hello following function.json, that retrieves a Mobile App table record with hello id of hello queue trigger message:</span></span>

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

<span data-ttu-id="1d5ba-133">Consulte Olá específico do idioma exemplo que usa o registro de entrada hello da associação de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-133">See hello language-specific sample that uses hello input record from hello binding.</span></span> <span data-ttu-id="1d5ba-134">exemplos de c# e F # Olá também modificam do registro Olá `text` propriedade.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-134">hello C# and F# samples also modify hello record's `text` property.</span></span>

* [<span data-ttu-id="1d5ba-135">C#</span><span class="sxs-lookup"><span data-stu-id="1d5ba-135">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="1d5ba-136">Node.js</span><span class="sxs-lookup"><span data-stu-id="1d5ba-136">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="1d5ba-137">Exemplo de entrada em C#</span><span class="sxs-lookup"><span data-stu-id="1d5ba-137">Input sample in C#</span></span> #

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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="1d5ba-138">Amostra de entrada no Node.js</span><span class="sxs-lookup"><span data-stu-id="1d5ba-138">Input sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a><span data-ttu-id="1d5ba-139">Associação de saída dos Aplicativos Móveis</span><span class="sxs-lookup"><span data-stu-id="1d5ba-139">Mobile Apps output binding</span></span>
<span data-ttu-id="1d5ba-140">Use Olá aplicativos móveis saída associação toowrite um ponto de extremidade de tabela de aplicativos móveis tooa registro novo.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-140">Use hello Mobile Apps output binding toowrite a new record tooa Mobile Apps table endpoint.</span></span>  

<span data-ttu-id="1d5ba-141">Olá aplicativos móveis de saída para uma função usa Olá seguinte objeto JSON na Olá `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="1d5ba-141">hello Mobile Apps output for a function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="1d5ba-142">Observe o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="1d5ba-142">Note hello following:</span></span>

* <span data-ttu-id="1d5ba-143">`connection`deve conter o nome de saudação de uma configuração de aplicativo em seu aplicativo de função, que por sua vez, contém Olá URL do seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-143">`connection` should contain hello name of an app setting in your function app, which in turn contains hello URL of your mobile app.</span></span> <span data-ttu-id="1d5ba-144">função Hello usa operações REST URL tooconstruct Olá necessárias em relação a seu aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-144">hello function uses this URL tooconstruct hello required REST operations against your mobile app.</span></span> <span data-ttu-id="1d5ba-145">Você [criar uma configuração de aplicativo em seu aplicativo de função]() que contém a URL do seu aplicativo móvel (que se parece com `http://<appname>.azurewebsites.net`), em seguida, especifique o nome de saudação de configuração do aplicativo hello no hello `connection` propriedade na associação de entrada.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-145">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify hello name of hello app setting in hello `connection` property in your input binding.</span></span> 
* <span data-ttu-id="1d5ba-146">Você precisa toospecify `apiKey` se você [implementar uma chave de API em seu back-end de aplicativo móvel Node. js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), ou [implementar uma chave de API em seu back-end de aplicativo móvel .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="1d5ba-146">You need toospecify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="1d5ba-147">toodo isso, você [criar uma configuração de aplicativo em seu aplicativo de função]() que contém a chave de API de saudação, em seguida, adicione Olá `apiKey` propriedade em sua associação de entrada com o nome da saudação de configuração do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-147">toodo this, you [create an app setting in your function app]() that contains hello API key, then add hello `apiKey` property in your input binding with hello name of hello app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="1d5ba-148">Essa chave de API não deve ser compartilhada com seus clientes de aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-148">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="1d5ba-149">Ele deve ser apenas clientes distribuídos do lado do tooservice com segurança, como funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-149">It should only be distributed securely tooservice-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="1d5ba-150">O Azure Functions armazena suas informações de conexão e as chaves de API como configurações de aplicativo, para que elas não sejam inseridas no repositório de controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-150">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="1d5ba-151">Isso protege as informações confidenciais.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-151">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="1d5ba-152">Uso de saída</span><span class="sxs-lookup"><span data-stu-id="1d5ba-152">Output usage</span></span>
<span data-ttu-id="1d5ba-153">Esta seção mostra como toouse seus aplicativos móveis de saída de associação no seu código de função.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-153">This section shows you how toouse your Mobile Apps output binding in your function code.</span></span> 

<span data-ttu-id="1d5ba-154">Em c# funções, use um parâmetro de saída nomeado do tipo `out object` tooaccess Olá registro de saída.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-154">In C# functions, use a named output parameter of type `out object` tooaccess hello output record.</span></span> <span data-ttu-id="1d5ba-155">Em funções do Node. js, use `context.bindings.<name>` tooaccess Olá registro de saída.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-155">In Node.js functions, use `context.bindings.<name>` tooaccess hello output record.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="1d5ba-156">Amostra de saída</span><span class="sxs-lookup"><span data-stu-id="1d5ba-156">Output sample</span></span>
<span data-ttu-id="1d5ba-157">Suponha que você tenha Olá function.json a seguir, que define um gatilho de fila e uma saída de aplicativos móveis:</span><span class="sxs-lookup"><span data-stu-id="1d5ba-157">Suppose you have hello following function.json, that defines a queue trigger and a Mobile Apps output:</span></span>

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

<span data-ttu-id="1d5ba-158">Consulte Olá específico do idioma exemplo que cria um registro no ponto de extremidade de tabela de aplicativos móveis a saudação com conteúdo de saudação de mensagem da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="1d5ba-158">See hello language-specific sample that creates a record in hello Mobile Apps table endpoint with hello content of hello queue message.</span></span>

* [<span data-ttu-id="1d5ba-159">C#</span><span class="sxs-lookup"><span data-stu-id="1d5ba-159">C#</span></span>](#outcsharp)
* [<span data-ttu-id="1d5ba-160">Node.js</span><span class="sxs-lookup"><span data-stu-id="1d5ba-160">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="1d5ba-161">Amostra de saída em C#</span><span class="sxs-lookup"><span data-stu-id="1d5ba-161">Output sample in C#</span></span> #

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

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="1d5ba-162">Amostra de saída no Node.js</span><span class="sxs-lookup"><span data-stu-id="1d5ba-162">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="1d5ba-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1d5ba-163">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

