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
# <a name="azure-functions-javascript-developer-guide"></a>Guia do desenvolvedor de JavaScript do Azure Functions
> [!div class="op_single_selector"]
> * [Script C#](functions-reference-csharp.md)
> * [Script em F#](functions-reference-fsharp.md)
> * [JavaScript](functions-reference-node.md)
> 
> 

Olá experiência de JavaScript para funções do Azure torna fácil tooexport uma função, que é passada como um `context` objeto para se comunicar com o tempo de execução de saudação e para receber e enviar dados por meio de associações.

Este artigo pressupõe que você já leu Olá [referência do desenvolvedor do Azure funções](functions-reference.md).

## <a name="exporting-a-function"></a>Exportando uma função
Todas as funções JavaScript devem exportar um único `function` via `module.exports` Olá Runtime toofind Olá função e executá-lo. Esta função sempre deve incluir um objeto `context` .

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

Associações de `direction === "in"` são passadas como argumentos de função, o que significa que você pode usar [ `arguments` ](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically lidar com novas entradas (por exemplo, usando `arguments.length` tooiterate em todas as suas entradas). Essa funcionalidade é conveniente quando você tem apenas um gatilho e nenhuma entrada adicional, pois é possível acessar seus dados de gatilho de maneira previsível, sem fazer referência ao objeto `context`.

argumentos Olá sempre são passados função toohello na ordem Olá ocorrem em *function.json*, mesmo se você não especificá-los em sua instrução de exportações. Por exemplo, se você tiver `function(context, a, b)` e alterá-la muito`function(context, a)`, ainda é possível obter o valor de saudação do `b` no código de função referindo-se muito`arguments[3]`.

Todas as associações, independentemente de direção, também são passadas Olá `context` objeto (consulte Olá script a seguir). 

## <a name="context-object"></a>objeto de contexto
saudação de tempo de execução usa um `context` tooand de dados do objeto toopass de sua função e toolet você se comunicar com o tempo de execução de saudação.

Olá objeto de contexto é sempre a primeira função de tooa parâmetro hello e deve ser incluído porque tem métodos como `context.done` e `context.log`, que são necessárias toouse Olá runtime corretamente. Você pode nomear o objeto hello como desejar (por exemplo, `ctx` ou `c`).

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a>Propriedade context.bindings

```
context.bindings
```
Retorna um objeto nomeado que contém todos os dados de entrada e saída. Olá, por exemplo, após a definição de associação no seu *function.json* permite que você acesse Olá conteúdo da fila de saudação do hello `context.bindings.myInput` objeto. 

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

### <a name="contextdone-method"></a>Método context.done
```
context.done([err],[propertyBag])
```

Informa Olá em tempo de execução que terminou de seu código. Você deve chamar `context.done`, ou tempo de execução else hello nunca sabe que sua função é concluída e execução de saudação atingirá o tempo limite. 

Olá `context.done` método permite que você toopass fazer um tempo de execução de toohello de erro definidas pelo usuário e um conjunto de propriedades de propriedades que substituir propriedades Olá Olá `context.bindings` objeto.

```javascript
// Even though we set myOutput toohave:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object toohello done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// hello done method will overwrite hello myOutput binding toobe: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a>Método context.log  

```
context.log(message)
```
Permite que você toowrite toohello console logs de streaming no nível de rastreamento padrão hello. Em `context.log`adicionais de log métodos estão disponíveis que permitem a você escrever toohello log de console em outros níveis de rastreamento:


| Método                 | Descrição                                |
| ---------------------- | ------------------------------------------ |
| **error(_message_)**   | Grava o nível de tooerror log ou inferior.   |
| **warn(_message_)**    | Grava o nível de toowarning log ou inferior. |
| **info(_message_)**    | Grava o nível de tooinfo log ou inferior.    |
| **verbose(_message_)** | Grava o log de nível de tooverbose.           |

Olá, exemplo a seguir grava toohello console no nível de rastreamento de aviso hello:

```javascript
context.log.warn("Something has happened."); 
```
Você pode definir o limite do nível de rastreamento Olá para registrar em log no arquivo de host.json hello, ou desativá-lo.  Para obter mais informações sobre como toowrite toohello registra, consulte Olá próxima seção.

## <a name="binding-data-type"></a>Tipo de dados de associação

toodefine tipo de dados de saudação para uma associação de entrada, use Olá `dataType` propriedade na definição de associação de saudação. Por exemplo, tooread Olá conteúdo de uma solicitação HTTP em formato binário, use o tipo de saudação `binary`:

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

Outras opções para `dataType` são `stream` e `string`.

## <a name="writing-trace-output-toohello-console"></a>Console de toohello de saída de rastreamento de gravação 

Em funções, você usar Olá `context.log` console toohello de saída de rastreamento do métodos toowrite. Neste ponto, você não pode usar `console.log` toowrite toohello console.

Quando você chama `context.log()`, a mensagem é gravada toohello console no nível de rastreamento padrão Olá, é hello _informações_ o nível de rastreamento. Olá código a seguir grava toohello console no nível de rastreamento de informações de saudação:

```javascript
context.log({hello: 'world'});  
```

Olá código anterior é equivalente toohello código a seguir:

```javascript
context.log.info({hello: 'world'});  
```

Olá código a seguir grava toohello console no nível de erro hello:

```javascript
context.log.error("An error has occurred.");  
```

Porque _erro_ for hello mais alto nível, este rastreamento é gravado toohello saída em todos os níveis de rastreamento como o log está habilitado.  


Todos os `context.log` métodos oferecem suporte a saudação mesmo formato do parâmetro que é suportado pelo Olá Node. js [util.format método](https://nodejs.org/api/util.html#util_util_format_format). Considere Olá código, que grava toohello console usando o nível de rastreamento saudação padrão a seguir:

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

Você também pode Olá gravação mesmo código Olá formato a seguir:

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-hello-trace-level-for-console-logging"></a>Configurar o nível de rastreamento de saudação do log de console

Funções permite definir o nível de rastreamento de limite de saudação para gravar toohello console, o que torna fácil toocontrol maneira de saudação os rastreamentos são gravados toohello console de suas funções. limite de saudação tooset para todos os rastreamentos gravados toohello console, use Olá `tracing.consoleLevel` propriedade no arquivo de host.json hello. Essa configuração se aplica a funções de tooall em seu aplicativo de função. Olá, exemplo a seguir define Olá rastreamento limite tooenable o log detalhado:

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

Valores de **consoleLevel** correspondem toohello nomes de saudação `context.log` métodos. toodisable toohello console, de log de rastreamento de todos os conjunto **consoleLevel** too_off_. Para obter mais informações sobre o arquivo de host.json hello, consulte Olá [tópico de referência host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).

## <a name="http-triggers-and-bindings"></a>Gatilhos e associações HTTP

HTTP e gatilhos de webhook HTTP de saída e associações de usam a solicitação e resposta objetos toorepresent Olá HTTP mensagens.  

### <a name="request-object"></a>Objeto da solicitação

Olá `request` objeto tem Olá propriedades a seguir:

| Propriedade      | Descrição                                                    |
| ------------- | -------------------------------------------------------------- |
| _body_        | Um objeto que contém o corpo de saudação da solicitação de saudação.               |
| _headers_     | Um objeto que contém os cabeçalhos de solicitação de saudação.                   |
| _method_      | método HTTP da solicitação de saudação do Hello.                                |
| _originalUrl_ | Olá URL de solicitação de saudação.                                        |
| _params_      | Um objeto que contém parâmetros de roteamento de saudação da solicitação de saudação. |
| _query_       | Um objeto que contém os parâmetros de consulta hello.                  |
| _rawBody_     | corpo de saudação de mensagem de saudação como uma cadeia de caracteres.                           |


### <a name="response-object"></a>Objeto de resposta

Olá `response` objeto tem Olá propriedades a seguir:

| Propriedade  | Descrição                                               |
| --------- | --------------------------------------------------------- |
| _body_    | Um objeto que contém Olá corpo da resposta de saudação.         |
| _headers_ | Um objeto que contém os cabeçalhos de resposta de saudação.             |
| _isRaw_   | Indica que a formatação é ignorada para a resposta de saudação.    |
| _status_  | código de status HTTP da resposta de saudação do Hello.                     |

### <a name="accessing-hello-request-and-response"></a>Acessando Olá solicitação e resposta 

Quando você trabalha com gatilhos HTTP, você pode acessar objetos de solicitação e resposta HTTP de saudação em qualquer uma das três maneiras:

+ De saudação denominado entrada e saída de associações. Dessa forma, o gatilho HTTP do hello e trabalho de associações Olá mesmo como qualquer outra associação. Olá exemplo a seguir define o objeto de resposta hello usando um conjunto nomeado `response` associação: 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ De `req` e `res` propriedades Olá `context` objeto. Dessa forma, você pode usar dados de tooaccess HTTP de padrão convencional de saudação do objeto de contexto Olá, em vez de ter toouse Olá completo `context.bindings.name` padrão. Olá mostrado no exemplo a seguir como Olá tooaccess `req` e `res` objetos Olá `context`:

    ```javascript
    // You can access your http request off hello context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ Chamando `context.done()`. Um tipo especial de associação HTTP retorna a resposta de saudação que é passada toohello `context.done()` método. Olá seguir HTTP de saída associação define um `$return` parâmetro de saída:

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    Essa associação de saída espera toosupply resposta de hello quando você chamar `done()`, da seguinte maneira:

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a>Versão do Node e gerenciamento de pacote
versão do nó Hello está bloqueada no momento em `6.5.0`. Estamos investigando a adição de suporte para mais versões e para torná-las configuráveis.

Olá, as etapas a seguir permitem que você incluir pacotes em seu aplicativo de função: 

1. Vá muito`https://<function_app_name>.scm.azurewebsites.net`.

2. Clique em **Console de Depuração** > **CMD**.

3. Vá muito`D:\home\site\wwwroot`e, em seguida, arraste o toohello de arquivo Package. JSON **wwwroot** pasta na metade superior do hello da página de saudação.  
    Você também pode carregar arquivos tooyour função aplicativo de outras maneiras. Para obter mais informações, consulte [tooupdate funcionamento arquivos do aplicativo](functions-reference.md#fileupdate). 

4. Depois de saudação Package. JSON arquivo é carregado, execute Olá `npm install` do hello **console de execução remota de Kudu**.  
    Essa ação baixa pacotes de saudação indicados no arquivo de Package. JSON hello e reinicia Olá função app.

Depois de hello pacotes necessários estão instalados, importá-los função tooyour chamando `require('packagename')`, conforme mostrado no exemplo a seguir de saudação:

```javascript
// Import hello underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

Você deve definir um `package.json` arquivo na raiz de saudação do seu aplicativo de função. Arquivo de saudação definição permite que todas as funções no compartilhamento de aplicativo hello Olá mesmo pacotes armazenados em cache, que oferece um melhor desempenho de saudação. Se ocorrer um conflito de versão, você pode resolvê-lo adicionando um `package.json` arquivo na pasta de saudação de uma função específica.  

## <a name="environment-variables"></a>Variáveis de ambiente
tooget uma variável de ambiente ou um valor de configuração do aplicativo, use `process.env`, conforme mostrado no hello exemplo de código a seguir:

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
## <a name="considerations-for-javascript-functions"></a>Considerações para funções em JavaScript

Quando você trabalha com funções JavaScript, lembre-se de considerações Olá Olá duas seções a seguir.

### <a name="choose-single-core-app-service-plans"></a>Escolher Planos do Serviço de Aplicativo de núcleo único

Quando você cria um aplicativo de função que usa Olá plano de serviço de aplicativo, é recomendável que você selecione um plano de núcleo único em vez de um plano com vários núcleos. Hoje, funções executa funções JavaScript com mais eficiência em VMs de núcleo único e usando as máquinas virtuais maiores não produz melhorias de desempenho Olá esperado. Quando for necessário, você poderá escalar horizontalmente manualmente adicionando mais instâncias de VM de núcleo único ou poderá habilitar o dimensionamento automático. Para saber mais, confira [Dimensionar a contagem de instâncias manual ou automaticamente](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).    

### <a name="typescript-and-coffeescript-support"></a>Suporte a TypeScript e CoffeeScript
Porque suporte direto ainda não existe para CoffeeScript ou TypeScript de compilação automática por meio do tempo de execução hello, esse suporte precisa toobe tratado fora do tempo de execução hello, no momento da implantação. 

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte Olá recursos a seguir:

* [Práticas recomendadas para o Azure Functions](functions-best-practices.md)
* [Referência do desenvolvedor do Azure Functions](functions-reference.md)
* [Referência do desenvolvedor de C# do Azure Functions](functions-reference-csharp.md)
* [Referência do desenvolvedor em F# do Azure Functions](functions-reference-fsharp.md)
* [Gatilhos e de associações do Azure Functions](functions-triggers-bindings.md)

