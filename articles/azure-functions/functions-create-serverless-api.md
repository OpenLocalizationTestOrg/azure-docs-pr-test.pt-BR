---
title: "aaaCreate uma API serverless usando funções do Azure | Microsoft Docs"
description: "Como toocreate uma API serverless usando funções do Azure"
services: functions
author: mattchenderson
manager: erikre
ms.service: functions
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: mahender
ms.custom: mvc
ms.openlocfilehash: 877e3b229d5477fc5fec594ccd284fb55d7f3c07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a><span data-ttu-id="0383f-103">Criar uma API sem servidor usando o Azure Functions</span><span class="sxs-lookup"><span data-stu-id="0383f-103">Create a serverless API using Azure Functions</span></span>

<span data-ttu-id="0383f-104">Neste tutorial você aprenderá como funções do Azure permite que você toobuild APIs altamente dimensionável.</span><span class="sxs-lookup"><span data-stu-id="0383f-104">In this tutorial you will learn how Azure Functions allows you toobuild highly-scalable APIs.</span></span> <span data-ttu-id="0383f-105">As funções do Azure vem com uma coleção de internos HTTP gatilhos e associações que torna fácil tooauthor um ponto de extremidade em uma variedade de linguagens, incluindo Node. js, c# e muito mais.</span><span class="sxs-lookup"><span data-stu-id="0383f-105">Azure Functions comes with a collection of built-in HTTP triggers and bindings which make it easy tooauthor an endpoint in a variety of languages, including Node.JS, C#, and more.</span></span> <span data-ttu-id="0383f-106">Neste tutorial, você irá Personalizar ações específicas do gatilho toohandle um HTTP no seu projeto de API.</span><span class="sxs-lookup"><span data-stu-id="0383f-106">In this tutorial, you will customize an HTTP trigger toohandle specific actions in your API design.</span></span> <span data-ttu-id="0383f-107">Você também preparará a expansão de sua API integrando-a aos Proxies do Azure Functions e configurando APIs de simulação.</span><span class="sxs-lookup"><span data-stu-id="0383f-107">You will also prepare for growing your API by integrating it with Azure Functions Proxies and setting up mock APIs.</span></span> <span data-ttu-id="0383f-108">Tudo isso é feito sobre o ambiente de computação sem servidor funções de hello, portanto você não tem tooworry sobre como dimensionar recursos - assim, você pode se concentrar na lógica da sua API.</span><span class="sxs-lookup"><span data-stu-id="0383f-108">All of this is accomplished on top of hello Functions serverless compute environment, so you don't have tooworry about scaling resources - you can just focus on your API logic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0383f-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0383f-109">Prerequisites</span></span> 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

<span data-ttu-id="0383f-110">função resultante Olá será usada para o restante deste tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="0383f-110">hello resulting function will be used for hello rest of this tutorial.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="0383f-111">Entrar tooAzure</span><span class="sxs-lookup"><span data-stu-id="0383f-111">Sign in tooAzure</span></span>

<span data-ttu-id="0383f-112">Olá Abrir portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0383f-112">Open hello Azure portal.</span></span> <span data-ttu-id="0383f-113">toodo isso, entrar muito[https://portal.azure.com](https://portal.azure.com) com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="0383f-113">toodo this, sign in too[https://portal.azure.com](https://portal.azure.com) with your Azure account.</span></span>

## <a name="customize-your-http-function"></a><span data-ttu-id="0383f-114">Personalizar sua função HTTP</span><span class="sxs-lookup"><span data-stu-id="0383f-114">Customize your HTTP function</span></span>

<span data-ttu-id="0383f-115">Por padrão, a função disparado HTTP é tooaccept configurado qualquer método HTTP.</span><span class="sxs-lookup"><span data-stu-id="0383f-115">By default, your HTTP-triggered function is configured tooaccept any HTTP method.</span></span> <span data-ttu-id="0383f-116">Também é uma URL padrão do formulário de saudação `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span><span class="sxs-lookup"><span data-stu-id="0383f-116">There is also a default URL of hello form `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span></span> <span data-ttu-id="0383f-117">Se você seguiu quickstart hello, em seguida, `<funcname>` parece ser algo como "HttpTriggerJS1".</span><span class="sxs-lookup"><span data-stu-id="0383f-117">If you followed hello quickstart, then `<funcname>` probably looks something like "HttpTriggerJS1".</span></span> <span data-ttu-id="0383f-118">Nesta seção, você modificará a solicitações do hello função toorespond tooGET somente nos `/api/hello` rotear em vez disso.</span><span class="sxs-lookup"><span data-stu-id="0383f-118">In this section, you will modify hello function toorespond only tooGET requests against `/api/hello` route instead.</span></span> 

<span data-ttu-id="0383f-119">Navegue tooyour função hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0383f-119">Navigate tooyour function in hello Azure portal.</span></span> <span data-ttu-id="0383f-120">Selecione **integrar** em Olá barra de navegação esquerda.</span><span class="sxs-lookup"><span data-stu-id="0383f-120">Select **Integrate** in hello left navigation.</span></span>

![Personalizar uma função HTTP](./media/functions-create-serverless-api/customizing-http.png)

<span data-ttu-id="0383f-122">Use as configurações do disparador HTTP conforme especificado na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="0383f-122">Use the HTTP trigger settings as specified in hello table.</span></span>

| <span data-ttu-id="0383f-123">Campo</span><span class="sxs-lookup"><span data-stu-id="0383f-123">Field</span></span> | <span data-ttu-id="0383f-124">Valor de exemplo</span><span class="sxs-lookup"><span data-stu-id="0383f-124">Sample value</span></span> | <span data-ttu-id="0383f-125">Descrição</span><span class="sxs-lookup"><span data-stu-id="0383f-125">Description</span></span> |
|---|---|---|
| <span data-ttu-id="0383f-126">Métodos HTTP selecionados</span><span class="sxs-lookup"><span data-stu-id="0383f-126">Allowed HTTP methods</span></span> | <span data-ttu-id="0383f-127">Métodos selecionados</span><span class="sxs-lookup"><span data-stu-id="0383f-127">Selected methods</span></span> | <span data-ttu-id="0383f-128">Determina quais métodos HTTP podem ser usado tooinvoke esta função</span><span class="sxs-lookup"><span data-stu-id="0383f-128">Determines what HTTP methods may be used tooinvoke this function</span></span> |
| <span data-ttu-id="0383f-129">Métodos HTTP selecionados</span><span class="sxs-lookup"><span data-stu-id="0383f-129">Selected HTTP methods</span></span> | <span data-ttu-id="0383f-130">GET</span><span class="sxs-lookup"><span data-stu-id="0383f-130">GET</span></span> | <span data-ttu-id="0383f-131">Permite que somente selecionado toobe de métodos HTTP usadas tooinvoke esta função</span><span class="sxs-lookup"><span data-stu-id="0383f-131">Allows only selected HTTP methods toobe used tooinvoke this function</span></span> |
| <span data-ttu-id="0383f-132">Modelo de rota</span><span class="sxs-lookup"><span data-stu-id="0383f-132">Route template</span></span> | <span data-ttu-id="0383f-133">/hello</span><span class="sxs-lookup"><span data-stu-id="0383f-133">/hello</span></span> | <span data-ttu-id="0383f-134">Determina quais rota é tooinvoke usada nesta função</span><span class="sxs-lookup"><span data-stu-id="0383f-134">Determines what route is used tooinvoke this function</span></span> |

<span data-ttu-id="0383f-135">Observe que você não incluiu Olá `/api` de prefixo de caminho no modelo de rota Olá, como isso é tratado por uma configuração global.</span><span class="sxs-lookup"><span data-stu-id="0383f-135">Note that you did not include hello `/api` base path prefix in hello route template, as this is handled by a global setting.</span></span>

<span data-ttu-id="0383f-136">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="0383f-136">Click **Save**.</span></span>

<span data-ttu-id="0383f-137">Você pode aprender mais sobre a personalização de funções HTTP em [Associações HTTP e webhook do Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span><span class="sxs-lookup"><span data-stu-id="0383f-137">You can learn more about customizing HTTP functions in [Azure Functions HTTP and webhook bindings](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span></span>

### <a name="test-your-api"></a><span data-ttu-id="0383f-138">Testar sua API</span><span class="sxs-lookup"><span data-stu-id="0383f-138">Test your API</span></span>

<span data-ttu-id="0383f-139">Em seguida, teste sua função toosee-lo funcionar com a nova superfície de API hello.</span><span class="sxs-lookup"><span data-stu-id="0383f-139">Next, test your function toosee it working with hello new API surface.</span></span>

<span data-ttu-id="0383f-140">Navegue página de desenvolvimento toohello back clicando no nome da função de saudação na barra de navegação esquerda de saudação.</span><span class="sxs-lookup"><span data-stu-id="0383f-140">Navigate back toohello development page by clicking on hello function's name in hello left navigation.</span></span>

<span data-ttu-id="0383f-141">Clique em **obter URL de função** e copie a URL de saudação.</span><span class="sxs-lookup"><span data-stu-id="0383f-141">Click **Get function URL** and copy hello URL.</span></span> <span data-ttu-id="0383f-142">Você verá que ele usa Olá `/api/hello` rotear agora.</span><span class="sxs-lookup"><span data-stu-id="0383f-142">You should see that it uses hello `/api/hello` route now.</span></span>

<span data-ttu-id="0383f-143">Copie a URL de saudação em uma nova guia do navegador ou o cliente REST preferencial.</span><span class="sxs-lookup"><span data-stu-id="0383f-143">Copy hello URL into a new browser tab or your preferred REST client.</span></span> <span data-ttu-id="0383f-144">Navegadores usarão GET por padrão.</span><span class="sxs-lookup"><span data-stu-id="0383f-144">Browsers will use GET by default.</span></span>

<span data-ttu-id="0383f-145">Executar função hello e confirme se ele está funcionando.</span><span class="sxs-lookup"><span data-stu-id="0383f-145">Run hello function and confirm that it is working.</span></span> <span data-ttu-id="0383f-146">Parâmetro de "nome" hello tooprovide talvez seja necessário como um código de início rápido da saudação consulta cadeia de caracteres toosatisfy.</span><span class="sxs-lookup"><span data-stu-id="0383f-146">You may need tooprovide hello "name" parameter as a query string toosatisfy hello quickstart code.</span></span>

<span data-ttu-id="0383f-147">Você também pode tentar chamar o ponto de extremidade de saudação com outro tooconfirm de método HTTP que a função hello não é executada.</span><span class="sxs-lookup"><span data-stu-id="0383f-147">You can also try calling hello endpoint with another HTTP method tooconfirm that hello function is not executed.</span></span> <span data-ttu-id="0383f-148">Para isso, você precisará toouse um cliente REST, como rotação, carteiro ou o Fiddler.</span><span class="sxs-lookup"><span data-stu-id="0383f-148">For this, you will need toouse a REST client, such as cURL, Postman, or Fiddler.</span></span>

## <a name="proxies-overview"></a><span data-ttu-id="0383f-149">Visão geral dos proxies</span><span class="sxs-lookup"><span data-stu-id="0383f-149">Proxies overview</span></span>

<span data-ttu-id="0383f-150">Na próxima seção, Olá, você será superficial sua API por meio de um proxy.</span><span class="sxs-lookup"><span data-stu-id="0383f-150">In hello next section, you will surface your API through a proxy.</span></span> <span data-ttu-id="0383f-151">Proxies de funções do Azure é um recurso de visualização que permite que você tooforward solicitações tooother recursos.</span><span class="sxs-lookup"><span data-stu-id="0383f-151">Azure Functions Proxies is a preview feature that allows you tooforward requests tooother resources.</span></span> <span data-ttu-id="0383f-152">Definir um ponto de extremidade HTTP como com o gatilho HTTP, mas em vez de escrever código tooexecute quando é chamado de ponto de extremidade, você fornece uma implementação de remoto tooa URL.</span><span class="sxs-lookup"><span data-stu-id="0383f-152">You define an HTTP endpoint just like with HTTP trigger, but instead of writing code tooexecute when that endpoint is called, you provide a URL tooa remote implementation.</span></span> <span data-ttu-id="0383f-153">Isso permite que você toocompose API várias fontes em uma única superfície de API que é fácil para os clientes tooconsume.</span><span class="sxs-lookup"><span data-stu-id="0383f-153">This allows you toocompose multiple API sources into a single API surface which is easy for clients tooconsume.</span></span> <span data-ttu-id="0383f-154">Isso é particularmente útil se você quiser toobuild sua API como microservices.</span><span class="sxs-lookup"><span data-stu-id="0383f-154">This is particularly useful if you wish toobuild your API as microservices.</span></span>

<span data-ttu-id="0383f-155">Um proxy pode apontar o recurso de tooany HTTP, como:</span><span class="sxs-lookup"><span data-stu-id="0383f-155">A proxy can point tooany HTTP resource, such as:</span></span>
- <span data-ttu-id="0383f-156">Funções do Azure</span><span class="sxs-lookup"><span data-stu-id="0383f-156">Azure Functions</span></span> 
- <span data-ttu-id="0383f-157">Aplicativos de API no [Serviço de Aplicativo do Azure](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span><span class="sxs-lookup"><span data-stu-id="0383f-157">API apps in [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span></span>
- <span data-ttu-id="0383f-158">Contêineres de docker no [Serviço de Aplicativo no Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span><span class="sxs-lookup"><span data-stu-id="0383f-158">Docker containers in [App Service on Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span></span>
- <span data-ttu-id="0383f-159">Qualquer outra API hospedada</span><span class="sxs-lookup"><span data-stu-id="0383f-159">Any other hosted API</span></span>

<span data-ttu-id="0383f-160">toolearn mais sobre proxies, consulte [trabalhando com Proxies de funções do Azure (visualização)].</span><span class="sxs-lookup"><span data-stu-id="0383f-160">toolearn more about proxies, see [Working with Azure Functions Proxies (preview)].</span></span>

## <a name="create-your-first-proxy"></a><span data-ttu-id="0383f-161">Criar seu primeiro proxy</span><span class="sxs-lookup"><span data-stu-id="0383f-161">Create your first proxy</span></span>

<span data-ttu-id="0383f-162">Nesta seção, você criará um novo proxy que serve como um front-end tooyour API geral.</span><span class="sxs-lookup"><span data-stu-id="0383f-162">In this section, you will create a new proxy which serves as a frontend tooyour overall API.</span></span> 

### <a name="setting-up-hello-frontend-environment"></a><span data-ttu-id="0383f-163">Configurando o ambiente de front-end Olá</span><span class="sxs-lookup"><span data-stu-id="0383f-163">Setting up hello frontend environment</span></span>

<span data-ttu-id="0383f-164">Repita as etapas de saudação muito[criar um aplicativo de função](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate um novo aplicativo de função na qual você irá criar o proxy.</span><span class="sxs-lookup"><span data-stu-id="0383f-164">Repeat hello steps too[Create a function app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate a new function app in which you will create your proxy.</span></span> <span data-ttu-id="0383f-165">Esse novo aplicativo servirá como front-end Olá para nossa API e Olá função aplicativo que você estava editando anteriormente servirá como um back-end.</span><span class="sxs-lookup"><span data-stu-id="0383f-165">This new app will serve as hello frontend for our API, and hello function app you were previously editing will serve as a backend.</span></span>

<span data-ttu-id="0383f-166">Navegue tooyour novo aplicativo de front-end função no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="0383f-166">Navigate tooyour new frontend function app in hello portal.</span></span>

<span data-ttu-id="0383f-167">Escolha a opção **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="0383f-167">Select **Settings**.</span></span> <span data-ttu-id="0383f-168">Em seguida, alternar **habilitar Proxies de funções do Azure (visualização)** muito "On".</span><span class="sxs-lookup"><span data-stu-id="0383f-168">Then toggle **Enable Azure Functions Proxies (preview)** too"On".</span></span>

<span data-ttu-id="0383f-169">Selecione **Configurações de Plataforma** e escolha **Configurações de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="0383f-169">Select **Platform Settings** and choose **Application Settings**.</span></span>

<span data-ttu-id="0383f-170">Role para baixo demais**configurações do aplicativo** e criar uma nova configuração com a chave "HELLO_HOST".</span><span class="sxs-lookup"><span data-stu-id="0383f-170">Scroll down too**App settings** and create a new setting with key "HELLO_HOST".</span></span> <span data-ttu-id="0383f-171">Definir seu host toohello de valor do seu aplicativo de função de back-end, tais como `<YourApp>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="0383f-171">Set its value toohello host of your backend function app, such as `<YourApp>.azurewebsites.net`.</span></span> <span data-ttu-id="0383f-172">Isso faz parte da URL de saudação que você copiou anteriormente ao testar sua função HTTP.</span><span class="sxs-lookup"><span data-stu-id="0383f-172">This is part of hello URL that you copied earlier when testing your HTTP function.</span></span> <span data-ttu-id="0383f-173">Você vai fazer referência a essa configuração na configuração de hello mais tarde.</span><span class="sxs-lookup"><span data-stu-id="0383f-173">You'll reference this setting in hello configuration later.</span></span>

> [!NOTE] 
> <span data-ttu-id="0383f-174">Configurações do aplicativo são recomendadas para tooprevent de configuração de host Olá uma dependência de ambiente embutida para proxy hello.</span><span class="sxs-lookup"><span data-stu-id="0383f-174">App settings are recommended for hello host configuration tooprevent a hard-coded environment dependency for hello proxy.</span></span> <span data-ttu-id="0383f-175">Usando as configurações de aplicativo significa que você pode mover a configuração de proxy de saudação entre ambientes e configurações de aplicativo específico do ambiente hello serão aplicadas.</span><span class="sxs-lookup"><span data-stu-id="0383f-175">Using app settings means that you can move hello proxy configuration between environments, and hello environment-specific app settings will be applied.</span></span>

<span data-ttu-id="0383f-176">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="0383f-176">Click **Save**.</span></span>

### <a name="creating-a-proxy-on-hello-frontend"></a><span data-ttu-id="0383f-177">Criando um proxy no front-end Olá</span><span class="sxs-lookup"><span data-stu-id="0383f-177">Creating a proxy on hello frontend</span></span>

<span data-ttu-id="0383f-178">Navegue de aplicativo de função de front-end tooyour Voltar no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="0383f-178">Navigate back tooyour frontend function app in hello portal.</span></span>

<span data-ttu-id="0383f-179">Na navegação do lado esquerdo hello, clique em Olá sinal de mais próximo '+' muito "Proxies (visualização)".</span><span class="sxs-lookup"><span data-stu-id="0383f-179">In hello left-hand navigation, click hello plus sign '+' next too"Proxies (preview)".</span></span>

![Criação de um proxy](./media/functions-create-serverless-api/creating-proxy.png)

<span data-ttu-id="0383f-181">Use as configurações de proxy conforme especificado na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="0383f-181">Use proxy settings as specified in hello table.</span></span>

| <span data-ttu-id="0383f-182">Campo</span><span class="sxs-lookup"><span data-stu-id="0383f-182">Field</span></span> | <span data-ttu-id="0383f-183">Valor de exemplo</span><span class="sxs-lookup"><span data-stu-id="0383f-183">Sample value</span></span> | <span data-ttu-id="0383f-184">Descrição</span><span class="sxs-lookup"><span data-stu-id="0383f-184">Description</span></span> |
|---|---|---|
| <span data-ttu-id="0383f-185">Nome</span><span class="sxs-lookup"><span data-stu-id="0383f-185">Name</span></span> | <span data-ttu-id="0383f-186">HelloProxy</span><span class="sxs-lookup"><span data-stu-id="0383f-186">HelloProxy</span></span> | <span data-ttu-id="0383f-187">Um nome amigável usado apenas para gerenciamento</span><span class="sxs-lookup"><span data-stu-id="0383f-187">A friendly name used only for management</span></span> |
| <span data-ttu-id="0383f-188">Modelo de rota</span><span class="sxs-lookup"><span data-stu-id="0383f-188">Route template</span></span> | <span data-ttu-id="0383f-189">/api/hello</span><span class="sxs-lookup"><span data-stu-id="0383f-189">/api/hello</span></span> | <span data-ttu-id="0383f-190">Determina quais rota é usada tooinvoke esse proxy</span><span class="sxs-lookup"><span data-stu-id="0383f-190">Determines what route is used tooinvoke this proxy</span></span> |
| <span data-ttu-id="0383f-191">URL do back-end</span><span class="sxs-lookup"><span data-stu-id="0383f-191">Backend URL</span></span> | <span data-ttu-id="0383f-192">https://%HELLO_HOST%/api/hello</span><span class="sxs-lookup"><span data-stu-id="0383f-192">https://%HELLO_HOST%/api/hello</span></span> | <span data-ttu-id="0383f-193">Especifica a solicitação de Olá Olá ponto de extremidade toowhich deve ser delegada</span><span class="sxs-lookup"><span data-stu-id="0383f-193">Specifies hello endpoint toowhich hello request should be proxied</span></span> |

<span data-ttu-id="0383f-194">Observe que os Proxies não fornecer Olá `/api` prefixo de caminho base e este deve ser incluído no modelo de rota hello.</span><span class="sxs-lookup"><span data-stu-id="0383f-194">Note that Proxies does not provide hello `/api` base path prefix, and this must be included in hello route template.</span></span>

<span data-ttu-id="0383f-195">Olá `%HELLO_HOST%` sintaxe fará referência a configuração do aplicativo hello criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0383f-195">hello `%HELLO_HOST%` syntax will reference hello app setting you created earlier.</span></span> <span data-ttu-id="0383f-196">Olá resolvido que URL de ponto de função original tooyour.</span><span class="sxs-lookup"><span data-stu-id="0383f-196">hello resolved URL will point tooyour original function.</span></span>

<span data-ttu-id="0383f-197">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="0383f-197">Click **Create**.</span></span>

<span data-ttu-id="0383f-198">Você pode testar seu novo proxy copiando Olá URL do Proxy e testá-lo no navegador de saudação ou com o cliente HTTP favorito.</span><span class="sxs-lookup"><span data-stu-id="0383f-198">You can try out your new proxy by copying hello Proxy URL and testing it in hello browser or with your favorite HTTP client.</span></span>

## <a name="create-a-mock-api"></a><span data-ttu-id="0383f-199">Criar uma API de simulação</span><span class="sxs-lookup"><span data-stu-id="0383f-199">Create a mock API</span></span>

<span data-ttu-id="0383f-200">Em seguida, você usará um proxy toocreate uma API de simulação para sua solução.</span><span class="sxs-lookup"><span data-stu-id="0383f-200">Next, you will use a proxy toocreate a mock API for your solution.</span></span> <span data-ttu-id="0383f-201">Isso permite o desenvolvimento de cliente tooprogress, sem a necessidade de back-end de saudação totalmente implementado.</span><span class="sxs-lookup"><span data-stu-id="0383f-201">This allows client development tooprogress, without needing hello backend fully implemented.</span></span> <span data-ttu-id="0383f-202">Mais tarde no desenvolvimento, você pode criar um novo aplicativo de função que dá suporte a essa lógica e redirecionar seu tooit de proxy.</span><span class="sxs-lookup"><span data-stu-id="0383f-202">Later in development, you could create a new function app which supports this logic and redirect your proxy tooit.</span></span>

<span data-ttu-id="0383f-203">toocreate isso simular API, vamos criar um novo proxy, desta vez usando Olá [Editor de aplicativo de serviço](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span><span class="sxs-lookup"><span data-stu-id="0383f-203">toocreate this mock API, we will create a new proxy, this time using hello [App Service Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span></span> <span data-ttu-id="0383f-204">tooget iniciado, navegue tooyour função aplicativo no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="0383f-204">tooget started, navigate tooyour function app in hello portal.</span></span> <span data-ttu-id="0383f-205">Selecione **Recursos da plataforma** e localize o **Editor do Serviço de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="0383f-205">Select **Platform features** and find **App Service Editor**.</span></span> <span data-ttu-id="0383f-206">Isso permite abrir Olá Editor de aplicativo de serviço em uma nova guia.</span><span class="sxs-lookup"><span data-stu-id="0383f-206">Clicking this will open hello App Service Editor in a new tab.</span></span>

<span data-ttu-id="0383f-207">Selecione `proxies.json` na barra de navegação esquerda de saudação.</span><span class="sxs-lookup"><span data-stu-id="0383f-207">Select `proxies.json` in hello left navigation.</span></span> <span data-ttu-id="0383f-208">Este é o arquivo de saudação que armazena a configuração de Olá para todos os proxies.</span><span class="sxs-lookup"><span data-stu-id="0383f-208">This is hello file which stores hello configuration for all of your proxies.</span></span> <span data-ttu-id="0383f-209">Se você usar uma saudação [métodos de implantação de funções](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), este é o arquivo hello serão mantidas no controle de origem.</span><span class="sxs-lookup"><span data-stu-id="0383f-209">If you use one of hello [Functions deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), this is hello file you will maintain in source control.</span></span> <span data-ttu-id="0383f-210">toolearn mais sobre esse arquivo, consulte [configuração avançada de Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span><span class="sxs-lookup"><span data-stu-id="0383f-210">toolearn more about this file, see [Proxies advanced configuration](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span></span>

<span data-ttu-id="0383f-211">Se você acompanhou até aqui até agora, seu proxies.json deve ter a aparência Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="0383f-211">If you've followed along so far, your proxies.json should look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        }
    }
}
```

<span data-ttu-id="0383f-212">Em seguida, você adicionará sua API de simulação.</span><span class="sxs-lookup"><span data-stu-id="0383f-212">Next you'll add your mock API.</span></span> <span data-ttu-id="0383f-213">Substitua o arquivo proxies.json com os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="0383f-213">Replace your proxies.json file with hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        },
        "GetUserByName" : {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/users/{username}"
            },
            "responseOverrides": {
                "response.statusCode": "200",
                "response.headers.Content-Type" : "application/json",
                "response.body": {
                    "name": "{username}",
                    "description": "Awesome developer and master of serverless APIs",
                    "skills": [
                        "Serverless",
                        "APIs",
                        "Azure",
                        "Cloud"
                    ]
                }
            }
        }
    }
}
```

<span data-ttu-id="0383f-214">Isso adiciona um novo proxy de, "GetUserByName", sem a propriedade de backendUri hello.</span><span class="sxs-lookup"><span data-stu-id="0383f-214">This adds a new proxy, "GetUserByName", without hello backendUri property.</span></span> <span data-ttu-id="0383f-215">Em vez de chamar outro recurso, ele modifica a resposta de padrão de saudação do Proxies usando uma substituição de resposta.</span><span class="sxs-lookup"><span data-stu-id="0383f-215">Instead of calling another resource, it modifies hello default response from Proxies using a response override.</span></span> <span data-ttu-id="0383f-216">Substituições de solicitação e resposta também podem ser usadas em conjunto com uma URL de back-end.</span><span class="sxs-lookup"><span data-stu-id="0383f-216">Request and response overrides can also be used in conjunction with a backend URL.</span></span> <span data-ttu-id="0383f-217">Isso é particularmente útil quando o proxy tooa sistema herdado, em que talvez seja necessário toomodify cabeçalhos, parâmetros de consulta, etc. toolearn mais informações sobre substituições de solicitação e resposta, consulte [modificando solicitações e respostas no Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span><span class="sxs-lookup"><span data-stu-id="0383f-217">This is particularly useful when proxying tooa legacy system, where you might need toomodify headers, query parameters, etc. toolearn more about request and response overrides, see [Modifying requests and responses in Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span></span>

<span data-ttu-id="0383f-218">Testar sua API fictícia chamada hello `/api/users/{username}` ponto de extremidade usando um navegador ou o cliente REST favorito.</span><span class="sxs-lookup"><span data-stu-id="0383f-218">Test your mock API by calling hello `/api/users/{username}` endpoint using a browser or your favorite REST client.</span></span> <span data-ttu-id="0383f-219">Ser tooreplace se _{username}_ com um valor de cadeia de caracteres que representa um nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="0383f-219">Be sure tooreplace _{username}_ with a string value representing a username.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0383f-220">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0383f-220">Next steps</span></span>

<span data-ttu-id="0383f-221">Neste tutorial, você aprendeu como toobuild e personalizar uma API em funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="0383f-221">In this tutorial, you learned how toobuild and customize an API on Azure Functions.</span></span> <span data-ttu-id="0383f-222">Você também aprendeu como toobring várias APIs, incluindo mocks, juntos como uma superfície de API unificada.</span><span class="sxs-lookup"><span data-stu-id="0383f-222">You also learned how toobring multiple APIs, including mocks, together as a unified API surface.</span></span> <span data-ttu-id="0383f-223">Você pode usar esses toobuild técnicas out APIs de qualquer complexidade, todos os durante a execução em Olá serverless computação modelo fornecido pelas funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="0383f-223">You can use these techniques toobuild out APIs of any complexity, all while running on hello serverless compute model provided by Azure Functions.</span></span>

<span data-ttu-id="0383f-224">Olá referências a seguir podem ser úteis à medida que desenvolve sua API adicional:</span><span class="sxs-lookup"><span data-stu-id="0383f-224">hello following references may be helpful as you develop your API further:</span></span>

- [<span data-ttu-id="0383f-225">Associações HTTP e de webhook do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="0383f-225">Azure Functions HTTP and webhook bindings</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- <span data-ttu-id="0383f-226">[trabalhando com Proxies de funções do Azure (visualização)]</span><span class="sxs-lookup"><span data-stu-id="0383f-226">[Working with Azure Functions Proxies (preview)]</span></span>
- [<span data-ttu-id="0383f-227">Documentar uma API do Azure Functions (visualização)</span><span class="sxs-lookup"><span data-stu-id="0383f-227">Documenting an Azure Functions API (preview)</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[trabalhando com Proxies de funções do Azure (visualização)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
