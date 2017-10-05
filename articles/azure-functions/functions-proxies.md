---
title: Trabalhar com proxies no Azure Functions | Microsoft Docs
description: "Visão geral de como usar Proxies do Azure Functions"
services: functions
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/11/2017
ms.author: mahender
ms.openlocfilehash: 102e54627a8fee721d3ed85e86a8009e706bb5b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a><span data-ttu-id="3520f-103">Trabalhar com proxies do Azure Functions (visualização)</span><span class="sxs-lookup"><span data-stu-id="3520f-103">Work with Azure Functions Proxies (preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="3520f-104">Proxies do Azure Functions está atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="3520f-104">Azure Functions Proxies is currently in preview.</span></span> <span data-ttu-id="3520f-105">É gratuito enquanto na visualização, mas as funções padrão cobrança se aplica para execuções de proxy.</span><span class="sxs-lookup"><span data-stu-id="3520f-105">It is free while in preview, but standard Functions billing applies to proxy executions.</span></span> <span data-ttu-id="3520f-106">Para saber mais, confira [Preços do Azure Functions](https://azure.microsoft.com/pricing/details/functions/).</span><span class="sxs-lookup"><span data-stu-id="3520f-106">For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).</span></span>

<span data-ttu-id="3520f-107">Este artigo explica como configurar e trabalhar com proxies do Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="3520f-107">This article explains how to configure and work with Azure Functions Proxies.</span></span> <span data-ttu-id="3520f-108">Com esse recurso, você pode especificar os pontos de extremidade em seu aplicativo de funções que são implementados por outro recurso.</span><span class="sxs-lookup"><span data-stu-id="3520f-108">With this feature, you can specify endpoints on your function app that are implemented by another resource.</span></span> <span data-ttu-id="3520f-109">Você pode usar esses proxies para dividir uma API grande em vários aplicativos de função (como uma arquitetura de microsserviços), enquanto ainda apresenta uma única superfície de API para clientes.</span><span class="sxs-lookup"><span data-stu-id="3520f-109">You can use these proxies to break a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <span data-ttu-id="3520f-110"><a name="enable"></a>Habilitar proxies do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="3520f-110"><a name="enable"></a>Enable Azure Functions Proxies</span></span>

<span data-ttu-id="3520f-111">Os proxies não estão habilitados por padrão.</span><span class="sxs-lookup"><span data-stu-id="3520f-111">Proxies are not enabled by default.</span></span> <span data-ttu-id="3520f-112">Você pode criar proxies enquanto o recurso estiver desativado, mas não será executado.</span><span class="sxs-lookup"><span data-stu-id="3520f-112">You can create proxies while the feature is disabled, but they will not execute.</span></span> <span data-ttu-id="3520f-113">Para habilitar proxies, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="3520f-113">To enable proxies, do the following:</span></span>

1. <span data-ttu-id="3520f-114">Abra o [Portal do Azure] e navegue até seu aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="3520f-114">Open the [Azure portal], and then go to your function app.</span></span>
2. <span data-ttu-id="3520f-115">Selecione **Configurações do aplicativo de funções**.</span><span class="sxs-lookup"><span data-stu-id="3520f-115">Select **Function app settings**.</span></span>
3. <span data-ttu-id="3520f-116">Alterne **Habilitar Proxies do Azure Functions (visualização)** para **Ativado**.</span><span class="sxs-lookup"><span data-stu-id="3520f-116">Switch **Enable Azure Functions Proxies (preview)** to **On**.</span></span>

<span data-ttu-id="3520f-117">Você também pode retornar aqui para atualizar o tempo de execução do proxy medida que novos recursos forem disponibilizados.</span><span class="sxs-lookup"><span data-stu-id="3520f-117">You can also return here to update the proxy runtime as new features become available.</span></span>


## <span data-ttu-id="3520f-118"><a name="create"></a>Criar um proxy</span><span class="sxs-lookup"><span data-stu-id="3520f-118"><a name="create"></a>Create a proxy</span></span>

<span data-ttu-id="3520f-119">Esta seção mostra como criar um proxy no portal do Functions.</span><span class="sxs-lookup"><span data-stu-id="3520f-119">This section shows you how to create a proxy in the Functions portal.</span></span>

1. <span data-ttu-id="3520f-120">Abra o [Portal do Azure] e navegue até seu aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="3520f-120">Open the [Azure portal], and then go to your function app.</span></span>
2. <span data-ttu-id="3520f-121">No painel esquerdo, selecione **Novo proxy**.</span><span class="sxs-lookup"><span data-stu-id="3520f-121">In the left pane, select **New proxy**.</span></span>
3. <span data-ttu-id="3520f-122">Forneça um nome para seu proxy.</span><span class="sxs-lookup"><span data-stu-id="3520f-122">Provide a name for your proxy.</span></span>
4. <span data-ttu-id="3520f-123">Configurar o ponto de extremidade exposto no aplicativo de função especificando o **modelo de rota** e **Métodos HTTP**.</span><span class="sxs-lookup"><span data-stu-id="3520f-123">Configure the endpoint that's exposed on this function app by specifying the **route template** and **HTTP methods**.</span></span> <span data-ttu-id="3520f-124">Esses parâmetros se comportam de acordo com as regras de [gatilhos HTTP].</span><span class="sxs-lookup"><span data-stu-id="3520f-124">These parameters behave according to the rules for [HTTP triggers].</span></span>
5. <span data-ttu-id="3520f-125">Defina a **URL de back-end** para outro ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="3520f-125">Set the **backend URL** to another endpoint.</span></span> <span data-ttu-id="3520f-126">Esse ponto de extremidade pode ser uma função em outro aplicativo de funções, ou pode ser qualquer outra API.</span><span class="sxs-lookup"><span data-stu-id="3520f-126">This endpoint could be a function in another function app, or it could be any other API.</span></span> <span data-ttu-id="3520f-127">O valor não precisa ser estático e pode fazer referência as [configurações do aplicativo] e os [parâmetros da solicitação original do cliente].</span><span class="sxs-lookup"><span data-stu-id="3520f-127">The value does not need to be static, and it can reference [application settings] and [parameters from the original client request].</span></span>
6. <span data-ttu-id="3520f-128">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3520f-128">Click **Create**.</span></span>

<span data-ttu-id="3520f-129">Seu proxy agora existe como um novo ponto de extremidade em seu aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="3520f-129">Your proxy now exists as a new endpoint on your function app.</span></span> <span data-ttu-id="3520f-130">Da perspectiva do cliente, é equivalente a um HttpTrigger no Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="3520f-130">From a client perspective, it is equivalent to an HttpTrigger in Azure Functions.</span></span> <span data-ttu-id="3520f-131">Você pode testar seu novo proxy copiando a URL do Proxy e testá-lo com seu cliente HTTP favorito.</span><span class="sxs-lookup"><span data-stu-id="3520f-131">You can try out your new proxy by copying the Proxy URL and testing it with your favorite HTTP client.</span></span>

## <span data-ttu-id="3520f-132"><a name="modify-requests-responses"></a>Modificar solicitações e respostas</span><span class="sxs-lookup"><span data-stu-id="3520f-132"><a name="modify-requests-responses"></a>Modify requests and responses</span></span>

<span data-ttu-id="3520f-133">Com os proxies do Azure Functions, você pode modificar solicitações e respostas do back-end.</span><span class="sxs-lookup"><span data-stu-id="3520f-133">With Azure Functions Proxies, you can modify requests to and responses from the back end.</span></span> <span data-ttu-id="3520f-134">Essas transformações podem usar variáveis, conforme definido em [Usar variáveis].</span><span class="sxs-lookup"><span data-stu-id="3520f-134">These transformations can use variables as defined in [Use variables].</span></span>

### <span data-ttu-id="3520f-135"><a name="modify-backend-request"></a>Modificar a solicitação de back-end</span><span class="sxs-lookup"><span data-stu-id="3520f-135"><a name="modify-backend-request"></a>Modify the back-end request</span></span>

<span data-ttu-id="3520f-136">Por padrão, a solicitação de back-end é inicializada como uma cópia da solicitação original.</span><span class="sxs-lookup"><span data-stu-id="3520f-136">By default, the back-end request is initialized as a copy of the original request.</span></span> <span data-ttu-id="3520f-137">Além de definir a URL de back-end, é possível fazer alterações no método HTTP, cabeçalhos e parâmetros de cadeia de consulta.</span><span class="sxs-lookup"><span data-stu-id="3520f-137">In addition to setting the back-end URL, you can make changes to the HTTP method, headers, and query string parameters.</span></span> <span data-ttu-id="3520f-138">Os valores modificados podem referenciar as [configurações do aplicativo] e os [parâmetros da solicitação original do cliente].</span><span class="sxs-lookup"><span data-stu-id="3520f-138">The modified values can reference [application settings] and [parameters from the original client request].</span></span>

<span data-ttu-id="3520f-139">Atualmente, não há experiência no portal para modificar as solicitações de back-end.</span><span class="sxs-lookup"><span data-stu-id="3520f-139">Currently, there is no portal experience for modifying back-end requests.</span></span> <span data-ttu-id="3520f-140">Para saber como aplicar essa capacidade a partir de proxies.json, confira [Definir um objeto requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="3520f-140">To learn how to apply this capability from proxies.json, see [Define a requestOverrides object].</span></span>

### <span data-ttu-id="3520f-141"><a name="modify-response"></a>Modificar a resposta</span><span class="sxs-lookup"><span data-stu-id="3520f-141"><a name="modify-response"></a>Modify the response</span></span>

<span data-ttu-id="3520f-142">Por padrão, a resposta do cliente é inicializada como uma cópia da resposta de back-end.</span><span class="sxs-lookup"><span data-stu-id="3520f-142">By default, the client response is initialized as a copy of the back-end response.</span></span> <span data-ttu-id="3520f-143">Você pode fazer alterações no código de status, na frase de motivo, nos cabeçalhos e no corpo da resposta.</span><span class="sxs-lookup"><span data-stu-id="3520f-143">You can make changes to the response's status code, reason phrase, headers, and body.</span></span> <span data-ttu-id="3520f-144">Os valores modificados podem referenciar as [configurações do aplicativo], os [parâmetros da solicitação original do cliente] e os [parâmetros da resposta de back-end].</span><span class="sxs-lookup"><span data-stu-id="3520f-144">The modified values can reference [application settings], [parameters from the original client request], and [parameters from the back-end response].</span></span>

<span data-ttu-id="3520f-145">Atualmente, não há experiência no portal para modificar as respostas.</span><span class="sxs-lookup"><span data-stu-id="3520f-145">Currently, there is no portal experience for modifying responses.</span></span> <span data-ttu-id="3520f-146">Para saber como aplicar essa capacidade a partir de proxies.json, confira [Definir um objeto responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="3520f-146">To learn how to apply this capability from proxies.json, see [Define a responseOverrides object].</span></span>

## <span data-ttu-id="3520f-147"><a name="using-variables"></a>Usar variáveis</span><span class="sxs-lookup"><span data-stu-id="3520f-147"><a name="using-variables"></a>Use variables</span></span>

<span data-ttu-id="3520f-148">A configuração de um proxy não precisa ser estática.</span><span class="sxs-lookup"><span data-stu-id="3520f-148">The configuration for a proxy does not need to be static.</span></span> <span data-ttu-id="3520f-149">Você pode condicioná-la a usar as variáveis da solicitação original, da resposta de back-end ou das configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3520f-149">You can condition it to use variables from the original request, the back-end response, or application settings.</span></span>

### <span data-ttu-id="3520f-150"><a name="request-parameters"></a>Parâmetros de solicitação de referência</span><span class="sxs-lookup"><span data-stu-id="3520f-150"><a name="request-parameters"></a>Reference request parameters</span></span>

<span data-ttu-id="3520f-151">Use os parâmetros de solicitação como entradas para a propriedade de URL de back-end ou como parte da modificação de solicitações e respostas.</span><span class="sxs-lookup"><span data-stu-id="3520f-151">You can use request parameters as inputs to the back-end URL property or as part of modifying requests and responses.</span></span> <span data-ttu-id="3520f-152">Alguns parâmetros podem ser limitados ao modelo de rota especificado na configuração do proxy base, enquanto outros são obtidos de propriedades da solicitação de entrada.</span><span class="sxs-lookup"><span data-stu-id="3520f-152">Some parameters can be bound from the route template that's specified in the base proxy configuration, and others can come from properties of the incoming request.</span></span>

#### <a name="route-template-parameters"></a><span data-ttu-id="3520f-153">Parâmetros de modelo de rota</span><span class="sxs-lookup"><span data-stu-id="3520f-153">Route template parameters</span></span>
<span data-ttu-id="3520f-154">Os parâmetros usados no modelo de rota estão disponíveis para serem referenciados pelo nome.</span><span class="sxs-lookup"><span data-stu-id="3520f-154">Parameters that are used in the route template are available to be referenced by name.</span></span> <span data-ttu-id="3520f-155">Os nomes de parâmetro são colocados entre chaves ({}).</span><span class="sxs-lookup"><span data-stu-id="3520f-155">The parameter names are enclosed in braces ({}).</span></span>

<span data-ttu-id="3520f-156">Por exemplo, se um proxy tem um modelo de rota como `/pets/{petId}`, a URL do back-end pode incluir o valor de `{petId}`, como em `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span><span class="sxs-lookup"><span data-stu-id="3520f-156">For example, if a proxy has a route template, such as `/pets/{petId}`, the back-end URL can include the value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span></span> <span data-ttu-id="3520f-157">Se o modelo de rota termina em um caractere curinga, como `/api/{*restOfPath}`, o valor `{restOfPath}` será uma representação de cadeia de caracteres dos segmentos de caminho restantes da solicitação de entrada.</span><span class="sxs-lookup"><span data-stu-id="3520f-157">If the route template terminates in a wildcard, such as `/api/{*restOfPath}`, the value `{restOfPath}` is a string representation of the remaining path segments from the incoming request.</span></span>

#### <a name="additional-request-parameters"></a><span data-ttu-id="3520f-158">Parâmetros de solicitação adicionais</span><span class="sxs-lookup"><span data-stu-id="3520f-158">Additional request parameters</span></span>
<span data-ttu-id="3520f-159">Além dos parâmetros do modelo de rota, os seguintes valores podem ser usados em valores de configuração:</span><span class="sxs-lookup"><span data-stu-id="3520f-159">In addition to the route template parameters, the following values can be used in config values:</span></span>

* <span data-ttu-id="3520f-160">**{request.method}**: o método HTTP usado na solicitação original.</span><span class="sxs-lookup"><span data-stu-id="3520f-160">**{request.method}**: The HTTP method that's used on the original request.</span></span>
* <span data-ttu-id="3520f-161">**{request.headers.\<HeaderName\>}**: um cabeçalho que pode ser lido por meio da solicitação original.</span><span class="sxs-lookup"><span data-stu-id="3520f-161">**{request.headers.\<HeaderName\>}**: A header that can be read from the original request.</span></span> <span data-ttu-id="3520f-162">Substitua *\<HeaderName\>* pelo nome do cabeçalho que você deseja ler.</span><span class="sxs-lookup"><span data-stu-id="3520f-162">Replace *\<HeaderName\>* with the name of the header that you want to read.</span></span> <span data-ttu-id="3520f-163">Se o cabeçalho não estiver incluído na solicitação, o valor será a cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="3520f-163">If the header is not included on the request, the value will be the empty string.</span></span>
* <span data-ttu-id="3520f-164">**{request.querystring.\<ParameterName\>}**: um parâmetro de cadeia de consulta que pode ser lido por meio da solicitação original.</span><span class="sxs-lookup"><span data-stu-id="3520f-164">**{request.querystring.\<ParameterName\>}**: A query string parameter that can be read from the original request.</span></span> <span data-ttu-id="3520f-165">Substitua *\<ParameterName\>* pelo nome do parâmetro que você deseja ler.</span><span class="sxs-lookup"><span data-stu-id="3520f-165">Replace *\<ParameterName\>* with the name of the parameter that you want to read.</span></span> <span data-ttu-id="3520f-166">Se o parâmetro não estiver incluído na solicitação, o valor será a cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="3520f-166">If the parameter is not included on the request, the value will be the empty string.</span></span>

### <span data-ttu-id="3520f-167"><a name="response-parameters"></a>Parâmetros de resposta de back-end de referência</span><span class="sxs-lookup"><span data-stu-id="3520f-167"><a name="response-parameters"></a>Reference back-end response parameters</span></span>

<span data-ttu-id="3520f-168">Parâmetros de resposta podem ser usados como parte da modificação da resposta ao cliente.</span><span class="sxs-lookup"><span data-stu-id="3520f-168">Response parameters can be used as part of modifying the response to the client.</span></span> <span data-ttu-id="3520f-169">Os seguintes valores podem ser usados em valores de configuração:</span><span class="sxs-lookup"><span data-stu-id="3520f-169">The following values can be used in config values:</span></span>

* <span data-ttu-id="3520f-170">**{backend.response.statusCode}**: o código de status HTTP retornado na resposta de back-end.</span><span class="sxs-lookup"><span data-stu-id="3520f-170">**{backend.response.statusCode}**: The HTTP status code that's returned on the back-end response.</span></span>
* <span data-ttu-id="3520f-171">**{backend.response.statusReason}**: a frase de motivo HTTP retornada na resposta de back-end.</span><span class="sxs-lookup"><span data-stu-id="3520f-171">**{backend.response.statusReason}**: The HTTP reason phrase that's returned on the back-end response.</span></span>
* <span data-ttu-id="3520f-172">**{backend.response.headers.\<HeaderName\>}**: um cabeçalho que pode ser lido por meio da resposta de back-end.</span><span class="sxs-lookup"><span data-stu-id="3520f-172">**{backend.response.headers.\<HeaderName\>}**: A header that can be read from the back-end response.</span></span> <span data-ttu-id="3520f-173">Substitua *\<HeaderName\>* pelo nome do cabeçalho que você deseja ler.</span><span class="sxs-lookup"><span data-stu-id="3520f-173">Replace *\<HeaderName\>* with the name of the header you want to read.</span></span> <span data-ttu-id="3520f-174">Se o cabeçalho não estiver incluído na solicitação, o valor será a cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="3520f-174">If the header is not included on the request, the value will be the empty string.</span></span>

### <span data-ttu-id="3520f-175"><a name="use-appsettings"></a>Configurações do aplicativo de referência</span><span class="sxs-lookup"><span data-stu-id="3520f-175"><a name="use-appsettings"></a>Reference application settings</span></span>

<span data-ttu-id="3520f-176">Você também referenciar as [configurações do aplicativo definidas para o aplicativo de funções](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) envolvendo o nome da configuração entre sinais de percentual (%).</span><span class="sxs-lookup"><span data-stu-id="3520f-176">You can also reference [application settings defined for the function app](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding the setting name with percent signs (%).</span></span>

<span data-ttu-id="3520f-177">Por exemplo, em uma URL de back-end *https://%ORDER_PROCESSING_HOST%/api/orders*, "% ORDER_PROCESSING_HOST %" será substituído pelo valor da configuração ORDER_PROCESSING_HOST.</span><span class="sxs-lookup"><span data-stu-id="3520f-177">For example, a back-end URL of *https://%ORDER_PROCESSING_HOST%/api/orders* would have "%ORDER_PROCESSING_HOST%" replaced with the value of the ORDER_PROCESSING_HOST setting.</span></span>

> [!TIP] 
> <span data-ttu-id="3520f-178">Usar configurações do aplicativo para hosts de back-end quando você tem várias implantações ou ambientes de teste.</span><span class="sxs-lookup"><span data-stu-id="3520f-178">Use application settings for back-end hosts when you have multiple deployments or test environments.</span></span> <span data-ttu-id="3520f-179">Dessa forma, você pode garantir que você sempre está se comunicando com o back-end à direita para esse ambiente.</span><span class="sxs-lookup"><span data-stu-id="3520f-179">That way, you can make sure that you are always talking to the right back end for that environment.</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="3520f-180">Configuração avançada</span><span class="sxs-lookup"><span data-stu-id="3520f-180">Advanced configuration</span></span>

<span data-ttu-id="3520f-181">Os proxies que você configura são armazenados em um arquivo proxies.json, localizado na raiz do diretório de aplicativo função.</span><span class="sxs-lookup"><span data-stu-id="3520f-181">The proxies that you configure are stored in a proxies.json file, which is located in the root of a function app directory.</span></span> <span data-ttu-id="3520f-182">Você pode editar esse arquivo manualmente e implantá-lo como parte do seu aplicativo ao usar qualquer um dos [métodos de implantação](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) que ofereça suporte a funções.</span><span class="sxs-lookup"><span data-stu-id="3520f-182">You can manually edit this file and deploy it as part of your app when you use any of the [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span></span> <span data-ttu-id="3520f-183">O recurso deve ser [habilitado](#enable) para que o arquivo seja processado.</span><span class="sxs-lookup"><span data-stu-id="3520f-183">The feature must be [enabled](#enable) for the file to be processed.</span></span> 

> [!TIP] 
> <span data-ttu-id="3520f-184">Se você não tiver definido um dos métodos de implantação, também poderá trabalhar com o arquivo proxies.json no portal.</span><span class="sxs-lookup"><span data-stu-id="3520f-184">If you have not set up one of the deployment methods, you can also work with the proxies.json file in the portal.</span></span> <span data-ttu-id="3520f-185">Vá até o aplicativo de funções e selecione **Recursos da plataforma** e,depois, selecione **Editor do Serviço de Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="3520f-185">Go to your function app, select **Platform features**, and then select **App Service Editor**.</span></span> <span data-ttu-id="3520f-186">Isso permitirá que você veja toda a estrutura de arquivo do aplicativo de funções e faça alterações.</span><span class="sxs-lookup"><span data-stu-id="3520f-186">By doing so, you can view the entire file structure of your function app and then make changes.</span></span>

<span data-ttu-id="3520f-187">Proxies.json é definido por um objeto de proxies, composto de proxies nomeados e suas definições.</span><span class="sxs-lookup"><span data-stu-id="3520f-187">Proxies.json is defined by a proxies object, which is composed of named proxies and their definitions.</span></span> <span data-ttu-id="3520f-188">Opcionalmente, você pode referenciar um [esquema JSON](http://json.schemastore.org/proxies) para o preenchimento do código, caso seu editor dê suporte a isso.</span><span class="sxs-lookup"><span data-stu-id="3520f-188">Optionally, if your editor supports it, you can reference a [JSON schema](http://json.schemastore.org/proxies) for code completion.</span></span> <span data-ttu-id="3520f-189">Um arquivo de exemplo pode parecer com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="3520f-189">An example file might look like the following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>"
        }
    }
}
```

<span data-ttu-id="3520f-190">Cada proxy tem um nome amigável, como *proxy1*, no exemplo acima.</span><span class="sxs-lookup"><span data-stu-id="3520f-190">Each proxy has a friendly name, such as *proxy1* in the preceding example.</span></span> <span data-ttu-id="3520f-191">O objeto de definição de proxy correspondente é definido pelas seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="3520f-191">The corresponding proxy definition object is defined by the following properties:</span></span>

* <span data-ttu-id="3520f-192">**matchCondition**: obrigatório - um objeto que define as solicitações que disparam a execução desse proxy.</span><span class="sxs-lookup"><span data-stu-id="3520f-192">**matchCondition**: Required--an object defining the requests that trigger the execution of this proxy.</span></span> <span data-ttu-id="3520f-193">Ele contém duas propriedades compartilhadas com [gatilhos HTTP]:</span><span class="sxs-lookup"><span data-stu-id="3520f-193">It contains two properties that are shared with [HTTP triggers]:</span></span>
    * <span data-ttu-id="3520f-194">_métodos_: uma matriz dos métodos HTTP aos quais o proxy responde.</span><span class="sxs-lookup"><span data-stu-id="3520f-194">_methods_: An array of the HTTP methods that the proxy responds to.</span></span> <span data-ttu-id="3520f-195">Se não for especificado, o proxy responderá a todos os métodos HTTP na rota.</span><span class="sxs-lookup"><span data-stu-id="3520f-195">If it is not specified, the proxy responds to all HTTP methods on the route.</span></span>
    * <span data-ttu-id="3520f-196">_route_: obrigatório - define o modelo da rota, controlando para quais URLs de solicitação seu proxy responde.</span><span class="sxs-lookup"><span data-stu-id="3520f-196">_route_: Required--defines the route template, controlling which request URLs your proxy responds to.</span></span> <span data-ttu-id="3520f-197">Ao contrário de disparadores HTTP, não há nenhum valor padrão.</span><span class="sxs-lookup"><span data-stu-id="3520f-197">Unlike in HTTP triggers, there is no default value.</span></span>
* <span data-ttu-id="3520f-198">**backendUri**: a URL do recurso de back-end ao qual a solicitação deve ser transmitida por proxy.</span><span class="sxs-lookup"><span data-stu-id="3520f-198">**backendUri**: The URL of the back-end resource to which the request should be proxied.</span></span> <span data-ttu-id="3520f-199">Esse valor pode referenciar as configurações do aplicativo e os parâmetros da solicitação original do cliente.</span><span class="sxs-lookup"><span data-stu-id="3520f-199">This value can reference application settings and parameters from the original client request.</span></span> <span data-ttu-id="3520f-200">Se esta propriedade não for incluída, o Azure Functions responderá com um HTTP 200 OK.</span><span class="sxs-lookup"><span data-stu-id="3520f-200">If this property is not included, Azure Functions responds with an HTTP 200 OK.</span></span>
* <span data-ttu-id="3520f-201">**requestOverrides**: um objeto que define as transformações para a solicitação de back-end.</span><span class="sxs-lookup"><span data-stu-id="3520f-201">**requestOverrides**: An object that defines transformations to the back-end request.</span></span> <span data-ttu-id="3520f-202">Confira [Definir um objeto requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="3520f-202">See [Define a requestOverrides object].</span></span>
* <span data-ttu-id="3520f-203">**requestOverrides**: um objeto que define as transformações para a resposta do cliente.</span><span class="sxs-lookup"><span data-stu-id="3520f-203">**responseOverrides**: An object that defines transformations to the client response.</span></span> <span data-ttu-id="3520f-204">Confira [Definir um objeto responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="3520f-204">See [Define a responseOverrides object].</span></span>

> [!NOTE] 
> <span data-ttu-id="3520f-205">Os proxies do Azure Functions da propriedade route não respeitam a propriedade routePrefix da configuração de host do Functions.</span><span class="sxs-lookup"><span data-stu-id="3520f-205">The route property Azure Functions Proxies does not honor the routePrefix property of the Functions host configuration.</span></span> <span data-ttu-id="3520f-206">Se você quiser incluir um prefixo, como /api, ela deve ser incluída na propriedade de rota.</span><span class="sxs-lookup"><span data-stu-id="3520f-206">If you want to include a prefix such as /api, it must be included in the route property.</span></span>

### <span data-ttu-id="3520f-207"><a name="requestOverrides"></a>Definir um objeto requestOverrides</span><span class="sxs-lookup"><span data-stu-id="3520f-207"><a name="requestOverrides"></a>Define a requestOverrides object</span></span>

<span data-ttu-id="3520f-208">O objeto requestOverrides define as alterações feitas à solicitação quando o recurso de back-end é chamado.</span><span class="sxs-lookup"><span data-stu-id="3520f-208">The requestOverrides object defines changes made to the request when the back-end resource is called.</span></span> <span data-ttu-id="3520f-209">O objeto é definido pelas seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="3520f-209">The object is defined by the following properties:</span></span>

* <span data-ttu-id="3520f-210">**backend.request.method**: o método HTTP que será usado para chamar o back-end.</span><span class="sxs-lookup"><span data-stu-id="3520f-210">**backend.request.method**: The HTTP method that's used to call the back end.</span></span>
* <span data-ttu-id="3520f-211">**backend.request.querystring.\<ParameterName\>**: um parâmetro de cadeia de consulta que pode ser definido para a chamada ao back-end.</span><span class="sxs-lookup"><span data-stu-id="3520f-211">**backend.request.querystring.\<ParameterName\>**: A query string parameter that can be set for the call to the back end.</span></span> <span data-ttu-id="3520f-212">Substitua *\<ParameterName\>* pelo nome do parâmetro que você deseja definir.</span><span class="sxs-lookup"><span data-stu-id="3520f-212">Replace *\<ParameterName\>* with the name of the parameter that you want to set.</span></span> <span data-ttu-id="3520f-213">Se a cadeia de caracteres vazia for fornecida, o parâmetro não será incluído na solicitação de back-end.</span><span class="sxs-lookup"><span data-stu-id="3520f-213">If the empty string is provided, the parameter is not included on the back-end request.</span></span>
* <span data-ttu-id="3520f-214">**backend.request.headers.\<HeaderName\>**: um cabeçalho que pode ser definido para a chamada ao back-end.</span><span class="sxs-lookup"><span data-stu-id="3520f-214">**backend.request.headers.\<HeaderName\>**: A header that can be set for the call to the back end.</span></span> <span data-ttu-id="3520f-215">Substitua *\<HeaderName\>* pelo nome do cabeçalho que você deseja definir.</span><span class="sxs-lookup"><span data-stu-id="3520f-215">Replace *\<HeaderName\>* with the name of the header that you want to set.</span></span> <span data-ttu-id="3520f-216">Se você fornecer a cadeia de caracteres vazia, o cabeçalho não será incluído na solicitação de back-end.</span><span class="sxs-lookup"><span data-stu-id="3520f-216">If you provide the empty string, the header is not included on the back-end request.</span></span>

<span data-ttu-id="3520f-217">Os valores podem referenciar as configurações do aplicativo e os parâmetros da solicitação original do cliente.</span><span class="sxs-lookup"><span data-stu-id="3520f-217">Values can reference application settings and parameters from the original client request.</span></span>

<span data-ttu-id="3520f-218">Uma configuração de exemplo pode ser parecida com a seguinte:</span><span class="sxs-lookup"><span data-stu-id="3520f-218">An example configuration might look like the following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>",
            "requestOverrides": {
                "backend.request.headers.Accept": "application/xml",
                "backend.request.headers.x-functions-key": "%ANOTHERAPP_API_KEY%"
            }
        }
    }
}
```

### <span data-ttu-id="3520f-219"><a name="responseOverrides"></a>Definir um objeto responseOverrides</span><span class="sxs-lookup"><span data-stu-id="3520f-219"><a name="responseOverrides"></a>Define a responseOverrides object</span></span>

<span data-ttu-id="3520f-220">O objeto requestOverrides define as alterações feitas à resposta passada novamente ao cliente.</span><span class="sxs-lookup"><span data-stu-id="3520f-220">The requestOverrides object defines changes that are made to the response that's passed back to the client.</span></span> <span data-ttu-id="3520f-221">O objeto é definido pelas seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="3520f-221">The object is defined by the following properties:</span></span>

* <span data-ttu-id="3520f-222">**response.statusCode**: o código de status HTTP a ser retornado ao cliente.</span><span class="sxs-lookup"><span data-stu-id="3520f-222">**response.statusCode**: The HTTP status code to be returned to the client.</span></span>
* <span data-ttu-id="3520f-223">**response.statusReason**: a frase de motivo do HTTP a ser retornada ao cliente.</span><span class="sxs-lookup"><span data-stu-id="3520f-223">**response.statusReason**: The HTTP reason phrase to be returned to the client.</span></span>
* <span data-ttu-id="3520f-224">**response.body**: a representação de cadeia de caracteres do corpo a ser retornada ao cliente.</span><span class="sxs-lookup"><span data-stu-id="3520f-224">**response.body**: The string representation of the body to be returned to the client.</span></span>
* <span data-ttu-id="3520f-225">**response.headers.\<HeaderName\>**: um cabeçalho que pode ser definido para a resposta ao cliente.</span><span class="sxs-lookup"><span data-stu-id="3520f-225">**response.headers.\<HeaderName\>**: A header that can be set for the response to the client.</span></span> <span data-ttu-id="3520f-226">Substitua *\<HeaderName\>* pelo nome do cabeçalho que você deseja definir.</span><span class="sxs-lookup"><span data-stu-id="3520f-226">Replace *\<HeaderName\>* with the name of the header that you want to set.</span></span> <span data-ttu-id="3520f-227">Se você fornecer a cadeia de caracteres vazia, o cabeçalho não será incluído na resposta.</span><span class="sxs-lookup"><span data-stu-id="3520f-227">If you provide the empty string, the header is not included on the response.</span></span>

<span data-ttu-id="3520f-228">Os valores podem referenciar as configurações do aplicativo, os parâmetros da solicitação original do cliente e os parâmetros da resposta de back-end.</span><span class="sxs-lookup"><span data-stu-id="3520f-228">Values can reference application settings, parameters from the original client request, and parameters from the back-end response.</span></span>

<span data-ttu-id="3520f-229">Uma configuração de exemplo pode ser parecida com a seguinte:</span><span class="sxs-lookup"><span data-stu-id="3520f-229">An example configuration might look like the following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "responseOverrides": {
                "response.body": "Hello, {test}",
                "response.headers.Content-Type": "text/plain"
            }
        }
    }
}
```
> [!NOTE] 
> <span data-ttu-id="3520f-230">Neste exemplo, o corpo está sendo definido diretamente e, portanto, nenhuma propriedade `backendUri` é necessária.</span><span class="sxs-lookup"><span data-stu-id="3520f-230">In this example, the body is being set directly, so no `backendUri` property is needed.</span></span> <span data-ttu-id="3520f-231">O exemplo mostra como você pode usar os Proxies do Azure Functions para simular APIs.</span><span class="sxs-lookup"><span data-stu-id="3520f-231">The example shows how you might use Azure Functions Proxies for mocking APIs.</span></span>

<span data-ttu-id="3520f-232">[Portal do Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="3520f-232">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="3520f-233">[gatilhos HTTP]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger</span><span class="sxs-lookup"><span data-stu-id="3520f-233">[HTTP triggers]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger</span></span>
[Modify the back-end request]: #modify-backend-request
[Modify the response]: #modify-response
<span data-ttu-id="3520f-234">[Definir um objeto requestOverrides]: #requestOverrides</span><span class="sxs-lookup"><span data-stu-id="3520f-234">[Define a requestOverrides object]: #requestOverrides</span></span>
<span data-ttu-id="3520f-235">[Definir um objeto responseOverrides]: #responseOverrides</span><span class="sxs-lookup"><span data-stu-id="3520f-235">[Define a responseOverrides object]: #responseOverrides</span></span>
<span data-ttu-id="3520f-236">[configurações do aplicativo]: #use-appsettings</span><span class="sxs-lookup"><span data-stu-id="3520f-236">[application settings]: #use-appsettings</span></span>
<span data-ttu-id="3520f-237">[Usar variáveis]: #using-variables</span><span class="sxs-lookup"><span data-stu-id="3520f-237">[Use variables]: #using-variables</span></span>
<span data-ttu-id="3520f-238">[parâmetros da solicitação original do cliente]: #request-parameters</span><span class="sxs-lookup"><span data-stu-id="3520f-238">[parameters from the original client request]: #request-parameters</span></span>
<span data-ttu-id="3520f-239">[parâmetros da resposta de back-end]: #response-parameters</span><span class="sxs-lookup"><span data-stu-id="3520f-239">[parameters from the back-end response]: #response-parameters</span></span>
