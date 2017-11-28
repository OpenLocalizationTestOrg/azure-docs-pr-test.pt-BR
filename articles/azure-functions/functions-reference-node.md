---
title: "referência do desenvolvedor aaaJavaScript para funções do Azure | Microsoft Docs"
description: Entendeu o funcionamento do toodevelop usando JavaScript.
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
ms.openlocfilehash: 6220b42f965b6ee2463341aaf270836623fdf7fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-javascript-developer-guide"></a><span data-ttu-id="9ddf0-104">Guia do desenvolvedor de JavaScript do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="9ddf0-104">Azure Functions JavaScript developer guide</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9ddf0-105">Script C#</span><span class="sxs-lookup"><span data-stu-id="9ddf0-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="9ddf0-106">Script em F#</span><span class="sxs-lookup"><span data-stu-id="9ddf0-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="9ddf0-107">JavaScript</span><span class="sxs-lookup"><span data-stu-id="9ddf0-107">JavaScript</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="9ddf0-108">Olá experiência de JavaScript para funções do Azure torna fácil tooexport uma função, que é passada como um `context` objeto para se comunicar com o tempo de execução de saudação e para receber e enviar dados por meio de associações.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-108">hello JavaScript experience for Azure Functions makes it easy tooexport a function, which is passed as a `context` object for communicating with hello runtime and for receiving and sending data via bindings.</span></span>

<span data-ttu-id="9ddf0-109">Este artigo pressupõe que você já leu Olá [referência do desenvolvedor do Azure funções](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="9ddf0-109">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="exporting-a-function"></a><span data-ttu-id="9ddf0-110">Exportando uma função</span><span class="sxs-lookup"><span data-stu-id="9ddf0-110">Exporting a function</span></span>
<span data-ttu-id="9ddf0-111">Todas as funções JavaScript devem exportar um único `function` via `module.exports` Olá Runtime toofind Olá função e executá-lo.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-111">All JavaScript functions must export a single `function` via `module.exports` for hello runtime toofind hello function and run it.</span></span> <span data-ttu-id="9ddf0-112">Esta função sempre deve incluir um objeto `context` .</span><span class="sxs-lookup"><span data-stu-id="9ddf0-112">This function must always include a `context` object.</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by hello arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

<span data-ttu-id="9ddf0-113">Associações de `direction === "in"` são passadas como argumentos de função, o que significa que você pode usar [ `arguments` ](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically lidar com novas entradas (por exemplo, usando `arguments.length` tooiterate em todas as suas entradas).</span><span class="sxs-lookup"><span data-stu-id="9ddf0-113">Bindings of `direction === "in"` are passed along as function arguments, which means that you can use [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically handle new inputs (for example, by using `arguments.length` tooiterate over all your inputs).</span></span> <span data-ttu-id="9ddf0-114">Essa funcionalidade é conveniente quando você tem apenas um gatilho e nenhuma entrada adicional, pois é possível acessar seus dados de gatilho de maneira previsível, sem fazer referência ao objeto `context`.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-114">This functionality is convenient when you have only a trigger and no additional inputs, because you can predictably access your trigger data without referencing your `context` object.</span></span>

<span data-ttu-id="9ddf0-115">argumentos Olá sempre são passados função toohello na ordem Olá ocorrem em *function.json*, mesmo se você não especificá-los em sua instrução de exportações.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-115">hello arguments are always passed along toohello function in hello order in which they occur in *function.json*, even if you don't specify them in your exports statement.</span></span> <span data-ttu-id="9ddf0-116">Por exemplo, se você tiver `function(context, a, b)` e alterá-la muito`function(context, a)`, ainda é possível obter o valor de saudação do `b` no código de função referindo-se muito`arguments[3]`.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-116">For example, if you have `function(context, a, b)` and change it too`function(context, a)`, you can still get hello value of `b` in function code by referring too`arguments[3]`.</span></span>

<span data-ttu-id="9ddf0-117">Todas as associações, independentemente de direção, também são passadas Olá `context` objeto (consulte Olá script a seguir).</span><span class="sxs-lookup"><span data-stu-id="9ddf0-117">All bindings, regardless of direction, are also passed along on hello `context` object (see hello following script).</span></span> 

## <a name="context-object"></a><span data-ttu-id="9ddf0-118">objeto de contexto</span><span class="sxs-lookup"><span data-stu-id="9ddf0-118">context object</span></span>
<span data-ttu-id="9ddf0-119">saudação de tempo de execução usa um `context` tooand de dados do objeto toopass de sua função e toolet você se comunicar com o tempo de execução de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-119">hello runtime uses a `context` object toopass data tooand from your function and toolet you communicate with hello runtime.</span></span>

<span data-ttu-id="9ddf0-120">Olá objeto de contexto é sempre a primeira função de tooa parâmetro hello e deve ser incluído porque tem métodos como `context.done` e `context.log`, que são necessárias toouse Olá runtime corretamente.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-120">hello context object is always hello first parameter tooa function and must be included because it has methods such as `context.done` and `context.log`, which are required toouse hello runtime correctly.</span></span> <span data-ttu-id="9ddf0-121">Você pode nomear o objeto hello como desejar (por exemplo, `ctx` ou `c`).</span><span class="sxs-lookup"><span data-stu-id="9ddf0-121">You can name hello object whatever you would like (for example, `ctx` or `c`).</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a><span data-ttu-id="9ddf0-122">Propriedade context.bindings</span><span class="sxs-lookup"><span data-stu-id="9ddf0-122">context.bindings property</span></span>

```
context.bindings
```
<span data-ttu-id="9ddf0-123">Retorna um objeto nomeado que contém todos os dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-123">Returns a named object that contains all your input and output data.</span></span> <span data-ttu-id="9ddf0-124">Olá, por exemplo, após a definição de associação no seu *function.json* permite que você acesse Olá conteúdo da fila de saudação do hello `context.bindings.myInput` objeto.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-124">For example, hello following binding definition in your *function.json* lets you access hello contents of hello queue from hello `context.bindings.myInput` object.</span></span> 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains hello input data, which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a><span data-ttu-id="9ddf0-125">Método context.done</span><span class="sxs-lookup"><span data-stu-id="9ddf0-125">context.done method</span></span>
```
context.done([err],[propertyBag])
```

<span data-ttu-id="9ddf0-126">Informa Olá em tempo de execução que terminou de seu código.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-126">Informs hello runtime that your code has finished.</span></span> <span data-ttu-id="9ddf0-127">Você deve chamar `context.done`, ou tempo de execução else hello nunca sabe que sua função é concluída e execução de saudação atingirá o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-127">You must call `context.done`, or else hello runtime never knows that your function is complete, and hello execution will time out.</span></span> 

<span data-ttu-id="9ddf0-128">Olá `context.done` método permite que você toopass fazer um tempo de execução de toohello de erro definidas pelo usuário e um conjunto de propriedades de propriedades que substituir propriedades Olá Olá `context.bindings` objeto.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-128">hello `context.done` method allows you toopass back both a user-defined error toohello runtime and a property bag of properties that overwrite hello properties on hello `context.bindings` object.</span></span>

```javascript
// Even though we set myOutput toohave:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object toohello done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// hello done method will overwrite hello myOutput binding toobe: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a><span data-ttu-id="9ddf0-129">Método context.log</span><span class="sxs-lookup"><span data-stu-id="9ddf0-129">context.log method</span></span>  

```
context.log(message)
```
<span data-ttu-id="9ddf0-130">Permite que você toowrite toohello console logs de streaming no nível de rastreamento padrão hello.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-130">Allows you toowrite toohello streaming console logs at hello default trace level.</span></span> <span data-ttu-id="9ddf0-131">Em `context.log`adicionais de log métodos estão disponíveis que permitem a você escrever toohello log de console em outros níveis de rastreamento:</span><span class="sxs-lookup"><span data-stu-id="9ddf0-131">On `context.log`, additional logging methods are available that let you write toohello console log at other trace levels:</span></span>


| <span data-ttu-id="9ddf0-132">Método</span><span class="sxs-lookup"><span data-stu-id="9ddf0-132">Method</span></span>                 | <span data-ttu-id="9ddf0-133">Descrição</span><span class="sxs-lookup"><span data-stu-id="9ddf0-133">Description</span></span>                                |
| ---------------------- | ------------------------------------------ |
| <span data-ttu-id="9ddf0-134">**error(_message_)**</span><span class="sxs-lookup"><span data-stu-id="9ddf0-134">**error(_message_)**</span></span>   | <span data-ttu-id="9ddf0-135">Grava o nível de tooerror log ou inferior.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-135">Writes tooerror level logging, or lower.</span></span>   |
| <span data-ttu-id="9ddf0-136">**warn(_message_)**</span><span class="sxs-lookup"><span data-stu-id="9ddf0-136">**warn(_message_)**</span></span>    | <span data-ttu-id="9ddf0-137">Grava o nível de toowarning log ou inferior.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-137">Writes toowarning level logging, or lower.</span></span> |
| <span data-ttu-id="9ddf0-138">**info(_message_)**</span><span class="sxs-lookup"><span data-stu-id="9ddf0-138">**info(_message_)**</span></span>    | <span data-ttu-id="9ddf0-139">Grava o nível de tooinfo log ou inferior.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-139">Writes tooinfo level logging, or lower.</span></span>    |
| <span data-ttu-id="9ddf0-140">**verbose(_message_)**</span><span class="sxs-lookup"><span data-stu-id="9ddf0-140">**verbose(_message_)**</span></span> | <span data-ttu-id="9ddf0-141">Grava o log de nível de tooverbose.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-141">Writes tooverbose level logging.</span></span>           |

<span data-ttu-id="9ddf0-142">Olá, exemplo a seguir grava toohello console no nível de rastreamento de aviso hello:</span><span class="sxs-lookup"><span data-stu-id="9ddf0-142">hello following example writes toohello console at hello warning trace level:</span></span>

```javascript
context.log.warn("Something has happened."); 
```
<span data-ttu-id="9ddf0-143">Você pode definir o limite do nível de rastreamento Olá para registrar em log no arquivo de host.json hello, ou desativá-lo.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-143">You can set hello trace-level threshold for logging in hello host.json file, or turn it off.</span></span>  <span data-ttu-id="9ddf0-144">Para obter mais informações sobre como toowrite toohello registra, consulte Olá próxima seção.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-144">For more information about how toowrite toohello logs, see hello next section.</span></span>

## <a name="binding-data-type"></a><span data-ttu-id="9ddf0-145">Tipo de dados de associação</span><span class="sxs-lookup"><span data-stu-id="9ddf0-145">Binding data type</span></span>

<span data-ttu-id="9ddf0-146">toodefine tipo de dados de saudação para uma associação de entrada, use Olá `dataType` propriedade na definição de associação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-146">toodefine hello data type for an input binding, use hello `dataType` property in hello binding definition.</span></span> <span data-ttu-id="9ddf0-147">Por exemplo, tooread Olá conteúdo de uma solicitação HTTP em formato binário, use o tipo de saudação `binary`:</span><span class="sxs-lookup"><span data-stu-id="9ddf0-147">For example, tooread hello content of an HTTP request in binary format, use hello type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="9ddf0-148">Outras opções para `dataType` são `stream` e `string`.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-148">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="writing-trace-output-toohello-console"></a><span data-ttu-id="9ddf0-149">Console de toohello de saída de rastreamento de gravação</span><span class="sxs-lookup"><span data-stu-id="9ddf0-149">Writing trace output toohello console</span></span> 

<span data-ttu-id="9ddf0-150">Em funções, você usar Olá `context.log` console toohello de saída de rastreamento do métodos toowrite.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-150">In Functions, you use hello `context.log` methods toowrite trace output toohello console.</span></span> <span data-ttu-id="9ddf0-151">Neste ponto, você não pode usar `console.log` toowrite toohello console.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-151">At this point, you cannot use `console.log` toowrite toohello console.</span></span>

<span data-ttu-id="9ddf0-152">Quando você chama `context.log()`, a mensagem é gravada toohello console no nível de rastreamento padrão Olá, é hello _informações_ o nível de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-152">When you call `context.log()`, your message is written toohello console at hello default trace level, which is hello _info_ trace level.</span></span> <span data-ttu-id="9ddf0-153">Olá código a seguir grava toohello console no nível de rastreamento de informações de saudação:</span><span class="sxs-lookup"><span data-stu-id="9ddf0-153">hello following code writes toohello console at hello info trace level:</span></span>

```javascript
context.log({hello: 'world'});  
```

<span data-ttu-id="9ddf0-154">Olá código anterior é equivalente toohello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ddf0-154">hello preceding code is equivalent toohello following code:</span></span>

```javascript
context.log.info({hello: 'world'});  
```

<span data-ttu-id="9ddf0-155">Olá código a seguir grava toohello console no nível de erro hello:</span><span class="sxs-lookup"><span data-stu-id="9ddf0-155">hello following code writes toohello console at hello error level:</span></span>

```javascript
context.log.error("An error has occurred.");  
```

<span data-ttu-id="9ddf0-156">Porque _erro_ for hello mais alto nível, este rastreamento é gravado toohello saída em todos os níveis de rastreamento como o log está habilitado.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-156">Because _error_ is hello highest trace level, this trace is written toohello output at all trace levels as long as logging is enabled.</span></span>  


<span data-ttu-id="9ddf0-157">Todos os `context.log` métodos oferecem suporte a saudação mesmo formato do parâmetro que é suportado pelo Olá Node. js [util.format método](https://nodejs.org/api/util.html#util_util_format_format).</span><span class="sxs-lookup"><span data-stu-id="9ddf0-157">All `context.log` methods support hello same parameter format that's supported by hello Node.js [util.format method](https://nodejs.org/api/util.html#util_util_format_format).</span></span> <span data-ttu-id="9ddf0-158">Considere Olá código, que grava toohello console usando o nível de rastreamento saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ddf0-158">Consider hello following code, which writes toohello console by using hello default trace level:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

<span data-ttu-id="9ddf0-159">Você também pode Olá gravação mesmo código Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ddf0-159">You can also write hello same code in hello following format:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-hello-trace-level-for-console-logging"></a><span data-ttu-id="9ddf0-160">Configurar o nível de rastreamento de saudação do log de console</span><span class="sxs-lookup"><span data-stu-id="9ddf0-160">Configure hello trace level for console logging</span></span>

<span data-ttu-id="9ddf0-161">Funções permite definir o nível de rastreamento de limite de saudação para gravar toohello console, o que torna fácil toocontrol maneira de saudação os rastreamentos são gravados toohello console de suas funções.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-161">Functions lets you define hello threshold trace level for writing toohello console, which makes it easy toocontrol hello way traces are written toohello console from your functions.</span></span> <span data-ttu-id="9ddf0-162">limite de saudação tooset para todos os rastreamentos gravados toohello console, use Olá `tracing.consoleLevel` propriedade no arquivo de host.json hello.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-162">tooset hello threshold for all traces written toohello console, use hello `tracing.consoleLevel` property in hello host.json file.</span></span> <span data-ttu-id="9ddf0-163">Essa configuração se aplica a funções de tooall em seu aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-163">This setting applies tooall functions in your function app.</span></span> <span data-ttu-id="9ddf0-164">Olá, exemplo a seguir define Olá rastreamento limite tooenable o log detalhado:</span><span class="sxs-lookup"><span data-stu-id="9ddf0-164">hello following example sets hello trace threshold tooenable verbose logging:</span></span>

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

<span data-ttu-id="9ddf0-165">Valores de **consoleLevel** correspondem toohello nomes de saudação `context.log` métodos.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-165">Values of **consoleLevel** correspond toohello names of hello `context.log` methods.</span></span> <span data-ttu-id="9ddf0-166">toodisable toohello console, de log de rastreamento de todos os conjunto **consoleLevel** too_off_.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-166">toodisable all trace logging toohello console, set **consoleLevel** too_off_.</span></span> <span data-ttu-id="9ddf0-167">Para obter mais informações sobre o arquivo de host.json hello, consulte Olá [tópico de referência host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="9ddf0-167">For more information about hello host.json file, see hello [host.json reference topic](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>

## <a name="http-triggers-and-bindings"></a><span data-ttu-id="9ddf0-168">Gatilhos e associações HTTP</span><span class="sxs-lookup"><span data-stu-id="9ddf0-168">HTTP triggers and bindings</span></span>

<span data-ttu-id="9ddf0-169">HTTP e gatilhos de webhook HTTP de saída e associações de usam a solicitação e resposta objetos toorepresent Olá HTTP mensagens.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-169">HTTP and webhook triggers and HTTP output bindings use request and response objects toorepresent hello HTTP messaging.</span></span>  

### <a name="request-object"></a><span data-ttu-id="9ddf0-170">Objeto da solicitação</span><span class="sxs-lookup"><span data-stu-id="9ddf0-170">Request object</span></span>

<span data-ttu-id="9ddf0-171">Olá `request` objeto tem Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ddf0-171">hello `request` object has hello following properties:</span></span>

| <span data-ttu-id="9ddf0-172">Propriedade</span><span class="sxs-lookup"><span data-stu-id="9ddf0-172">Property</span></span>      | <span data-ttu-id="9ddf0-173">Descrição</span><span class="sxs-lookup"><span data-stu-id="9ddf0-173">Description</span></span>                                                    |
| ------------- | -------------------------------------------------------------- |
| <span data-ttu-id="9ddf0-174">_body_</span><span class="sxs-lookup"><span data-stu-id="9ddf0-174">_body_</span></span>        | <span data-ttu-id="9ddf0-175">Um objeto que contém o corpo de saudação da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-175">An object that contains hello body of hello request.</span></span>               |
| <span data-ttu-id="9ddf0-176">_headers_</span><span class="sxs-lookup"><span data-stu-id="9ddf0-176">_headers_</span></span>     | <span data-ttu-id="9ddf0-177">Um objeto que contém os cabeçalhos de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-177">An object that contains hello request headers.</span></span>                   |
| <span data-ttu-id="9ddf0-178">_method_</span><span class="sxs-lookup"><span data-stu-id="9ddf0-178">_method_</span></span>      | <span data-ttu-id="9ddf0-179">método HTTP da solicitação de saudação do Hello.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-179">hello HTTP method of hello request.</span></span>                                |
| <span data-ttu-id="9ddf0-180">_originalUrl_</span><span class="sxs-lookup"><span data-stu-id="9ddf0-180">_originalUrl_</span></span> | <span data-ttu-id="9ddf0-181">Olá URL de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-181">hello URL of hello request.</span></span>                                        |
| <span data-ttu-id="9ddf0-182">_params_</span><span class="sxs-lookup"><span data-stu-id="9ddf0-182">_params_</span></span>      | <span data-ttu-id="9ddf0-183">Um objeto que contém parâmetros de roteamento de saudação da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-183">An object that contains hello routing parameters of hello request.</span></span> |
| <span data-ttu-id="9ddf0-184">_query_</span><span class="sxs-lookup"><span data-stu-id="9ddf0-184">_query_</span></span>       | <span data-ttu-id="9ddf0-185">Um objeto que contém os parâmetros de consulta hello.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-185">An object that contains hello query parameters.</span></span>                  |
| <span data-ttu-id="9ddf0-186">_rawBody_</span><span class="sxs-lookup"><span data-stu-id="9ddf0-186">_rawBody_</span></span>     | <span data-ttu-id="9ddf0-187">corpo de saudação de mensagem de saudação como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-187">hello body of hello message as a string.</span></span>                           |


### <a name="response-object"></a><span data-ttu-id="9ddf0-188">Objeto de resposta</span><span class="sxs-lookup"><span data-stu-id="9ddf0-188">Response object</span></span>

<span data-ttu-id="9ddf0-189">Olá `response` objeto tem Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ddf0-189">hello `response` object has hello following properties:</span></span>

| <span data-ttu-id="9ddf0-190">Propriedade</span><span class="sxs-lookup"><span data-stu-id="9ddf0-190">Property</span></span>  | <span data-ttu-id="9ddf0-191">Descrição</span><span class="sxs-lookup"><span data-stu-id="9ddf0-191">Description</span></span>                                               |
| --------- | --------------------------------------------------------- |
| <span data-ttu-id="9ddf0-192">_body_</span><span class="sxs-lookup"><span data-stu-id="9ddf0-192">_body_</span></span>    | <span data-ttu-id="9ddf0-193">Um objeto que contém Olá corpo da resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-193">An object that contains hello body of hello response.</span></span>         |
| <span data-ttu-id="9ddf0-194">_headers_</span><span class="sxs-lookup"><span data-stu-id="9ddf0-194">_headers_</span></span> | <span data-ttu-id="9ddf0-195">Um objeto que contém os cabeçalhos de resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-195">An object that contains hello response headers.</span></span>             |
| <span data-ttu-id="9ddf0-196">_isRaw_</span><span class="sxs-lookup"><span data-stu-id="9ddf0-196">_isRaw_</span></span>   | <span data-ttu-id="9ddf0-197">Indica que a formatação é ignorada para a resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-197">Indicates that formatting is skipped for hello response.</span></span>    |
| <span data-ttu-id="9ddf0-198">_status_</span><span class="sxs-lookup"><span data-stu-id="9ddf0-198">_status_</span></span>  | <span data-ttu-id="9ddf0-199">código de status HTTP da resposta de saudação do Hello.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-199">hello HTTP status code of hello response.</span></span>                     |

### <a name="accessing-hello-request-and-response"></a><span data-ttu-id="9ddf0-200">Acessando Olá solicitação e resposta</span><span class="sxs-lookup"><span data-stu-id="9ddf0-200">Accessing hello request and response</span></span> 

<span data-ttu-id="9ddf0-201">Quando você trabalha com gatilhos HTTP, você pode acessar objetos de solicitação e resposta HTTP de saudação em qualquer uma das três maneiras:</span><span class="sxs-lookup"><span data-stu-id="9ddf0-201">When you work with HTTP triggers, you can access hello HTTP request and response objects in any of three ways:</span></span>

+ <span data-ttu-id="9ddf0-202">De saudação denominado entrada e saída de associações.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-202">From hello named input and output bindings.</span></span> <span data-ttu-id="9ddf0-203">Dessa forma, o gatilho HTTP do hello e trabalho de associações Olá mesmo como qualquer outra associação.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-203">In this way, hello HTTP trigger and bindings work hello same as any other binding.</span></span> <span data-ttu-id="9ddf0-204">Olá exemplo a seguir define o objeto de resposta hello usando um conjunto nomeado `response` associação:</span><span class="sxs-lookup"><span data-stu-id="9ddf0-204">hello following example sets hello response object by using a named `response` binding:</span></span> 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ <span data-ttu-id="9ddf0-205">De `req` e `res` propriedades Olá `context` objeto.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-205">From `req` and `res` properties on hello `context` object.</span></span> <span data-ttu-id="9ddf0-206">Dessa forma, você pode usar dados de tooaccess HTTP de padrão convencional de saudação do objeto de contexto Olá, em vez de ter toouse Olá completo `context.bindings.name` padrão.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-206">In this way, you can use hello conventional pattern tooaccess HTTP data from hello context object, instead of having toouse hello full `context.bindings.name` pattern.</span></span> <span data-ttu-id="9ddf0-207">Olá mostrado no exemplo a seguir como Olá tooaccess `req` e `res` objetos Olá `context`:</span><span class="sxs-lookup"><span data-stu-id="9ddf0-207">hello following example shows how tooaccess hello `req` and `res` objects on hello `context`:</span></span>

    ```javascript
    // You can access your http request off hello context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ <span data-ttu-id="9ddf0-208">Chamando `context.done()`.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-208">By calling `context.done()`.</span></span> <span data-ttu-id="9ddf0-209">Um tipo especial de associação HTTP retorna a resposta de saudação que é passada toohello `context.done()` método.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-209">A special kind of HTTP binding returns hello response that is passed toohello `context.done()` method.</span></span> <span data-ttu-id="9ddf0-210">Olá seguir HTTP de saída associação define um `$return` parâmetro de saída:</span><span class="sxs-lookup"><span data-stu-id="9ddf0-210">hello following HTTP output binding defines a `$return` output parameter:</span></span>

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    <span data-ttu-id="9ddf0-211">Essa associação de saída espera toosupply resposta de hello quando você chamar `done()`, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="9ddf0-211">This output binding expects you toosupply hello response when you call `done()`, as follows:</span></span>

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a><span data-ttu-id="9ddf0-212">Versão do Node e gerenciamento de pacote</span><span class="sxs-lookup"><span data-stu-id="9ddf0-212">Node version and Package Management</span></span>
<span data-ttu-id="9ddf0-213">versão do nó Hello está bloqueada no momento em `6.5.0`.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-213">hello node version is currently locked at `6.5.0`.</span></span> <span data-ttu-id="9ddf0-214">Estamos investigando a adição de suporte para mais versões e para torná-las configuráveis.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-214">We're investigating adding support for more versions and making it configurable.</span></span>

<span data-ttu-id="9ddf0-215">Olá, as etapas a seguir permitem que você incluir pacotes em seu aplicativo de função:</span><span class="sxs-lookup"><span data-stu-id="9ddf0-215">hello following steps let you include packages in your function app:</span></span> 

1. <span data-ttu-id="9ddf0-216">Vá muito`https://<function_app_name>.scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-216">Go too`https://<function_app_name>.scm.azurewebsites.net`.</span></span>

2. <span data-ttu-id="9ddf0-217">Clique em **Console de Depuração** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-217">Click **Debug Console** > **CMD**.</span></span>

3. <span data-ttu-id="9ddf0-218">Vá muito`D:\home\site\wwwroot`e, em seguida, arraste o toohello de arquivo Package. JSON **wwwroot** pasta na metade superior do hello da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-218">Go too`D:\home\site\wwwroot`, and then drag your package.json file toohello **wwwroot** folder at hello top half of hello page.</span></span>  
    <span data-ttu-id="9ddf0-219">Você também pode carregar arquivos tooyour função aplicativo de outras maneiras.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-219">You can upload files tooyour function app in other ways also.</span></span> <span data-ttu-id="9ddf0-220">Para obter mais informações, consulte [tooupdate funcionamento arquivos do aplicativo](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="9ddf0-220">For more information, see [How tooupdate function app files](functions-reference.md#fileupdate).</span></span> 

4. <span data-ttu-id="9ddf0-221">Depois de saudação Package. JSON arquivo é carregado, execute Olá `npm install` do hello **console de execução remota de Kudu**.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-221">After hello package.json file is uploaded, run hello `npm install` command in hello **Kudu remote execution console**.</span></span>  
    <span data-ttu-id="9ddf0-222">Essa ação baixa pacotes de saudação indicados no arquivo de Package. JSON hello e reinicia Olá função app.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-222">This action downloads hello packages indicated in hello package.json file and restarts hello function app.</span></span>

<span data-ttu-id="9ddf0-223">Depois de hello pacotes necessários estão instalados, importá-los função tooyour chamando `require('packagename')`, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="9ddf0-223">After hello packages you need are installed, you import them tooyour function by calling `require('packagename')`, as in hello following example:</span></span>

```javascript
// Import hello underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

<span data-ttu-id="9ddf0-224">Você deve definir um `package.json` arquivo na raiz de saudação do seu aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-224">You should define a `package.json` file at hello root of your function app.</span></span> <span data-ttu-id="9ddf0-225">Arquivo de saudação definição permite que todas as funções no compartilhamento de aplicativo hello Olá mesmo pacotes armazenados em cache, que oferece um melhor desempenho de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-225">Defining hello file lets all functions in hello app share hello same cached packages, which gives hello best performance.</span></span> <span data-ttu-id="9ddf0-226">Se ocorrer um conflito de versão, você pode resolvê-lo adicionando um `package.json` arquivo na pasta de saudação de uma função específica.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-226">If a version conflict arises, you can resolve it by adding a `package.json` file in hello folder of a specific function.</span></span>  

## <a name="environment-variables"></a><span data-ttu-id="9ddf0-227">Variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="9ddf0-227">Environment variables</span></span>
<span data-ttu-id="9ddf0-228">tooget uma variável de ambiente ou um valor de configuração do aplicativo, use `process.env`, conforme mostrado no hello exemplo de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ddf0-228">tooget an environment variable or an app setting value, use `process.env`, as shown in hello following code example:</span></span>

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
## <a name="considerations-for-javascript-functions"></a><span data-ttu-id="9ddf0-229">Considerações para funções em JavaScript</span><span class="sxs-lookup"><span data-stu-id="9ddf0-229">Considerations for JavaScript functions</span></span>

<span data-ttu-id="9ddf0-230">Quando você trabalha com funções JavaScript, lembre-se de considerações Olá Olá duas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-230">When you work with JavaScript functions, be aware of hello considerations in hello following two sections.</span></span>

### <a name="choose-single-core-app-service-plans"></a><span data-ttu-id="9ddf0-231">Escolher Planos do Serviço de Aplicativo de núcleo único</span><span class="sxs-lookup"><span data-stu-id="9ddf0-231">Choose single-core App Service plans</span></span>

<span data-ttu-id="9ddf0-232">Quando você cria um aplicativo de função que usa Olá plano de serviço de aplicativo, é recomendável que você selecione um plano de núcleo único em vez de um plano com vários núcleos.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-232">When you create a function app that uses hello App Service plan, we recommend that you select a single-core plan rather than a plan with multiple cores.</span></span> <span data-ttu-id="9ddf0-233">Hoje, funções executa funções JavaScript com mais eficiência em VMs de núcleo único e usando as máquinas virtuais maiores não produz melhorias de desempenho Olá esperado.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-233">Today, Functions runs JavaScript functions more efficiently on single-core VMs, and using larger VMs does not produce hello expected performance improvements.</span></span> <span data-ttu-id="9ddf0-234">Quando for necessário, você poderá escalar horizontalmente manualmente adicionando mais instâncias de VM de núcleo único ou poderá habilitar o dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-234">When necessary, you can manually scale out by adding more single-core VM instances, or you can enable auto-scale.</span></span> <span data-ttu-id="9ddf0-235">Para saber mais, confira [Dimensionar a contagem de instâncias manual ou automaticamente](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9ddf0-235">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span></span>    

### <a name="typescript-and-coffeescript-support"></a><span data-ttu-id="9ddf0-236">Suporte a TypeScript e CoffeeScript</span><span class="sxs-lookup"><span data-stu-id="9ddf0-236">TypeScript and CoffeeScript support</span></span>
<span data-ttu-id="9ddf0-237">Porque suporte direto ainda não existe para CoffeeScript ou TypeScript de compilação automática por meio do tempo de execução hello, esse suporte precisa toobe tratado fora do tempo de execução hello, no momento da implantação.</span><span class="sxs-lookup"><span data-stu-id="9ddf0-237">Because direct support does not yet exist for auto-compiling TypeScript or CoffeeScript via hello runtime, such support needs toobe handled outside hello runtime, at deployment time.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9ddf0-238">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9ddf0-238">Next steps</span></span>
<span data-ttu-id="9ddf0-239">Para obter mais informações, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ddf0-239">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="9ddf0-240">Práticas recomendadas para o Azure Functions</span><span class="sxs-lookup"><span data-stu-id="9ddf0-240">Best practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="9ddf0-241">Referência do desenvolvedor do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="9ddf0-241">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="9ddf0-242">Referência do desenvolvedor de C# do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="9ddf0-242">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="9ddf0-243">Referência do desenvolvedor em F# do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="9ddf0-243">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="9ddf0-244">Gatilhos e de associações do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="9ddf0-244">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

