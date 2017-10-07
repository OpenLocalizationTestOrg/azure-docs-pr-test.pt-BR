---
title: "associações de HTTP de funções e webhook aaaAzure | Microsoft Docs"
description: "Entender como toouse HTTP e webhook gatilhos e associações em funções do Azure."
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, funções, processamento de eventos, webhooks, computação dinâmica, arquitetura sem servidor, HTTP, API, REST"
ms.assetid: 2b12200d-63d8-4ec1-9da8-39831d5a51b1
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/18/2016
ms.author: mahender
ms.openlocfilehash: c23b7a1443d492ed78c595e97d1d778a7ab12416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a>Associações HTTP e de webhook do Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artigo explica como tooconfigure e trabalhar com HTTP dispara e associações em funções do Azure.
Com isso, você pode usar funções do Azure toobuild serverless APIs e responder toowebhooks.

As funções do Azure fornece Olá associações a seguir:
- Um [gatilho HTTP](#httptrigger) permite invocar uma função com uma solicitação HTTP. Isso pode ser personalizado toorespond muito[webhooks](#hooktrigger).
- Um [HTTP de saída associação](#output) permite que você toorespond toohello solicitação.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a>Gatilho HTTP
gatilho HTTP Olá executará a função na solicitação HTTP tooan resposta. Você pode personalizá-lo toorespond tooa URL em particular ou conjunto de métodos HTTP. Um gatilho HTTP também pode ser configurado toorespond toowebhooks. 

Se usando o portal de funções hello, você pode também começar imediatamente usando um modelo predefinido. Selecione **nova função** e escolha "API & Webhooks" hello **cenário** lista suspensa. Selecione um dos modelos de saudação e clique em **criar**.

Por padrão, um gatilho HTTP responderá toohello solicitação com um código de status HTTP 200 Okey e um corpo vazio. toomodify Olá resposta, configure um [associação de saída HTTP](#output)

### <a name="configuring-an-http-trigger"></a>Configuração de um gatilho HTTP
Um gatilho HTTP é definido, incluindo um toohello semelhante do objeto JSON a seguir no hello `bindings` matriz de function.json:

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function",
    "methods": [ "get" ],
    "route": "values/{id}"
},
```
associação de saudação oferece suporte a saudação propriedades a seguir:

* **nome** : necessária – o nome da variável Olá usado no código de função para solicitação de saudação ou o corpo da solicitação. Veja [Como trabalhar com um gatilho HTTP no código](#httptriggerusage).
* **tipo** : necessária - deve ser definido muito "httpTrigger".
* **direção** : necessária - deve ser definido muito "in".
* _authLevel_ : Isso determina quais chaves, se houver, toobe presente na solicitação de saudação na função de saudação tooinvoke order. Veja [Como trabalhar com chaves](#keys) abaixo. valor de saudação pode ser um dos seguintes hello:
    * _anonymous_: nenhuma chave API é obrigatória.
    * _function_: uma chave de API específica de função é obrigatória. Este é o valor de padrão de saudação se nenhum for fornecido.
    * _administrador_ : Olá mestre chave é necessária.
* **métodos** : esta é uma matriz dos métodos Olá HTTP função hello de toowhich responderá. Se não for especificado, a função hello responderá métodos tooall HTTP. Consulte [Personalizando o ponto de extremidade Olá HTTP](#url).
* **rota** : Isso define o modelo de rota hello, controlando toowhich solicitar URLs sua função responderá. Olá valor padrão se nenhum for fornecido é `<functionname>`. Consulte [Personalizando o ponto de extremidade Olá HTTP](#url).
* **webHookType** : Isso configura Olá HTTP gatilho tooact como um receptor do webhook para o provedor especificado hello. Olá _métodos_ propriedade não deve ser definida se isso for escolhido. Consulte [toowebhooks respondendo](#hooktrigger). valor de saudação pode ser um dos seguintes hello:
    * _genericJson_: um ponto de extremidade de webhook de finalidade geral sem lógica para um provedor específico.
    * _GitHub_ : função hello responderá tooGitHub webhooks. Olá _authLevel_ propriedade não deve ser definida se isso for escolhido.
    * _margem de atraso_ : função hello responderá tooSlack webhooks. Olá _authLevel_ propriedade não deve ser definida se isso for escolhido.

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a>Como trabalhar com um gatilho HTTP no código
Para funções do c# e F #, você pode declarar tipo de saudação do seu toobe de entrada do gatilho ou `HttpRequestMessage` ou um tipo personalizado. Se você escolher `HttpRequestMessage`, em seguida, você obterá o objeto de solicitação de toohello acesso completo. Para um tipo personalizado (como um POCO), funções tentarão corpo da solicitação tooparse hello como propriedades do objeto JSON toopopulate hello.

Para funções do Node. js, o tempo de execução de funções de saudação fornece corpo da solicitação Olá em vez do objeto de solicitação de saudação.

Veja [Exemplos de gatilho HTTP](#httptriggersample) para ver os exemplos de uso.


<a name="output"></a>
## <a name="http-response-output-binding"></a>Associação de saída de resposta HTTP
Use Olá HTTP saída associação toorespond toohello HTTP solicitação remetente. Essa associação requer um gatilho HTTP e permite resposta de saudação toocustomize associada à solicitação do disparador hello. Se a associação de saída HTTP não for fornecida, um gatilho HTTP retornará HTTP 200 OK com um corpo vazio. 

### <a name="configuring-an-http-output-binding"></a>Configuração de uma associação de saída HTTP
Olá HTTP de saída associação é definida, incluindo um toohello semelhante do objeto JSON a seguir no hello `bindings` matriz de function.json:

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
associação de saudação contém Olá propriedades a seguir:

* **nome** : necessária - Olá usado no código de função para a resposta de saudação do nome de variável. Veja [Como trabalhar com uma associação de saída no código](#outputusage).
* **tipo** : necessária - deve ser definido muito "http".
* **direção** : necessária - deve ser definido muito "out".

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a>Como trabalhar com uma associação de saída no código
Você pode usar o hello saída parâmetro (por exemplo, "res") toorespond toohello http ou webhook chamador. Como alternativa, você pode usar o padrão `Request.CreateResponse()` (c#) ou `context.res` (Node. js) padrão tooreturn sua resposta. Para obter exemplos de como toouse Olá último método, consulte [exemplos de gatilho HTTP](#httptriggersample) e [exemplos de gatilho de Webhook](#hooktriggersample).


<a name="hooktrigger"></a>
## <a name="responding-toowebhooks"></a>Responder toowebhooks
Um gatilho HTTP com hello _webHookType_ propriedade serão configurado toorespond muito[webhooks](https://en.wikipedia.org/wiki/Webhook). configuração básica do Hello usa configuração de "genericJson" hello. Isso restringe solicitações tooonly aqueles usando HTTP POST e Olá `application/json` tipo de conteúdo.

Olá gatilho pode ser personalizada tooa webhook específico provedor (por exemplo, [GitHub](https://developer.github.com/webhooks/) e [Slack](https://api.slack.com/outgoing-webhooks)). Se um provedor for especificado, tempo de execução de funções hello pode cuidar da lógica de validação do provedor Olá para você.  

### <a name="configuring-github-as-a-webhook-provider"></a>Configurando o GitHub como um provedor de webhook
toorespond tooGitHub webhooks, primeiro crie a função com um gatilho de HTTP e defina Olá _webHookType_ propriedade muito "github". Em seguida, copie a [URL](#url) e a [chave de API](#keys) na página **Adicionar webhook** do seu repositório GitHub. Veja a documentação sobre [como criar webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) do GitHub para saber mais.

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a>Configuração do Slack como um provedor de webhook
webhook atraso Hello gera um token para você em vez de deixar a especificá-lo, portanto você deve configurar uma chave específica de função com o token de saudação do atraso. Veja [Como trabalhar com chaves](#keys).

<a name="url"></a>
## <a name="customizing-hello-http-endpoint"></a>Personalizando o ponto de extremidade HTTP Olá
Por padrão quando você cria uma função para um gatilho HTTP ou WebHook, função hello é endereçável com uma rota do formulário de saudação:

    http://<yourapp>.azurewebsites.net/api/<funcname> 

Você pode personalizar essa rota usando Olá opcional `route` propriedade no disparador Olá HTTP da associação de entrada. Por exemplo, Olá a seguir *function.json* arquivo define uma `route` propriedade para um gatilho HTTP:

```json
    {
      "bindings": [
        {
          "type": "httpTrigger",
          "name": "req",
          "direction": "in",
          "methods": [ "get" ],
          "route": "products/{category:alpha}/{id:int?}"
        },
        {
          "type": "http",
          "name": "res",
          "direction": "out"
        }
      ]
    }
```

Usando esta configuração, função hello agora é endereçável por hello rota em vez de rota originais Olá a seguir.

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

Isso permite que o código de função hello toosupport dois parâmetros no endereço hello, "categoria" e "id". Você pode usar qualquer [Restrição de rota de API Web](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) com seus parâmetros. Olá código da função c# a seguir faz uso de ambos os parâmetros.

```csharp
    public static Task<HttpResponseMessage> Run(HttpRequestMessage req, string category, int? id, 
                                                    TraceWriter log)
    {
        if (id == null)
           return  req.CreateResponse(HttpStatusCode.OK, $"All {category} items were requested.");
        else
           return  req.CreateResponse(HttpStatusCode.OK, $"{category} item with id = {id} has been requested.");
    }
```

Aqui está saudação do Node. js função código toouse os mesmos parâmetros de rota.

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

Por padrão, todas as rotas de função são prefixadas com *api*. Você também pode personalizar ou remover prefixo hello usando Olá `http.routePrefix` propriedade em seu *host.json* arquivo. Olá, exemplo a seguir remove Olá *api* prefixo da rota usando uma cadeia de caracteres vazia para o prefixo Olá Olá *host.json* arquivo.

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

Para obter informações detalhadas sobre como Olá tooupdate *host.json* arquivo de sua função, consulte [tooupdate funcionamento arquivos do aplicativo](functions-reference.md#fileupdate). 

Para obter informações sobre outras propriedades que você pode configurar no seu arquivo *host.json*, consulte [referência host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).


<a name="keys"></a>
## <a name="working-with-keys"></a>Como trabalhar com chaves
HttpTriggers pode aproveitar as chaves para aumentar a segurança. Um padrão HttpTrigger pode usá-los como uma chave de API, a necessidade Olá a chave toobe presente na solicitação de saudação. Webhooks pode usar chaves tooauthorize solicitações de várias maneiras, dependendo de qual provedor Olá oferece suporte.

As chaves são armazenadas como parte do seu aplicativo de funções no Azure e criptografadas em repouso. tooview suas chaves, criar novos roll toonew valores de chaves, navegar tooone das funções no portal de saudação e selecione "Gerenciar". 

Há dois tipos de chave:
- **As chaves de host**: essas chaves são compartilhadas por todas as funções no aplicativo de função hello. Quando usado como uma chave de API, elas permitem acesso tooany função no aplicativo de função hello.
- **Teclas de função**: essas chaves se aplicam somente toohello funções específicas sob as quais elas são definidas. Quando usado como uma chave de API, somente permite acesso toothat função.

Cada chave é nomeado para referência e há uma chave padrão (denominada "padrão") no nível de host e a função hello. Olá **chave mestra** uma chave de host padrão chamada "_master" que é definido para cada função de aplicativo e não pode ser revogado. Ele fornece acesso administrativo toohello runtime APIs. Usando `"authLevel": "admin"` em Olá associação JSON exigirá essa chave toobe apresentada na solicitação Olá; qualquer outra chave resultará em uma falha de autorização.

> [!NOTE]
> Vencimento toohello elevados de permissões concedidas pela chave mestra de saudação, você não deve compartilhar essa chave com terceiros ou distribuí-lo em aplicativos cliente nativo. Tenha cuidado ao escolher o nível de autorização do administrador de saudação.
> 
> 

### <a name="api-key-authorization"></a>Autorização da chave de API
Por padrão, um HttpTrigger requer uma chave de API na solicitação HTTP hello. Portanto, sua solicitação HTTP geralmente se parecerá como esta:

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

chave de saudação pode ser incluído em uma variável de cadeia de caracteres de consulta chamada `code`, como acima, ou ele pode ser incluído em um `x-functions-key` cabeçalho HTTP. valor de saudação da chave Olá pode ser qualquer tecla de função definido para a função hello, ou qualquer chave de host.

Você pode escolher solicitações tooallow sem chaves ou especificar a chave mestra Olá deve ser usado por meio da alteração Olá `authLevel` propriedade Olá associação JSON (consulte [gatilho HTTP](#httptrigger)).

### <a name="keys-and-webhooks"></a>Chaves e webhooks
Autorização de Webhook é tratada pelo componente de receptor de webhook Olá, parte da saudação HttpTrigger e mecanismo Olá varia com base no tipo de webhook Olá. No entanto, cada mecanismo depende de uma chave. Por padrão, a tecla de função hello denominada "padrão" será usada. Se você desejar toouse uma chave diferente, você precisará tooconfigure Olá provedor toosend Olá chave o nome do webhook com solicitação de saudação em uma saudação maneiras a seguir:

- **Cadeia de caracteres de consulta**: provedor Olá passa o nome da chave Olá Olá `clientid` parâmetro de cadeia de caracteres de consulta (por exemplo, `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).
- **Cabeçalho de solicitação**: provedor Olá passa o nome da chave Olá Olá `x-functions-clientid` cabeçalho.

> [!NOTE]
> As chaves de função têm precedência sobre as chaves de host. Se duas chaves são definidas com o mesmo nome, hello de saudação tecla de função que será usada.
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a>Exemplos de gatilho HTTP
Suponha que você tenha Olá seguindo gatilho HTTP no hello `bindings` matriz de function.json:

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

Consulte Olá específico do idioma exemplo procura um `name` parâmetro na cadeia de caracteres de consulta de saudação ou corpo de saudação da solicitação de saudação HTTP.

* [C#](#httptriggercsharp)
* [F#](#httptriggerfsharp)
* [Node.js](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a>Exemplo de gatilho HTTP em C# #
```csharp
using System.Net;
using System.Threading.Tasks;

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
{
    log.Info($"C# HTTP trigger function processed a request. RequestUri={req.RequestUri}");

    // parse query parameter
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    // Get request body
    dynamic data = await req.Content.ReadAsAsync<object>();

    // Set name tooquery string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

Você também pode associar tooa POCO em vez de `HttpRequestMessage`. Isso será ser serializado do corpo de saudação da solicitação hello, analisada como JSON. Da mesma forma, um tipo pode ser passado a saída de resposta de toohello HTTP de associação, e isso será retornado como o corpo da resposta hello, com um código de 200 status.
```csharp
using System.Net;
using System.Threading.Tasks;

public static string Run(CustomObject req, TraceWriter log)
{
    return "Hello " + req?.name;
}

public class CustomObject {
     public String name {get; set;}
}
}
```

<a name="httptriggerfsharp"></a>
### <a name="http-trigger-sample-in-f"></a>Exemplo de gatilho HTTP em F# #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic

let Run(req: HttpRequestMessage) =
    async {
        let q =
            req.GetQueryNameValuePairs()
                |> Seq.tryFind (fun kv -> kv.Key = "name")
        match q with
        | Some kv ->
            return req.CreateResponse(HttpStatusCode.OK, "Hello " + kv.Value)
        | None ->
            let! data = Async.AwaitTask(req.Content.ReadAsAsync<obj>())
            try
                return req.CreateResponse(HttpStatusCode.OK, "Hello " + data?name)
            with e ->
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
    } |> Async.StartAsTask
```

É necessário um `project.json` arquivo que usa NuGet tooreference Olá `FSharp.Interop.Dynamic` e `Dynamitey` assemblies, como este:

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

Isso usará NuGet toofetch suas dependências e fará referência-los em seu script.

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a>Exemplo de gatilho HTTP em Node.JS
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults too200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a>Exemplos de webhook
Suponha que você tenha Olá seguindo gatilho webhook Olá `bindings` matriz de function.json:

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

Consulte Olá específico do idioma exemplo registra comentários de problema do GitHub.

* [C#](#hooktriggercsharp)
* [F#](#hooktriggerfsharp)
* [Node.js](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a>Exemplo de webhook em C# #
```csharp
#r "Newtonsoft.Json"

using System;
using System.Net;
using System.Threading.Tasks;
using Newtonsoft.Json;

public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
{
    string jsonContent = await req.Content.ReadAsStringAsync();
    dynamic data = JsonConvert.DeserializeObject(jsonContent);

    log.Info($"WebHook was triggered! Comment: {data.comment.body}");

    return req.CreateResponse(HttpStatusCode.OK, new {
        body = $"New GitHub comment: {data.comment.body}"
    });
}
```

<a name="hooktriggerfsharp"></a>

### <a name="webhook-sample-in-f"></a>Exemplo de webhook em F# #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Response = {
    body: string
}

let Run(req: HttpRequestMessage, log: TraceWriter) =
    async {
        let! content = req.Content.ReadAsStringAsync() |> Async.AwaitTask
        let data = content |> JsonConvert.DeserializeObject
        log.Info(sprintf "GitHub WebHook triggered! %s" data?comment?body)
        return req.CreateResponse(
            HttpStatusCode.OK,
            { body = sprintf "New GitHub comment: %s" data?comment?body })
    } |> Async.StartAsTask
```

<a name="hooktriggernodejs"></a>

### <a name="webhook-sample-in-nodejs"></a>Exemplo de webhook em Node.JS
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

