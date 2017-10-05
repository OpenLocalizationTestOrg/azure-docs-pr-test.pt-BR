---
title: "Referência do desenvolvedor de JavaScript do Azure Functions | Microsoft Docs"
description: "Entenda como desenvolver funções usando JavaScript."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, functions, processamento de eventos, webhooks, computação dinâmica, arquitetura sem servidor"
ms.assetid: 45dedd78-3ff9-411f-bb4b-16d29a11384c
ms.service: functions
ms.devlang: nodejs
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: 7ea81ed47f391fbce1432c2b11ac176ab6c04ae0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-javascript-developer-guide"></a><span data-ttu-id="21b8e-104">Guia do desenvolvedor de JavaScript do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="21b8e-104">Azure Functions JavaScript developer guide</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="21b8e-105">Script C#</span><span class="sxs-lookup"><span data-stu-id="21b8e-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="21b8e-106">Script em F#</span><span class="sxs-lookup"><span data-stu-id="21b8e-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="21b8e-107">JavaScript</span><span class="sxs-lookup"><span data-stu-id="21b8e-107">JavaScript</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="21b8e-108">A experiência de JavaScript para o Azure Functions torna mais fácil exportar uma função que é passada como um objeto `context` para se comunicar com o tempo de execução e para receber e enviar dados por meio de associações.</span><span class="sxs-lookup"><span data-stu-id="21b8e-108">The JavaScript experience for Azure Functions makes it easy to export a function, which is passed as a `context` object for communicating with the runtime and for receiving and sending data via bindings.</span></span>

<span data-ttu-id="21b8e-109">Este artigo pressupõe que você já tenha lido a [referência do desenvolvedor do Azure Functions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="21b8e-109">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="exporting-a-function"></a><span data-ttu-id="21b8e-110">Exportando uma função</span><span class="sxs-lookup"><span data-stu-id="21b8e-110">Exporting a function</span></span>
<span data-ttu-id="21b8e-111">Todas as funções JavaScript devem exportar uma única `function` via `module.exports` para o tempo de execução localizar a função e executá-la.</span><span class="sxs-lookup"><span data-stu-id="21b8e-111">All JavaScript functions must export a single `function` via `module.exports` for the runtime to find the function and run it.</span></span> <span data-ttu-id="21b8e-112">Esta função sempre deve incluir um objeto `context` .</span><span class="sxs-lookup"><span data-stu-id="21b8e-112">This function must always include a `context` object.</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by the arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

<span data-ttu-id="21b8e-113">As associações de `direction === "in"` são passadas como argumentos de função, o que significa que você pode usar [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) para lidar dinamicamente com novas entradas (por exemplo, usando `arguments.length` para iterar por todas as suas entradas).</span><span class="sxs-lookup"><span data-stu-id="21b8e-113">Bindings of `direction === "in"` are passed along as function arguments, which means that you can use [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) to dynamically handle new inputs (for example, by using `arguments.length` to iterate over all your inputs).</span></span> <span data-ttu-id="21b8e-114">Essa funcionalidade é conveniente quando você tem apenas um gatilho e nenhuma entrada adicional, pois é possível acessar seus dados de gatilho de maneira previsível, sem fazer referência ao objeto `context`.</span><span class="sxs-lookup"><span data-stu-id="21b8e-114">This functionality is convenient when you have only a trigger and no additional inputs, because you can predictably access your trigger data without referencing your `context` object.</span></span>

<span data-ttu-id="21b8e-115">Os argumentos sempre são passados para a função na ordem em que ocorrem em *function.json*, mesmo se você não especificá-los na sua instrução de exportações.</span><span class="sxs-lookup"><span data-stu-id="21b8e-115">The arguments are always passed along to the function in the order in which they occur in *function.json*, even if you don't specify them in your exports statement.</span></span> <span data-ttu-id="21b8e-116">Por exemplo, se tiver `function(context, a, b)` e alterá-lo para `function(context, a)`, você ainda poderá obter o valor de `b` no código de função, fazendo referência ao `arguments[3]`.</span><span class="sxs-lookup"><span data-stu-id="21b8e-116">For example, if you have `function(context, a, b)` and change it to `function(context, a)`, you can still get the value of `b` in function code by referring to `arguments[3]`.</span></span>

<span data-ttu-id="21b8e-117">Todas as associações, independentemente da direção, também são transmitidas por todo o objeto `context` (veja o script a seguir).</span><span class="sxs-lookup"><span data-stu-id="21b8e-117">All bindings, regardless of direction, are also passed along on the `context` object (see the following script).</span></span> 

## <a name="context-object"></a><span data-ttu-id="21b8e-118">objeto de contexto</span><span class="sxs-lookup"><span data-stu-id="21b8e-118">context object</span></span>
<span data-ttu-id="21b8e-119">O tempo de execução usa um objeto `context` para passar dados de/para sua função e permitir que você se comunique com o tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="21b8e-119">The runtime uses a `context` object to pass data to and from your function and to let you communicate with the runtime.</span></span>

<span data-ttu-id="21b8e-120">O objeto de contexto sempre é o primeiro parâmetro para uma função e deve ser incluído porque tem métodos como `context.done` e `context.log`, que são necessários para usar corretamente o tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="21b8e-120">The context object is always the first parameter to a function and must be included because it has methods such as `context.done` and `context.log`, which are required to use the runtime correctly.</span></span> <span data-ttu-id="21b8e-121">Você pode nomear o objeto de acordo com a sua preferência (por exemplo, `ctx` ou `c`).</span><span class="sxs-lookup"><span data-stu-id="21b8e-121">You can name the object whatever you would like (for example, `ctx` or `c`).</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a><span data-ttu-id="21b8e-122">Propriedade context.bindings</span><span class="sxs-lookup"><span data-stu-id="21b8e-122">context.bindings property</span></span>

```
context.bindings
```
<span data-ttu-id="21b8e-123">Retorna um objeto nomeado que contém todos os dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="21b8e-123">Returns a named object that contains all your input and output data.</span></span> <span data-ttu-id="21b8e-124">Por exemplo, a seguinte definição de associação em seu *function.json*, permite que você acesse o conteúdo da fila por meio do objeto `context.bindings.myInput`.</span><span class="sxs-lookup"><span data-stu-id="21b8e-124">For example, the following binding definition in your *function.json* lets you access the contents of the queue from the `context.bindings.myInput` object.</span></span> 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains the input data, which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a><span data-ttu-id="21b8e-125">Método context.done</span><span class="sxs-lookup"><span data-stu-id="21b8e-125">context.done method</span></span>
```
context.done([err],[propertyBag])
```

<span data-ttu-id="21b8e-126">Informa ao tempo de execução que seu código terminou.</span><span class="sxs-lookup"><span data-stu-id="21b8e-126">Informs the runtime that your code has finished.</span></span> <span data-ttu-id="21b8e-127">Você deve chamar `context.done`, ou o tempo de execução nunca saberá que sua função terminou e a execução atingirá o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="21b8e-127">You must call `context.done`, or else the runtime never knows that your function is complete, and the execution will time out.</span></span> 

<span data-ttu-id="21b8e-128">O método `context.done` permite que você passe um erro definido pelo usuário de volta ao tempo de execução, e um recipiente de propriedades que substitui as propriedades no objeto `context.bindings`.</span><span class="sxs-lookup"><span data-stu-id="21b8e-128">The `context.done` method allows you to pass back both a user-defined error to the runtime and a property bag of properties that overwrite the properties on the `context.bindings` object.</span></span>

```javascript
// Even though we set myOutput to have:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object to the done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// the done method will overwrite the myOutput binding to be: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a><span data-ttu-id="21b8e-129">Método context.log</span><span class="sxs-lookup"><span data-stu-id="21b8e-129">context.log method</span></span>  

```
context.log(message)
```
<span data-ttu-id="21b8e-130">Permite que você grave nos logs do console de streaming no nível de rastreamento padrão.</span><span class="sxs-lookup"><span data-stu-id="21b8e-130">Allows you to write to the streaming console logs at the default trace level.</span></span> <span data-ttu-id="21b8e-131">Há métodos adicionais de registro em log disponíveis no `context.log` que permitem a gravação no log de console em outros níveis de rastreamento:</span><span class="sxs-lookup"><span data-stu-id="21b8e-131">On `context.log`, additional logging methods are available that let you write to the console log at other trace levels:</span></span>


| <span data-ttu-id="21b8e-132">Método</span><span class="sxs-lookup"><span data-stu-id="21b8e-132">Method</span></span>                 | <span data-ttu-id="21b8e-133">Descrição</span><span class="sxs-lookup"><span data-stu-id="21b8e-133">Description</span></span>                                |
| ---------------------- | ------------------------------------------ |
| <span data-ttu-id="21b8e-134">**error(_message_)**</span><span class="sxs-lookup"><span data-stu-id="21b8e-134">**error(_message_)**</span></span>   | <span data-ttu-id="21b8e-135">Grava no registro em log no nível do erro, ou em um nível inferior.</span><span class="sxs-lookup"><span data-stu-id="21b8e-135">Writes to error level logging, or lower.</span></span>   |
| <span data-ttu-id="21b8e-136">**warn(_message_)**</span><span class="sxs-lookup"><span data-stu-id="21b8e-136">**warn(_message_)**</span></span>    | <span data-ttu-id="21b8e-137">Grava no registro em log no nível do aviso, ou em um nível inferior.</span><span class="sxs-lookup"><span data-stu-id="21b8e-137">Writes to warning level logging, or lower.</span></span> |
| <span data-ttu-id="21b8e-138">**info(_message_)**</span><span class="sxs-lookup"><span data-stu-id="21b8e-138">**info(_message_)**</span></span>    | <span data-ttu-id="21b8e-139">Grava no registro em log no nível da informação, ou em um nível inferior.</span><span class="sxs-lookup"><span data-stu-id="21b8e-139">Writes to info level logging, or lower.</span></span>    |
| <span data-ttu-id="21b8e-140">**verbose(_message_)**</span><span class="sxs-lookup"><span data-stu-id="21b8e-140">**verbose(_message_)**</span></span> | <span data-ttu-id="21b8e-141">Grava no registro em log no nível detalhado.</span><span class="sxs-lookup"><span data-stu-id="21b8e-141">Writes to verbose level logging.</span></span>           |

<span data-ttu-id="21b8e-142">O exemplo a seguir grava no console no nível de rastreamento de aviso:</span><span class="sxs-lookup"><span data-stu-id="21b8e-142">The following example writes to the console at the warning trace level:</span></span>

```javascript
context.log.warn("Something has happened."); 
```
<span data-ttu-id="21b8e-143">Você pode definir o limite do nível de rastreamento para registrar em log no arquivo host.json, ou desativá-lo.</span><span class="sxs-lookup"><span data-stu-id="21b8e-143">You can set the trace-level threshold for logging in the host.json file, or turn it off.</span></span>  <span data-ttu-id="21b8e-144">Para saber mais sobre como gravar nos logs, veja a próxima seção.</span><span class="sxs-lookup"><span data-stu-id="21b8e-144">For more information about how to write to the logs, see the next section.</span></span>

## <a name="binding-data-type"></a><span data-ttu-id="21b8e-145">Tipo de dados de associação</span><span class="sxs-lookup"><span data-stu-id="21b8e-145">Binding data type</span></span>

<span data-ttu-id="21b8e-146">Para definir o tipo de dados para uma associação de entrada, use a propriedade `dataType` na definição de associação.</span><span class="sxs-lookup"><span data-stu-id="21b8e-146">To define the data type for an input binding, use the `dataType` property in the binding definition.</span></span> <span data-ttu-id="21b8e-147">Por exemplo, para ler o conteúdo de uma solicitação HTTP em formato binário, use o tipo `binary`:</span><span class="sxs-lookup"><span data-stu-id="21b8e-147">For example, to read the content of an HTTP request in binary format, use the type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="21b8e-148">Outras opções para `dataType` são `stream` e `string`.</span><span class="sxs-lookup"><span data-stu-id="21b8e-148">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="writing-trace-output-to-the-console"></a><span data-ttu-id="21b8e-149">Gravar a saída de rastreamento no console</span><span class="sxs-lookup"><span data-stu-id="21b8e-149">Writing trace output to the console</span></span> 

<span data-ttu-id="21b8e-150">No Functions, use os métodos `context.log` para gravar a saída de rastreamento no console.</span><span class="sxs-lookup"><span data-stu-id="21b8e-150">In Functions, you use the `context.log` methods to write trace output to the console.</span></span> <span data-ttu-id="21b8e-151">Neste ponto, não é possível usar `console.log` para gravar no console.</span><span class="sxs-lookup"><span data-stu-id="21b8e-151">At this point, you cannot use `console.log` to write to the console.</span></span>

<span data-ttu-id="21b8e-152">Quando você chama `context.log()`, sua mensagem é gravada no console no nível de rastreamento padrão, que é o nível de rastreamento de _informações_.</span><span class="sxs-lookup"><span data-stu-id="21b8e-152">When you call `context.log()`, your message is written to the console at the default trace level, which is the _info_ trace level.</span></span> <span data-ttu-id="21b8e-153">O código a seguir grava no console no nível de rastreamento de informações:</span><span class="sxs-lookup"><span data-stu-id="21b8e-153">The following code writes to the console at the info trace level:</span></span>

```javascript
context.log({hello: 'world'});  
```

<span data-ttu-id="21b8e-154">O código anterior é o equivalente ao código a seguir:</span><span class="sxs-lookup"><span data-stu-id="21b8e-154">The preceding code is equivalent to the following code:</span></span>

```javascript
context.log.info({hello: 'world'});  
```

<span data-ttu-id="21b8e-155">O código a seguir grava no console no nível do erro:</span><span class="sxs-lookup"><span data-stu-id="21b8e-155">The following code writes to the console at the error level:</span></span>

```javascript
context.log.error("An error has occurred.");  
```

<span data-ttu-id="21b8e-156">Como _erro_ é o nível de rastreamento mais alto, esse rastreamento é gravado na saída em todos os níveis de rastreamento enquanto o registro em log estiver habilitado.</span><span class="sxs-lookup"><span data-stu-id="21b8e-156">Because _error_ is the highest trace level, this trace is written to the output at all trace levels as long as logging is enabled.</span></span>  


<span data-ttu-id="21b8e-157">Todos os métodos `context.log` dão suporte ao mesmo formato de parâmetro que o [método util.format](https://nodejs.org/api/util.html#util_util_format_format) de Node.js.</span><span class="sxs-lookup"><span data-stu-id="21b8e-157">All `context.log` methods support the same parameter format that's supported by the Node.js [util.format method](https://nodejs.org/api/util.html#util_util_format_format).</span></span> <span data-ttu-id="21b8e-158">Considere o código a seguir, que grava no console usando o nível de rastreamento padrão:</span><span class="sxs-lookup"><span data-stu-id="21b8e-158">Consider the following code, which writes to the console by using the default trace level:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

<span data-ttu-id="21b8e-159">Você também pode escrever o mesmo código no formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="21b8e-159">You can also write the same code in the following format:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-the-trace-level-for-console-logging"></a><span data-ttu-id="21b8e-160">Configurar o nível de rastreamento para o registro em log no console</span><span class="sxs-lookup"><span data-stu-id="21b8e-160">Configure the trace level for console logging</span></span>

<span data-ttu-id="21b8e-161">O Functions permite a definição do nível de rastreamento de limite para gravar no console, o que facilita o controle do modo de gravação dos rastreamentos no console a partir de suas funções.</span><span class="sxs-lookup"><span data-stu-id="21b8e-161">Functions lets you define the threshold trace level for writing to the console, which makes it easy to control the way traces are written to the console from your functions.</span></span> <span data-ttu-id="21b8e-162">Para definir o limite para todos os rastreamentos gravados no console, use a propriedade `tracing.consoleLevel` no arquivo host.json.</span><span class="sxs-lookup"><span data-stu-id="21b8e-162">To set the threshold for all traces written to the console, use the `tracing.consoleLevel` property in the host.json file.</span></span> <span data-ttu-id="21b8e-163">Essa configuração se aplica a todas as funções em seu aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="21b8e-163">This setting applies to all functions in your function app.</span></span> <span data-ttu-id="21b8e-164">O exemplo a seguir define o limite de rastreamento para habilitar o registro em log detalhado:</span><span class="sxs-lookup"><span data-stu-id="21b8e-164">The following example sets the trace threshold to enable verbose logging:</span></span>

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

<span data-ttu-id="21b8e-165">Os valores de **consoleLevel** correspondem aos nomes dos métodos `context.log`.</span><span class="sxs-lookup"><span data-stu-id="21b8e-165">Values of **consoleLevel** correspond to the names of the `context.log` methods.</span></span> <span data-ttu-id="21b8e-166">Para desabilitar todo o registro em log do rastreamento no console, defina **consoleLevel** como _off_.</span><span class="sxs-lookup"><span data-stu-id="21b8e-166">To disable all trace logging to the console, set **consoleLevel** to _off_.</span></span> <span data-ttu-id="21b8e-167">Para saber mais sobre o arquivo host.json, consulte o [tópico de referência sobre host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="21b8e-167">For more information about the host.json file, see the [host.json reference topic](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>

## <a name="http-triggers-and-bindings"></a><span data-ttu-id="21b8e-168">Gatilhos e associações HTTP</span><span class="sxs-lookup"><span data-stu-id="21b8e-168">HTTP triggers and bindings</span></span>

<span data-ttu-id="21b8e-169">HTTP e gatilhos de webhook e associações de saída HTTP usam objetos de solicitação e resposta para representar as mensagens HTTP.</span><span class="sxs-lookup"><span data-stu-id="21b8e-169">HTTP and webhook triggers and HTTP output bindings use request and response objects to represent the HTTP messaging.</span></span>  

### <a name="request-object"></a><span data-ttu-id="21b8e-170">Objeto da solicitação</span><span class="sxs-lookup"><span data-stu-id="21b8e-170">Request object</span></span>

<span data-ttu-id="21b8e-171">O objeto `request` tem as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="21b8e-171">The `request` object has the following properties:</span></span>

| <span data-ttu-id="21b8e-172">Propriedade</span><span class="sxs-lookup"><span data-stu-id="21b8e-172">Property</span></span>      | <span data-ttu-id="21b8e-173">Descrição</span><span class="sxs-lookup"><span data-stu-id="21b8e-173">Description</span></span>                                                    |
| ------------- | -------------------------------------------------------------- |
| <span data-ttu-id="21b8e-174">_body_</span><span class="sxs-lookup"><span data-stu-id="21b8e-174">_body_</span></span>        | <span data-ttu-id="21b8e-175">Um objeto que contém o corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="21b8e-175">An object that contains the body of the request.</span></span>               |
| <span data-ttu-id="21b8e-176">_headers_</span><span class="sxs-lookup"><span data-stu-id="21b8e-176">_headers_</span></span>     | <span data-ttu-id="21b8e-177">Um objeto que contém os cabeçalhos da solicitação.</span><span class="sxs-lookup"><span data-stu-id="21b8e-177">An object that contains the request headers.</span></span>                   |
| <span data-ttu-id="21b8e-178">_method_</span><span class="sxs-lookup"><span data-stu-id="21b8e-178">_method_</span></span>      | <span data-ttu-id="21b8e-179">O método HTTP da solicitação.</span><span class="sxs-lookup"><span data-stu-id="21b8e-179">The HTTP method of the request.</span></span>                                |
| <span data-ttu-id="21b8e-180">_originalUrl_</span><span class="sxs-lookup"><span data-stu-id="21b8e-180">_originalUrl_</span></span> | <span data-ttu-id="21b8e-181">A URL da solicitação.</span><span class="sxs-lookup"><span data-stu-id="21b8e-181">The URL of the request.</span></span>                                        |
| <span data-ttu-id="21b8e-182">_params_</span><span class="sxs-lookup"><span data-stu-id="21b8e-182">_params_</span></span>      | <span data-ttu-id="21b8e-183">Um objeto que contém os parâmetros de roteamento da solicitação.</span><span class="sxs-lookup"><span data-stu-id="21b8e-183">An object that contains the routing parameters of the request.</span></span> |
| <span data-ttu-id="21b8e-184">_query_</span><span class="sxs-lookup"><span data-stu-id="21b8e-184">_query_</span></span>       | <span data-ttu-id="21b8e-185">Um objeto que contém os parâmetros da consulta.</span><span class="sxs-lookup"><span data-stu-id="21b8e-185">An object that contains the query parameters.</span></span>                  |
| <span data-ttu-id="21b8e-186">_rawBody_</span><span class="sxs-lookup"><span data-stu-id="21b8e-186">_rawBody_</span></span>     | <span data-ttu-id="21b8e-187">O corpo da mensagem como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="21b8e-187">The body of the message as a string.</span></span>                           |


### <a name="response-object"></a><span data-ttu-id="21b8e-188">Objeto de resposta</span><span class="sxs-lookup"><span data-stu-id="21b8e-188">Response object</span></span>

<span data-ttu-id="21b8e-189">O objeto `response` tem as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="21b8e-189">The `response` object has the following properties:</span></span>

| <span data-ttu-id="21b8e-190">Propriedade</span><span class="sxs-lookup"><span data-stu-id="21b8e-190">Property</span></span>  | <span data-ttu-id="21b8e-191">Descrição</span><span class="sxs-lookup"><span data-stu-id="21b8e-191">Description</span></span>                                               |
| --------- | --------------------------------------------------------- |
| <span data-ttu-id="21b8e-192">_body_</span><span class="sxs-lookup"><span data-stu-id="21b8e-192">_body_</span></span>    | <span data-ttu-id="21b8e-193">Um objeto que contém o corpo da resposta.</span><span class="sxs-lookup"><span data-stu-id="21b8e-193">An object that contains the body of the response.</span></span>         |
| <span data-ttu-id="21b8e-194">_headers_</span><span class="sxs-lookup"><span data-stu-id="21b8e-194">_headers_</span></span> | <span data-ttu-id="21b8e-195">Um objeto que contém os cabeçalhos da resposta.</span><span class="sxs-lookup"><span data-stu-id="21b8e-195">An object that contains the response headers.</span></span>             |
| <span data-ttu-id="21b8e-196">_isRaw_</span><span class="sxs-lookup"><span data-stu-id="21b8e-196">_isRaw_</span></span>   | <span data-ttu-id="21b8e-197">Indica que a formatação foi ignorada para a resposta.</span><span class="sxs-lookup"><span data-stu-id="21b8e-197">Indicates that formatting is skipped for the response.</span></span>    |
| <span data-ttu-id="21b8e-198">_status_</span><span class="sxs-lookup"><span data-stu-id="21b8e-198">_status_</span></span>  | <span data-ttu-id="21b8e-199">O código de status HTTP da resposta.</span><span class="sxs-lookup"><span data-stu-id="21b8e-199">The HTTP status code of the response.</span></span>                     |

### <a name="accessing-the-request-and-response"></a><span data-ttu-id="21b8e-200">Acessar a solicitação e a resposta</span><span class="sxs-lookup"><span data-stu-id="21b8e-200">Accessing the request and response</span></span> 

<span data-ttu-id="21b8e-201">Ao trabalhar com gatilhos HTTP, há três maneiras de acessar os objetos de solicitação e resposta HTTP:</span><span class="sxs-lookup"><span data-stu-id="21b8e-201">When you work with HTTP triggers, you can access the HTTP request and response objects in any of three ways:</span></span>

+ <span data-ttu-id="21b8e-202">A partir das associações de entrada e saída nomeadas.</span><span class="sxs-lookup"><span data-stu-id="21b8e-202">From the named input and output bindings.</span></span> <span data-ttu-id="21b8e-203">Dessa forma, o gatilho e as associações de HTTP funcionam da mesma forma que qualquer outra associação.</span><span class="sxs-lookup"><span data-stu-id="21b8e-203">In this way, the HTTP trigger and bindings work the same as any other binding.</span></span> <span data-ttu-id="21b8e-204">O exemplo a seguir define o objeto de resposta usando uma associação chamada `response`:</span><span class="sxs-lookup"><span data-stu-id="21b8e-204">The following example sets the response object by using a named `response` binding:</span></span> 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ <span data-ttu-id="21b8e-205">Das propriedades `req` e `res` no objeto `context`.</span><span class="sxs-lookup"><span data-stu-id="21b8e-205">From `req` and `res` properties on the `context` object.</span></span> <span data-ttu-id="21b8e-206">Dessa forma, você pode usar o padrão convencional para acessar os dados HTTP a partir do objeto de contexto, em vez de usar o padrão `context.bindings.name` completo.</span><span class="sxs-lookup"><span data-stu-id="21b8e-206">In this way, you can use the conventional pattern to access HTTP data from the context object, instead of having to use the full `context.bindings.name` pattern.</span></span> <span data-ttu-id="21b8e-207">O exemplo a seguir mostra como acessar os objetos `req` e `res` no `context`:</span><span class="sxs-lookup"><span data-stu-id="21b8e-207">The following example shows how to access the `req` and `res` objects on the `context`:</span></span>

    ```javascript
    // You can access your http request off the context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ <span data-ttu-id="21b8e-208">Chamando `context.done()`.</span><span class="sxs-lookup"><span data-stu-id="21b8e-208">By calling `context.done()`.</span></span> <span data-ttu-id="21b8e-209">Um tipo especial de associação HTTP que retorna a resposta passada ao método `context.done()`.</span><span class="sxs-lookup"><span data-stu-id="21b8e-209">A special kind of HTTP binding returns the response that is passed to the `context.done()` method.</span></span> <span data-ttu-id="21b8e-210">A seguinte associação de saída HTTP define um parâmetro de saída `$return`:</span><span class="sxs-lookup"><span data-stu-id="21b8e-210">The following HTTP output binding defines a `$return` output parameter:</span></span>

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    <span data-ttu-id="21b8e-211">Essa associação de saída espera que você forneça a resposta ao chamar `done()` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="21b8e-211">This output binding expects you to supply the response when you call `done()`, as follows:</span></span>

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a><span data-ttu-id="21b8e-212">Versão do Node e gerenciamento de pacote</span><span class="sxs-lookup"><span data-stu-id="21b8e-212">Node version and Package Management</span></span>
<span data-ttu-id="21b8e-213">A versão do Node está bloqueada em `6.5.0`no momento.</span><span class="sxs-lookup"><span data-stu-id="21b8e-213">The node version is currently locked at `6.5.0`.</span></span> <span data-ttu-id="21b8e-214">Estamos investigando a adição de suporte para mais versões e para torná-las configuráveis.</span><span class="sxs-lookup"><span data-stu-id="21b8e-214">We're investigating adding support for more versions and making it configurable.</span></span>

<span data-ttu-id="21b8e-215">As etapas a seguir permitem que você inclua pacotes em seu aplicativo de função:</span><span class="sxs-lookup"><span data-stu-id="21b8e-215">The following steps let you include packages in your function app:</span></span> 

1. <span data-ttu-id="21b8e-216">Vá para `https://<function_app_name>.scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="21b8e-216">Go to `https://<function_app_name>.scm.azurewebsites.net`.</span></span>

2. <span data-ttu-id="21b8e-217">Clique em **Console de Depuração** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="21b8e-217">Click **Debug Console** > **CMD**.</span></span>

3. <span data-ttu-id="21b8e-218">Acesse `D:\home\site\wwwroot`e arraste o arquivo package.json para a pasta **wwwroot** na metade superior da página.</span><span class="sxs-lookup"><span data-stu-id="21b8e-218">Go to `D:\home\site\wwwroot`, and then drag your package.json file to the **wwwroot** folder at the top half of the page.</span></span>  
    <span data-ttu-id="21b8e-219">Também há outras maneiras de carregar arquivos em seu aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="21b8e-219">You can upload files to your function app in other ways also.</span></span> <span data-ttu-id="21b8e-220">Para saber mais, confira [Como atualizar os arquivos do aplicativo de função](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="21b8e-220">For more information, see [How to update function app files](functions-reference.md#fileupdate).</span></span> 

4. <span data-ttu-id="21b8e-221">Depois que o arquivo package.json é carregado, execute o comando `npm install` no **console de execução remota do Kudu**.</span><span class="sxs-lookup"><span data-stu-id="21b8e-221">After the package.json file is uploaded, run the `npm install` command in the **Kudu remote execution console**.</span></span>  
    <span data-ttu-id="21b8e-222">Essa ação baixa os pacotes indicados no arquivo package.json e reinicia o aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="21b8e-222">This action downloads the packages indicated in the package.json file and restarts the function app.</span></span>

<span data-ttu-id="21b8e-223">Após a instalação dos pacotes necessários, você os importa para sua função chamando `require('packagename')`, como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="21b8e-223">After the packages you need are installed, you import them to your function by calling `require('packagename')`, as in the following example:</span></span>

```javascript
// Import the underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

<span data-ttu-id="21b8e-224">Você deve definir um arquivo `package.json` na raiz de seu aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="21b8e-224">You should define a `package.json` file at the root of your function app.</span></span> <span data-ttu-id="21b8e-225">A definição de arquivo permite que todas as funções no aplicativo compartilhem os mesmos pacotes armazenados em cache, o que oferece o melhor desempenho.</span><span class="sxs-lookup"><span data-stu-id="21b8e-225">Defining the file lets all functions in the app share the same cached packages, which gives the best performance.</span></span> <span data-ttu-id="21b8e-226">Se houver conflitos de versão, você poderá resolver o conflito adicionando um arquivo `package.json` na pasta de uma função específica.</span><span class="sxs-lookup"><span data-stu-id="21b8e-226">If a version conflict arises, you can resolve it by adding a `package.json` file in the folder of a specific function.</span></span>  

## <a name="environment-variables"></a><span data-ttu-id="21b8e-227">Variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="21b8e-227">Environment variables</span></span>
<span data-ttu-id="21b8e-228">Para obter uma variável de ambiente ou um valor de configuração do aplicativo, use `process.env`, conforme mostrado no exemplo de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="21b8e-228">To get an environment variable or an app setting value, use `process.env`, as shown in the following code example:</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    context.log('Node.js timer trigger function ran!', timeStamp);   
    context.log(GetEnvironmentVariable("AzureWebJobsStorage"));
    context.log(GetEnvironmentVariable("WEBSITE_SITE_NAME"));

    context.done();
};

function GetEnvironmentVariable(name)
{
    return name + ": " + process.env[name];
}
```
## <a name="considerations-for-javascript-functions"></a><span data-ttu-id="21b8e-229">Considerações para funções em JavaScript</span><span class="sxs-lookup"><span data-stu-id="21b8e-229">Considerations for JavaScript functions</span></span>

<span data-ttu-id="21b8e-230">Ao trabalhar com funções em JavaScript, lembre-se das considerações nas duas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="21b8e-230">When you work with JavaScript functions, be aware of the considerations in the following two sections.</span></span>

### <a name="choose-single-core-app-service-plans"></a><span data-ttu-id="21b8e-231">Escolher Planos do Serviço de Aplicativo de núcleo único</span><span class="sxs-lookup"><span data-stu-id="21b8e-231">Choose single-core App Service plans</span></span>

<span data-ttu-id="21b8e-232">Ao criar um aplicativo de função que usa o Plano do Serviço de Aplicativo, recomendamos que você selecione um plano de núcleo único em vez de um plano com vários núcleos.</span><span class="sxs-lookup"><span data-stu-id="21b8e-232">When you create a function app that uses the App Service plan, we recommend that you select a single-core plan rather than a plan with multiple cores.</span></span> <span data-ttu-id="21b8e-233">Atualmente, o Functions executa funções em JavaScript com mais eficiência em VMs de núcleo único, e o uso de VMs maiores não produz os aprimoramentos de desempenho esperados.</span><span class="sxs-lookup"><span data-stu-id="21b8e-233">Today, Functions runs JavaScript functions more efficiently on single-core VMs, and using larger VMs does not produce the expected performance improvements.</span></span> <span data-ttu-id="21b8e-234">Quando for necessário, você poderá escalar horizontalmente manualmente adicionando mais instâncias de VM de núcleo único ou poderá habilitar o dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="21b8e-234">When necessary, you can manually scale out by adding more single-core VM instances, or you can enable auto-scale.</span></span> <span data-ttu-id="21b8e-235">Para saber mais, confira [Dimensionar a contagem de instâncias manual ou automaticamente](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="21b8e-235">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span></span>    

### <a name="typescript-and-coffeescript-support"></a><span data-ttu-id="21b8e-236">Suporte a TypeScript e CoffeeScript</span><span class="sxs-lookup"><span data-stu-id="21b8e-236">TypeScript and CoffeeScript support</span></span>
<span data-ttu-id="21b8e-237">Como ainda não há suporte direto para compilação automática de TypeScript ou CoffeeScript por meio do tempo de execução, esse suporte precisa ser manipulado fora do tempo de execução, no tempo de implantação.</span><span class="sxs-lookup"><span data-stu-id="21b8e-237">Because direct support does not yet exist for auto-compiling TypeScript or CoffeeScript via the runtime, such support needs to be handled outside the runtime, at deployment time.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="21b8e-238">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="21b8e-238">Next steps</span></span>
<span data-ttu-id="21b8e-239">Para saber mais, consulte os recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="21b8e-239">For more information, see the following resources:</span></span>

* [<span data-ttu-id="21b8e-240">Práticas recomendadas para o Azure Functions</span><span class="sxs-lookup"><span data-stu-id="21b8e-240">Best practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="21b8e-241">Referência do desenvolvedor do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="21b8e-241">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="21b8e-242">Referência do desenvolvedor de C# do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="21b8e-242">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="21b8e-243">Referência do desenvolvedor em F# do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="21b8e-243">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="21b8e-244">Gatilhos e de associações do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="21b8e-244">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

