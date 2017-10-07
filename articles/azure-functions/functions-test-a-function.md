---
title: "aaaTesting funções do Azure | Microsoft Docs"
description: Teste o Azure Functions usando Postman, cURL e Node.js.
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, funções, processamento de eventos, webhooks, computação dinâmica, arquitetura sem servidor, testes"
ms.assetid: c00f3082-30d2-46b3-96ea-34faf2f15f77
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/02/2017
ms.author: wesmc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a084f8dbc8089356c3c19d789dc9098f2bb63052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="strategies-for-testing-your-code-in-azure-functions"></a>Estratégias para testar seu código no Azure Functions

Este tópico demonstra Olá abordagens de várias funções de tootest maneiras, incluindo o uso de saudação gerais a seguir:

+ Ferramentas baseadas em HTTP, como cURL, Postman e até mesmo um navegador da Web para gatilhos baseados na Web
+ Gerenciador de armazenamento do Azure, os gatilhos tootest baseado no armazenamento do Azure
+ Guia de teste no portal do Azure funções hello
+ Função disparada por timer
+ Teste de aplicativo ou de estrutura

Todos esses métodos de teste usam uma função de gatilho HTTP que aceita entrada por meio de um corpo de solicitação uma consulta cadeia de caracteres hello ou de parâmetro. Você pode criar essa função na primeira seção do hello.

## <a name="create-a-function-for-testing"></a>Criar uma função para teste
Na maior parte deste tutorial, usamos uma versão ligeiramente modificada do hello HttpTrigger JavaScript template de função que está disponível quando você criar uma função. Se você precisar de ajuda para criar uma função, examinar isso [tutorial](functions-create-first-azure-function.md). Escolha Olá **HttpTrigger - JavaScript** modelo ao criar a função de teste hello no hello [portal do Azure].

Olá template de função padrão é basicamente uma função de "hello world" que exibe o nome de saudação voltar de solicitação corpo ou consulta de cadeia de caracteres parâmetro hello, `name=<your name>`.  Vamos atualizar código Olá tooalso permitem tooprovide Olá nome e um endereço como o conteúdo no corpo da solicitação de saudação do JSON. Função hello exibe essas cliente toohello voltar quando disponível.   

Atualize função hello com hello código, que usaremos para testar a seguir:

```javascript
module.exports = function (context, req) {
    context.log("HTTP trigger function processed a request. RequestUri=%s", req.originalUrl);
    context.log("Request Headers = " + JSON.stringify(req.headers));
    var res;

    if (req.query.name || (req.body && req.body.name)) {
        if (typeof req.query.name != "undefined") {
            context.log("Name was provided as a query string param...");
            res = ProcessNewUserInformation(context, req.query.name);
        }
        else {
            context.log("Processing user info from request body...");
            res = ProcessNewUserInformation(context, req.body.name, req.body.address);
        }
    }
    else {
        res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done(null, res);
};
function ProcessNewUserInformation(context, name, address) {
    context.log("Processing user information...");
    context.log("name = " + name);
    var echoString = "Hello " + name;
    var res;

    if (typeof address != "undefined") {
        echoString += "\n" + "hello address you provided is " + address;
        context.log("address = " + address);
    }
    res = {
        // status: 200, /* Defaults too200 */
        body: echoString
    };
    return res;
}
```

## <a name="test-a-function-with-tools"></a>Testar uma função com ferramentas
Fora Olá portal do Azure, há várias ferramentas que você pode usar tootrigger suas funções para teste. Elas incluem as ferramentas de teste de HTTP (baseado na interface do usuário e de linha de comando), ferramentas de acesso ao Armazenamento do Azure e até mesmo um navegador da web simples.

### <a name="test-with-a-browser"></a>Testar com um navegador
navegador da web de saudação é funções de tootrigger uma maneira simples por meio de HTTP. Você pode usar um navegador para solicitações GET que não exigem uma carga de corpo e usam apenas parâmetros de cadeia de caracteres de consulta.

função de saudação tootest anterior, definimos Olá cópia **função Url** do portal de saudação. Ele tem Olá formulário a seguir:

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

Acrescentar Olá `name` cadeia de caracteres de consulta do parâmetro toohello. Usar um nome real para Olá `<Enter a name here>` espaço reservado.

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

Colar Olá URL em seu navegador e você deve receber uma resposta semelhante toohello a seguir.

![Guia do navegador de captura de tela de cromo com resposta de teste](./media/functions-test-a-function/browser-test.png)

Este exemplo é navegador Chrome hello, o que encapsula Olá retornada a cadeia de caracteres em XML. Outros navegadores exibem apenas valor de cadeia de caracteres de saudação.

No portal de saudação **Logs** janela de saída a seguir toohello semelhante é registrada na execução de função hello:

    2016-03-23T07:34:59  Welcome, you are now connected toolog-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a>Testar com o Postman
Olá recomendado ferramenta tootest a maioria das funções é carteiro, que integra com o navegador Chrome de saudação. tooinstall carteiro, consulte [carteiro obter](https://www.getpostman.com/). O Postman fornece controle sobre muito mais atributos de uma solicitação HTTP.

> [!TIP]
> Use Olá HTTP ferramenta de teste que você está mais familiarizado. Aqui estão alguns tooPostman alternativas:  
>
> * [Fiddler](http://www.telerik.com/fiddler)  
> * [Paw](https://luckymarmot.com/paw)  
>
>

função de saudação tootest com um corpo de solicitação no carteiro:

1. Iniciar carteiro da saudação **aplicativos** botão no canto superior esquerdo de saudação de uma janela do navegador Chrome.
2. Copie a **Url da Função** e cole-a no Postman. Ele inclui um parâmetro de cadeia de caracteres de consulta Olá código de acesso.
3. Alterar o método hello HTTP muito**POST**.
4. Clique em **corpo** > **bruto**e adicione o seguinte de toohello semelhante de corpo de solicitação de JSON:

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. Clique em **Enviar**.

Olá imagem a seguir mostra exemplo de função do teste hello eco simples neste tutorial.

![Interface de usuário de captura de tela de Postman](./media/functions-test-a-function/postman-test.png)

No portal de saudação **Logs** janela de saída a seguir toohello semelhante é registrada na execução de função hello:

    2016-03-23T08:04:51  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-hello-command-line"></a>Teste com a rotação da linha de comando Olá
Muitas vezes, quando você estiver testando o software, não é necessário toolook qualquer adicional de Olá a linha de comando toohelp depurar seu aplicativo. Isso não é diferente com funções de teste. Observe que ondulação hello está disponível por padrão nos sistemas baseados em Linux. No Windows, você deve primeiro baixar e instalar Olá [ondulação ferramenta](https://curl.haxx.se/).

função de hello tootest que definimos anteriormente, Olá cópia **função URL** do portal de saudação. Ele tem Olá formulário a seguir:

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

Esta é a URL de saudação para o disparo de sua função. Testar isso, usando o comando de ondulação Olá Olá toomake de linha de comando de GET (`-G` ou `--get`) solicitação em relação a função hello:

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

Esse exemplo específico exige um parâmetro de cadeia de caracteres de consulta, que pode ser passado como dados (`-d`) no hello cURL comando:

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

Comando de execução Olá e você verá Olá após a saída da função hello na linha de comando hello:

![Saída de tela do Prompt de comando](./media/functions-test-a-function/curl-test.png)

No portal de saudação **Logs** janela de saída a seguir toohello semelhante é registrada na execução de função hello:

    2016-04-05T21:55:09  Welcome, you are now connected toolog-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a>Testar um gatilho de blob usando o Gerenciador de Armazenamento
Você pode testar uma função de gatilho de blob usando o [Gerenciador de Armazenamento do Azure](http://storageexplorer.com/).

1. Em Olá [portal do Azure] para seu aplicativo de função, crie uma função de gatilho de blob do c#, F # ou JavaScript. Definir Olá caminho toomonitor toohello nome do seu contêiner de blob. Por exemplo:

        files
2. Clique em Olá  **+**  botão tooselect ou criar conta de armazenamento Olá toouse desejado. Em seguida, clique em **Criar**.
3. Criar um arquivo de texto com hello texto a seguir e salve-o:

        A text file for blob trigger function testing.
4. Executar [Azure Storage Explorer](http://storageexplorer.com/)e conecte-se o contêiner de blob toohello na conta de armazenamento hello está sendo monitorada.
5. Clique em **carregar** arquivo de texto de saudação tooupload.

    ![Captura de tela do Gerenciador de Armazenamento](./media/functions-test-a-function/azure-storage-explorer-test.png)

o código de função de gatilho do saudação padrão blob relata o processamento de saudação do blob Olá Olá logs:

    2016-03-24T11:30:10  Welcome, you are now connected toolog-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a>Testar uma função dentro de funções
Olá portal funções do Azure é projetado toolet teste HTTP e timer disparado funções. Você também pode criar funções tootrigger outras funções que você está testando.

### <a name="test-with-hello-functions-portal-run-button"></a>Teste com o botão de portal executar Olá funções
Olá portal fornece um **executar** botão que você pode usar algumas toodo limitado de testes. Você pode fornecer um corpo de solicitação usando o botão hello, mas você não pode fornecer parâmetros de cadeia de caracteres de consulta ou atualização de cabeçalhos de solicitação.

Testar função do gatilho Olá HTTP criado anteriormente, adicionando um toohello semelhante da cadeia de caracteres JSON a seguir no hello **corpo da solicitação** campo. Em seguida, clique em Olá **executar** botão.

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

No portal de saudação **Logs** janela de saída a seguir toohello semelhante é registrada na execução de função hello:

    2016-03-23T08:03:12  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a>Testar com um gatilho de temporizador
Algumas funções não podem ser testadas adequadamente com ferramentas Olá mencionadas anteriormente. Por exemplo, considere uma função de gatilho de fila executada quando uma mensagem é inserida no [Armazenamento de Filas do Azure](../storage/queues/storage-dotnet-how-to-use-queues.md). Você sempre pode escrever uma mensagem de toodrop de código em sua fila, e um exemplo em um projeto de console é fornecido neste artigo. No entanto, há outra abordagem que você pode usar para testar com funções diretamente.  

Você pode usar um gatilho de temporizador configurado com uma associação de saída da fila. Esse código de gatilho de timer, em seguida, pode gravar a fila de toohello de mensagens de teste hello. Esta seção explica um exemplo.

Para obter informações mais detalhadas sobre como usar associações com funções do Azure, consulte Olá [referência do desenvolvedor do Azure funções](functions-reference.md).

#### <a name="create-a-queue-trigger-for-testing"></a>Criar um gatilho de fila para teste
toodemonstrate essa abordagem, podemos primeiro criar uma função de gatilho de fila que queremos tootest para uma fila denominada `queue-newusers`. Essa função processa as informações de nome e endereço soltas no armazenamento de Filas para um novo usuário.

> [!NOTE]
> Se você usar um nome de fila diferente, certifique-se de toohello está de acordo com nome hello usado [nomeando filas e metadados](https://msdn.microsoft.com/library/dd179349.aspx) regras. Caso contrário, você obterá um erro.
>
>

1. Em Olá [portal do Azure] para seu aplicativo de função, clique em **nova função** > **QueueTrigger - C#**.
2. Digite toobe de nome de fila Olá monitorado pela função de fila hello:

        queue-newusers
3. Clique em Olá  **+**  botão tooselect ou criar conta de armazenamento Olá toouse desejado. Em seguida, clique em **Criar**.
4. Deixe essa janela de navegador portal aberto, para que você possa monitorar entradas de log Olá para o código de modelo de função de fila do saudação padrão.

#### <a name="create-a-timer-trigger-toodrop-a-message-in-hello-queue"></a>Criar um toodrop de gatilho de timer uma mensagem na fila de saudação
1. Olá abrir [portal do Azure] em uma nova janela do navegador e navegue tooyour função app.
2. Clique em **Nova Função** > **TimerTrigger - C#**. Insira um tooset de expressão cron frequência hello timer código testa sua função de fila. Em seguida, clique em **Criar**. Se você quiser Olá teste toorun a cada 30 segundos, você pode usar o seguinte Olá [expressão CRON](https://wikipedia.org/wiki/Cron#CRON_expression):

        */30 * * * * *
3. Clique em Olá **integrar** guia para seu novo gatilho de timer.
4. Em **saída**, clique em **+ nova saída**. Em seguida, clique em **fila** e **selecione**.
5. Nome da observação Olá usar para Olá **objeto de mensagem da fila**. Você pode usar isso no código da função hello timer.

        myQueue
6. Insira o nome da fila Olá onde a mensagem é enviada:

        queue-newusers
7. Clique em Olá  **+**  tooselect conta de armazenamento de saudação você usou anteriormente com um gatilho de fila de saudação de botão. Em seguida, clique em **Salvar**.
8. Clique em Olá **desenvolver** guia para o gatilho de timer.
9. Você pode usar o hello seguindo o código para a função de temporizador hello c#, desde que você usou Olá mesmo nome de objeto de mensagem mostrada anteriormente da fila. Em seguida, clique em **Salvar**.

    ```cs
    using System;

    public static void Run(TimerInfo myTimer, out String myQueue, TraceWriter log)
    {
        String newUser =
        "{\"name\":\"User testing from C# timer function\",\"address\":\"XYZ\"}";

        log.Verbose($"C# Timer trigger function executed at: {DateTime.Now}");   
        log.Verbose($"{newUser}");   

        myQueue = newUser;
    }
    ```

Neste ponto, Olá função c# de timer executa a cada 30 segundos se você usou a expressão de cron de exemplo hello. cada execução de relatório de logs Olá para a função de temporizador hello:

    2016-03-24T10:27:02  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

Na janela do navegador para a função de fila Olá Olá, você pode ver cada mensagem que está sendo processada:

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a>Testar uma função com código
Talvez seja necessário toocreate um tootest externo do aplicativo ou framework suas funções.

### <a name="test-an-http-trigger-function-with-code-nodejs"></a>Testar uma função de gatilho HTTP com código: Node.js
Você pode usar um aplicativo de Node. js tooexecute um tootest de solicitação HTTP em sua função.
Verifique se tooset:

* Olá `host` no host de aplicativo hello solicitação opções tooyour função.
* O nome da função no hello `path`.
* O código de acesso (`<your code>`) no hello `path`.

Exemplo de código:

```javascript
var http = require("http");

var nameQueryString = "name=Wes%20Query%20String%20Test%20From%20Node.js";

var nameBodyJSON = {
    name : "Wes testing with Node.JS code",
    address : "Dallas, T.X. 75201"
};

var bodyString = JSON.stringify(nameBodyJSON);

var options = {
  host: "functions841def78.azurewebsites.net",
  //path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9&" + nameQueryString,
  path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9",
  method: "POST",
  headers : {
      "Content-Type":"application/json",
      "Content-Length": Buffer.byteLength(bodyString)
    }    
};

callback = function(response) {
  var str = ""
  response.on("data", function (chunk) {
    str += chunk;
  });

  response.on("end", function () {
    console.log(str);
  });
}

var req = http.request(options, callback);
console.log("*** Sending name and address in body ***");
console.log(bodyString);
req.end(bodyString);
```


Saída:

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    hello address you provided is Dallas, T.X. 75201

No portal de saudação **Logs** janela de saída a seguir toohello semelhante é registrada na execução de função hello:

    2016-03-23T08:08:55  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a>Testar uma função de gatilho de fila com o código: C# #
Mencionamos anteriormente que você pode testar um gatilho de fila usando código toodrop uma mensagem na fila. Olá, código de exemplo a seguir baseia-se Olá c# código apresentado Olá [guia de Introdução ao armazenamento de fila do Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) tutorial. Também há código para outras linguagens disponível nesse link.

tootest esse código em um aplicativo de console, você deve:

* [Configurar a cadeia de caracteres de conexão de armazenamento no arquivo App. config de saudação](../storage/queues/storage-dotnet-how-to-use-queues.md).
* Passar um `name` e `address` como parâmetros toohello aplicativo. Por exemplo: `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`. (Este código aceita Olá nome e endereço de um novo usuário como argumentos de linha de comando durante o tempo de execução.)

Código C# de exemplo:

```cs
static void Main(string[] args)
{
    string name = null;
    string address = null;
    string queueName = "queue-newusers";
    string JSON = null;

    if (args.Length > 0)
    {
        name = args[0];
    }
    if (args.Length > 1)
    {
        address = args[1];
    }

    // Retrieve storage account from connection string
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["StorageConnectionString"]);

    // Create hello queue client
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

    // Retrieve a reference tooa queue
    CloudQueue queue = queueClient.GetQueueReference(queueName);

    // Create hello queue if it doesn't already exist
    queue.CreateIfNotExists();

    // Create a message and add it toohello queue.
    if (name != null)
    {
        if (address != null)
            JSON = String.Format("{{\"name\":\"{0}\",\"address\":\"{1}\"}}", name, address);
        else
            JSON = String.Format("{{\"name\":\"{0}\"}}", name);
    }

    Console.WriteLine("Adding message too" + queueName + "...");
    Console.WriteLine(JSON);

    CloudQueueMessage message = new CloudQueueMessage(JSON);
    queue.AddMessage(message);
}
```

Na janela do navegador para a função de fila Olá Olá, você pode ver cada mensagem que está sendo processada:

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[portal do Azure]: https://portal.azure.com
