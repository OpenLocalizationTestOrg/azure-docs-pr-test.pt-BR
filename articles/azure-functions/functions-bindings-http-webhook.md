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
# <a name="azure-functions-http-and-webhook-bindings"></a><span data-ttu-id="5a030-104">Associações HTTP e de webhook do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="5a030-104">Azure Functions HTTP and webhook bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="5a030-105">Este artigo explica como tooconfigure e trabalhar com HTTP dispara e associações em funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a030-105">This article explains how tooconfigure and work with HTTP triggers and bindings in Azure Functions.</span></span>
<span data-ttu-id="5a030-106">Com isso, você pode usar funções do Azure toobuild serverless APIs e responder toowebhooks.</span><span class="sxs-lookup"><span data-stu-id="5a030-106">With these, you can use Azure Functions toobuild serverless APIs and respond toowebhooks.</span></span>

<span data-ttu-id="5a030-107">As funções do Azure fornece Olá associações a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a030-107">Azure Functions provides hello following bindings:</span></span>
- <span data-ttu-id="5a030-108">Um [gatilho HTTP](#httptrigger) permite invocar uma função com uma solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="5a030-108">An [HTTP trigger](#httptrigger) lets you invoke a function with an HTTP request.</span></span> <span data-ttu-id="5a030-109">Isso pode ser personalizado toorespond muito[webhooks](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="5a030-109">This can be customized toorespond too[webhooks](#hooktrigger).</span></span>
- <span data-ttu-id="5a030-110">Um [HTTP de saída associação](#output) permite que você toorespond toohello solicitação.</span><span class="sxs-lookup"><span data-stu-id="5a030-110">An [HTTP output binding](#output) allows you toorespond toohello request.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a><span data-ttu-id="5a030-111">Gatilho HTTP</span><span class="sxs-lookup"><span data-stu-id="5a030-111">HTTP trigger</span></span>
<span data-ttu-id="5a030-112">gatilho HTTP Olá executará a função na solicitação HTTP tooan resposta.</span><span class="sxs-lookup"><span data-stu-id="5a030-112">hello HTTP trigger will execute your function in response tooan HTTP request.</span></span> <span data-ttu-id="5a030-113">Você pode personalizá-lo toorespond tooa URL em particular ou conjunto de métodos HTTP.</span><span class="sxs-lookup"><span data-stu-id="5a030-113">You can customize it toorespond tooa particular URL or set of HTTP methods.</span></span> <span data-ttu-id="5a030-114">Um gatilho HTTP também pode ser configurado toorespond toowebhooks.</span><span class="sxs-lookup"><span data-stu-id="5a030-114">An HTTP trigger can also be configured toorespond toowebhooks.</span></span> 

<span data-ttu-id="5a030-115">Se usando o portal de funções hello, você pode também começar imediatamente usando um modelo predefinido.</span><span class="sxs-lookup"><span data-stu-id="5a030-115">If using hello Functions portal, you can also get started right away using a pre-made template.</span></span> <span data-ttu-id="5a030-116">Selecione **nova função** e escolha "API & Webhooks" hello **cenário** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="5a030-116">Select **New function** and choose "API & Webhooks" from hello **Scenario** dropdown.</span></span> <span data-ttu-id="5a030-117">Selecione um dos modelos de saudação e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="5a030-117">Select one of hello templates and click **Create**.</span></span>

<span data-ttu-id="5a030-118">Por padrão, um gatilho HTTP responderá toohello solicitação com um código de status HTTP 200 Okey e um corpo vazio.</span><span class="sxs-lookup"><span data-stu-id="5a030-118">By default, an HTTP trigger will respond toohello request with an HTTP 200 OK status code and an empty body.</span></span> <span data-ttu-id="5a030-119">toomodify Olá resposta, configure um [associação de saída HTTP](#output)</span><span class="sxs-lookup"><span data-stu-id="5a030-119">toomodify hello response, configure an [HTTP output binding](#output)</span></span>

### <a name="configuring-an-http-trigger"></a><span data-ttu-id="5a030-120">Configuração de um gatilho HTTP</span><span class="sxs-lookup"><span data-stu-id="5a030-120">Configuring an HTTP trigger</span></span>
<span data-ttu-id="5a030-121">Um gatilho HTTP é definido, incluindo um toohello semelhante do objeto JSON a seguir no hello `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="5a030-121">An HTTP trigger is defined by including a JSON object similar toohello following in hello `bindings` array of function.json:</span></span>

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
<span data-ttu-id="5a030-122">associação de saudação oferece suporte a saudação propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a030-122">hello binding supports hello following properties:</span></span>

* <span data-ttu-id="5a030-123">**nome** : necessária – o nome da variável Olá usado no código de função para solicitação de saudação ou o corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="5a030-123">**name** : Required - hello variable name used in function code for hello request or request body.</span></span> <span data-ttu-id="5a030-124">Veja [Como trabalhar com um gatilho HTTP no código](#httptriggerusage).</span><span class="sxs-lookup"><span data-stu-id="5a030-124">See [Working with an HTTP trigger from code](#httptriggerusage).</span></span>
* <span data-ttu-id="5a030-125">**tipo** : necessária - deve ser definido muito "httpTrigger".</span><span class="sxs-lookup"><span data-stu-id="5a030-125">**type** : Required - must be set too"httpTrigger".</span></span>
* <span data-ttu-id="5a030-126">**direção** : necessária - deve ser definido muito "in".</span><span class="sxs-lookup"><span data-stu-id="5a030-126">**direction** : Required - must be set too"in".</span></span>
* <span data-ttu-id="5a030-127">_authLevel_ : Isso determina quais chaves, se houver, toobe presente na solicitação de saudação na função de saudação tooinvoke order.</span><span class="sxs-lookup"><span data-stu-id="5a030-127">_authLevel_ : This determines what keys, if any, need toobe present on hello request in order tooinvoke hello function.</span></span> <span data-ttu-id="5a030-128">Veja [Como trabalhar com chaves](#keys) abaixo.</span><span class="sxs-lookup"><span data-stu-id="5a030-128">See [Working with keys](#keys) below.</span></span> <span data-ttu-id="5a030-129">valor de saudação pode ser um dos seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="5a030-129">hello value can be one of hello following:</span></span>
    * <span data-ttu-id="5a030-130">_anonymous_: nenhuma chave API é obrigatória.</span><span class="sxs-lookup"><span data-stu-id="5a030-130">_anonymous_: No API key is required.</span></span>
    * <span data-ttu-id="5a030-131">_function_: uma chave de API específica de função é obrigatória.</span><span class="sxs-lookup"><span data-stu-id="5a030-131">_function_: A function-specific API key is required.</span></span> <span data-ttu-id="5a030-132">Este é o valor de padrão de saudação se nenhum for fornecido.</span><span class="sxs-lookup"><span data-stu-id="5a030-132">This is hello default value if none is provided.</span></span>
    * <span data-ttu-id="5a030-133">_administrador_ : Olá mestre chave é necessária.</span><span class="sxs-lookup"><span data-stu-id="5a030-133">_admin_ : hello master key is required.</span></span>
* <span data-ttu-id="5a030-134">**métodos** : esta é uma matriz dos métodos Olá HTTP função hello de toowhich responderá.</span><span class="sxs-lookup"><span data-stu-id="5a030-134">**methods** : This is an array of hello HTTP methods toowhich hello function will respond.</span></span> <span data-ttu-id="5a030-135">Se não for especificado, a função hello responderá métodos tooall HTTP.</span><span class="sxs-lookup"><span data-stu-id="5a030-135">If not specified, hello function will respond tooall HTTP methods.</span></span> <span data-ttu-id="5a030-136">Consulte [Personalizando o ponto de extremidade Olá HTTP](#url).</span><span class="sxs-lookup"><span data-stu-id="5a030-136">See [Customizing hello HTTP endpoint](#url).</span></span>
* <span data-ttu-id="5a030-137">**rota** : Isso define o modelo de rota hello, controlando toowhich solicitar URLs sua função responderá.</span><span class="sxs-lookup"><span data-stu-id="5a030-137">**route** : This defines hello route template, controlling toowhich request URLs your function will respond.</span></span> <span data-ttu-id="5a030-138">Olá valor padrão se nenhum for fornecido é `<functionname>`.</span><span class="sxs-lookup"><span data-stu-id="5a030-138">hello default value if none is provided is `<functionname>`.</span></span> <span data-ttu-id="5a030-139">Consulte [Personalizando o ponto de extremidade Olá HTTP](#url).</span><span class="sxs-lookup"><span data-stu-id="5a030-139">See [Customizing hello HTTP endpoint](#url).</span></span>
* <span data-ttu-id="5a030-140">**webHookType** : Isso configura Olá HTTP gatilho tooact como um receptor do webhook para o provedor especificado hello.</span><span class="sxs-lookup"><span data-stu-id="5a030-140">**webHookType** : This configures hello HTTP trigger tooact as a webhook reciever for hello specified provider.</span></span> <span data-ttu-id="5a030-141">Olá _métodos_ propriedade não deve ser definida se isso for escolhido.</span><span class="sxs-lookup"><span data-stu-id="5a030-141">hello _methods_ property should not be set if this is chosen.</span></span> <span data-ttu-id="5a030-142">Consulte [toowebhooks respondendo](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="5a030-142">See [Responding toowebhooks](#hooktrigger).</span></span> <span data-ttu-id="5a030-143">valor de saudação pode ser um dos seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="5a030-143">hello value can be one of hello following:</span></span>
    * <span data-ttu-id="5a030-144">_genericJson_: um ponto de extremidade de webhook de finalidade geral sem lógica para um provedor específico.</span><span class="sxs-lookup"><span data-stu-id="5a030-144">_genericJson_ : A general purpose webhook endpoint without logic for a specific provider.</span></span>
    * <span data-ttu-id="5a030-145">_GitHub_ : função hello responderá tooGitHub webhooks.</span><span class="sxs-lookup"><span data-stu-id="5a030-145">_github_ : hello function will respond tooGitHub webhooks.</span></span> <span data-ttu-id="5a030-146">Olá _authLevel_ propriedade não deve ser definida se isso for escolhido.</span><span class="sxs-lookup"><span data-stu-id="5a030-146">hello _authLevel_ property should not be set if this is chosen.</span></span>
    * <span data-ttu-id="5a030-147">_margem de atraso_ : função hello responderá tooSlack webhooks.</span><span class="sxs-lookup"><span data-stu-id="5a030-147">_slack_ : hello function will respond tooSlack webhooks.</span></span> <span data-ttu-id="5a030-148">Olá _authLevel_ propriedade não deve ser definida se isso for escolhido.</span><span class="sxs-lookup"><span data-stu-id="5a030-148">hello _authLevel_ property should not be set if this is chosen.</span></span>

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a><span data-ttu-id="5a030-149">Como trabalhar com um gatilho HTTP no código</span><span class="sxs-lookup"><span data-stu-id="5a030-149">Working with an HTTP trigger from code</span></span>
<span data-ttu-id="5a030-150">Para funções do c# e F #, você pode declarar tipo de saudação do seu toobe de entrada do gatilho ou `HttpRequestMessage` ou um tipo personalizado.</span><span class="sxs-lookup"><span data-stu-id="5a030-150">For C# and F# functions, you can declare hello type of your trigger input toobe either `HttpRequestMessage` or a custom type.</span></span> <span data-ttu-id="5a030-151">Se você escolher `HttpRequestMessage`, em seguida, você obterá o objeto de solicitação de toohello acesso completo.</span><span class="sxs-lookup"><span data-stu-id="5a030-151">If you choose `HttpRequestMessage`, then you will get full access toohello request object.</span></span> <span data-ttu-id="5a030-152">Para um tipo personalizado (como um POCO), funções tentarão corpo da solicitação tooparse hello como propriedades do objeto JSON toopopulate hello.</span><span class="sxs-lookup"><span data-stu-id="5a030-152">For a custom type (such as a POCO), Functions will attempt tooparse hello request body as JSON toopopulate hello object properties.</span></span>

<span data-ttu-id="5a030-153">Para funções do Node. js, o tempo de execução de funções de saudação fornece corpo da solicitação Olá em vez do objeto de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a030-153">For Node.js functions, hello Functions runtime provides hello request body instead of hello request object.</span></span>

<span data-ttu-id="5a030-154">Veja [Exemplos de gatilho HTTP](#httptriggersample) para ver os exemplos de uso.</span><span class="sxs-lookup"><span data-stu-id="5a030-154">See [HTTP trigger samples](#httptriggersample) for example usages.</span></span>


<a name="output"></a>
## <a name="http-response-output-binding"></a><span data-ttu-id="5a030-155">Associação de saída de resposta HTTP</span><span class="sxs-lookup"><span data-stu-id="5a030-155">HTTP response output binding</span></span>
<span data-ttu-id="5a030-156">Use Olá HTTP saída associação toorespond toohello HTTP solicitação remetente.</span><span class="sxs-lookup"><span data-stu-id="5a030-156">Use hello HTTP output binding toorespond toohello HTTP request sender.</span></span> <span data-ttu-id="5a030-157">Essa associação requer um gatilho HTTP e permite resposta de saudação toocustomize associada à solicitação do disparador hello.</span><span class="sxs-lookup"><span data-stu-id="5a030-157">This binding requires an HTTP trigger and allows you toocustomize hello response associated with hello trigger's request.</span></span> <span data-ttu-id="5a030-158">Se a associação de saída HTTP não for fornecida, um gatilho HTTP retornará HTTP 200 OK com um corpo vazio.</span><span class="sxs-lookup"><span data-stu-id="5a030-158">If an HTTP output binding is not provided, an HTTP trigger will return HTTP 200 OK with an empty body.</span></span> 

### <a name="configuring-an-http-output-binding"></a><span data-ttu-id="5a030-159">Configuração de uma associação de saída HTTP</span><span class="sxs-lookup"><span data-stu-id="5a030-159">Configuring an HTTP output binding</span></span>
<span data-ttu-id="5a030-160">Olá HTTP de saída associação é definida, incluindo um toohello semelhante do objeto JSON a seguir no hello `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="5a030-160">hello HTTP output binding is defined by including a JSON object similar toohello following in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
<span data-ttu-id="5a030-161">associação de saudação contém Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a030-161">hello binding contains hello following properties:</span></span>

* <span data-ttu-id="5a030-162">**nome** : necessária - Olá usado no código de função para a resposta de saudação do nome de variável.</span><span class="sxs-lookup"><span data-stu-id="5a030-162">**name** : Required - hello variable name used in function code for hello response.</span></span> <span data-ttu-id="5a030-163">Veja [Como trabalhar com uma associação de saída no código](#outputusage).</span><span class="sxs-lookup"><span data-stu-id="5a030-163">See [Working with an HTTP output binding from code](#outputusage).</span></span>
* <span data-ttu-id="5a030-164">**tipo** : necessária - deve ser definido muito "http".</span><span class="sxs-lookup"><span data-stu-id="5a030-164">**type** : Required - must be set too"http".</span></span>
* <span data-ttu-id="5a030-165">**direção** : necessária - deve ser definido muito "out".</span><span class="sxs-lookup"><span data-stu-id="5a030-165">**direction** : Required - must be set too"out".</span></span>

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a><span data-ttu-id="5a030-166">Como trabalhar com uma associação de saída no código</span><span class="sxs-lookup"><span data-stu-id="5a030-166">Working with an HTTP output binding from code</span></span>
<span data-ttu-id="5a030-167">Você pode usar o hello saída parâmetro (por exemplo, "res") toorespond toohello http ou webhook chamador.</span><span class="sxs-lookup"><span data-stu-id="5a030-167">You can use hello output parameter (e.g., "res") toorespond toohello http or webhook caller.</span></span> <span data-ttu-id="5a030-168">Como alternativa, você pode usar o padrão `Request.CreateResponse()` (c#) ou `context.res` (Node. js) padrão tooreturn sua resposta.</span><span class="sxs-lookup"><span data-stu-id="5a030-168">Alternatively, you can use the standard `Request.CreateResponse()` (C#) or `context.res` (Node.JS) pattern tooreturn your response.</span></span> <span data-ttu-id="5a030-169">Para obter exemplos de como toouse Olá último método, consulte [exemplos de gatilho HTTP](#httptriggersample) e [exemplos de gatilho de Webhook](#hooktriggersample).</span><span class="sxs-lookup"><span data-stu-id="5a030-169">For examples on how toouse hello latter method, see [HTTP trigger samples](#httptriggersample) and [Webhook trigger samples](#hooktriggersample).</span></span>


<a name="hooktrigger"></a>
## <a name="responding-toowebhooks"></a><span data-ttu-id="5a030-170">Responder toowebhooks</span><span class="sxs-lookup"><span data-stu-id="5a030-170">Responding toowebhooks</span></span>
<span data-ttu-id="5a030-171">Um gatilho HTTP com hello _webHookType_ propriedade serão configurado toorespond muito[webhooks](https://en.wikipedia.org/wiki/Webhook).</span><span class="sxs-lookup"><span data-stu-id="5a030-171">An HTTP trigger with hello _webHookType_ property will be configured toorespond too[webhooks](https://en.wikipedia.org/wiki/Webhook).</span></span> <span data-ttu-id="5a030-172">configuração básica do Hello usa configuração de "genericJson" hello.</span><span class="sxs-lookup"><span data-stu-id="5a030-172">hello basic configuration uses hello "genericJson" setting.</span></span> <span data-ttu-id="5a030-173">Isso restringe solicitações tooonly aqueles usando HTTP POST e Olá `application/json` tipo de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="5a030-173">This restricts requests tooonly those using HTTP POST and with hello `application/json` content type.</span></span>

<span data-ttu-id="5a030-174">Olá gatilho pode ser personalizada tooa webhook específico provedor (por exemplo, [GitHub](https://developer.github.com/webhooks/) e [Slack](https://api.slack.com/outgoing-webhooks)).</span><span class="sxs-lookup"><span data-stu-id="5a030-174">hello trigger can additionally be tailored tooa specific webhook provider (e.g., [GitHub](https://developer.github.com/webhooks/) and [Slack](https://api.slack.com/outgoing-webhooks)).</span></span> <span data-ttu-id="5a030-175">Se um provedor for especificado, tempo de execução de funções hello pode cuidar da lógica de validação do provedor Olá para você.</span><span class="sxs-lookup"><span data-stu-id="5a030-175">If a provider is specified, hello Functions runtime can take care of hello provider's validation logic for you.</span></span>  

### <a name="configuring-github-as-a-webhook-provider"></a><span data-ttu-id="5a030-176">Configurando o GitHub como um provedor de webhook</span><span class="sxs-lookup"><span data-stu-id="5a030-176">Configuring GitHub as a webhook provider</span></span>
<span data-ttu-id="5a030-177">toorespond tooGitHub webhooks, primeiro crie a função com um gatilho de HTTP e defina Olá _webHookType_ propriedade muito "github".</span><span class="sxs-lookup"><span data-stu-id="5a030-177">toorespond tooGitHub webhooks, first create your function with an HTTP Trigger, and set hello _webHookType_ property too"github".</span></span> <span data-ttu-id="5a030-178">Em seguida, copie a [URL](#url) e a [chave de API](#keys) na página **Adicionar webhook** do seu repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="5a030-178">Then copy its [URL](#url) and [API key](#keys) into your GitHub repository's **Add webhook** page.</span></span> <span data-ttu-id="5a030-179">Veja a documentação sobre [como criar webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) do GitHub para saber mais.</span><span class="sxs-lookup"><span data-stu-id="5a030-179">See GitHub's [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentation for more.</span></span>

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a><span data-ttu-id="5a030-180">Configuração do Slack como um provedor de webhook</span><span class="sxs-lookup"><span data-stu-id="5a030-180">Configuring Slack as a webhook provider</span></span>
<span data-ttu-id="5a030-181">webhook atraso Hello gera um token para você em vez de deixar a especificá-lo, portanto você deve configurar uma chave específica de função com o token de saudação do atraso.</span><span class="sxs-lookup"><span data-stu-id="5a030-181">hello Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with hello token from Slack.</span></span> <span data-ttu-id="5a030-182">Veja [Como trabalhar com chaves](#keys).</span><span class="sxs-lookup"><span data-stu-id="5a030-182">See [Working with keys](#keys).</span></span>

<a name="url"></a>
## <a name="customizing-hello-http-endpoint"></a><span data-ttu-id="5a030-183">Personalizando o ponto de extremidade HTTP Olá</span><span class="sxs-lookup"><span data-stu-id="5a030-183">Customizing hello HTTP endpoint</span></span>
<span data-ttu-id="5a030-184">Por padrão quando você cria uma função para um gatilho HTTP ou WebHook, função hello é endereçável com uma rota do formulário de saudação:</span><span class="sxs-lookup"><span data-stu-id="5a030-184">By default when you create a function for an HTTP trigger, or WebHook, hello function is addressable with a route of hello form:</span></span>

    http://<yourapp>.azurewebsites.net/api/<funcname> 

<span data-ttu-id="5a030-185">Você pode personalizar essa rota usando Olá opcional `route` propriedade no disparador Olá HTTP da associação de entrada.</span><span class="sxs-lookup"><span data-stu-id="5a030-185">You can customize this route using hello optional `route` property on hello HTTP trigger's input binding.</span></span> <span data-ttu-id="5a030-186">Por exemplo, Olá a seguir *function.json* arquivo define uma `route` propriedade para um gatilho HTTP:</span><span class="sxs-lookup"><span data-stu-id="5a030-186">As an example, hello following *function.json* file defines a `route` property for an HTTP trigger:</span></span>

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

<span data-ttu-id="5a030-187">Usando esta configuração, função hello agora é endereçável por hello rota em vez de rota originais Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="5a030-187">Using this configuration, hello function is now addressable with hello following route instead of hello original route.</span></span>

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

<span data-ttu-id="5a030-188">Isso permite que o código de função hello toosupport dois parâmetros no endereço hello, "categoria" e "id".</span><span class="sxs-lookup"><span data-stu-id="5a030-188">This allows hello function code toosupport two parameters in hello address, "category" and "id".</span></span> <span data-ttu-id="5a030-189">Você pode usar qualquer [Restrição de rota de API Web](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) com seus parâmetros.</span><span class="sxs-lookup"><span data-stu-id="5a030-189">You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span></span> <span data-ttu-id="5a030-190">Olá código da função c# a seguir faz uso de ambos os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="5a030-190">hello following C# function code makes use of both parameters.</span></span>

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

<span data-ttu-id="5a030-191">Aqui está saudação do Node. js função código toouse os mesmos parâmetros de rota.</span><span class="sxs-lookup"><span data-stu-id="5a030-191">Here is Node.js function code toouse hello same route parameters.</span></span>

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

<span data-ttu-id="5a030-192">Por padrão, todas as rotas de função são prefixadas com *api*.</span><span class="sxs-lookup"><span data-stu-id="5a030-192">By default, all function routes are prefixed with *api*.</span></span> <span data-ttu-id="5a030-193">Você também pode personalizar ou remover prefixo hello usando Olá `http.routePrefix` propriedade em seu *host.json* arquivo.</span><span class="sxs-lookup"><span data-stu-id="5a030-193">You can also customize or remove hello prefix using hello `http.routePrefix` property in your *host.json* file.</span></span> <span data-ttu-id="5a030-194">Olá, exemplo a seguir remove Olá *api* prefixo da rota usando uma cadeia de caracteres vazia para o prefixo Olá Olá *host.json* arquivo.</span><span class="sxs-lookup"><span data-stu-id="5a030-194">hello following example removes hello *api* route prefix by using an empty string for hello prefix in hello *host.json* file.</span></span>

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

<span data-ttu-id="5a030-195">Para obter informações detalhadas sobre como Olá tooupdate *host.json* arquivo de sua função, consulte [tooupdate funcionamento arquivos do aplicativo](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="5a030-195">For detailed information on how tooupdate hello *host.json* file for your function, See, [How tooupdate function app files](functions-reference.md#fileupdate).</span></span> 

<span data-ttu-id="5a030-196">Para obter informações sobre outras propriedades que você pode configurar no seu arquivo *host.json*, consulte [referência host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="5a030-196">For information on other properties you can configure in your *host.json* file, see [host.json reference](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>


<a name="keys"></a>
## <a name="working-with-keys"></a><span data-ttu-id="5a030-197">Como trabalhar com chaves</span><span class="sxs-lookup"><span data-stu-id="5a030-197">Working with keys</span></span>
<span data-ttu-id="5a030-198">HttpTriggers pode aproveitar as chaves para aumentar a segurança.</span><span class="sxs-lookup"><span data-stu-id="5a030-198">HttpTriggers can leverage keys for added security.</span></span> <span data-ttu-id="5a030-199">Um padrão HttpTrigger pode usá-los como uma chave de API, a necessidade Olá a chave toobe presente na solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a030-199">A standard HttpTrigger can use these as an API key, requiring hello key toobe present on hello request.</span></span> <span data-ttu-id="5a030-200">Webhooks pode usar chaves tooauthorize solicitações de várias maneiras, dependendo de qual provedor Olá oferece suporte.</span><span class="sxs-lookup"><span data-stu-id="5a030-200">Webhooks can use keys tooauthorize requests in a variety of ways, depending on what hello provider supports.</span></span>

<span data-ttu-id="5a030-201">As chaves são armazenadas como parte do seu aplicativo de funções no Azure e criptografadas em repouso.</span><span class="sxs-lookup"><span data-stu-id="5a030-201">Keys are stored as part of your function app in Azure and are encrypted at rest.</span></span> <span data-ttu-id="5a030-202">tooview suas chaves, criar novos roll toonew valores de chaves, navegar tooone das funções no portal de saudação e selecione "Gerenciar".</span><span class="sxs-lookup"><span data-stu-id="5a030-202">tooview your keys, create new ones, or roll keys toonew values, navigate tooone of your functions within hello portal and select "Manage."</span></span> 

<span data-ttu-id="5a030-203">Há dois tipos de chave:</span><span class="sxs-lookup"><span data-stu-id="5a030-203">There are two types of keys:</span></span>
- <span data-ttu-id="5a030-204">**As chaves de host**: essas chaves são compartilhadas por todas as funções no aplicativo de função hello.</span><span class="sxs-lookup"><span data-stu-id="5a030-204">**Host keys**: These keys are shared by all functions within hello function app.</span></span> <span data-ttu-id="5a030-205">Quando usado como uma chave de API, elas permitem acesso tooany função no aplicativo de função hello.</span><span class="sxs-lookup"><span data-stu-id="5a030-205">When used as an API key, these allow access tooany function within hello function app.</span></span>
- <span data-ttu-id="5a030-206">**Teclas de função**: essas chaves se aplicam somente toohello funções específicas sob as quais elas são definidas.</span><span class="sxs-lookup"><span data-stu-id="5a030-206">**Function keys**: These keys apply only toohello specific functions under which they are defined.</span></span> <span data-ttu-id="5a030-207">Quando usado como uma chave de API, somente permite acesso toothat função.</span><span class="sxs-lookup"><span data-stu-id="5a030-207">When used as an API key, these only allow access toothat function.</span></span>

<span data-ttu-id="5a030-208">Cada chave é nomeado para referência e há uma chave padrão (denominada "padrão") no nível de host e a função hello.</span><span class="sxs-lookup"><span data-stu-id="5a030-208">Each key is named for reference, and there is a default key (named "default") at hello function and host level.</span></span> <span data-ttu-id="5a030-209">Olá **chave mestra** uma chave de host padrão chamada "_master" que é definido para cada função de aplicativo e não pode ser revogado.</span><span class="sxs-lookup"><span data-stu-id="5a030-209">hello **master key** is a default host key named "_master" that is defined for each function app and cannot be revoked.</span></span> <span data-ttu-id="5a030-210">Ele fornece acesso administrativo toohello runtime APIs.</span><span class="sxs-lookup"><span data-stu-id="5a030-210">It provides administrative access toohello runtime APIs.</span></span> <span data-ttu-id="5a030-211">Usando `"authLevel": "admin"` em Olá associação JSON exigirá essa chave toobe apresentada na solicitação Olá; qualquer outra chave resultará em uma falha de autorização.</span><span class="sxs-lookup"><span data-stu-id="5a030-211">Using `"authLevel": "admin"` in hello binding JSON will require this key toobe presented on hello request; any other key will result in a authorization failure.</span></span>

> [!NOTE]
> <span data-ttu-id="5a030-212">Vencimento toohello elevados de permissões concedidas pela chave mestra de saudação, você não deve compartilhar essa chave com terceiros ou distribuí-lo em aplicativos cliente nativo.</span><span class="sxs-lookup"><span data-stu-id="5a030-212">Due toohello elevated permissions granted by hello master key, you should not share this key with third parties or distribute it in native client applications.</span></span> <span data-ttu-id="5a030-213">Tenha cuidado ao escolher o nível de autorização do administrador de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a030-213">Exercise caution when choosing hello admin authorization level.</span></span>
> 
> 

### <a name="api-key-authorization"></a><span data-ttu-id="5a030-214">Autorização da chave de API</span><span class="sxs-lookup"><span data-stu-id="5a030-214">API key authorization</span></span>
<span data-ttu-id="5a030-215">Por padrão, um HttpTrigger requer uma chave de API na solicitação HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="5a030-215">By default, an HttpTrigger requires an API key in hello HTTP request.</span></span> <span data-ttu-id="5a030-216">Portanto, sua solicitação HTTP geralmente se parecerá como esta:</span><span class="sxs-lookup"><span data-stu-id="5a030-216">So your HTTP request normally looks like this:</span></span>

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

<span data-ttu-id="5a030-217">chave de saudação pode ser incluído em uma variável de cadeia de caracteres de consulta chamada `code`, como acima, ou ele pode ser incluído em um `x-functions-key` cabeçalho HTTP.</span><span class="sxs-lookup"><span data-stu-id="5a030-217">hello key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span></span> <span data-ttu-id="5a030-218">valor de saudação da chave Olá pode ser qualquer tecla de função definido para a função hello, ou qualquer chave de host.</span><span class="sxs-lookup"><span data-stu-id="5a030-218">hello value of hello key can be any function key defined for hello function, or any host key.</span></span>

<span data-ttu-id="5a030-219">Você pode escolher solicitações tooallow sem chaves ou especificar a chave mestra Olá deve ser usado por meio da alteração Olá `authLevel` propriedade Olá associação JSON (consulte [gatilho HTTP](#httptrigger)).</span><span class="sxs-lookup"><span data-stu-id="5a030-219">You can choose tooallow requests without keys or specify that hello master key must be used by changing hello `authLevel` property in hello binding JSON (see [HTTP trigger](#httptrigger)).</span></span>

### <a name="keys-and-webhooks"></a><span data-ttu-id="5a030-220">Chaves e webhooks</span><span class="sxs-lookup"><span data-stu-id="5a030-220">Keys and webhooks</span></span>
<span data-ttu-id="5a030-221">Autorização de Webhook é tratada pelo componente de receptor de webhook Olá, parte da saudação HttpTrigger e mecanismo Olá varia com base no tipo de webhook Olá.</span><span class="sxs-lookup"><span data-stu-id="5a030-221">Webhook authorization is handled by hello webhook reciever component, part of hello HttpTrigger, and hello mechanism varies based on hello webhook type.</span></span> <span data-ttu-id="5a030-222">No entanto, cada mecanismo depende de uma chave.</span><span class="sxs-lookup"><span data-stu-id="5a030-222">Each mechanism does, however rely on a key.</span></span> <span data-ttu-id="5a030-223">Por padrão, a tecla de função hello denominada "padrão" será usada.</span><span class="sxs-lookup"><span data-stu-id="5a030-223">By default, hello function key named "default" will be used.</span></span> <span data-ttu-id="5a030-224">Se você desejar toouse uma chave diferente, você precisará tooconfigure Olá provedor toosend Olá chave o nome do webhook com solicitação de saudação em uma saudação maneiras a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a030-224">If you wish toouse a different key, you will need tooconfigure hello webhook provider toosend hello key name with hello request in one of hello following ways:</span></span>

- <span data-ttu-id="5a030-225">**Cadeia de caracteres de consulta**: provedor Olá passa o nome da chave Olá Olá `clientid` parâmetro de cadeia de caracteres de consulta (por exemplo, `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span><span class="sxs-lookup"><span data-stu-id="5a030-225">**Query string**: hello provider passes hello key name in hello `clientid` query string parameter (e.g., `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span></span>
- <span data-ttu-id="5a030-226">**Cabeçalho de solicitação**: provedor Olá passa o nome da chave Olá Olá `x-functions-clientid` cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="5a030-226">**Request header**: hello provider passes hello key name in hello `x-functions-clientid` header.</span></span>

> [!NOTE]
> <span data-ttu-id="5a030-227">As chaves de função têm precedência sobre as chaves de host.</span><span class="sxs-lookup"><span data-stu-id="5a030-227">Function keys take precedence over host keys.</span></span> <span data-ttu-id="5a030-228">Se duas chaves são definidas com o mesmo nome, hello de saudação tecla de função que será usada.</span><span class="sxs-lookup"><span data-stu-id="5a030-228">If two keys are defined with hello same name, hello function key will be used.</span></span>
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a><span data-ttu-id="5a030-229">Exemplos de gatilho HTTP</span><span class="sxs-lookup"><span data-stu-id="5a030-229">HTTP trigger samples</span></span>
<span data-ttu-id="5a030-230">Suponha que você tenha Olá seguindo gatilho HTTP no hello `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="5a030-230">Suppose you have hello following HTTP trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

<span data-ttu-id="5a030-231">Consulte Olá específico do idioma exemplo procura um `name` parâmetro na cadeia de caracteres de consulta de saudação ou corpo de saudação da solicitação de saudação HTTP.</span><span class="sxs-lookup"><span data-stu-id="5a030-231">See hello language-specific sample that looks for a `name` parameter either in hello query string or hello body of hello HTTP request.</span></span>

* [<span data-ttu-id="5a030-232">C#</span><span class="sxs-lookup"><span data-stu-id="5a030-232">C#</span></span>](#httptriggercsharp)
* [<span data-ttu-id="5a030-233">F#</span><span class="sxs-lookup"><span data-stu-id="5a030-233">F#</span></span>](#httptriggerfsharp)
* [<span data-ttu-id="5a030-234">Node.js</span><span class="sxs-lookup"><span data-stu-id="5a030-234">Node.js</span></span>](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a><span data-ttu-id="5a030-235">Exemplo de gatilho HTTP em C#</span><span class="sxs-lookup"><span data-stu-id="5a030-235">HTTP trigger sample in C#</span></span> #
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

<span data-ttu-id="5a030-236">Você também pode associar tooa POCO em vez de `HttpRequestMessage`.</span><span class="sxs-lookup"><span data-stu-id="5a030-236">You can also bind tooa POCO instead of `HttpRequestMessage`.</span></span> <span data-ttu-id="5a030-237">Isso será ser serializado do corpo de saudação da solicitação hello, analisada como JSON.</span><span class="sxs-lookup"><span data-stu-id="5a030-237">This will be hydrated from hello body of hello request, parsed as JSON.</span></span> <span data-ttu-id="5a030-238">Da mesma forma, um tipo pode ser passado a saída de resposta de toohello HTTP de associação, e isso será retornado como o corpo da resposta hello, com um código de 200 status.</span><span class="sxs-lookup"><span data-stu-id="5a030-238">Similarly, a type can be passed toohello HTTP response output binding, and this will be returned as hello response body, with a 200 status code.</span></span>
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
### <a name="http-trigger-sample-in-f"></a><span data-ttu-id="5a030-239">Exemplo de gatilho HTTP em F#</span><span class="sxs-lookup"><span data-stu-id="5a030-239">HTTP trigger sample in F#</span></span> #
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

<span data-ttu-id="5a030-240">É necessário um `project.json` arquivo que usa NuGet tooreference Olá `FSharp.Interop.Dynamic` e `Dynamitey` assemblies, como este:</span><span class="sxs-lookup"><span data-stu-id="5a030-240">You need a `project.json` file that uses NuGet tooreference hello `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, like this:</span></span>

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

<span data-ttu-id="5a030-241">Isso usará NuGet toofetch suas dependências e fará referência-los em seu script.</span><span class="sxs-lookup"><span data-stu-id="5a030-241">This will use NuGet toofetch your dependencies and will reference them in your script.</span></span>

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a><span data-ttu-id="5a030-242">Exemplo de gatilho HTTP em Node.JS</span><span class="sxs-lookup"><span data-stu-id="5a030-242">HTTP trigger sample in Node.JS</span></span>
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
## <a name="webhook-samples"></a><span data-ttu-id="5a030-243">Exemplos de webhook</span><span class="sxs-lookup"><span data-stu-id="5a030-243">Webhook samples</span></span>
<span data-ttu-id="5a030-244">Suponha que você tenha Olá seguindo gatilho webhook Olá `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="5a030-244">Suppose you have hello following webhook trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

<span data-ttu-id="5a030-245">Consulte Olá específico do idioma exemplo registra comentários de problema do GitHub.</span><span class="sxs-lookup"><span data-stu-id="5a030-245">See hello language-specific sample that logs GitHub issue comments.</span></span>

* [<span data-ttu-id="5a030-246">C#</span><span class="sxs-lookup"><span data-stu-id="5a030-246">C#</span></span>](#hooktriggercsharp)
* [<span data-ttu-id="5a030-247">F#</span><span class="sxs-lookup"><span data-stu-id="5a030-247">F#</span></span>](#hooktriggerfsharp)
* [<span data-ttu-id="5a030-248">Node.js</span><span class="sxs-lookup"><span data-stu-id="5a030-248">Node.js</span></span>](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a><span data-ttu-id="5a030-249">Exemplo de webhook em C#</span><span class="sxs-lookup"><span data-stu-id="5a030-249">Webhook sample in C#</span></span> #
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

### <a name="webhook-sample-in-f"></a><span data-ttu-id="5a030-250">Exemplo de webhook em F#</span><span class="sxs-lookup"><span data-stu-id="5a030-250">Webhook sample in F#</span></span> #
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

### <a name="webhook-sample-in-nodejs"></a><span data-ttu-id="5a030-251">Exemplo de webhook em Node.JS</span><span class="sxs-lookup"><span data-stu-id="5a030-251">Webhook sample in Node.JS</span></span>
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a><span data-ttu-id="5a030-252">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5a030-252">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

