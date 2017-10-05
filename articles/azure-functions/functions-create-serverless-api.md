---
title: Criar uma API sem servidor usando o Azure Functions| Microsoft Docs
description: Como criar uma API sem servidor usando o Azure Functions
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
ms.openlocfilehash: 28056a385b058f7daeca2253ccb304116b49eba0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a><span data-ttu-id="f5c46-103">Criar uma API sem servidor usando o Azure Functions</span><span class="sxs-lookup"><span data-stu-id="f5c46-103">Create a serverless API using Azure Functions</span></span>

<span data-ttu-id="f5c46-104">Neste tutorial, você aprenderá como o Azure Functions permite que você crie APIs altamente escalonáveis.</span><span class="sxs-lookup"><span data-stu-id="f5c46-104">In this tutorial you will learn how Azure Functions allows you to build highly-scalable APIs.</span></span> <span data-ttu-id="f5c46-105">O Azure Functions vem com uma coleção interna de gatilhos e associações HTTP que facilitam a criação de um ponto de extremidade em várias linguagens, incluindo Node.JS, C# e muito mais.</span><span class="sxs-lookup"><span data-stu-id="f5c46-105">Azure Functions comes with a collection of built-in HTTP triggers and bindings which make it easy to author an endpoint in a variety of languages, including Node.JS, C#, and more.</span></span> <span data-ttu-id="f5c46-106">Neste tutorial, você personalizará um gatilho HTTP para lidar com ações específicas em seu projeto de API.</span><span class="sxs-lookup"><span data-stu-id="f5c46-106">In this tutorial, you will customize an HTTP trigger to handle specific actions in your API design.</span></span> <span data-ttu-id="f5c46-107">Você também preparará a expansão de sua API integrando-a aos Proxies do Azure Functions e configurando APIs de simulação.</span><span class="sxs-lookup"><span data-stu-id="f5c46-107">You will also prepare for growing your API by integrating it with Azure Functions Proxies and setting up mock APIs.</span></span> <span data-ttu-id="f5c46-108">Tudo isso é realizado no ambiente de computação sem servidor do Functions, portanto você não precisa se preocupar com o dimensionamento de recursos, você pode se concentrar apenas na lógica de sua API.</span><span class="sxs-lookup"><span data-stu-id="f5c46-108">All of this is accomplished on top of the Functions serverless compute environment, so you don't have to worry about scaling resources - you can just focus on your API logic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5c46-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f5c46-109">Prerequisites</span></span> 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

<span data-ttu-id="f5c46-110">A função resultante será ser usada no restante deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="f5c46-110">The resulting function will be used for the rest of this tutorial.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="f5c46-111">Entrar no Azure</span><span class="sxs-lookup"><span data-stu-id="f5c46-111">Sign in to Azure</span></span>

<span data-ttu-id="f5c46-112">Abra o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f5c46-112">Open the Azure portal.</span></span> <span data-ttu-id="f5c46-113">Para fazer isso, entre em [https://portal.azure.com](https://portal.azure.com) usando sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="f5c46-113">To do this, sign in to [https://portal.azure.com](https://portal.azure.com) with your Azure account.</span></span>

## <a name="customize-your-http-function"></a><span data-ttu-id="f5c46-114">Personalizar sua função HTTP</span><span class="sxs-lookup"><span data-stu-id="f5c46-114">Customize your HTTP function</span></span>

<span data-ttu-id="f5c46-115">Por padrão, sua função disparada por HTTP é configurada para aceitar qualquer método HTTP.</span><span class="sxs-lookup"><span data-stu-id="f5c46-115">By default, your HTTP-triggered function is configured to accept any HTTP method.</span></span> <span data-ttu-id="f5c46-116">Também há uma URL padrão no formato `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span><span class="sxs-lookup"><span data-stu-id="f5c46-116">There is also a default URL of the form `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span></span> <span data-ttu-id="f5c46-117">Se você seguiu o guia de início rápido, `<funcname>` provavelmente se parece com algo como "HttpTriggerJS1".</span><span class="sxs-lookup"><span data-stu-id="f5c46-117">If you followed the quickstart, then `<funcname>` probably looks something like "HttpTriggerJS1".</span></span> <span data-ttu-id="f5c46-118">Nesta seção, você modificará a função para responder apenas a solicitações GET na rota `/api/hello`.</span><span class="sxs-lookup"><span data-stu-id="f5c46-118">In this section, you will modify the function to respond only to GET requests against `/api/hello` route instead.</span></span> 

<span data-ttu-id="f5c46-119">Navegue até sua função no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f5c46-119">Navigate to your function in the Azure portal.</span></span> <span data-ttu-id="f5c46-120">Selecione **Integrar** no painel de navegação esquerdo.</span><span class="sxs-lookup"><span data-stu-id="f5c46-120">Select **Integrate** in the left navigation.</span></span>

![Personalizar uma função HTTP](./media/functions-create-serverless-api/customizing-http.png)

<span data-ttu-id="f5c46-122">Use as configurações do gatilho HTTP conforme especificado na tabela.</span><span class="sxs-lookup"><span data-stu-id="f5c46-122">Use the HTTP trigger settings as specified in the table.</span></span>

| <span data-ttu-id="f5c46-123">Campo</span><span class="sxs-lookup"><span data-stu-id="f5c46-123">Field</span></span> | <span data-ttu-id="f5c46-124">Valor de exemplo</span><span class="sxs-lookup"><span data-stu-id="f5c46-124">Sample value</span></span> | <span data-ttu-id="f5c46-125">Descrição</span><span class="sxs-lookup"><span data-stu-id="f5c46-125">Description</span></span> |
|---|---|---|
| <span data-ttu-id="f5c46-126">Métodos HTTP selecionados</span><span class="sxs-lookup"><span data-stu-id="f5c46-126">Allowed HTTP methods</span></span> | <span data-ttu-id="f5c46-127">Métodos selecionados</span><span class="sxs-lookup"><span data-stu-id="f5c46-127">Selected methods</span></span> | <span data-ttu-id="f5c46-128">Determina quais métodos HTTP podem ser usados para chamar essa função</span><span class="sxs-lookup"><span data-stu-id="f5c46-128">Determines what HTTP methods may be used to invoke this function</span></span> |
| <span data-ttu-id="f5c46-129">Métodos HTTP selecionados</span><span class="sxs-lookup"><span data-stu-id="f5c46-129">Selected HTTP methods</span></span> | <span data-ttu-id="f5c46-130">GET</span><span class="sxs-lookup"><span data-stu-id="f5c46-130">GET</span></span> | <span data-ttu-id="f5c46-131">Permite que apenas os métodos HTTP selecionados possam ser usados para chamar essa função</span><span class="sxs-lookup"><span data-stu-id="f5c46-131">Allows only selected HTTP methods to be used to invoke this function</span></span> |
| <span data-ttu-id="f5c46-132">Modelo de rota</span><span class="sxs-lookup"><span data-stu-id="f5c46-132">Route template</span></span> | <span data-ttu-id="f5c46-133">/hello</span><span class="sxs-lookup"><span data-stu-id="f5c46-133">/hello</span></span> | <span data-ttu-id="f5c46-134">Determina qual rota pode ser usada para chamar essa função</span><span class="sxs-lookup"><span data-stu-id="f5c46-134">Determines what route is used to invoke this function</span></span> |

<span data-ttu-id="f5c46-135">Observe que você não incluiu o prefixo de caminho base `/api` no modelo de rota, pois isso é tratado por uma configuração global.</span><span class="sxs-lookup"><span data-stu-id="f5c46-135">Note that you did not include the `/api` base path prefix in the route template, as this is handled by a global setting.</span></span>

<span data-ttu-id="f5c46-136">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f5c46-136">Click **Save**.</span></span>

<span data-ttu-id="f5c46-137">Você pode aprender mais sobre a personalização de funções HTTP em [Associações HTTP e webhook do Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span><span class="sxs-lookup"><span data-stu-id="f5c46-137">You can learn more about customizing HTTP functions in [Azure Functions HTTP and webhook bindings](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span></span>

### <a name="test-your-api"></a><span data-ttu-id="f5c46-138">Testar sua API</span><span class="sxs-lookup"><span data-stu-id="f5c46-138">Test your API</span></span>

<span data-ttu-id="f5c46-139">Em seguida, teste sua função para vê-la funcionando com a nova superfície de API.</span><span class="sxs-lookup"><span data-stu-id="f5c46-139">Next, test your function to see it working with the new API surface.</span></span>

<span data-ttu-id="f5c46-140">Navegue de volta para a página de desenvolvimento clicando no nome da função no painel de navegação esquerdo.</span><span class="sxs-lookup"><span data-stu-id="f5c46-140">Navigate back to the development page by clicking on the function's name in the left navigation.</span></span>

<span data-ttu-id="f5c46-141">Clique em **Obter URL de função** e copie a URL.</span><span class="sxs-lookup"><span data-stu-id="f5c46-141">Click **Get function URL** and copy the URL.</span></span> <span data-ttu-id="f5c46-142">Você verá que agora ela usa a rota `/api/hello`.</span><span class="sxs-lookup"><span data-stu-id="f5c46-142">You should see that it uses the `/api/hello` route now.</span></span>

<span data-ttu-id="f5c46-143">Copie a URL em uma nova guia do navegador ou o cliente REST preferencial.</span><span class="sxs-lookup"><span data-stu-id="f5c46-143">Copy the URL into a new browser tab or your preferred REST client.</span></span> <span data-ttu-id="f5c46-144">Navegadores usarão GET por padrão.</span><span class="sxs-lookup"><span data-stu-id="f5c46-144">Browsers will use GET by default.</span></span>

<span data-ttu-id="f5c46-145">Execute a função e confirme se ela está funcionando.</span><span class="sxs-lookup"><span data-stu-id="f5c46-145">Run the function and confirm that it is working.</span></span> <span data-ttu-id="f5c46-146">Talvez seja necessário fornecer o parâmetro "name" como uma cadeia de caracteres de consulta para atender ao código de início rápido.</span><span class="sxs-lookup"><span data-stu-id="f5c46-146">You may need to provide the "name" parameter as a query string to satisfy the quickstart code.</span></span>

<span data-ttu-id="f5c46-147">Você também pode tentar chamar o ponto de extremidade com outro método HTTP para confirmar a não execução da função.</span><span class="sxs-lookup"><span data-stu-id="f5c46-147">You can also try calling the endpoint with another HTTP method to confirm that the function is not executed.</span></span> <span data-ttu-id="f5c46-148">Para isso, será necessário usar um cliente REST, como cURL, Postman ou Fiddler.</span><span class="sxs-lookup"><span data-stu-id="f5c46-148">For this, you will need to use a REST client, such as cURL, Postman, or Fiddler.</span></span>

## <a name="proxies-overview"></a><span data-ttu-id="f5c46-149">Visão geral dos proxies</span><span class="sxs-lookup"><span data-stu-id="f5c46-149">Proxies overview</span></span>

<span data-ttu-id="f5c46-150">Na próxima seção, você mostrará sua API através de um proxy.</span><span class="sxs-lookup"><span data-stu-id="f5c46-150">In the next section, you will surface your API through a proxy.</span></span> <span data-ttu-id="f5c46-151">Os Proxies do Azure Functions são um recurso de visualização que permite o encaminhamento de solicitações para outros recursos.</span><span class="sxs-lookup"><span data-stu-id="f5c46-151">Azure Functions Proxies is a preview feature that allows you to forward requests to other resources.</span></span> <span data-ttu-id="f5c46-152">Defina um ponto de extremidade HTTP, como com o gatilho HTTP, mas em vez de escrever um código para executar durante a chamada para o ponto de extremidade, forneça uma URL para uma implementação remota.</span><span class="sxs-lookup"><span data-stu-id="f5c46-152">You define an HTTP endpoint just like with HTTP trigger, but instead of writing code to execute when that endpoint is called, you provide a URL to a remote implementation.</span></span> <span data-ttu-id="f5c46-153">Isso permite a composição de várias fontes de API em uma única superfície de API, o que é fácil para os clientes usarem.</span><span class="sxs-lookup"><span data-stu-id="f5c46-153">This allows you to compose multiple API sources into a single API surface which is easy for clients to consume.</span></span> <span data-ttu-id="f5c46-154">Isso é particularmente útil se você quiser criar sua API como microsserviços.</span><span class="sxs-lookup"><span data-stu-id="f5c46-154">This is particularly useful if you wish to build your API as microservices.</span></span>

<span data-ttu-id="f5c46-155">Um proxy pode apontar para qualquer recurso HTTP, como:</span><span class="sxs-lookup"><span data-stu-id="f5c46-155">A proxy can point to any HTTP resource, such as:</span></span>
- <span data-ttu-id="f5c46-156">Funções do Azure</span><span class="sxs-lookup"><span data-stu-id="f5c46-156">Azure Functions</span></span> 
- <span data-ttu-id="f5c46-157">Aplicativos de API no [Serviço de Aplicativo do Azure](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span><span class="sxs-lookup"><span data-stu-id="f5c46-157">API apps in [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span></span>
- <span data-ttu-id="f5c46-158">Contêineres de docker no [Serviço de Aplicativo no Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span><span class="sxs-lookup"><span data-stu-id="f5c46-158">Docker containers in [App Service on Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span></span>
- <span data-ttu-id="f5c46-159">Qualquer outra API hospedada</span><span class="sxs-lookup"><span data-stu-id="f5c46-159">Any other hosted API</span></span>

<span data-ttu-id="f5c46-160">Para saber mais sobre proxies, confira [Trabalhar com Proxies do Azure Functions (visualização)].</span><span class="sxs-lookup"><span data-stu-id="f5c46-160">To learn more about proxies, see [Working with Azure Functions Proxies (preview)].</span></span>

## <a name="create-your-first-proxy"></a><span data-ttu-id="f5c46-161">Criar seu primeiro proxy</span><span class="sxs-lookup"><span data-stu-id="f5c46-161">Create your first proxy</span></span>

<span data-ttu-id="f5c46-162">Nesta seção, você criará um novo proxy que servirá como um front-end para sua API geral.</span><span class="sxs-lookup"><span data-stu-id="f5c46-162">In this section, you will create a new proxy which serves as a frontend to your overall API.</span></span> 

### <a name="setting-up-the-frontend-environment"></a><span data-ttu-id="f5c46-163">Configurar o ambiente front-end</span><span class="sxs-lookup"><span data-stu-id="f5c46-163">Setting up the frontend environment</span></span>

<span data-ttu-id="f5c46-164">Repita as etapas para [Criar um aplicativo de função](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) a fim de criar um novo aplicativo de função no qual você criará o proxy.</span><span class="sxs-lookup"><span data-stu-id="f5c46-164">Repeat the steps to [Create a function app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) to create a new function app in which you will create your proxy.</span></span> <span data-ttu-id="f5c46-165">Esse novo aplicativo servirá como o front-end de nossa API, e o aplicativo de função que você estava editando anteriormente servirá como um back-end.</span><span class="sxs-lookup"><span data-stu-id="f5c46-165">This new app will serve as the frontend for our API, and the function app you were previously editing will serve as a backend.</span></span>

<span data-ttu-id="f5c46-166">Navegue até seu novo aplicativo de função front-end no portal.</span><span class="sxs-lookup"><span data-stu-id="f5c46-166">Navigate to your new frontend function app in the portal.</span></span>

<span data-ttu-id="f5c46-167">Escolha a opção **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="f5c46-167">Select **Settings**.</span></span> <span data-ttu-id="f5c46-168">Depois, alterne **Habilitar Proxies do Azure Functions (visualização)** para "Ativado".</span><span class="sxs-lookup"><span data-stu-id="f5c46-168">Then toggle **Enable Azure Functions Proxies (preview)** to "On".</span></span>

<span data-ttu-id="f5c46-169">Selecione **Configurações de Plataforma** e escolha **Configurações de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="f5c46-169">Select **Platform Settings** and choose **Application Settings**.</span></span>

<span data-ttu-id="f5c46-170">Role para baixo até **Configurações do aplicativo** e crie uma nova configuração com a chave "HELLO_HOST".</span><span class="sxs-lookup"><span data-stu-id="f5c46-170">Scroll down to **App settings** and create a new setting with key "HELLO_HOST".</span></span> <span data-ttu-id="f5c46-171">Defina o valor dela como o host de seu aplicativo de função de back-end, como `<YourApp>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="f5c46-171">Set its value to the host of your backend function app, such as `<YourApp>.azurewebsites.net`.</span></span> <span data-ttu-id="f5c46-172">Isso faz parte da URL que você copiou anteriormente ao testar sua função HTTP.</span><span class="sxs-lookup"><span data-stu-id="f5c46-172">This is part of the URL that you copied earlier when testing your HTTP function.</span></span> <span data-ttu-id="f5c46-173">Você fará referência a essa configuração mais adiante na configuração.</span><span class="sxs-lookup"><span data-stu-id="f5c46-173">You'll reference this setting in the configuration later.</span></span>

> [!NOTE] 
> <span data-ttu-id="f5c46-174">As configurações do aplicativo são recomendadas para a configuração do host a fim de evitar uma dependência do ambiente embutida no código para o proxy.</span><span class="sxs-lookup"><span data-stu-id="f5c46-174">App settings are recommended for the host configuration to prevent a hard-coded environment dependency for the proxy.</span></span> <span data-ttu-id="f5c46-175">Usar configurações do aplicativo significa que você pode mover a configuração do proxy entre ambientes, e as configurações de aplicativo específicas ao ambiente serão aplicadas.</span><span class="sxs-lookup"><span data-stu-id="f5c46-175">Using app settings means that you can move the proxy configuration between environments, and the environment-specific app settings will be applied.</span></span>

<span data-ttu-id="f5c46-176">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f5c46-176">Click **Save**.</span></span>

### <a name="creating-a-proxy-on-the-frontend"></a><span data-ttu-id="f5c46-177">Criar um proxy no front-end</span><span class="sxs-lookup"><span data-stu-id="f5c46-177">Creating a proxy on the frontend</span></span>

<span data-ttu-id="f5c46-178">Navegue novamente até seu aplicativo de função front-end no portal.</span><span class="sxs-lookup"><span data-stu-id="f5c46-178">Navigate back to your frontend function app in the portal.</span></span>

<span data-ttu-id="f5c46-179">No painel de navegação esquerdo, clique no sinal '+' ao lado de "Proxies (visualização)".</span><span class="sxs-lookup"><span data-stu-id="f5c46-179">In the left-hand navigation, click the plus sign '+' next to "Proxies (preview)".</span></span>

![Criação de um proxy](./media/functions-create-serverless-api/creating-proxy.png)

<span data-ttu-id="f5c46-181">Use as configurações de proxy conforme especificado na tabela.</span><span class="sxs-lookup"><span data-stu-id="f5c46-181">Use proxy settings as specified in the table.</span></span>

| <span data-ttu-id="f5c46-182">Campo</span><span class="sxs-lookup"><span data-stu-id="f5c46-182">Field</span></span> | <span data-ttu-id="f5c46-183">Valor de exemplo</span><span class="sxs-lookup"><span data-stu-id="f5c46-183">Sample value</span></span> | <span data-ttu-id="f5c46-184">Descrição</span><span class="sxs-lookup"><span data-stu-id="f5c46-184">Description</span></span> |
|---|---|---|
| <span data-ttu-id="f5c46-185">Nome</span><span class="sxs-lookup"><span data-stu-id="f5c46-185">Name</span></span> | <span data-ttu-id="f5c46-186">HelloProxy</span><span class="sxs-lookup"><span data-stu-id="f5c46-186">HelloProxy</span></span> | <span data-ttu-id="f5c46-187">Um nome amigável usado apenas para gerenciamento</span><span class="sxs-lookup"><span data-stu-id="f5c46-187">A friendly name used only for management</span></span> |
| <span data-ttu-id="f5c46-188">Modelo de rota</span><span class="sxs-lookup"><span data-stu-id="f5c46-188">Route template</span></span> | <span data-ttu-id="f5c46-189">/api/hello</span><span class="sxs-lookup"><span data-stu-id="f5c46-189">/api/hello</span></span> | <span data-ttu-id="f5c46-190">Determina qual rota pode ser usada para chamar esse proxy</span><span class="sxs-lookup"><span data-stu-id="f5c46-190">Determines what route is used to invoke this proxy</span></span> |
| <span data-ttu-id="f5c46-191">URL do back-end</span><span class="sxs-lookup"><span data-stu-id="f5c46-191">Backend URL</span></span> | <span data-ttu-id="f5c46-192">https://%HELLO_HOST%/api/hello</span><span class="sxs-lookup"><span data-stu-id="f5c46-192">https://%HELLO_HOST%/api/hello</span></span> | <span data-ttu-id="f5c46-193">Especifica o ponto de extremidade ao qual a solicitação deve ser transmitida por proxy</span><span class="sxs-lookup"><span data-stu-id="f5c46-193">Specifies the endpoint to which the request should be proxied</span></span> |

<span data-ttu-id="f5c46-194">Observe que os Proxies não fornecem o prefixo de caminho base `/api`, e ele deve ser incluído no modelo de rota.</span><span class="sxs-lookup"><span data-stu-id="f5c46-194">Note that Proxies does not provide the `/api` base path prefix, and this must be included in the route template.</span></span>

<span data-ttu-id="f5c46-195">A sintaxe `%HELLO_HOST%` fará referência a configuração do aplicativo que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f5c46-195">The `%HELLO_HOST%` syntax will reference the app setting you created earlier.</span></span> <span data-ttu-id="f5c46-196">A URL resolvida apontará para sua função original.</span><span class="sxs-lookup"><span data-stu-id="f5c46-196">The resolved URL will point to your original function.</span></span>

<span data-ttu-id="f5c46-197">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f5c46-197">Click **Create**.</span></span>

<span data-ttu-id="f5c46-198">Você pode testar seu novo proxy copiando a URL do Proxy e o testando no navegador ou com seu cliente HTTP favorito.</span><span class="sxs-lookup"><span data-stu-id="f5c46-198">You can try out your new proxy by copying the Proxy URL and testing it in the browser or with your favorite HTTP client.</span></span>

## <a name="create-a-mock-api"></a><span data-ttu-id="f5c46-199">Criar uma API de simulação</span><span class="sxs-lookup"><span data-stu-id="f5c46-199">Create a mock API</span></span>

<span data-ttu-id="f5c46-200">Em seguida, você usará um proxy para criar uma API de simulação para sua solução.</span><span class="sxs-lookup"><span data-stu-id="f5c46-200">Next, you will use a proxy to create a mock API for your solution.</span></span> <span data-ttu-id="f5c46-201">Isso permite o progresso do desenvolvimento do cliente, sem a necessidade de implementar totalmente o back-end.</span><span class="sxs-lookup"><span data-stu-id="f5c46-201">This allows client development to progress, without needing the backend fully implemented.</span></span> <span data-ttu-id="f5c46-202">Posteriormente no desenvolvimento, você poderá criar um novo aplicativo de função que oferece suporte a essa lógica e redirecionar seu proxy até ele.</span><span class="sxs-lookup"><span data-stu-id="f5c46-202">Later in development, you could create a new function app which supports this logic and redirect your proxy to it.</span></span>

<span data-ttu-id="f5c46-203">Para criar essa API de simulação, criaremos um novo proxy, dessa vez usando o [Editor do Serviço de Aplicativo](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span><span class="sxs-lookup"><span data-stu-id="f5c46-203">To create this mock API, we will create a new proxy, this time using the [App Service Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span></span> <span data-ttu-id="f5c46-204">Para começar, navegue até seu aplicativo de função no portal.</span><span class="sxs-lookup"><span data-stu-id="f5c46-204">To get started, navigate to your function app in the portal.</span></span> <span data-ttu-id="f5c46-205">Selecione **Recursos da plataforma** e localize o **Editor do Serviço de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="f5c46-205">Select **Platform features** and find **App Service Editor**.</span></span> <span data-ttu-id="f5c46-206">Clique nele para abrir o Editor de Serviço de Aplicativo em uma nova guia.</span><span class="sxs-lookup"><span data-stu-id="f5c46-206">Clicking this will open the App Service Editor in a new tab.</span></span>

<span data-ttu-id="f5c46-207">Selecione `proxies.json` no painel de navegação esquerdo.</span><span class="sxs-lookup"><span data-stu-id="f5c46-207">Select `proxies.json` in the left navigation.</span></span> <span data-ttu-id="f5c46-208">Este é o arquivo que armazena a configuração de todos os seus proxies.</span><span class="sxs-lookup"><span data-stu-id="f5c46-208">This is the file which stores the configuration for all of your proxies.</span></span> <span data-ttu-id="f5c46-209">Se você usar um dos [métodos de implantação do Functions](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), esse será o arquivo mantido no controle de origem.</span><span class="sxs-lookup"><span data-stu-id="f5c46-209">If you use one of the [Functions deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), this is the file you will maintain in source control.</span></span> <span data-ttu-id="f5c46-210">Para saber mais sobre esse arquivo, confira [Configuração avançada de proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span><span class="sxs-lookup"><span data-stu-id="f5c46-210">To learn more about this file, see [Proxies advanced configuration](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span></span>

<span data-ttu-id="f5c46-211">Se você acompanhou até agora, o proxies.json deve ser semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="f5c46-211">If you've followed along so far, your proxies.json should look like the following:</span></span>

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

<span data-ttu-id="f5c46-212">Em seguida, você adicionará sua API de simulação.</span><span class="sxs-lookup"><span data-stu-id="f5c46-212">Next you'll add your mock API.</span></span> <span data-ttu-id="f5c46-213">Substitua o arquivo proxies.json pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="f5c46-213">Replace your proxies.json file with the following:</span></span>

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

<span data-ttu-id="f5c46-214">Isso adiciona um novo proxy "GetUserByName", sem a propriedade backendUri.</span><span class="sxs-lookup"><span data-stu-id="f5c46-214">This adds a new proxy, "GetUserByName", without the backendUri property.</span></span> <span data-ttu-id="f5c46-215">Em vez de chamar outro recurso, ele modifica a resposta padrão dos Proxies usando uma substituição de resposta.</span><span class="sxs-lookup"><span data-stu-id="f5c46-215">Instead of calling another resource, it modifies the default response from Proxies using a response override.</span></span> <span data-ttu-id="f5c46-216">Substituições de solicitação e resposta também podem ser usadas em conjunto com uma URL de back-end.</span><span class="sxs-lookup"><span data-stu-id="f5c46-216">Request and response overrides can also be used in conjunction with a backend URL.</span></span> <span data-ttu-id="f5c46-217">Isso é particularmente útil ao transmitir por proxy para um sistema herdado, quando talvez você precise modificar cabeçalhos, consultar parâmetros etc. Para saber mais sobre as substituições de solicitação e resposta, Confira [Modificar solicitações e respostas em Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span><span class="sxs-lookup"><span data-stu-id="f5c46-217">This is particularly useful when proxying to a legacy system, where you might need to modify headers, query parameters, etc. To learn more about request and response overrides, see [Modifying requests and responses in Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span></span>

<span data-ttu-id="f5c46-218">Teste sua API de simulação chamando o ponto de extremidade `/api/users/{username}` usando um navegador ou seu cliente REST favorito.</span><span class="sxs-lookup"><span data-stu-id="f5c46-218">Test your mock API by calling the `/api/users/{username}` endpoint using a browser or your favorite REST client.</span></span> <span data-ttu-id="f5c46-219">Não deixe de substituir _{username}_ por um valor de cadeia de caracteres que represente um nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="f5c46-219">Be sure to replace _{username}_ with a string value representing a username.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5c46-220">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f5c46-220">Next steps</span></span>

<span data-ttu-id="f5c46-221">Neste tutorial, você aprendeu a compilar e personalizar uma API no Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="f5c46-221">In this tutorial, you learned how to build and customize an API on Azure Functions.</span></span> <span data-ttu-id="f5c46-222">Você também aprendeu a unir várias APIs, incluindo objetos fictícios, como uma superfície de API unificada.</span><span class="sxs-lookup"><span data-stu-id="f5c46-222">You also learned how to bring multiple APIs, including mocks, together as a unified API surface.</span></span> <span data-ttu-id="f5c46-223">Use essas técnicas para compilar APIs de qualquer complexidade durante a execução no modelo de computação sem servidor fornecido pelo Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="f5c46-223">You can use these techniques to build out APIs of any complexity, all while running on the serverless compute model provided by Azure Functions.</span></span>

<span data-ttu-id="f5c46-224">As referências a seguir podem ser úteis durante o desenvolvimento de sua API:</span><span class="sxs-lookup"><span data-stu-id="f5c46-224">The following references may be helpful as you develop your API further:</span></span>

- [<span data-ttu-id="f5c46-225">Associações HTTP e de webhook do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="f5c46-225">Azure Functions HTTP and webhook bindings</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- <span data-ttu-id="f5c46-226">[Trabalhar com Proxies do Azure Functions (visualização)]</span><span class="sxs-lookup"><span data-stu-id="f5c46-226">[Working with Azure Functions Proxies (preview)]</span></span>
- [<span data-ttu-id="f5c46-227">Documentar uma API do Azure Functions (visualização)</span><span class="sxs-lookup"><span data-stu-id="f5c46-227">Documenting an Azure Functions API (preview)</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[Trabalhar com Proxies do Azure Functions (visualização)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
