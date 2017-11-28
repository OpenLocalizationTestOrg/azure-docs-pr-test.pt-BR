---
title: "aaaWork com proxies em funções do Azure | Microsoft Docs"
description: "Visão geral de como toouse Proxies de funções do Azure"
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
ms.openlocfilehash: 4d94c89e8f8f2d2c771b01bae142bf9a4f3b7f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a><span data-ttu-id="ce04a-103">Trabalhar com proxies do Azure Functions (visualização)</span><span class="sxs-lookup"><span data-stu-id="ce04a-103">Work with Azure Functions Proxies (preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="ce04a-104">Proxies do Azure Functions está atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="ce04a-104">Azure Functions Proxies is currently in preview.</span></span> <span data-ttu-id="ce04a-105">É gratuito enquanto na visualização, mas as funções padrão cobrança aplica tooproxy execuções.</span><span class="sxs-lookup"><span data-stu-id="ce04a-105">It is free while in preview, but standard Functions billing applies tooproxy executions.</span></span> <span data-ttu-id="ce04a-106">Para saber mais, confira [Preços do Azure Functions](https://azure.microsoft.com/pricing/details/functions/).</span><span class="sxs-lookup"><span data-stu-id="ce04a-106">For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).</span></span>

<span data-ttu-id="ce04a-107">Este artigo explica como tooconfigure e trabalhar com Proxies de funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce04a-107">This article explains how tooconfigure and work with Azure Functions Proxies.</span></span> <span data-ttu-id="ce04a-108">Com esse recurso, você pode especificar os pontos de extremidade em seu aplicativo de funções que são implementados por outro recurso.</span><span class="sxs-lookup"><span data-stu-id="ce04a-108">With this feature, you can specify endpoints on your function app that are implemented by another resource.</span></span> <span data-ttu-id="ce04a-109">Você pode usar esses toobreak proxies uma API grande em vários aplicativos de função (como em uma arquitetura de microsserviço), enquanto ainda apresentar uma superfície de API simples para clientes.</span><span class="sxs-lookup"><span data-stu-id="ce04a-109">You can use these proxies toobreak a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <span data-ttu-id="ce04a-110"><a name="enable"></a>Habilitar proxies do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="ce04a-110"><a name="enable"></a>Enable Azure Functions Proxies</span></span>

<span data-ttu-id="ce04a-111">Os proxies não estão habilitados por padrão.</span><span class="sxs-lookup"><span data-stu-id="ce04a-111">Proxies are not enabled by default.</span></span> <span data-ttu-id="ce04a-112">Você pode criar proxies enquanto Olá recurso está desabilitado, mas elas não serão executadas.</span><span class="sxs-lookup"><span data-stu-id="ce04a-112">You can create proxies while hello feature is disabled, but they will not execute.</span></span> <span data-ttu-id="ce04a-113">tooenable proxies, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce04a-113">tooenable proxies, do hello following:</span></span>

1. <span data-ttu-id="ce04a-114">Olá abrir [portal do Azure], e em seguida, acesse o aplicativo de função tooyour.</span><span class="sxs-lookup"><span data-stu-id="ce04a-114">Open hello [Azure portal], and then go tooyour function app.</span></span>
2. <span data-ttu-id="ce04a-115">Selecione **Configurações do aplicativo de funções**.</span><span class="sxs-lookup"><span data-stu-id="ce04a-115">Select **Function app settings**.</span></span>
3. <span data-ttu-id="ce04a-116">Opção **habilitar Proxies de funções do Azure (visualização)** muito**em**.</span><span class="sxs-lookup"><span data-stu-id="ce04a-116">Switch **Enable Azure Functions Proxies (preview)** too**On**.</span></span>

<span data-ttu-id="ce04a-117">Você também pode retornar aqui tooupdate Olá proxy runtime conforme novos recursos se tornam disponíveis.</span><span class="sxs-lookup"><span data-stu-id="ce04a-117">You can also return here tooupdate hello proxy runtime as new features become available.</span></span>


## <span data-ttu-id="ce04a-118"><a name="create"></a>Criar um proxy</span><span class="sxs-lookup"><span data-stu-id="ce04a-118"><a name="create"></a>Create a proxy</span></span>

<span data-ttu-id="ce04a-119">Esta seção mostra como toocreate um proxy no hello portal de funções.</span><span class="sxs-lookup"><span data-stu-id="ce04a-119">This section shows you how toocreate a proxy in hello Functions portal.</span></span>

1. <span data-ttu-id="ce04a-120">Olá abrir [portal do Azure], e em seguida, acesse o aplicativo de função tooyour.</span><span class="sxs-lookup"><span data-stu-id="ce04a-120">Open hello [Azure portal], and then go tooyour function app.</span></span>
2. <span data-ttu-id="ce04a-121">No painel esquerdo do hello, selecione **novo proxy**.</span><span class="sxs-lookup"><span data-stu-id="ce04a-121">In hello left pane, select **New proxy**.</span></span>
3. <span data-ttu-id="ce04a-122">Forneça um nome para seu proxy.</span><span class="sxs-lookup"><span data-stu-id="ce04a-122">Provide a name for your proxy.</span></span>
4. <span data-ttu-id="ce04a-123">Configurar o ponto de extremidade de saudação que é exposto no aplicativo função especificando Olá **modelo de rota** e **métodos HTTP**.</span><span class="sxs-lookup"><span data-stu-id="ce04a-123">Configure hello endpoint that's exposed on this function app by specifying hello **route template** and **HTTP methods**.</span></span> <span data-ttu-id="ce04a-124">Esses parâmetros se comportam de acordo regras toohello para [HTTP gatilhos].</span><span class="sxs-lookup"><span data-stu-id="ce04a-124">These parameters behave according toohello rules for [HTTP triggers].</span></span>
5. <span data-ttu-id="ce04a-125">Saudação de conjunto **URL de back-end** tooanother de ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="ce04a-125">Set hello **backend URL** tooanother endpoint.</span></span> <span data-ttu-id="ce04a-126">Esse ponto de extremidade pode ser uma função em outro aplicativo de funções, ou pode ser qualquer outra API.</span><span class="sxs-lookup"><span data-stu-id="ce04a-126">This endpoint could be a function in another function app, or it could be any other API.</span></span> <span data-ttu-id="ce04a-127">Olá valor não precisa toobe estático, e ele pode fazer referência [configurações do aplicativo] e [parâmetros da solicitação de cliente original Olá].</span><span class="sxs-lookup"><span data-stu-id="ce04a-127">hello value does not need toobe static, and it can reference [application settings] and [parameters from hello original client request].</span></span>
6. <span data-ttu-id="ce04a-128">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ce04a-128">Click **Create**.</span></span>

<span data-ttu-id="ce04a-129">Seu proxy agora existe como um novo ponto de extremidade em seu aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="ce04a-129">Your proxy now exists as a new endpoint on your function app.</span></span> <span data-ttu-id="ce04a-130">Da perspectiva do cliente, é equivalente tooan HttpTrigger em funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce04a-130">From a client perspective, it is equivalent tooan HttpTrigger in Azure Functions.</span></span> <span data-ttu-id="ce04a-131">Você pode testar seu novo proxy copiando Olá URL do Proxy e testá-lo com seu cliente HTTP favorito.</span><span class="sxs-lookup"><span data-stu-id="ce04a-131">You can try out your new proxy by copying hello Proxy URL and testing it with your favorite HTTP client.</span></span>

## <span data-ttu-id="ce04a-132"><a name="modify-requests-responses"></a>Modificar solicitações e respostas</span><span class="sxs-lookup"><span data-stu-id="ce04a-132"><a name="modify-requests-responses"></a>Modify requests and responses</span></span>

<span data-ttu-id="ce04a-133">Com Proxies de funções do Azure, você pode modificar solicitações tooand respostas de back-end hello.</span><span class="sxs-lookup"><span data-stu-id="ce04a-133">With Azure Functions Proxies, you can modify requests tooand responses from hello back end.</span></span> <span data-ttu-id="ce04a-134">Essas transformações podem usar variáveis, conforme definido em [Usar variáveis].</span><span class="sxs-lookup"><span data-stu-id="ce04a-134">These transformations can use variables as defined in [Use variables].</span></span>

### <span data-ttu-id="ce04a-135"><a name="modify-backend-request"></a>Modificar a solicitação de back-end Olá</span><span class="sxs-lookup"><span data-stu-id="ce04a-135"><a name="modify-backend-request"></a>Modify hello back-end request</span></span>

<span data-ttu-id="ce04a-136">Por padrão, a solicitação de back-end de saudação é inicializado como uma cópia da solicitação original hello.</span><span class="sxs-lookup"><span data-stu-id="ce04a-136">By default, hello back-end request is initialized as a copy of hello original request.</span></span> <span data-ttu-id="ce04a-137">Além disso toosetting Olá back-end URL, você pode fazer alterações toohello HTTP método, cabeçalhos e parâmetros de cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="ce04a-137">In addition toosetting hello back-end URL, you can make changes toohello HTTP method, headers, and query string parameters.</span></span> <span data-ttu-id="ce04a-138">Olá valores modificados podem fazer referência a [configurações do aplicativo] e [parâmetros da solicitação de cliente original Olá].</span><span class="sxs-lookup"><span data-stu-id="ce04a-138">hello modified values can reference [application settings] and [parameters from hello original client request].</span></span>

<span data-ttu-id="ce04a-139">Atualmente, não há experiência no portal para modificar as solicitações de back-end.</span><span class="sxs-lookup"><span data-stu-id="ce04a-139">Currently, there is no portal experience for modifying back-end requests.</span></span> <span data-ttu-id="ce04a-140">toolearn como tooapply essa capacidade de proxies.json, consulte [definir um objeto requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="ce04a-140">toolearn how tooapply this capability from proxies.json, see [Define a requestOverrides object].</span></span>

### <span data-ttu-id="ce04a-141"><a name="modify-response"></a>Modificar a resposta de saudação</span><span class="sxs-lookup"><span data-stu-id="ce04a-141"><a name="modify-response"></a>Modify hello response</span></span>

<span data-ttu-id="ce04a-142">Por padrão, resposta de cliente Olá é inicializada como uma cópia da resposta de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce04a-142">By default, hello client response is initialized as a copy of hello back-end response.</span></span> <span data-ttu-id="ce04a-143">Você pode fazer o código de status da resposta de toohello alterações, frase de motivo, cabeçalhos e corpo.</span><span class="sxs-lookup"><span data-stu-id="ce04a-143">You can make changes toohello response's status code, reason phrase, headers, and body.</span></span> <span data-ttu-id="ce04a-144">Olá valores modificados podem fazer referência a [configurações do aplicativo], [parâmetros da solicitação de cliente original Olá], e [parâmetros de resposta de back-end Olá].</span><span class="sxs-lookup"><span data-stu-id="ce04a-144">hello modified values can reference [application settings], [parameters from hello original client request], and [parameters from hello back-end response].</span></span>

<span data-ttu-id="ce04a-145">Atualmente, não há experiência no portal para modificar as respostas.</span><span class="sxs-lookup"><span data-stu-id="ce04a-145">Currently, there is no portal experience for modifying responses.</span></span> <span data-ttu-id="ce04a-146">toolearn como tooapply essa capacidade de proxies.json, consulte [definir um objeto responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="ce04a-146">toolearn how tooapply this capability from proxies.json, see [Define a responseOverrides object].</span></span>

## <span data-ttu-id="ce04a-147"><a name="using-variables"></a>Usar variáveis</span><span class="sxs-lookup"><span data-stu-id="ce04a-147"><a name="using-variables"></a>Use variables</span></span>

<span data-ttu-id="ce04a-148">configuração de saudação para um proxy não precisa toobe estático.</span><span class="sxs-lookup"><span data-stu-id="ce04a-148">hello configuration for a proxy does not need toobe static.</span></span> <span data-ttu-id="ce04a-149">Você pode condição ele toouse variáveis de solicitação original hello, resposta de back-end de saudação ou as configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce04a-149">You can condition it toouse variables from hello original request, hello back-end response, or application settings.</span></span>

### <span data-ttu-id="ce04a-150"><a name="request-parameters"></a>Parâmetros de solicitação de referência</span><span class="sxs-lookup"><span data-stu-id="ce04a-150"><a name="request-parameters"></a>Reference request parameters</span></span>

<span data-ttu-id="ce04a-151">Você pode usar parâmetros de solicitação como entradas toohello propriedade de URL de back-end ou como parte da modificação de solicitações e respostas.</span><span class="sxs-lookup"><span data-stu-id="ce04a-151">You can use request parameters as inputs toohello back-end URL property or as part of modifying requests and responses.</span></span> <span data-ttu-id="ce04a-152">Alguns parâmetros podem ser vinculados de modelo de rota de saudação que é especificado na configuração de proxy base hello e outras pessoas podem vir de propriedades de solicitação de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="ce04a-152">Some parameters can be bound from hello route template that's specified in hello base proxy configuration, and others can come from properties of hello incoming request.</span></span>

#### <a name="route-template-parameters"></a><span data-ttu-id="ce04a-153">Parâmetros de modelo de rota</span><span class="sxs-lookup"><span data-stu-id="ce04a-153">Route template parameters</span></span>
<span data-ttu-id="ce04a-154">Parâmetros que são usados no modelo de rota Olá estão disponível toobe referenciada por nome.</span><span class="sxs-lookup"><span data-stu-id="ce04a-154">Parameters that are used in hello route template are available toobe referenced by name.</span></span> <span data-ttu-id="ce04a-155">nomes de parâmetro Hello são colocados entre chaves ({}).</span><span class="sxs-lookup"><span data-stu-id="ce04a-155">hello parameter names are enclosed in braces ({}).</span></span>

<span data-ttu-id="ce04a-156">Por exemplo, se um proxy tem um modelo de rota, como `/pets/{petId}`, Olá URL de back-end pode incluir o valor de saudação do `{petId}`, como em `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span><span class="sxs-lookup"><span data-stu-id="ce04a-156">For example, if a proxy has a route template, such as `/pets/{petId}`, hello back-end URL can include hello value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span></span> <span data-ttu-id="ce04a-157">Se o modelo de rota Olá termina em um caractere curinga, como `/api/{*restOfPath}`, Olá valor `{restOfPath}` é uma representação de cadeia de caracteres de saudação restantes segmentos de caminho da solicitação de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="ce04a-157">If hello route template terminates in a wildcard, such as `/api/{*restOfPath}`, hello value `{restOfPath}` is a string representation of hello remaining path segments from hello incoming request.</span></span>

#### <a name="additional-request-parameters"></a><span data-ttu-id="ce04a-158">Parâmetros de solicitação adicionais</span><span class="sxs-lookup"><span data-stu-id="ce04a-158">Additional request parameters</span></span>
<span data-ttu-id="ce04a-159">Além do toohello parâmetros de modelo de rota, Olá valores a seguir pode ser usado em valores de configuração:</span><span class="sxs-lookup"><span data-stu-id="ce04a-159">In addition toohello route template parameters, hello following values can be used in config values:</span></span>

* <span data-ttu-id="ce04a-160">**{Request}** : Olá o método HTTP usado na solicitação original hello.</span><span class="sxs-lookup"><span data-stu-id="ce04a-160">**{request.method}**: hello HTTP method that's used on hello original request.</span></span>
* <span data-ttu-id="ce04a-161">**{: Request. Headers. \<HeaderName\>}**: um cabeçalho que pode ser lido da solicitação original hello.</span><span class="sxs-lookup"><span data-stu-id="ce04a-161">**{request.headers.\<HeaderName\>}**: A header that can be read from hello original request.</span></span> <span data-ttu-id="ce04a-162">Substituir  *\<HeaderName\>*  com o nome de saudação do cabeçalho de saudação que você deseja tooread.</span><span class="sxs-lookup"><span data-stu-id="ce04a-162">Replace *\<HeaderName\>* with hello name of hello header that you want tooread.</span></span> <span data-ttu-id="ce04a-163">Se o cabeçalho de saudação não está incluído na solicitação Olá, o valor de Olá será a cadeia de caracteres vazia hello.</span><span class="sxs-lookup"><span data-stu-id="ce04a-163">If hello header is not included on hello request, hello value will be hello empty string.</span></span>
* <span data-ttu-id="ce04a-164">**{Request. QueryString. \<ParameterName\>}**: um parâmetro de cadeia de caracteres de consulta que possa ser lido da solicitação original hello.</span><span class="sxs-lookup"><span data-stu-id="ce04a-164">**{request.querystring.\<ParameterName\>}**: A query string parameter that can be read from hello original request.</span></span> <span data-ttu-id="ce04a-165">Substituir  *\<ParameterName\>*  com o nome de saudação do parâmetro hello que você deseja tooread.</span><span class="sxs-lookup"><span data-stu-id="ce04a-165">Replace *\<ParameterName\>* with hello name of hello parameter that you want tooread.</span></span> <span data-ttu-id="ce04a-166">Se o parâmetro hello não está incluído na solicitação Olá, o valor de saudação será a cadeia de caracteres vazia hello.</span><span class="sxs-lookup"><span data-stu-id="ce04a-166">If hello parameter is not included on hello request, hello value will be hello empty string.</span></span>

### <span data-ttu-id="ce04a-167"><a name="response-parameters"></a>Parâmetros de resposta de back-end de referência</span><span class="sxs-lookup"><span data-stu-id="ce04a-167"><a name="response-parameters"></a>Reference back-end response parameters</span></span>

<span data-ttu-id="ce04a-168">Parâmetros de resposta podem ser usados como parte de modificar Olá resposta toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="ce04a-168">Response parameters can be used as part of modifying hello response toohello client.</span></span> <span data-ttu-id="ce04a-169">Olá valores a seguir pode ser usado em valores de configuração:</span><span class="sxs-lookup"><span data-stu-id="ce04a-169">hello following values can be used in config values:</span></span>

* <span data-ttu-id="ce04a-170">**{backend.response.statusCode}** : Olá código de status HTTP retornado na resposta de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce04a-170">**{backend.response.statusCode}**: hello HTTP status code that's returned on hello back-end response.</span></span>
* <span data-ttu-id="ce04a-171">**{backend.response.statusReason}** : frase de motivo Olá HTTP que é retornado na resposta de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce04a-171">**{backend.response.statusReason}**: hello HTTP reason phrase that's returned on hello back-end response.</span></span>
* <span data-ttu-id="ce04a-172">**{backend.response.headers. \<HeaderName\>}**: um cabeçalho que pode ser lido da resposta de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce04a-172">**{backend.response.headers.\<HeaderName\>}**: A header that can be read from hello back-end response.</span></span> <span data-ttu-id="ce04a-173">Substituir  *\<HeaderName\>*  com o nome de saudação do cabeçalho de saudação você deseja tooread.</span><span class="sxs-lookup"><span data-stu-id="ce04a-173">Replace *\<HeaderName\>* with hello name of hello header you want tooread.</span></span> <span data-ttu-id="ce04a-174">Se o cabeçalho de saudação não está incluído na solicitação Olá, o valor de Olá será a cadeia de caracteres vazia hello.</span><span class="sxs-lookup"><span data-stu-id="ce04a-174">If hello header is not included on hello request, hello value will be hello empty string.</span></span>

### <span data-ttu-id="ce04a-175"><a name="use-appsettings"></a>Configurações do aplicativo de referência</span><span class="sxs-lookup"><span data-stu-id="ce04a-175"><a name="use-appsettings"></a>Reference application settings</span></span>

<span data-ttu-id="ce04a-176">Você também pode referenciar [configurações de aplicativo definidas para o aplicativo de função hello](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) envolvendo o nome da configuração Olá sinais de porcentagem (%).</span><span class="sxs-lookup"><span data-stu-id="ce04a-176">You can also reference [application settings defined for hello function app](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding hello setting name with percent signs (%).</span></span>

<span data-ttu-id="ce04a-177">Por exemplo, uma URL de back-end de *https://%ORDER_PROCESSING_HOST%/api/orders* teria "% ORDER_PROCESSING_HOST %" substituído pelo valor de saudação da configuração de ORDER_PROCESSING_HOST hello.</span><span class="sxs-lookup"><span data-stu-id="ce04a-177">For example, a back-end URL of *https://%ORDER_PROCESSING_HOST%/api/orders* would have "%ORDER_PROCESSING_HOST%" replaced with hello value of hello ORDER_PROCESSING_HOST setting.</span></span>

> [!TIP] 
> <span data-ttu-id="ce04a-178">Usar configurações do aplicativo para hosts de back-end quando você tem várias implantações ou ambientes de teste.</span><span class="sxs-lookup"><span data-stu-id="ce04a-178">Use application settings for back-end hosts when you have multiple deployments or test environments.</span></span> <span data-ttu-id="ce04a-179">Dessa forma, você pode garantir que estamos falando sempre toohello volta terminar para esse ambiente.</span><span class="sxs-lookup"><span data-stu-id="ce04a-179">That way, you can make sure that you are always talking toohello right back end for that environment.</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="ce04a-180">Configuração avançada</span><span class="sxs-lookup"><span data-stu-id="ce04a-180">Advanced configuration</span></span>

<span data-ttu-id="ce04a-181">proxies de saudação que você configura são armazenados em um arquivo proxies.json, que está localizado na raiz de saudação de um diretório de aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="ce04a-181">hello proxies that you configure are stored in a proxies.json file, which is located in hello root of a function app directory.</span></span> <span data-ttu-id="ce04a-182">Você pode editar esse arquivo manualmente e implantá-lo como parte do seu aplicativo quando você usar qualquer Olá [métodos de implantação](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) que ofereça suporte a funções.</span><span class="sxs-lookup"><span data-stu-id="ce04a-182">You can manually edit this file and deploy it as part of your app when you use any of hello [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span></span> <span data-ttu-id="ce04a-183">saudação de recurso deve ser [habilitado](#enable) para toobe do arquivo hello processado.</span><span class="sxs-lookup"><span data-stu-id="ce04a-183">hello feature must be [enabled](#enable) for hello file toobe processed.</span></span> 

> [!TIP] 
> <span data-ttu-id="ce04a-184">Se você não configurou um dos métodos de implantação Olá, você também pode trabalhar com arquivos de proxies.json Olá no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce04a-184">If you have not set up one of hello deployment methods, you can also work with hello proxies.json file in hello portal.</span></span> <span data-ttu-id="ce04a-185">Aplicativo de função tooyour vá, selecione **recursos de plataforma**e, em seguida, selecione **Editor de aplicativo de serviço**.</span><span class="sxs-lookup"><span data-stu-id="ce04a-185">Go tooyour function app, select **Platform features**, and then select **App Service Editor**.</span></span> <span data-ttu-id="ce04a-186">Fazendo isso, você pode exibir estrutura de todo o arquivo de saudação do seu aplicativo de função e, em seguida, fazer alterações.</span><span class="sxs-lookup"><span data-stu-id="ce04a-186">By doing so, you can view hello entire file structure of your function app and then make changes.</span></span>

<span data-ttu-id="ce04a-187">Proxies.json é definido por um objeto de proxies, composto de proxies nomeados e suas definições.</span><span class="sxs-lookup"><span data-stu-id="ce04a-187">Proxies.json is defined by a proxies object, which is composed of named proxies and their definitions.</span></span> <span data-ttu-id="ce04a-188">Opcionalmente, você pode referenciar um [esquema JSON](http://json.schemastore.org/proxies) para o preenchimento do código, caso seu editor dê suporte a isso.</span><span class="sxs-lookup"><span data-stu-id="ce04a-188">Optionally, if your editor supports it, you can reference a [JSON schema](http://json.schemastore.org/proxies) for code completion.</span></span> <span data-ttu-id="ce04a-189">Um exemplo de arquivo pode parecer Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce04a-189">An example file might look like hello following:</span></span>

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

<span data-ttu-id="ce04a-190">Cada proxy tem um nome amigável, como *proxy1* em Olá anterior de exemplo.</span><span class="sxs-lookup"><span data-stu-id="ce04a-190">Each proxy has a friendly name, such as *proxy1* in hello preceding example.</span></span> <span data-ttu-id="ce04a-191">objeto de definição de proxy correspondente Olá é definido pela Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce04a-191">hello corresponding proxy definition object is defined by hello following properties:</span></span>

* <span data-ttu-id="ce04a-192">**matchCondition**: necessário – um objeto que define as solicitações de saudação que disparam execução Olá desse proxy.</span><span class="sxs-lookup"><span data-stu-id="ce04a-192">**matchCondition**: Required--an object defining hello requests that trigger hello execution of this proxy.</span></span> <span data-ttu-id="ce04a-193">Ele contém duas propriedades compartilhadas com [HTTP gatilhos]:</span><span class="sxs-lookup"><span data-stu-id="ce04a-193">It contains two properties that are shared with [HTTP triggers]:</span></span>
    * <span data-ttu-id="ce04a-194">_métodos_: uma matriz de métodos de saudação HTTP que Olá proxy responde.</span><span class="sxs-lookup"><span data-stu-id="ce04a-194">_methods_: An array of hello HTTP methods that hello proxy responds to.</span></span> <span data-ttu-id="ce04a-195">Se não for especificado, o proxy de saudação responde tooall métodos HTTP na rota de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce04a-195">If it is not specified, hello proxy responds tooall HTTP methods on hello route.</span></span>
    * <span data-ttu-id="ce04a-196">_rota_: exigido-- define o modelo de rota hello, controlar qual solicitação URLs seu proxy responde.</span><span class="sxs-lookup"><span data-stu-id="ce04a-196">_route_: Required--defines hello route template, controlling which request URLs your proxy responds to.</span></span> <span data-ttu-id="ce04a-197">Ao contrário de disparadores HTTP, não há nenhum valor padrão.</span><span class="sxs-lookup"><span data-stu-id="ce04a-197">Unlike in HTTP triggers, there is no default value.</span></span>
* <span data-ttu-id="ce04a-198">**backendUri**: Olá URL de solicitação de Olá Olá recursos de back-end toowhich deve usar o proxy.</span><span class="sxs-lookup"><span data-stu-id="ce04a-198">**backendUri**: hello URL of hello back-end resource toowhich hello request should be proxied.</span></span> <span data-ttu-id="ce04a-199">Esse valor pode referenciar parâmetros e configurações do aplicativo da solicitação de cliente original hello.</span><span class="sxs-lookup"><span data-stu-id="ce04a-199">This value can reference application settings and parameters from hello original client request.</span></span> <span data-ttu-id="ce04a-200">Se esta propriedade não for incluída, o Azure Functions responderá com um HTTP 200 OK.</span><span class="sxs-lookup"><span data-stu-id="ce04a-200">If this property is not included, Azure Functions responds with an HTTP 200 OK.</span></span>
* <span data-ttu-id="ce04a-201">**requestOverrides**: um objeto que define a solicitação de back-end toohello transformações.</span><span class="sxs-lookup"><span data-stu-id="ce04a-201">**requestOverrides**: An object that defines transformations toohello back-end request.</span></span> <span data-ttu-id="ce04a-202">Confira [definir um objeto requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="ce04a-202">See [Define a requestOverrides object].</span></span>
* <span data-ttu-id="ce04a-203">**responseOverrides**: um objeto que define a resposta de cliente toohello transformações.</span><span class="sxs-lookup"><span data-stu-id="ce04a-203">**responseOverrides**: An object that defines transformations toohello client response.</span></span> <span data-ttu-id="ce04a-204">Confira [definir um objeto responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="ce04a-204">See [Define a responseOverrides object].</span></span>

> [!NOTE] 
> <span data-ttu-id="ce04a-205">propriedade de rota Olá Proxies de funções do Azure não aceita a propriedade de routePrefix Olá Olá funções da configuração do host.</span><span class="sxs-lookup"><span data-stu-id="ce04a-205">hello route property Azure Functions Proxies does not honor hello routePrefix property of hello Functions host configuration.</span></span> <span data-ttu-id="ce04a-206">Se você quiser tooinclude um prefixo, como /api, ela deve ser incluída na propriedade de rota hello.</span><span class="sxs-lookup"><span data-stu-id="ce04a-206">If you want tooinclude a prefix such as /api, it must be included in hello route property.</span></span>

### <span data-ttu-id="ce04a-207"><a name="requestOverrides"></a>Definir um objeto requestOverrides</span><span class="sxs-lookup"><span data-stu-id="ce04a-207"><a name="requestOverrides"></a>Define a requestOverrides object</span></span>

<span data-ttu-id="ce04a-208">objeto de requestOverrides de saudação define as alterações feitas a solicitação toohello quando recursos de back-end de saudação é chamado.</span><span class="sxs-lookup"><span data-stu-id="ce04a-208">hello requestOverrides object defines changes made toohello request when hello back-end resource is called.</span></span> <span data-ttu-id="ce04a-209">objeto de saudação é definido pela Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce04a-209">hello object is defined by hello following properties:</span></span>

* <span data-ttu-id="ce04a-210">**backend.Request.Method**: Olá método HTTP que foi usado o back-end de saudação toocall.</span><span class="sxs-lookup"><span data-stu-id="ce04a-210">**backend.request.method**: hello HTTP method that's used toocall hello back end.</span></span>
* <span data-ttu-id="ce04a-211">**backend.Request.QueryString. \<ParameterName\>**: um parâmetro de cadeia de caracteres de consulta que pode ser definido para Olá chamada toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="ce04a-211">**backend.request.querystring.\<ParameterName\>**: A query string parameter that can be set for hello call toohello back end.</span></span> <span data-ttu-id="ce04a-212">Substituir  *\<ParameterName\>*  com o nome de saudação do parâmetro hello que você deseja tooset.</span><span class="sxs-lookup"><span data-stu-id="ce04a-212">Replace *\<ParameterName\>* with hello name of hello parameter that you want tooset.</span></span> <span data-ttu-id="ce04a-213">Se a cadeia de caracteres vazia Olá for fornecida, o parâmetro hello não está incluído na solicitação de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce04a-213">If hello empty string is provided, hello parameter is not included on hello back-end request.</span></span>
* <span data-ttu-id="ce04a-214">**backend.Request.Headers. \<HeaderName\>**: um cabeçalho que pode ser definido para Olá chamada toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="ce04a-214">**backend.request.headers.\<HeaderName\>**: A header that can be set for hello call toohello back end.</span></span> <span data-ttu-id="ce04a-215">Substituir  *\<HeaderName\>*  com o nome de saudação do cabeçalho de saudação que você deseja tooset.</span><span class="sxs-lookup"><span data-stu-id="ce04a-215">Replace *\<HeaderName\>* with hello name of hello header that you want tooset.</span></span> <span data-ttu-id="ce04a-216">Se você fornecer a cadeia de caracteres vazia hello, cabeçalho de saudação não está incluído na solicitação de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce04a-216">If you provide hello empty string, hello header is not included on hello back-end request.</span></span>

<span data-ttu-id="ce04a-217">Valores podem referenciar parâmetros e configurações do aplicativo da solicitação de cliente original hello.</span><span class="sxs-lookup"><span data-stu-id="ce04a-217">Values can reference application settings and parameters from hello original client request.</span></span>

<span data-ttu-id="ce04a-218">Um exemplo de configuração pode parecer com hello seguinte:</span><span class="sxs-lookup"><span data-stu-id="ce04a-218">An example configuration might look like hello following:</span></span>

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

### <span data-ttu-id="ce04a-219"><a name="responseOverrides"></a>Definir um objeto responseOverrides</span><span class="sxs-lookup"><span data-stu-id="ce04a-219"><a name="responseOverrides"></a>Define a responseOverrides object</span></span>

<span data-ttu-id="ce04a-220">objeto de requestOverrides Olá define as alterações feitas resposta toohello que passou toohello back cliente.</span><span class="sxs-lookup"><span data-stu-id="ce04a-220">hello requestOverrides object defines changes that are made toohello response that's passed back toohello client.</span></span> <span data-ttu-id="ce04a-221">objeto de saudação é definido pela Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce04a-221">hello object is defined by hello following properties:</span></span>

* <span data-ttu-id="ce04a-222">**response.statusCode**: Olá HTTP toobe de código de status retornado toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="ce04a-222">**response.statusCode**: hello HTTP status code toobe returned toohello client.</span></span>
* <span data-ttu-id="ce04a-223">**response.statusReason**: toobe de frase de motivo Olá HTTP retornado toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="ce04a-223">**response.statusReason**: hello HTTP reason phrase toobe returned toohello client.</span></span>
* <span data-ttu-id="ce04a-224">**Response.body**: representação de cadeia de caracteres de saudação do hello corpo toobe retornado toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="ce04a-224">**response.body**: hello string representation of hello body toobe returned toohello client.</span></span>
* <span data-ttu-id="ce04a-225">**Response.Headers. \<HeaderName\>**: um cabeçalho que pode ser definido para o cliente do hello resposta toohello.</span><span class="sxs-lookup"><span data-stu-id="ce04a-225">**response.headers.\<HeaderName\>**: A header that can be set for hello response toohello client.</span></span> <span data-ttu-id="ce04a-226">Substituir  *\<HeaderName\>*  com o nome de saudação do cabeçalho de saudação que você deseja tooset.</span><span class="sxs-lookup"><span data-stu-id="ce04a-226">Replace *\<HeaderName\>* with hello name of hello header that you want tooset.</span></span> <span data-ttu-id="ce04a-227">Se você fornecer a cadeia de caracteres vazia hello, cabeçalho de saudação não está incluído na resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce04a-227">If you provide hello empty string, hello header is not included on hello response.</span></span>

<span data-ttu-id="ce04a-228">Valores podem referenciar as configurações do aplicativo, parâmetros de solicitação de cliente original hello e parâmetros da resposta de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce04a-228">Values can reference application settings, parameters from hello original client request, and parameters from hello back-end response.</span></span>

<span data-ttu-id="ce04a-229">Um exemplo de configuração pode parecer com hello seguinte:</span><span class="sxs-lookup"><span data-stu-id="ce04a-229">An example configuration might look like hello following:</span></span>

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
> <span data-ttu-id="ce04a-230">Neste exemplo, o corpo de hello está sendo definido diretamente, portanto não `backendUri` propriedade é necessária.</span><span class="sxs-lookup"><span data-stu-id="ce04a-230">In this example, hello body is being set directly, so no `backendUri` property is needed.</span></span> <span data-ttu-id="ce04a-231">exemplo Hello mostra como você pode usar Proxies de funções do Azure para APIs de simulação.</span><span class="sxs-lookup"><span data-stu-id="ce04a-231">hello example shows how you might use Azure Functions Proxies for mocking APIs.</span></span>

[portal do Azure]: https://portal.azure.com
[HTTP gatilhos]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify hello back-end request]: #modify-backend-request
[Modify hello response]: #modify-response
[definir um objeto requestOverrides]: #requestOverrides
[definir um objeto responseOverrides]: #responseOverrides
[configurações do aplicativo]: #use-appsettings
[Usar variáveis]: #using-variables
[parâmetros da solicitação de cliente original Olá]: #request-parameters
[parâmetros de resposta de back-end Olá]: #response-parameters
