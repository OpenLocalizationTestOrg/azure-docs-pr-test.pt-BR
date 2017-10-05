---
title: Testando o Azure Functions | Microsoft Docs
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
ms.openlocfilehash: aca03ba4137893157fcbe6650336782ab88cd234
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="strategies-for-testing-your-code-in-azure-functions"></a><span data-ttu-id="1ce48-104">Estratégias para testar seu código no Azure Functions</span><span class="sxs-lookup"><span data-stu-id="1ce48-104">Strategies for testing your code in Azure Functions</span></span>

<span data-ttu-id="1ce48-105">Este tópico demonstra as várias maneiras de testar as funções, incluindo o uso das seguintes abordagens gerais:</span><span class="sxs-lookup"><span data-stu-id="1ce48-105">This topic demonstrates the various ways to test functions, including using the following general approaches:</span></span>

+ <span data-ttu-id="1ce48-106">Ferramentas baseadas em HTTP, como cURL, Postman e até mesmo um navegador da Web para gatilhos baseados na Web</span><span class="sxs-lookup"><span data-stu-id="1ce48-106">HTTP-based tools, such as cURL, Postman, and even a web browser for web-based triggers</span></span>
+ <span data-ttu-id="1ce48-107">Gerenciador de Armazenamento do Azure para testar gatilhos baseados no Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="1ce48-107">Azure Storage Explorer, to test Azure Storage-based triggers</span></span>
+ <span data-ttu-id="1ce48-108">Guia Teste no portal do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="1ce48-108">Test tab in the Azure Functions portal</span></span>
+ <span data-ttu-id="1ce48-109">Função disparada por timer</span><span class="sxs-lookup"><span data-stu-id="1ce48-109">Timer-triggered function</span></span>
+ <span data-ttu-id="1ce48-110">Teste de aplicativo ou de estrutura</span><span class="sxs-lookup"><span data-stu-id="1ce48-110">Testing application or framework</span></span>

<span data-ttu-id="1ce48-111">Todos esses métodos de testes usam uma função de gatilho HTTP que aceita entrada por meio de um parâmetro de cadeia de caracteres de consulta ou o corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="1ce48-111">All these testing methods use an HTTP trigger function that accepts input through either a query string parameter or the request body.</span></span> <span data-ttu-id="1ce48-112">Você cria esta função na primeira seção.</span><span class="sxs-lookup"><span data-stu-id="1ce48-112">You create this function in the first section.</span></span>

## <a name="create-a-function-for-testing"></a><span data-ttu-id="1ce48-113">Criar uma função para teste</span><span class="sxs-lookup"><span data-stu-id="1ce48-113">Create a function for testing</span></span>
<span data-ttu-id="1ce48-114">Durante a maior parte deste tutorial, usamos uma versão ligeiramente modificada do modelo da função JavaScript HttpTrigger disponível quando você criar uma função.</span><span class="sxs-lookup"><span data-stu-id="1ce48-114">For most of this tutorial, we use a slightly modified version of the HttpTrigger JavaScript function template that is available when you create a function.</span></span> <span data-ttu-id="1ce48-115">Se você precisar de ajuda para criar uma função, examinar isso [tutorial](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="1ce48-115">If you need help creating a function, review this [tutorial](functions-create-first-azure-function.md).</span></span> <span data-ttu-id="1ce48-116">Escolha o modelo **HttpTrigger- JavaScript** ao criar a função de teste no [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="1ce48-116">Choose the **HttpTrigger- JavaScript** template when creating the test function in the [Azure portal].</span></span>

<span data-ttu-id="1ce48-117">O modelo da função padrão é basicamente uma função “hello world” que retorna o nome do corpo da solicitação do parâmetro de cadeia de caracteres da consulta, `name=<your name>`.</span><span class="sxs-lookup"><span data-stu-id="1ce48-117">The default function template is basically a "hello world" function that echoes back the name from the request body or query string parameter, `name=<your name>`.</span></span>  <span data-ttu-id="1ce48-118">Atualizamos o código para permitir também que você forneça o nome e um endereço como conteúdo JSON no corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="1ce48-118">We'll update the code to also allow you to provide the name and an address as JSON content in the request body.</span></span> <span data-ttu-id="1ce48-119">Em seguida, a função retorna para o cliente quando disponível.</span><span class="sxs-lookup"><span data-stu-id="1ce48-119">Then the function echoes these back to the client when available.</span></span>   

<span data-ttu-id="1ce48-120">Atualize a função com o código a seguir, que usaremos para teste:</span><span class="sxs-lookup"><span data-stu-id="1ce48-120">Update the function with the following code, which we will use for testing:</span></span>

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
            body: "Please pass a name on the query string or in the request body"
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
        echoString += "\n" + "The address you provided is " + address;
        context.log("address = " + address);
    }
    res = {
        // status: 200, /* Defaults to 200 */
        body: echoString
    };
    return res;
}
```

## <a name="test-a-function-with-tools"></a><span data-ttu-id="1ce48-121">Testar uma função com ferramentas</span><span class="sxs-lookup"><span data-stu-id="1ce48-121">Test a function with tools</span></span>
<span data-ttu-id="1ce48-122">Fora do portal do Azure, há várias ferramentas que podem ser usadas para disparar as funções para teste.</span><span class="sxs-lookup"><span data-stu-id="1ce48-122">Outside the Azure portal, there are various tools that you can use to trigger your functions for testing.</span></span> <span data-ttu-id="1ce48-123">Elas incluem as ferramentas de teste de HTTP (baseado na interface do usuário e de linha de comando), ferramentas de acesso ao Armazenamento do Azure e até mesmo um navegador da web simples.</span><span class="sxs-lookup"><span data-stu-id="1ce48-123">These include HTTP testing tools (both UI-based and command line), Azure Storage access tools, and even a simple web browser.</span></span>

### <a name="test-with-a-browser"></a><span data-ttu-id="1ce48-124">Testar com um navegador</span><span class="sxs-lookup"><span data-stu-id="1ce48-124">Test with a browser</span></span>
<span data-ttu-id="1ce48-125">O navegador da web é uma maneira simples de funções de gatilho via HTTP.</span><span class="sxs-lookup"><span data-stu-id="1ce48-125">The web browser is a simple way to trigger functions via HTTP.</span></span> <span data-ttu-id="1ce48-126">Você pode usar um navegador para solicitações GET que não exigem uma carga de corpo e usam apenas parâmetros de cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="1ce48-126">You can use a browser for GET requests that do not require a body payload, and that use only query string parameters.</span></span>

<span data-ttu-id="1ce48-127">Para testar a função que definimos anteriormente, copie a **Url da Função** do portal.</span><span class="sxs-lookup"><span data-stu-id="1ce48-127">To test the function we defined earlier, copy the **Function Url** from the portal.</span></span> <span data-ttu-id="1ce48-128">Ele tem o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="1ce48-128">It has the following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="1ce48-129">Acrescente a `name` parâmetro para a cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="1ce48-129">Append the `name` parameter to the query string.</span></span> <span data-ttu-id="1ce48-130">Usar um nome real para o `<Enter a name here>` espaço reservado.</span><span class="sxs-lookup"><span data-stu-id="1ce48-130">Use an actual name for the `<Enter a name here>` placeholder.</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

<span data-ttu-id="1ce48-131">Cole a URL no seu navegador e você obterá uma resposta semelhante à seguinte.</span><span class="sxs-lookup"><span data-stu-id="1ce48-131">Paste the URL into your browser, and you should get a response similar to the following.</span></span>

![Guia do navegador de captura de tela de cromo com resposta de teste](./media/functions-test-a-function/browser-test.png)

<span data-ttu-id="1ce48-133">Este exemplo é o navegador Chrome, que encapsula a cadeia de caracteres retornada em XML.</span><span class="sxs-lookup"><span data-stu-id="1ce48-133">This example is the Chrome browser, which wraps the returned string in XML.</span></span> <span data-ttu-id="1ce48-134">Outros navegadores exibem apenas o valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="1ce48-134">Other browsers display just the string value.</span></span>

<span data-ttu-id="1ce48-135">Na janela **Logs** do portal, é registrada uma saída semelhante à seguinte ao executar a função:</span><span class="sxs-lookup"><span data-stu-id="1ce48-135">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T07:34:59  Welcome, you are now connected to log-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a><span data-ttu-id="1ce48-136">Testar com o Postman</span><span class="sxs-lookup"><span data-stu-id="1ce48-136">Test with Postman</span></span>
<span data-ttu-id="1ce48-137">A ferramenta recomendada para a maioria das funções de teste é carteiro, que integra o navegador Chrome.</span><span class="sxs-lookup"><span data-stu-id="1ce48-137">The recommended tool to test most of your functions is Postman, which integrates with the Chrome browser.</span></span> <span data-ttu-id="1ce48-138">Para instalar o Postman, consulte [Obter o Postman](https://www.getpostman.com/).</span><span class="sxs-lookup"><span data-stu-id="1ce48-138">To install Postman, see [Get Postman](https://www.getpostman.com/).</span></span> <span data-ttu-id="1ce48-139">O Postman fornece controle sobre muito mais atributos de uma solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="1ce48-139">Postman provides control over many more attributes of an HTTP request.</span></span>

> [!TIP]
> <span data-ttu-id="1ce48-140">Use o HTTP que estiver mais familiarizado com a ferramenta de teste.</span><span class="sxs-lookup"><span data-stu-id="1ce48-140">Use the HTTP testing tool that you are most comfortable with.</span></span> <span data-ttu-id="1ce48-141">Aqui estão algumas alternativas ao Postman:</span><span class="sxs-lookup"><span data-stu-id="1ce48-141">Here are some alternatives to Postman:</span></span>  
>
> * [<span data-ttu-id="1ce48-142">Fiddler</span><span class="sxs-lookup"><span data-stu-id="1ce48-142">Fiddler</span></span>](http://www.telerik.com/fiddler)  
> * [<span data-ttu-id="1ce48-143">Paw</span><span class="sxs-lookup"><span data-stu-id="1ce48-143">Paw</span></span>](https://luckymarmot.com/paw)  
>
>

<span data-ttu-id="1ce48-144">Para testar a função com um corpo de solicitação no Postman:</span><span class="sxs-lookup"><span data-stu-id="1ce48-144">To test the function with a request body in Postman:</span></span>

1. <span data-ttu-id="1ce48-145">Inicie o Postman com o botão **Aplicativos** no canto superior esquerdo de uma janela do navegador Chrome.</span><span class="sxs-lookup"><span data-stu-id="1ce48-145">Start Postman from the **Apps** button in the upper-left corner of a Chrome browser window.</span></span>
2. <span data-ttu-id="1ce48-146">Copie a **Url da Função** e cole-a no Postman.</span><span class="sxs-lookup"><span data-stu-id="1ce48-146">Copy your **Function Url**, and paste it into Postman.</span></span> <span data-ttu-id="1ce48-147">Ele inclui o parâmetro de cadeia de caracteres de consulta do código de acesso.</span><span class="sxs-lookup"><span data-stu-id="1ce48-147">It includes the access code query string parameter.</span></span>
3. <span data-ttu-id="1ce48-148">Altere o método HTTP para **POST**.</span><span class="sxs-lookup"><span data-stu-id="1ce48-148">Change the HTTP method to **POST**.</span></span>
4. <span data-ttu-id="1ce48-149">Clique em **Corpo** > **bruto** e adicione um corpo da solicitação JSON da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1ce48-149">Click **Body** > **raw**, and add a JSON request body similar to the following:</span></span>

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. <span data-ttu-id="1ce48-150">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="1ce48-150">Click **Send**.</span></span>

<span data-ttu-id="1ce48-151">A imagem a seguir mostra como testar o exemplo de função de eco simples neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="1ce48-151">The following image shows testing the simple echo function example in this tutorial.</span></span>

![Interface de usuário de captura de tela de Postman](./media/functions-test-a-function/postman-test.png)

<span data-ttu-id="1ce48-153">Na janela **Logs** do portal, é registrada uma saída semelhante à seguinte ao executar a função:</span><span class="sxs-lookup"><span data-stu-id="1ce48-153">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:04:51  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-the-command-line"></a><span data-ttu-id="1ce48-154">Teste com rotação da linha de comando</span><span class="sxs-lookup"><span data-stu-id="1ce48-154">Test with cURL from the command line</span></span>
<span data-ttu-id="1ce48-155">Muitas vezes, quando você estiver testando software, não será necessário procurar além da linha de comando para ajudar a depurar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ce48-155">Often when you're testing software, it's not necessary to look any further than the command line to help debug your application.</span></span> <span data-ttu-id="1ce48-156">Isso não é diferente com funções de teste.</span><span class="sxs-lookup"><span data-stu-id="1ce48-156">This is no different with testing functions.</span></span> <span data-ttu-id="1ce48-157">Observe que a rotação está disponível por padrão nos sistemas baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="1ce48-157">Note that the cURL is available by default on Linux-based systems.</span></span> <span data-ttu-id="1ce48-158">No Windows, você deve primeiro baixar e instalar o [cURL ferramenta](https://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="1ce48-158">On Windows, you must first download and install the [cURL tool](https://curl.haxx.se/).</span></span>

<span data-ttu-id="1ce48-159">Para testar a função que definimos acima, copie a **URL da Função** do portal.</span><span class="sxs-lookup"><span data-stu-id="1ce48-159">To test the function that we defined earlier, copy the **Function URL** from the portal.</span></span> <span data-ttu-id="1ce48-160">Ele tem o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="1ce48-160">It has the following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="1ce48-161">Esta é a URL para o disparo de sua função.</span><span class="sxs-lookup"><span data-stu-id="1ce48-161">This is the URL for triggering your function.</span></span> <span data-ttu-id="1ce48-162">Esse teste, use o comando cURL na linha de comando para fazer um GET (`-G` ou `--get`) solicitação em relação a função:</span><span class="sxs-lookup"><span data-stu-id="1ce48-162">Test this by using the cURL command on the command line to make a GET (`-G` or `--get`) request against the function:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="1ce48-163">Esse exemplo específico exige um parâmetro de cadeia de caracteres de consulta que pode ser passado como Dados (`-d`) no comando cURL:</span><span class="sxs-lookup"><span data-stu-id="1ce48-163">This particular example requires a query string parameter, which can be passed as Data (`-d`) in the cURL command:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

<span data-ttu-id="1ce48-164">Execute o comando e você verá a seguinte saída da função na linha de comando:</span><span class="sxs-lookup"><span data-stu-id="1ce48-164">Run the command, and you see the following output of the function on the command line:</span></span>

![Saída de tela do Prompt de comando](./media/functions-test-a-function/curl-test.png)

<span data-ttu-id="1ce48-166">Na janela **Logs** do portal, é registrada uma saída semelhante à seguinte ao executar a função:</span><span class="sxs-lookup"><span data-stu-id="1ce48-166">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-04-05T21:55:09  Welcome, you are now connected to log-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a><span data-ttu-id="1ce48-167">Testar um gatilho de blob usando o Gerenciador de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="1ce48-167">Test a blob trigger by using Storage Explorer</span></span>
<span data-ttu-id="1ce48-168">Você pode testar uma função de gatilho de blob usando o [Gerenciador de Armazenamento do Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="1ce48-168">You can test a blob trigger function by using [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

1. <span data-ttu-id="1ce48-169">No [portal do Azure] para seu aplicativo de funções, crie uma função de gatilho de blob do C#, do F# ou do JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1ce48-169">In the [Azure portal] for your function app, create a C#, F# or JavaScript blob trigger function.</span></span> <span data-ttu-id="1ce48-170">Defina o caminho a ser monitorado para o nome do seu contêiner de blobs.</span><span class="sxs-lookup"><span data-stu-id="1ce48-170">Set the path to monitor to the name of your blob container.</span></span> <span data-ttu-id="1ce48-171">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1ce48-171">For example:</span></span>

        files
2. <span data-ttu-id="1ce48-172">Clique no botão **+** para selecionar ou criar a conta de armazenamento que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="1ce48-172">Click the **+** button to select or create the storage account you want to use.</span></span> <span data-ttu-id="1ce48-173">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1ce48-173">Then click **Create**.</span></span>
3. <span data-ttu-id="1ce48-174">Crie um arquivo de texto com o texto a seguir e salve-o:</span><span class="sxs-lookup"><span data-stu-id="1ce48-174">Create a text file with the following text, and save it:</span></span>

        A text file for blob trigger function testing.
4. <span data-ttu-id="1ce48-175">Execute o [Gerenciador de Armazenamento do Azure](http://storageexplorer.com/) e conecte-se ao contêiner de blob na conta de armazenamento que está sendo monitorada.</span><span class="sxs-lookup"><span data-stu-id="1ce48-175">Run [Azure Storage Explorer](http://storageexplorer.com/), and connect to the blob container in the storage account being monitored.</span></span>
5. <span data-ttu-id="1ce48-176">Clique em **Carregar** para carregar o arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="1ce48-176">Click **Upload** to upload the text file.</span></span>

    ![Captura de tela do Gerenciador de Armazenamento](./media/functions-test-a-function/azure-storage-explorer-test.png)

<span data-ttu-id="1ce48-178">O código de função do gatilho de blob padrão relata o processamento do blob nos logs:</span><span class="sxs-lookup"><span data-stu-id="1ce48-178">The default blob trigger function code reports the processing of the blob in the logs:</span></span>

    2016-03-24T11:30:10  Welcome, you are now connected to log-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a><span data-ttu-id="1ce48-179">Testar uma função dentro de funções</span><span class="sxs-lookup"><span data-stu-id="1ce48-179">Test a function within functions</span></span>
<span data-ttu-id="1ce48-180">O portal do Azure Functions foi projetado para permitir que você teste as funções de timer e HTTP acionadas.</span><span class="sxs-lookup"><span data-stu-id="1ce48-180">The Azure Functions portal is designed to let you test HTTP and timer triggered functions.</span></span> <span data-ttu-id="1ce48-181">Você também pode criar funções para disparar outras funções que você está testando.</span><span class="sxs-lookup"><span data-stu-id="1ce48-181">You can also create functions to trigger other functions that you are testing.</span></span>

### <a name="test-with-the-functions-portal-run-button"></a><span data-ttu-id="1ce48-182">Testar com o botão Executar do portal do Functions</span><span class="sxs-lookup"><span data-stu-id="1ce48-182">Test with the Functions portal Run button</span></span>
<span data-ttu-id="1ce48-183">O portal fornece um **executar** botão que você pode usar para fazer algumas limitada a testes.</span><span class="sxs-lookup"><span data-stu-id="1ce48-183">The portal provides a **Run** button that you can use to do some limited testing.</span></span> <span data-ttu-id="1ce48-184">Você pode fornecer um corpo de solicitação usando o botão, porém não é possível fornecer parâmetros de cadeia de caracteres de consulta ou atualizar os cabeçalhos de solicitação.</span><span class="sxs-lookup"><span data-stu-id="1ce48-184">You can provide a request body by using the button, but you can't provide query string parameters or update request headers.</span></span>

<span data-ttu-id="1ce48-185">Teste a função de gatilho HTTP criada anteriormente adicionando uma cadeia de caracteres JSON similar à seguinte no campo **Corpo da solicitação**.</span><span class="sxs-lookup"><span data-stu-id="1ce48-185">Test the HTTP trigger function we created earlier by adding a JSON string similar to the following in the **Request body** field.</span></span> <span data-ttu-id="1ce48-186">Em seguida, clique no botão **Executar**.</span><span class="sxs-lookup"><span data-stu-id="1ce48-186">Then click the **Run** button.</span></span>

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

<span data-ttu-id="1ce48-187">Na janela **Logs** do portal, é registrada uma saída semelhante à seguinte ao executar a função:</span><span class="sxs-lookup"><span data-stu-id="1ce48-187">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:03:12  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a><span data-ttu-id="1ce48-188">Testar com um gatilho de temporizador</span><span class="sxs-lookup"><span data-stu-id="1ce48-188">Test with a timer trigger</span></span>
<span data-ttu-id="1ce48-189">Para algumas funções, realmente não é possível testar adequadamente com as ferramentas já mencionadas.</span><span class="sxs-lookup"><span data-stu-id="1ce48-189">Some functions can't be adequately tested with the tools mentioned previously.</span></span> <span data-ttu-id="1ce48-190">Por exemplo, considere uma função de gatilho de fila executada quando uma mensagem é inserida no [Armazenamento de Filas do Azure](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="1ce48-190">For example, consider a queue trigger function that runs when a message is dropped into [Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="1ce48-191">Você sempre pode escrever código para remover uma mensagem da fila e um exemplo disso em um projeto de console fornecido posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="1ce48-191">You can always write code to drop a message into your queue, and an example of this in a console project is provided later in this article.</span></span> <span data-ttu-id="1ce48-192">No entanto, há outra abordagem que você pode usar para testar com funções diretamente.</span><span class="sxs-lookup"><span data-stu-id="1ce48-192">However, there is another approach you can use that tests functions directly.</span></span>  

<span data-ttu-id="1ce48-193">Você pode usar um gatilho de temporizador configurado com uma associação de saída da fila.</span><span class="sxs-lookup"><span data-stu-id="1ce48-193">You can use a timer trigger configured with a queue output binding.</span></span> <span data-ttu-id="1ce48-194">Esse código de gatilho de temporizador pode então escrever as mensagens de teste para a fila.</span><span class="sxs-lookup"><span data-stu-id="1ce48-194">That timer trigger code can then write the test messages to the queue.</span></span> <span data-ttu-id="1ce48-195">Esta seção explica um exemplo.</span><span class="sxs-lookup"><span data-stu-id="1ce48-195">This section walks through an example.</span></span>

<span data-ttu-id="1ce48-196">Para obter informações mais detalhadas sobre como usar associações com os Azure Functions, consulte a [Referência do desenvolvedor dos Azure Functions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="1ce48-196">For more in-depth information on using bindings with Azure Functions, see the [Azure Functions developer reference](functions-reference.md).</span></span>

#### <a name="create-a-queue-trigger-for-testing"></a><span data-ttu-id="1ce48-197">Criar um gatilho de fila para teste</span><span class="sxs-lookup"><span data-stu-id="1ce48-197">Create a queue trigger for testing</span></span>
<span data-ttu-id="1ce48-198">Para demonstrar essa abordagem, primeiro criaremos uma função de gatilho de fila que desejamos testar para uma fila denominada `queue-newusers`.</span><span class="sxs-lookup"><span data-stu-id="1ce48-198">To demonstrate this approach, we first create a queue trigger function that we want to test for a queue named `queue-newusers`.</span></span> <span data-ttu-id="1ce48-199">Essa função processa as informações de nome e endereço soltas no armazenamento de Filas para um novo usuário.</span><span class="sxs-lookup"><span data-stu-id="1ce48-199">This function processes name and address information dropped into Queue storage for a new user.</span></span>

> [!NOTE]
> <span data-ttu-id="1ce48-200">Se você usar um nome de fila diferente, verifique se o nome usado está de acordo com as regras de [Nomeação de Filas e Metadados](https://msdn.microsoft.com/library/dd179349.aspx) .</span><span class="sxs-lookup"><span data-stu-id="1ce48-200">If you use a different queue name, make sure the name you use conforms to the [Naming Queues and MetaData](https://msdn.microsoft.com/library/dd179349.aspx) rules.</span></span> <span data-ttu-id="1ce48-201">Caso contrário, você obterá um erro.</span><span class="sxs-lookup"><span data-stu-id="1ce48-201">Otherwise, you get an error.</span></span>
>
>

1. <span data-ttu-id="1ce48-202">No [portal do Azure] para seu aplicativo de Funções, clique em **Nova Função** > **QueueTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="1ce48-202">In the [Azure portal] for your function app, click **New Function** > **QueueTrigger - C#**.</span></span>
2. <span data-ttu-id="1ce48-203">Inserir o nome da fila a ser monitorada pela função de fila:</span><span class="sxs-lookup"><span data-stu-id="1ce48-203">Enter the queue name to be monitored by the queue function:</span></span>

        queue-newusers
3. <span data-ttu-id="1ce48-204">Clique no botão **+** para selecionar ou criar a conta de armazenamento que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="1ce48-204">Click the **+** button to select or create the storage account you want to use.</span></span> <span data-ttu-id="1ce48-205">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1ce48-205">Then click **Create**.</span></span>
4. <span data-ttu-id="1ce48-206">Deixe essa janela do navegador do portal aberta para que você possa monitorar as entradas de log para o código do modelo da função de fila padrão.</span><span class="sxs-lookup"><span data-stu-id="1ce48-206">Leave this portal browser window open, so you can monitor the log entries for the default queue function template code.</span></span>

#### <a name="create-a-timer-trigger-to-drop-a-message-in-the-queue"></a><span data-ttu-id="1ce48-207">Criar um gatilho de temporizador para remover uma mensagem na fila</span><span class="sxs-lookup"><span data-stu-id="1ce48-207">Create a timer trigger to drop a message in the queue</span></span>
1. <span data-ttu-id="1ce48-208">Abra o [portal do Azure] em uma nova janela do navegador e navegue para seu aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="1ce48-208">Open the [Azure portal] in a new browser window, and navigate to your function app.</span></span>
2. <span data-ttu-id="1ce48-209">Clique em **Nova Função** > **TimerTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="1ce48-209">Click **New Function** > **TimerTrigger - C#**.</span></span> <span data-ttu-id="1ce48-210">Insira uma expressão cron para definir com que frequência o código do temporizador testará sua função de fila.</span><span class="sxs-lookup"><span data-stu-id="1ce48-210">Enter a cron expression to set how often the timer code tests your queue function.</span></span> <span data-ttu-id="1ce48-211">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1ce48-211">Then click **Create**.</span></span> <span data-ttu-id="1ce48-212">Se você quiser que o teste seja executado cada 30 segundos, use a seguinte [expressão CRON](https://wikipedia.org/wiki/Cron#CRON_expression):</span><span class="sxs-lookup"><span data-stu-id="1ce48-212">If you want the test to run every 30 seconds, you can use the following [CRON expression](https://wikipedia.org/wiki/Cron#CRON_expression):</span></span>

        */30 * * * * *
3. <span data-ttu-id="1ce48-213">Clique na guia **Integrar** para o novo gatilho de temporizador.</span><span class="sxs-lookup"><span data-stu-id="1ce48-213">Click the **Integrate** tab for your new timer trigger.</span></span>
4. <span data-ttu-id="1ce48-214">Em **saída**, clique em **+ nova saída**.</span><span class="sxs-lookup"><span data-stu-id="1ce48-214">Under **Output**, click **+ New Output**.</span></span> <span data-ttu-id="1ce48-215">Em seguida, clique em **fila** e **selecione**.</span><span class="sxs-lookup"><span data-stu-id="1ce48-215">Then click **queue** and **Select**.</span></span>
5. <span data-ttu-id="1ce48-216">Observe o nome usado para o **objeto de mensagem da fila**.</span><span class="sxs-lookup"><span data-stu-id="1ce48-216">Note the name you use for the **queue message object**.</span></span> <span data-ttu-id="1ce48-217">Você pode usar isso no código da função timer.</span><span class="sxs-lookup"><span data-stu-id="1ce48-217">You use this in the timer function code.</span></span>

        myQueue
6. <span data-ttu-id="1ce48-218">Insira o nome da fila na qual a mensagem é enviada:</span><span class="sxs-lookup"><span data-stu-id="1ce48-218">Enter the queue name where the message is sent:</span></span>

        queue-newusers
7. <span data-ttu-id="1ce48-219">Clique no botão **+** para selecionar a conta de armazenamento que você usou anteriormente com o gatilho de fila.</span><span class="sxs-lookup"><span data-stu-id="1ce48-219">Click the **+** button to select the storage account you used previously with the queue trigger.</span></span> <span data-ttu-id="1ce48-220">Em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="1ce48-220">Then click **Save**.</span></span>
8. <span data-ttu-id="1ce48-221">Clique na guia **Desenvolver** do gatilho de temporizador.</span><span class="sxs-lookup"><span data-stu-id="1ce48-221">Click the **Develop** tab for your timer trigger.</span></span>
9. <span data-ttu-id="1ce48-222">Você pode usar o código a seguir para a função de temporizador C#, desde que tenha suado o mesmo nome de objeto de mensagem de fila mostrado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1ce48-222">You can use the following code for the C# timer function, as long as you used the same queue message object name shown earlier.</span></span> <span data-ttu-id="1ce48-223">Em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="1ce48-223">Then click **Save**.</span></span>

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

<span data-ttu-id="1ce48-224">Neste ponto, a função de temporizador do C# será executada a cada 30 segundos caso você tenha usado a expressão cron de exemplo.</span><span class="sxs-lookup"><span data-stu-id="1ce48-224">At this point, the C# timer function executes every 30 seconds if you used the example cron expression.</span></span> <span data-ttu-id="1ce48-225">Os logs da função de temporizador relatam cada execução:</span><span class="sxs-lookup"><span data-stu-id="1ce48-225">The logs for the timer function report each execution:</span></span>

    2016-03-24T10:27:02  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

<span data-ttu-id="1ce48-226">Na janela do navegador para a função de fila, você poderá ver cada mensagem que está sendo processada:</span><span class="sxs-lookup"><span data-stu-id="1ce48-226">In the browser window for the queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a><span data-ttu-id="1ce48-227">Testar uma função com código</span><span class="sxs-lookup"><span data-stu-id="1ce48-227">Test a function with code</span></span>
<span data-ttu-id="1ce48-228">Talvez seja necessário criar um aplicativo externo ou uma estrutura para testar suas funções.</span><span class="sxs-lookup"><span data-stu-id="1ce48-228">You may need to create an external application or framework to test your functions.</span></span>

### <a name="test-an-http-trigger-function-with-code-nodejs"></a><span data-ttu-id="1ce48-229">Testar uma função de gatilho HTTP com código: Node.js</span><span class="sxs-lookup"><span data-stu-id="1ce48-229">Test an HTTP trigger function with code: Node.js</span></span>
<span data-ttu-id="1ce48-230">Você pode usar um aplicativo Node.js para executar uma solicitação HTTP para testar sua função.</span><span class="sxs-lookup"><span data-stu-id="1ce48-230">You can use a Node.js app to execute an HTTP request to test your function.</span></span>
<span data-ttu-id="1ce48-231">Lembre-se de definir:</span><span class="sxs-lookup"><span data-stu-id="1ce48-231">Make sure to set:</span></span>

* <span data-ttu-id="1ce48-232">O `host` nas opções de solicitação para o host do aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="1ce48-232">The `host` in the request options to your function app host.</span></span>
* <span data-ttu-id="1ce48-233">O nome da função no `path`.</span><span class="sxs-lookup"><span data-stu-id="1ce48-233">Your function name in the `path`.</span></span>
* <span data-ttu-id="1ce48-234">Seu código de acesso (`<your code>`) em `path`.</span><span class="sxs-lookup"><span data-stu-id="1ce48-234">Your access code (`<your code>`) in the `path`.</span></span>

<span data-ttu-id="1ce48-235">Exemplo de código:</span><span class="sxs-lookup"><span data-stu-id="1ce48-235">Code example:</span></span>

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


<span data-ttu-id="1ce48-236">Saída:</span><span class="sxs-lookup"><span data-stu-id="1ce48-236">Output:</span></span>

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    The address you provided is Dallas, T.X. 75201

<span data-ttu-id="1ce48-237">Na janela **Logs** do portal, é registrada uma saída semelhante à seguinte ao executar a função:</span><span class="sxs-lookup"><span data-stu-id="1ce48-237">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:08:55  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a><span data-ttu-id="1ce48-238">Testar uma função de gatilho de fila com o código: C#</span><span class="sxs-lookup"><span data-stu-id="1ce48-238">Test a queue trigger function with code: C#</span></span> #
<span data-ttu-id="1ce48-239">Mencionamos anteriormente que você pode testar um gatilho de fila usando código para remover uma mensagem na fila.</span><span class="sxs-lookup"><span data-stu-id="1ce48-239">We mentioned earlier that you can test a queue trigger by using code to drop a message in your queue.</span></span> <span data-ttu-id="1ce48-240">O exemplo de código a seguir é baseado no código C# apresentado no tutorial [Introdução ao Armazenamento de Filas do Azure](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="1ce48-240">The following example code is based on the C# code presented in the [Getting started with Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md) tutorial.</span></span> <span data-ttu-id="1ce48-241">Também há código para outras linguagens disponível nesse link.</span><span class="sxs-lookup"><span data-stu-id="1ce48-241">Code for other languages is also available from that link.</span></span>

<span data-ttu-id="1ce48-242">Para testar esse código em um aplicativo de console, que você deve:</span><span class="sxs-lookup"><span data-stu-id="1ce48-242">To test this code in a console app, you must:</span></span>

* <span data-ttu-id="1ce48-243">[Configurar a cadeia de conexão de armazenamento no arquivo app.config](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="1ce48-243">[Configure your storage connection string in the app.config file](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>
* <span data-ttu-id="1ce48-244">Passe um `name` e `address` como parâmetros para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ce48-244">Pass a `name` and `address` as parameters to the app.</span></span> <span data-ttu-id="1ce48-245">Por exemplo: `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span><span class="sxs-lookup"><span data-stu-id="1ce48-245">For example, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span></span> <span data-ttu-id="1ce48-246">(Este código aceita o nome e o endereço de um novo usuário como argumentos de linha de comando durante o tempo de execução).</span><span class="sxs-lookup"><span data-stu-id="1ce48-246">(This code accepts the name and address for a new user as command-line arguments during runtime.)</span></span>

<span data-ttu-id="1ce48-247">Código C# de exemplo:</span><span class="sxs-lookup"><span data-stu-id="1ce48-247">Example C# code:</span></span>

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

    // Create the queue client
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

    // Retrieve a reference to a queue
    CloudQueue queue = queueClient.GetQueueReference(queueName);

    // Create the queue if it doesn't already exist
    queue.CreateIfNotExists();

    // Create a message and add it to the queue.
    if (name != null)
    {
        if (address != null)
            JSON = String.Format("{{\"name\":\"{0}\",\"address\":\"{1}\"}}", name, address);
        else
            JSON = String.Format("{{\"name\":\"{0}\"}}", name);
    }

    Console.WriteLine("Adding message to " + queueName + "...");
    Console.WriteLine(JSON);

    CloudQueueMessage message = new CloudQueueMessage(JSON);
    queue.AddMessage(message);
}
```

<span data-ttu-id="1ce48-248">Na janela do navegador para a função de fila, você poderá ver cada mensagem que está sendo processada:</span><span class="sxs-lookup"><span data-stu-id="1ce48-248">In the browser window for the queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[portal do Azure]: https://portal.azure.com
