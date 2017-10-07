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
# <a name="strategies-for-testing-your-code-in-azure-functions"></a><span data-ttu-id="66c58-104">Estratégias para testar seu código no Azure Functions</span><span class="sxs-lookup"><span data-stu-id="66c58-104">Strategies for testing your code in Azure Functions</span></span>

<span data-ttu-id="66c58-105">Este tópico demonstra Olá abordagens de várias funções de tootest maneiras, incluindo o uso de saudação gerais a seguir:</span><span class="sxs-lookup"><span data-stu-id="66c58-105">This topic demonstrates hello various ways tootest functions, including using hello following general approaches:</span></span>

+ <span data-ttu-id="66c58-106">Ferramentas baseadas em HTTP, como cURL, Postman e até mesmo um navegador da Web para gatilhos baseados na Web</span><span class="sxs-lookup"><span data-stu-id="66c58-106">HTTP-based tools, such as cURL, Postman, and even a web browser for web-based triggers</span></span>
+ <span data-ttu-id="66c58-107">Gerenciador de armazenamento do Azure, os gatilhos tootest baseado no armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="66c58-107">Azure Storage Explorer, tootest Azure Storage-based triggers</span></span>
+ <span data-ttu-id="66c58-108">Guia de teste no portal do Azure funções hello</span><span class="sxs-lookup"><span data-stu-id="66c58-108">Test tab in hello Azure Functions portal</span></span>
+ <span data-ttu-id="66c58-109">Função disparada por timer</span><span class="sxs-lookup"><span data-stu-id="66c58-109">Timer-triggered function</span></span>
+ <span data-ttu-id="66c58-110">Teste de aplicativo ou de estrutura</span><span class="sxs-lookup"><span data-stu-id="66c58-110">Testing application or framework</span></span>

<span data-ttu-id="66c58-111">Todos esses métodos de teste usam uma função de gatilho HTTP que aceita entrada por meio de um corpo de solicitação uma consulta cadeia de caracteres hello ou de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="66c58-111">All these testing methods use an HTTP trigger function that accepts input through either a query string parameter or hello request body.</span></span> <span data-ttu-id="66c58-112">Você pode criar essa função na primeira seção do hello.</span><span class="sxs-lookup"><span data-stu-id="66c58-112">You create this function in hello first section.</span></span>

## <a name="create-a-function-for-testing"></a><span data-ttu-id="66c58-113">Criar uma função para teste</span><span class="sxs-lookup"><span data-stu-id="66c58-113">Create a function for testing</span></span>
<span data-ttu-id="66c58-114">Na maior parte deste tutorial, usamos uma versão ligeiramente modificada do hello HttpTrigger JavaScript template de função que está disponível quando você criar uma função.</span><span class="sxs-lookup"><span data-stu-id="66c58-114">For most of this tutorial, we use a slightly modified version of hello HttpTrigger JavaScript function template that is available when you create a function.</span></span> <span data-ttu-id="66c58-115">Se você precisar de ajuda para criar uma função, examinar isso [tutorial](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="66c58-115">If you need help creating a function, review this [tutorial](functions-create-first-azure-function.md).</span></span> <span data-ttu-id="66c58-116">Escolha Olá **HttpTrigger - JavaScript** modelo ao criar a função de teste hello no hello [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="66c58-116">Choose hello **HttpTrigger- JavaScript** template when creating hello test function in hello [Azure portal].</span></span>

<span data-ttu-id="66c58-117">Olá template de função padrão é basicamente uma função de "hello world" que exibe o nome de saudação voltar de solicitação corpo ou consulta de cadeia de caracteres parâmetro hello, `name=<your name>`.</span><span class="sxs-lookup"><span data-stu-id="66c58-117">hello default function template is basically a "hello world" function that echoes back hello name from hello request body or query string parameter, `name=<your name>`.</span></span>  <span data-ttu-id="66c58-118">Vamos atualizar código Olá tooalso permitem tooprovide Olá nome e um endereço como o conteúdo no corpo da solicitação de saudação do JSON.</span><span class="sxs-lookup"><span data-stu-id="66c58-118">We'll update hello code tooalso allow you tooprovide hello name and an address as JSON content in hello request body.</span></span> <span data-ttu-id="66c58-119">Função hello exibe essas cliente toohello voltar quando disponível.</span><span class="sxs-lookup"><span data-stu-id="66c58-119">Then hello function echoes these back toohello client when available.</span></span>   

<span data-ttu-id="66c58-120">Atualize função hello com hello código, que usaremos para testar a seguir:</span><span class="sxs-lookup"><span data-stu-id="66c58-120">Update hello function with hello following code, which we will use for testing:</span></span>

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

## <a name="test-a-function-with-tools"></a><span data-ttu-id="66c58-121">Testar uma função com ferramentas</span><span class="sxs-lookup"><span data-stu-id="66c58-121">Test a function with tools</span></span>
<span data-ttu-id="66c58-122">Fora Olá portal do Azure, há várias ferramentas que você pode usar tootrigger suas funções para teste.</span><span class="sxs-lookup"><span data-stu-id="66c58-122">Outside hello Azure portal, there are various tools that you can use tootrigger your functions for testing.</span></span> <span data-ttu-id="66c58-123">Elas incluem as ferramentas de teste de HTTP (baseado na interface do usuário e de linha de comando), ferramentas de acesso ao Armazenamento do Azure e até mesmo um navegador da web simples.</span><span class="sxs-lookup"><span data-stu-id="66c58-123">These include HTTP testing tools (both UI-based and command line), Azure Storage access tools, and even a simple web browser.</span></span>

### <a name="test-with-a-browser"></a><span data-ttu-id="66c58-124">Testar com um navegador</span><span class="sxs-lookup"><span data-stu-id="66c58-124">Test with a browser</span></span>
<span data-ttu-id="66c58-125">navegador da web de saudação é funções de tootrigger uma maneira simples por meio de HTTP.</span><span class="sxs-lookup"><span data-stu-id="66c58-125">hello web browser is a simple way tootrigger functions via HTTP.</span></span> <span data-ttu-id="66c58-126">Você pode usar um navegador para solicitações GET que não exigem uma carga de corpo e usam apenas parâmetros de cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="66c58-126">You can use a browser for GET requests that do not require a body payload, and that use only query string parameters.</span></span>

<span data-ttu-id="66c58-127">função de saudação tootest anterior, definimos Olá cópia **função Url** do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="66c58-127">tootest hello function we defined earlier, copy hello **Function Url** from hello portal.</span></span> <span data-ttu-id="66c58-128">Ele tem Olá formulário a seguir:</span><span class="sxs-lookup"><span data-stu-id="66c58-128">It has hello following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="66c58-129">Acrescentar Olá `name` cadeia de caracteres de consulta do parâmetro toohello.</span><span class="sxs-lookup"><span data-stu-id="66c58-129">Append hello `name` parameter toohello query string.</span></span> <span data-ttu-id="66c58-130">Usar um nome real para Olá `<Enter a name here>` espaço reservado.</span><span class="sxs-lookup"><span data-stu-id="66c58-130">Use an actual name for hello `<Enter a name here>` placeholder.</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

<span data-ttu-id="66c58-131">Colar Olá URL em seu navegador e você deve receber uma resposta semelhante toohello a seguir.</span><span class="sxs-lookup"><span data-stu-id="66c58-131">Paste hello URL into your browser, and you should get a response similar toohello following.</span></span>

![Guia do navegador de captura de tela de cromo com resposta de teste](./media/functions-test-a-function/browser-test.png)

<span data-ttu-id="66c58-133">Este exemplo é navegador Chrome hello, o que encapsula Olá retornada a cadeia de caracteres em XML.</span><span class="sxs-lookup"><span data-stu-id="66c58-133">This example is hello Chrome browser, which wraps hello returned string in XML.</span></span> <span data-ttu-id="66c58-134">Outros navegadores exibem apenas valor de cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="66c58-134">Other browsers display just hello string value.</span></span>

<span data-ttu-id="66c58-135">No portal de saudação **Logs** janela de saída a seguir toohello semelhante é registrada na execução de função hello:</span><span class="sxs-lookup"><span data-stu-id="66c58-135">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T07:34:59  Welcome, you are now connected toolog-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a><span data-ttu-id="66c58-136">Testar com o Postman</span><span class="sxs-lookup"><span data-stu-id="66c58-136">Test with Postman</span></span>
<span data-ttu-id="66c58-137">Olá recomendado ferramenta tootest a maioria das funções é carteiro, que integra com o navegador Chrome de saudação.</span><span class="sxs-lookup"><span data-stu-id="66c58-137">hello recommended tool tootest most of your functions is Postman, which integrates with hello Chrome browser.</span></span> <span data-ttu-id="66c58-138">tooinstall carteiro, consulte [carteiro obter](https://www.getpostman.com/).</span><span class="sxs-lookup"><span data-stu-id="66c58-138">tooinstall Postman, see [Get Postman](https://www.getpostman.com/).</span></span> <span data-ttu-id="66c58-139">O Postman fornece controle sobre muito mais atributos de uma solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="66c58-139">Postman provides control over many more attributes of an HTTP request.</span></span>

> [!TIP]
> <span data-ttu-id="66c58-140">Use Olá HTTP ferramenta de teste que você está mais familiarizado.</span><span class="sxs-lookup"><span data-stu-id="66c58-140">Use hello HTTP testing tool that you are most comfortable with.</span></span> <span data-ttu-id="66c58-141">Aqui estão alguns tooPostman alternativas:</span><span class="sxs-lookup"><span data-stu-id="66c58-141">Here are some alternatives tooPostman:</span></span>  
>
> * [<span data-ttu-id="66c58-142">Fiddler</span><span class="sxs-lookup"><span data-stu-id="66c58-142">Fiddler</span></span>](http://www.telerik.com/fiddler)  
> * [<span data-ttu-id="66c58-143">Paw</span><span class="sxs-lookup"><span data-stu-id="66c58-143">Paw</span></span>](https://luckymarmot.com/paw)  
>
>

<span data-ttu-id="66c58-144">função de saudação tootest com um corpo de solicitação no carteiro:</span><span class="sxs-lookup"><span data-stu-id="66c58-144">tootest hello function with a request body in Postman:</span></span>

1. <span data-ttu-id="66c58-145">Iniciar carteiro da saudação **aplicativos** botão no canto superior esquerdo de saudação de uma janela do navegador Chrome.</span><span class="sxs-lookup"><span data-stu-id="66c58-145">Start Postman from hello **Apps** button in hello upper-left corner of a Chrome browser window.</span></span>
2. <span data-ttu-id="66c58-146">Copie a **Url da Função** e cole-a no Postman.</span><span class="sxs-lookup"><span data-stu-id="66c58-146">Copy your **Function Url**, and paste it into Postman.</span></span> <span data-ttu-id="66c58-147">Ele inclui um parâmetro de cadeia de caracteres de consulta Olá código de acesso.</span><span class="sxs-lookup"><span data-stu-id="66c58-147">It includes hello access code query string parameter.</span></span>
3. <span data-ttu-id="66c58-148">Alterar o método hello HTTP muito**POST**.</span><span class="sxs-lookup"><span data-stu-id="66c58-148">Change hello HTTP method too**POST**.</span></span>
4. <span data-ttu-id="66c58-149">Clique em **corpo** > **bruto**e adicione o seguinte de toohello semelhante de corpo de solicitação de JSON:</span><span class="sxs-lookup"><span data-stu-id="66c58-149">Click **Body** > **raw**, and add a JSON request body similar toohello following:</span></span>

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. <span data-ttu-id="66c58-150">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="66c58-150">Click **Send**.</span></span>

<span data-ttu-id="66c58-151">Olá imagem a seguir mostra exemplo de função do teste hello eco simples neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="66c58-151">hello following image shows testing hello simple echo function example in this tutorial.</span></span>

![Interface de usuário de captura de tela de Postman](./media/functions-test-a-function/postman-test.png)

<span data-ttu-id="66c58-153">No portal de saudação **Logs** janela de saída a seguir toohello semelhante é registrada na execução de função hello:</span><span class="sxs-lookup"><span data-stu-id="66c58-153">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:04:51  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-hello-command-line"></a><span data-ttu-id="66c58-154">Teste com a rotação da linha de comando Olá</span><span class="sxs-lookup"><span data-stu-id="66c58-154">Test with cURL from hello command line</span></span>
<span data-ttu-id="66c58-155">Muitas vezes, quando você estiver testando o software, não é necessário toolook qualquer adicional de Olá a linha de comando toohelp depurar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="66c58-155">Often when you're testing software, it's not necessary toolook any further than hello command line toohelp debug your application.</span></span> <span data-ttu-id="66c58-156">Isso não é diferente com funções de teste.</span><span class="sxs-lookup"><span data-stu-id="66c58-156">This is no different with testing functions.</span></span> <span data-ttu-id="66c58-157">Observe que ondulação hello está disponível por padrão nos sistemas baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="66c58-157">Note that hello cURL is available by default on Linux-based systems.</span></span> <span data-ttu-id="66c58-158">No Windows, você deve primeiro baixar e instalar Olá [ondulação ferramenta](https://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="66c58-158">On Windows, you must first download and install hello [cURL tool](https://curl.haxx.se/).</span></span>

<span data-ttu-id="66c58-159">função de hello tootest que definimos anteriormente, Olá cópia **função URL** do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="66c58-159">tootest hello function that we defined earlier, copy hello **Function URL** from hello portal.</span></span> <span data-ttu-id="66c58-160">Ele tem Olá formulário a seguir:</span><span class="sxs-lookup"><span data-stu-id="66c58-160">It has hello following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="66c58-161">Esta é a URL de saudação para o disparo de sua função.</span><span class="sxs-lookup"><span data-stu-id="66c58-161">This is hello URL for triggering your function.</span></span> <span data-ttu-id="66c58-162">Testar isso, usando o comando de ondulação Olá Olá toomake de linha de comando de GET (`-G` ou `--get`) solicitação em relação a função hello:</span><span class="sxs-lookup"><span data-stu-id="66c58-162">Test this by using hello cURL command on hello command line toomake a GET (`-G` or `--get`) request against hello function:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="66c58-163">Esse exemplo específico exige um parâmetro de cadeia de caracteres de consulta, que pode ser passado como dados (`-d`) no hello cURL comando:</span><span class="sxs-lookup"><span data-stu-id="66c58-163">This particular example requires a query string parameter, which can be passed as Data (`-d`) in hello cURL command:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

<span data-ttu-id="66c58-164">Comando de execução Olá e você verá Olá após a saída da função hello na linha de comando hello:</span><span class="sxs-lookup"><span data-stu-id="66c58-164">Run hello command, and you see hello following output of hello function on hello command line:</span></span>

![Saída de tela do Prompt de comando](./media/functions-test-a-function/curl-test.png)

<span data-ttu-id="66c58-166">No portal de saudação **Logs** janela de saída a seguir toohello semelhante é registrada na execução de função hello:</span><span class="sxs-lookup"><span data-stu-id="66c58-166">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-04-05T21:55:09  Welcome, you are now connected toolog-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a><span data-ttu-id="66c58-167">Testar um gatilho de blob usando o Gerenciador de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="66c58-167">Test a blob trigger by using Storage Explorer</span></span>
<span data-ttu-id="66c58-168">Você pode testar uma função de gatilho de blob usando o [Gerenciador de Armazenamento do Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="66c58-168">You can test a blob trigger function by using [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

1. <span data-ttu-id="66c58-169">Em Olá [portal do Azure] para seu aplicativo de função, crie uma função de gatilho de blob do c#, F # ou JavaScript.</span><span class="sxs-lookup"><span data-stu-id="66c58-169">In hello [Azure portal] for your function app, create a C#, F# or JavaScript blob trigger function.</span></span> <span data-ttu-id="66c58-170">Definir Olá caminho toomonitor toohello nome do seu contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="66c58-170">Set hello path toomonitor toohello name of your blob container.</span></span> <span data-ttu-id="66c58-171">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="66c58-171">For example:</span></span>

        files
2. <span data-ttu-id="66c58-172">Clique em Olá  **+**  botão tooselect ou criar conta de armazenamento Olá toouse desejado.</span><span class="sxs-lookup"><span data-stu-id="66c58-172">Click hello **+** button tooselect or create hello storage account you want toouse.</span></span> <span data-ttu-id="66c58-173">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="66c58-173">Then click **Create**.</span></span>
3. <span data-ttu-id="66c58-174">Criar um arquivo de texto com hello texto a seguir e salve-o:</span><span class="sxs-lookup"><span data-stu-id="66c58-174">Create a text file with hello following text, and save it:</span></span>

        A text file for blob trigger function testing.
4. <span data-ttu-id="66c58-175">Executar [Azure Storage Explorer](http://storageexplorer.com/)e conecte-se o contêiner de blob toohello na conta de armazenamento hello está sendo monitorada.</span><span class="sxs-lookup"><span data-stu-id="66c58-175">Run [Azure Storage Explorer](http://storageexplorer.com/), and connect toohello blob container in hello storage account being monitored.</span></span>
5. <span data-ttu-id="66c58-176">Clique em **carregar** arquivo de texto de saudação tooupload.</span><span class="sxs-lookup"><span data-stu-id="66c58-176">Click **Upload** tooupload hello text file.</span></span>

    ![Captura de tela do Gerenciador de Armazenamento](./media/functions-test-a-function/azure-storage-explorer-test.png)

<span data-ttu-id="66c58-178">o código de função de gatilho do saudação padrão blob relata o processamento de saudação do blob Olá Olá logs:</span><span class="sxs-lookup"><span data-stu-id="66c58-178">hello default blob trigger function code reports hello processing of hello blob in hello logs:</span></span>

    2016-03-24T11:30:10  Welcome, you are now connected toolog-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a><span data-ttu-id="66c58-179">Testar uma função dentro de funções</span><span class="sxs-lookup"><span data-stu-id="66c58-179">Test a function within functions</span></span>
<span data-ttu-id="66c58-180">Olá portal funções do Azure é projetado toolet teste HTTP e timer disparado funções.</span><span class="sxs-lookup"><span data-stu-id="66c58-180">hello Azure Functions portal is designed toolet you test HTTP and timer triggered functions.</span></span> <span data-ttu-id="66c58-181">Você também pode criar funções tootrigger outras funções que você está testando.</span><span class="sxs-lookup"><span data-stu-id="66c58-181">You can also create functions tootrigger other functions that you are testing.</span></span>

### <a name="test-with-hello-functions-portal-run-button"></a><span data-ttu-id="66c58-182">Teste com o botão de portal executar Olá funções</span><span class="sxs-lookup"><span data-stu-id="66c58-182">Test with hello Functions portal Run button</span></span>
<span data-ttu-id="66c58-183">Olá portal fornece um **executar** botão que você pode usar algumas toodo limitado de testes.</span><span class="sxs-lookup"><span data-stu-id="66c58-183">hello portal provides a **Run** button that you can use toodo some limited testing.</span></span> <span data-ttu-id="66c58-184">Você pode fornecer um corpo de solicitação usando o botão hello, mas você não pode fornecer parâmetros de cadeia de caracteres de consulta ou atualização de cabeçalhos de solicitação.</span><span class="sxs-lookup"><span data-stu-id="66c58-184">You can provide a request body by using hello button, but you can't provide query string parameters or update request headers.</span></span>

<span data-ttu-id="66c58-185">Testar função do gatilho Olá HTTP criado anteriormente, adicionando um toohello semelhante da cadeia de caracteres JSON a seguir no hello **corpo da solicitação** campo.</span><span class="sxs-lookup"><span data-stu-id="66c58-185">Test hello HTTP trigger function we created earlier by adding a JSON string similar toohello following in hello **Request body** field.</span></span> <span data-ttu-id="66c58-186">Em seguida, clique em Olá **executar** botão.</span><span class="sxs-lookup"><span data-stu-id="66c58-186">Then click hello **Run** button.</span></span>

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

<span data-ttu-id="66c58-187">No portal de saudação **Logs** janela de saída a seguir toohello semelhante é registrada na execução de função hello:</span><span class="sxs-lookup"><span data-stu-id="66c58-187">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:03:12  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a><span data-ttu-id="66c58-188">Testar com um gatilho de temporizador</span><span class="sxs-lookup"><span data-stu-id="66c58-188">Test with a timer trigger</span></span>
<span data-ttu-id="66c58-189">Algumas funções não podem ser testadas adequadamente com ferramentas Olá mencionadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="66c58-189">Some functions can't be adequately tested with hello tools mentioned previously.</span></span> <span data-ttu-id="66c58-190">Por exemplo, considere uma função de gatilho de fila executada quando uma mensagem é inserida no [Armazenamento de Filas do Azure](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="66c58-190">For example, consider a queue trigger function that runs when a message is dropped into [Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="66c58-191">Você sempre pode escrever uma mensagem de toodrop de código em sua fila, e um exemplo em um projeto de console é fornecido neste artigo.</span><span class="sxs-lookup"><span data-stu-id="66c58-191">You can always write code toodrop a message into your queue, and an example of this in a console project is provided later in this article.</span></span> <span data-ttu-id="66c58-192">No entanto, há outra abordagem que você pode usar para testar com funções diretamente.</span><span class="sxs-lookup"><span data-stu-id="66c58-192">However, there is another approach you can use that tests functions directly.</span></span>  

<span data-ttu-id="66c58-193">Você pode usar um gatilho de temporizador configurado com uma associação de saída da fila.</span><span class="sxs-lookup"><span data-stu-id="66c58-193">You can use a timer trigger configured with a queue output binding.</span></span> <span data-ttu-id="66c58-194">Esse código de gatilho de timer, em seguida, pode gravar a fila de toohello de mensagens de teste hello.</span><span class="sxs-lookup"><span data-stu-id="66c58-194">That timer trigger code can then write hello test messages toohello queue.</span></span> <span data-ttu-id="66c58-195">Esta seção explica um exemplo.</span><span class="sxs-lookup"><span data-stu-id="66c58-195">This section walks through an example.</span></span>

<span data-ttu-id="66c58-196">Para obter informações mais detalhadas sobre como usar associações com funções do Azure, consulte Olá [referência do desenvolvedor do Azure funções](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="66c58-196">For more in-depth information on using bindings with Azure Functions, see hello [Azure Functions developer reference](functions-reference.md).</span></span>

#### <a name="create-a-queue-trigger-for-testing"></a><span data-ttu-id="66c58-197">Criar um gatilho de fila para teste</span><span class="sxs-lookup"><span data-stu-id="66c58-197">Create a queue trigger for testing</span></span>
<span data-ttu-id="66c58-198">toodemonstrate essa abordagem, podemos primeiro criar uma função de gatilho de fila que queremos tootest para uma fila denominada `queue-newusers`.</span><span class="sxs-lookup"><span data-stu-id="66c58-198">toodemonstrate this approach, we first create a queue trigger function that we want tootest for a queue named `queue-newusers`.</span></span> <span data-ttu-id="66c58-199">Essa função processa as informações de nome e endereço soltas no armazenamento de Filas para um novo usuário.</span><span class="sxs-lookup"><span data-stu-id="66c58-199">This function processes name and address information dropped into Queue storage for a new user.</span></span>

> [!NOTE]
> <span data-ttu-id="66c58-200">Se você usar um nome de fila diferente, certifique-se de toohello está de acordo com nome hello usado [nomeando filas e metadados](https://msdn.microsoft.com/library/dd179349.aspx) regras.</span><span class="sxs-lookup"><span data-stu-id="66c58-200">If you use a different queue name, make sure hello name you use conforms toohello [Naming Queues and MetaData](https://msdn.microsoft.com/library/dd179349.aspx) rules.</span></span> <span data-ttu-id="66c58-201">Caso contrário, você obterá um erro.</span><span class="sxs-lookup"><span data-stu-id="66c58-201">Otherwise, you get an error.</span></span>
>
>

1. <span data-ttu-id="66c58-202">Em Olá [portal do Azure] para seu aplicativo de função, clique em **nova função** > **QueueTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="66c58-202">In hello [Azure portal] for your function app, click **New Function** > **QueueTrigger - C#**.</span></span>
2. <span data-ttu-id="66c58-203">Digite toobe de nome de fila Olá monitorado pela função de fila hello:</span><span class="sxs-lookup"><span data-stu-id="66c58-203">Enter hello queue name toobe monitored by hello queue function:</span></span>

        queue-newusers
3. <span data-ttu-id="66c58-204">Clique em Olá  **+**  botão tooselect ou criar conta de armazenamento Olá toouse desejado.</span><span class="sxs-lookup"><span data-stu-id="66c58-204">Click hello **+** button tooselect or create hello storage account you want toouse.</span></span> <span data-ttu-id="66c58-205">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="66c58-205">Then click **Create**.</span></span>
4. <span data-ttu-id="66c58-206">Deixe essa janela de navegador portal aberto, para que você possa monitorar entradas de log Olá para o código de modelo de função de fila do saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="66c58-206">Leave this portal browser window open, so you can monitor hello log entries for hello default queue function template code.</span></span>

#### <a name="create-a-timer-trigger-toodrop-a-message-in-hello-queue"></a><span data-ttu-id="66c58-207">Criar um toodrop de gatilho de timer uma mensagem na fila de saudação</span><span class="sxs-lookup"><span data-stu-id="66c58-207">Create a timer trigger toodrop a message in hello queue</span></span>
1. <span data-ttu-id="66c58-208">Olá abrir [portal do Azure] em uma nova janela do navegador e navegue tooyour função app.</span><span class="sxs-lookup"><span data-stu-id="66c58-208">Open hello [Azure portal] in a new browser window, and navigate tooyour function app.</span></span>
2. <span data-ttu-id="66c58-209">Clique em **Nova Função** > **TimerTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="66c58-209">Click **New Function** > **TimerTrigger - C#**.</span></span> <span data-ttu-id="66c58-210">Insira um tooset de expressão cron frequência hello timer código testa sua função de fila.</span><span class="sxs-lookup"><span data-stu-id="66c58-210">Enter a cron expression tooset how often hello timer code tests your queue function.</span></span> <span data-ttu-id="66c58-211">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="66c58-211">Then click **Create**.</span></span> <span data-ttu-id="66c58-212">Se você quiser Olá teste toorun a cada 30 segundos, você pode usar o seguinte Olá [expressão CRON](https://wikipedia.org/wiki/Cron#CRON_expression):</span><span class="sxs-lookup"><span data-stu-id="66c58-212">If you want hello test toorun every 30 seconds, you can use hello following [CRON expression](https://wikipedia.org/wiki/Cron#CRON_expression):</span></span>

        */30 * * * * *
3. <span data-ttu-id="66c58-213">Clique em Olá **integrar** guia para seu novo gatilho de timer.</span><span class="sxs-lookup"><span data-stu-id="66c58-213">Click hello **Integrate** tab for your new timer trigger.</span></span>
4. <span data-ttu-id="66c58-214">Em **saída**, clique em **+ nova saída**.</span><span class="sxs-lookup"><span data-stu-id="66c58-214">Under **Output**, click **+ New Output**.</span></span> <span data-ttu-id="66c58-215">Em seguida, clique em **fila** e **selecione**.</span><span class="sxs-lookup"><span data-stu-id="66c58-215">Then click **queue** and **Select**.</span></span>
5. <span data-ttu-id="66c58-216">Nome da observação Olá usar para Olá **objeto de mensagem da fila**.</span><span class="sxs-lookup"><span data-stu-id="66c58-216">Note hello name you use for hello **queue message object**.</span></span> <span data-ttu-id="66c58-217">Você pode usar isso no código da função hello timer.</span><span class="sxs-lookup"><span data-stu-id="66c58-217">You use this in hello timer function code.</span></span>

        myQueue
6. <span data-ttu-id="66c58-218">Insira o nome da fila Olá onde a mensagem é enviada:</span><span class="sxs-lookup"><span data-stu-id="66c58-218">Enter hello queue name where hello message is sent:</span></span>

        queue-newusers
7. <span data-ttu-id="66c58-219">Clique em Olá  **+**  tooselect conta de armazenamento de saudação você usou anteriormente com um gatilho de fila de saudação de botão.</span><span class="sxs-lookup"><span data-stu-id="66c58-219">Click hello **+** button tooselect hello storage account you used previously with hello queue trigger.</span></span> <span data-ttu-id="66c58-220">Em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="66c58-220">Then click **Save**.</span></span>
8. <span data-ttu-id="66c58-221">Clique em Olá **desenvolver** guia para o gatilho de timer.</span><span class="sxs-lookup"><span data-stu-id="66c58-221">Click hello **Develop** tab for your timer trigger.</span></span>
9. <span data-ttu-id="66c58-222">Você pode usar o hello seguindo o código para a função de temporizador hello c#, desde que você usou Olá mesmo nome de objeto de mensagem mostrada anteriormente da fila.</span><span class="sxs-lookup"><span data-stu-id="66c58-222">You can use hello following code for hello C# timer function, as long as you used hello same queue message object name shown earlier.</span></span> <span data-ttu-id="66c58-223">Em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="66c58-223">Then click **Save**.</span></span>

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

<span data-ttu-id="66c58-224">Neste ponto, Olá função c# de timer executa a cada 30 segundos se você usou a expressão de cron de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="66c58-224">At this point, hello C# timer function executes every 30 seconds if you used hello example cron expression.</span></span> <span data-ttu-id="66c58-225">cada execução de relatório de logs Olá para a função de temporizador hello:</span><span class="sxs-lookup"><span data-stu-id="66c58-225">hello logs for hello timer function report each execution:</span></span>

    2016-03-24T10:27:02  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

<span data-ttu-id="66c58-226">Na janela do navegador para a função de fila Olá Olá, você pode ver cada mensagem que está sendo processada:</span><span class="sxs-lookup"><span data-stu-id="66c58-226">In hello browser window for hello queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a><span data-ttu-id="66c58-227">Testar uma função com código</span><span class="sxs-lookup"><span data-stu-id="66c58-227">Test a function with code</span></span>
<span data-ttu-id="66c58-228">Talvez seja necessário toocreate um tootest externo do aplicativo ou framework suas funções.</span><span class="sxs-lookup"><span data-stu-id="66c58-228">You may need toocreate an external application or framework tootest your functions.</span></span>

### <a name="test-an-http-trigger-function-with-code-nodejs"></a><span data-ttu-id="66c58-229">Testar uma função de gatilho HTTP com código: Node.js</span><span class="sxs-lookup"><span data-stu-id="66c58-229">Test an HTTP trigger function with code: Node.js</span></span>
<span data-ttu-id="66c58-230">Você pode usar um aplicativo de Node. js tooexecute um tootest de solicitação HTTP em sua função.</span><span class="sxs-lookup"><span data-stu-id="66c58-230">You can use a Node.js app tooexecute an HTTP request tootest your function.</span></span>
<span data-ttu-id="66c58-231">Verifique se tooset:</span><span class="sxs-lookup"><span data-stu-id="66c58-231">Make sure tooset:</span></span>

* <span data-ttu-id="66c58-232">Olá `host` no host de aplicativo hello solicitação opções tooyour função.</span><span class="sxs-lookup"><span data-stu-id="66c58-232">hello `host` in hello request options tooyour function app host.</span></span>
* <span data-ttu-id="66c58-233">O nome da função no hello `path`.</span><span class="sxs-lookup"><span data-stu-id="66c58-233">Your function name in hello `path`.</span></span>
* <span data-ttu-id="66c58-234">O código de acesso (`<your code>`) no hello `path`.</span><span class="sxs-lookup"><span data-stu-id="66c58-234">Your access code (`<your code>`) in hello `path`.</span></span>

<span data-ttu-id="66c58-235">Exemplo de código:</span><span class="sxs-lookup"><span data-stu-id="66c58-235">Code example:</span></span>

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


<span data-ttu-id="66c58-236">Saída:</span><span class="sxs-lookup"><span data-stu-id="66c58-236">Output:</span></span>

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    hello address you provided is Dallas, T.X. 75201

<span data-ttu-id="66c58-237">No portal de saudação **Logs** janela de saída a seguir toohello semelhante é registrada na execução de função hello:</span><span class="sxs-lookup"><span data-stu-id="66c58-237">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:08:55  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a><span data-ttu-id="66c58-238">Testar uma função de gatilho de fila com o código: C#</span><span class="sxs-lookup"><span data-stu-id="66c58-238">Test a queue trigger function with code: C#</span></span> #
<span data-ttu-id="66c58-239">Mencionamos anteriormente que você pode testar um gatilho de fila usando código toodrop uma mensagem na fila.</span><span class="sxs-lookup"><span data-stu-id="66c58-239">We mentioned earlier that you can test a queue trigger by using code toodrop a message in your queue.</span></span> <span data-ttu-id="66c58-240">Olá, código de exemplo a seguir baseia-se Olá c# código apresentado Olá [guia de Introdução ao armazenamento de fila do Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="66c58-240">hello following example code is based on hello C# code presented in hello [Getting started with Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md) tutorial.</span></span> <span data-ttu-id="66c58-241">Também há código para outras linguagens disponível nesse link.</span><span class="sxs-lookup"><span data-stu-id="66c58-241">Code for other languages is also available from that link.</span></span>

<span data-ttu-id="66c58-242">tootest esse código em um aplicativo de console, você deve:</span><span class="sxs-lookup"><span data-stu-id="66c58-242">tootest this code in a console app, you must:</span></span>

* <span data-ttu-id="66c58-243">[Configurar a cadeia de caracteres de conexão de armazenamento no arquivo App. config de saudação](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="66c58-243">[Configure your storage connection string in hello app.config file](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>
* <span data-ttu-id="66c58-244">Passar um `name` e `address` como parâmetros toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="66c58-244">Pass a `name` and `address` as parameters toohello app.</span></span> <span data-ttu-id="66c58-245">Por exemplo: `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span><span class="sxs-lookup"><span data-stu-id="66c58-245">For example, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span></span> <span data-ttu-id="66c58-246">(Este código aceita Olá nome e endereço de um novo usuário como argumentos de linha de comando durante o tempo de execução.)</span><span class="sxs-lookup"><span data-stu-id="66c58-246">(This code accepts hello name and address for a new user as command-line arguments during runtime.)</span></span>

<span data-ttu-id="66c58-247">Código C# de exemplo:</span><span class="sxs-lookup"><span data-stu-id="66c58-247">Example C# code:</span></span>

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

<span data-ttu-id="66c58-248">Na janela do navegador para a função de fila Olá Olá, você pode ver cada mensagem que está sendo processada:</span><span class="sxs-lookup"><span data-stu-id="66c58-248">In hello browser window for hello queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[portal do Azure]: https://portal.azure.com
