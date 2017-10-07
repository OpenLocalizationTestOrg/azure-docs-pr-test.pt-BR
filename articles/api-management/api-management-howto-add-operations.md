---
title: "aaaHow tooadd operações tooan API no gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba como tooadd operações tooan API no gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 1158a023-1913-4e9c-93de-9164b672f9b3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: d57fa59a2b0ceb392cde23150a0cbb326e52d27d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-operations-tooan-api-in-azure-api-management"></a><span data-ttu-id="51de4-103">Como as operações de tooadd tooan API no gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="51de4-103">How tooadd operations tooan API in Azure API Management</span></span>
<span data-ttu-id="51de4-104">Antes que uma API no Gerenciamento de API possa ser usada, as operações devem ser adicionadas.</span><span class="sxs-lookup"><span data-stu-id="51de4-104">Before an API in API Management can be used, operations must be added.</span></span> <span data-ttu-id="51de4-105">Este guia mostra como tooadd e configurar os diferentes tipos de operações tooan API no gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="51de4-105">This guide shows how tooadd and configure different types of operations tooan API in API Management.</span></span>

## <span data-ttu-id="51de4-106"><a name="add-operation"> </a>Adicionar uma operação</span><span class="sxs-lookup"><span data-stu-id="51de4-106"><a name="add-operation"> </a>Add an operation</span></span>
<span data-ttu-id="51de4-107">As operações são adicionadas e configurados tooan API no portal do publicador Olá.</span><span class="sxs-lookup"><span data-stu-id="51de4-107">Operations are added and configured tooan API in hello publisher portal.</span></span> <span data-ttu-id="51de4-108">tooaccess Olá clique portal, publisher **portal do publicador** em hello Portal do Azure para seu serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="51de4-108">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portal do editor][api-management-management-console]

> <span data-ttu-id="51de4-110">Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="51de4-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="51de4-111">Selecione Olá desejado API no portal do publicador hello e, em seguida, selecione Olá **operações** guia.</span><span class="sxs-lookup"><span data-stu-id="51de4-111">Select hello desired API in hello publisher portal and then select hello **Operations** tab.</span></span> 

![Operações][api-management-operations]

<span data-ttu-id="51de4-113">Clique em **Adicionar operação** tooadd uma nova operação.</span><span class="sxs-lookup"><span data-stu-id="51de4-113">Click **Add Operation** tooadd a new operation.</span></span> <span data-ttu-id="51de4-114">Olá **nova operação** serão exibidas e Olá **assinatura** guia será selecionada por padrão.</span><span class="sxs-lookup"><span data-stu-id="51de4-114">hello **New operation** will be displayed and hello **Signature** tab will be selected by default.</span></span>

![Adicionar operação][api-management-add-operation]

<span data-ttu-id="51de4-116">Especifique a saudação **verbo HTTP** escolhendo na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="51de4-116">Specify hello **HTTP verb** by choosing from hello drop-down list.</span></span>

![Método HTTP][api-management-http-method]

<a name="url-template"></a>

<span data-ttu-id="51de4-118">Defina modelo de URL Olá digitando em um fragmento de URL que consiste em um ou mais segmentos de caminho de URL e zero ou mais parâmetros de cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="51de4-118">Define hello URL template by typing in a URL fragment consisting of one or more URL path segments and zero or more query string parameters.</span></span> <span data-ttu-id="51de4-119">modelo de URL Hello, toohello acrescentadas a URL base do hello API, identifica uma única operação HTTP.</span><span class="sxs-lookup"><span data-stu-id="51de4-119">hello URL template, appended toohello base URL of hello API, identifies a single HTTP operation.</span></span> <span data-ttu-id="51de4-120">Ele pode conter uma ou mais partes variáveis nomeadas que são identificadas por chaves.</span><span class="sxs-lookup"><span data-stu-id="51de4-120">It may contain one or more named variable parts that are identified by curly braces.</span></span> <span data-ttu-id="51de4-121">Essas partes variável são chamados de parâmetros de modelo e valores extraídos da URL de solicitação hello quando Olá solicitação está sendo processada pela plataforma de gerenciamento de API de saudação são atribuídos dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="51de4-121">These variable parts are called template parameters and are dynamically assigned values extracted from hello request's URL when hello request is being processed by hello API Management platform.</span></span>

> <span data-ttu-id="51de4-122">modelo de URL Olá pode incluir padrões de curinga.</span><span class="sxs-lookup"><span data-stu-id="51de4-122">hello URL template can include wildcard patterns.</span></span> <span data-ttu-id="51de4-123">Por exemplo, especificar `/*` encaminhar todas as solicitações para esse método toohello HTTP volta terminará serviço.</span><span class="sxs-lookup"><span data-stu-id="51de4-123">For example, specifying `/*` will forward all requests for that HTTP method toohello back end service.</span></span>

![Modelo do URL][api-management-url-template]

<a name="rewrite-url-template"></a>

<span data-ttu-id="51de4-125">Se desejar, especifique Olá **modelo regravar URL**.</span><span class="sxs-lookup"><span data-stu-id="51de4-125">If desired, specify hello **Rewrite URL template**.</span></span> <span data-ttu-id="51de4-126">Isso permite que você modelo de URL padrão do toouse Olá para processar as solicitações de entrada hello front-end, ao chamar hello back-end através de uma URL convertida de acordo com o toohello reconfiguração de modelo.</span><span class="sxs-lookup"><span data-stu-id="51de4-126">This allows you toouse hello standard URL template for processing incoming requests on hello front-end, while calling hello back-end via a converted URL according toohello rewrite template.</span></span> <span data-ttu-id="51de4-127">Parâmetros de modelo do modelo de URL Olá devem ser usados no modelo de regravação de saudação.</span><span class="sxs-lookup"><span data-stu-id="51de4-127">Template parameters from hello URL template should be used in hello rewrite template.</span></span> <span data-ttu-id="51de4-128">Olá exemplo a seguir mostra como conteúdo tipo codificado como o segmento de caminho no serviço da web de saudação do exemplo anterior Olá pode ser fornecido como um parâmetro de consulta em Olá API publicados por meio de saudação usando modelos de URL de saudação de plataforma de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="51de4-128">hello following example shows how content type encoded as path segment in hello web service from hello previous example can be provided as a query parameter in hello API published via hello API Management platform using hello URL templates.</span></span>

![Modelo de URL reescrito][api-management-url-template-rewrite]

<span data-ttu-id="51de4-130">Operação de toohello chamadores usará o formato de saudação `/customers?customerid=ALFKI` e isso será mapeado muito`/Customers('ALFKI')` quando o serviço de back-end de saudação é invocado.</span><span class="sxs-lookup"><span data-stu-id="51de4-130">Callers toohello operation will use hello format `/customers?customerid=ALFKI` and this will be mapped too`/Customers('ALFKI')` when hello back-end service is invoked.</span></span>

<span data-ttu-id="51de4-131">**Exibição** nome e **descrição** forneça uma descrição da operação de saudação e é usadas tooprovide documentação desenvolvedores toohello usando essa API no portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="51de4-131">**Display** name and **Description** provide a description of hello operation and are used tooprovide documentation toohello developers using this API in hello developer portal.</span></span>

![Descrição][api-management-description]

<span data-ttu-id="51de4-133">Descrição da operação Olá pode ser especificada como texto sem formatação ou HTML em Olá **descrição** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="51de4-133">hello operation description can be specified as plain text or HTML in hello **Description** text box.</span></span>

## <span data-ttu-id="51de4-134"><a name="operation-caching"> </a>Cache da operação</span><span class="sxs-lookup"><span data-stu-id="51de4-134"><a name="operation-caching"> </a>Operation caching</span></span>
<span data-ttu-id="51de4-135">Cache de resposta reduz a latência percebida pelos consumidores Olá API, reduz o consumo de largura de banda e diminui Olá carga sobre a implementação do serviço web do hello HTTP Olá API.</span><span class="sxs-lookup"><span data-stu-id="51de4-135">Response caching reduces latency perceived by hello API consumers, lowers bandwidth consumption and decreases hello load on hello HTTP web service implementing hello API.</span></span> 

<span data-ttu-id="51de4-136">tooeasily e habilitar rapidamente o cache para operação hello, selecione Olá **cache** guia e verifique Olá **habilitar** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="51de4-136">tooeasily and quickly enable caching for hello operation, select hello **Caching** tab and check hello **Enable** checkbox.</span></span>

![Cache][api-management-caching-tab]

<span data-ttu-id="51de4-138">**Duração** Especifica o período de tempo durante o qual Olá resposta de operação permanece no cache de saudação de saudação.</span><span class="sxs-lookup"><span data-stu-id="51de4-138">**Duration** specifies hello time period during which hello operation response remains in hello cache.</span></span> <span data-ttu-id="51de4-139">valor padrão de saudação é 3600 segundos ou 1 hora.</span><span class="sxs-lookup"><span data-stu-id="51de4-139">hello default value is 3600 seconds or 1 hour.</span></span>

<span data-ttu-id="51de4-140">Chaves de cache são toodifferentiate usado entre as respostas para que a resposta de saudação correspondente chave de cache diferentes tooeach obterá seu próprio valor armazenado em cache separado.</span><span class="sxs-lookup"><span data-stu-id="51de4-140">Cache keys are used toodifferentiate between responses so that hello response corresponding tooeach different cache key will get its own separate cached value.</span></span> <span data-ttu-id="51de4-141">Opcionalmente, insira parâmetros de cadeia de caracteres de consulta específicos e/ou toobe de cabeçalhos HTTP usada no cálculo de valores de chave de cache em Olá **variar por parâmetros de cadeia de caracteres de consulta** e **variam por cabeçalhos** nas caixas de texto respectivamente.</span><span class="sxs-lookup"><span data-stu-id="51de4-141">Optionally, enter specific query string parameters and/or HTTP headers toobe used in computing cache key values in hello **Vary by query string parameters** and **Vary by headers** text boxes respectively.</span></span> <span data-ttu-id="51de4-142">Quando nenhum é especificado, o total de solicitação de URL e Olá valores de cabeçalho HTTP a seguir é usado na geração de chave de cache: **aceitar** e **Accept-Charset**.</span><span class="sxs-lookup"><span data-stu-id="51de4-142">When none are specified, full request URL and hello following HTTP header values are used in cache key generation: **Accept** and **Accept-Charset**.</span></span>

> <span data-ttu-id="51de4-143">Para obter mais informações sobre o cache e cache de políticas, consulte [como os resultados de operação toocache no gerenciamento de API do Azure][How toocache operation results in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="51de4-143">For more information on caching and caching policies, see [How toocache operation results in Azure API Management][How toocache operation results in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="51de4-144"><a name="request-parameters"> </a>Parâmetros da solicitação</span><span class="sxs-lookup"><span data-stu-id="51de4-144"><a name="request-parameters"> </a>Request parameters</span></span>
<span data-ttu-id="51de4-145">Parâmetros de operação são gerenciados na guia parâmetros de saudação. Parâmetros especificados na Olá **modelo de URL** em Olá **assinatura** guia são adicionados automaticamente e podem ser alteradas somente com a edição do modelo de URL hello.</span><span class="sxs-lookup"><span data-stu-id="51de4-145">Operation parameters are managed on hello Parameters tab. Parameters specified in hello **URL Template** on hello **Signature** tab are added automatically and can be changed only by editing hello URL template.</span></span> <span data-ttu-id="51de4-146">Parâmetros adicionais podem ser inseridos manualmente.</span><span class="sxs-lookup"><span data-stu-id="51de4-146">Additional parameters can be entered manually.</span></span>

<span data-ttu-id="51de4-147">tooadd um novo parâmetro de consulta, clique em **Adicionar parâmetro de consulta** e digite Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="51de4-147">tooadd a new query parameter, click **Add Query Parameter** and enter hello following information:</span></span>

* <span data-ttu-id="51de4-148">**Nome** - nome do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="51de4-148">**Name** - parameter name.</span></span>
* <span data-ttu-id="51de4-149">**Descrição** -uma breve descrição do parâmetro hello (opcional).</span><span class="sxs-lookup"><span data-stu-id="51de4-149">**Description** - a brief description of hello parameter (optional).</span></span>
* <span data-ttu-id="51de4-150">**Tipo** -tipo de parâmetro selecionado na saudação da lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="51de4-150">**Type** - parameter type, selected in hello drop down.</span></span>
* <span data-ttu-id="51de4-151">**Valores** -valores que podem ser atribuídos toothis parâmetro.</span><span class="sxs-lookup"><span data-stu-id="51de4-151">**Values** - values that can be assigned toothis parameter.</span></span> <span data-ttu-id="51de4-152">Um dos valores de saudação pode ser marcado como padrão (opcional).</span><span class="sxs-lookup"><span data-stu-id="51de4-152">One of hello values can be marked as default (optional).</span></span>
* <span data-ttu-id="51de4-153">**Necessário** -tornar o parâmetro hello obrigatório, marcando a caixa de seleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="51de4-153">**Required** - make hello parameter mandatory by checking hello checkbox.</span></span> 

![Parâmetros da solicitação][api-management-request-parameters]

## <span data-ttu-id="51de4-155"><a name="request-body"> </a>Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="51de4-155"><a name="request-body"> </a>Request body</span></span>
<span data-ttu-id="51de4-156">Se a operação Olá permite (por exemplo, PUT, POST) e requer um corpo que você pode fornecer um exemplo dele em todos os Olá suporte para formatos de representação (por exemplo, json, XML).</span><span class="sxs-lookup"><span data-stu-id="51de4-156">If hello operation allows (e.g. PUT, POST) and requires a body you may provide an example of it in all of hello supported representation formats (e.g. json, XML).</span></span> 

> <span data-ttu-id="51de4-157">corpo da solicitação Olá é usado para fins de documentação somente e não é validado.</span><span class="sxs-lookup"><span data-stu-id="51de4-157">hello request body is used for documentation purposes only and is not validated.</span></span>
> 
> 

<span data-ttu-id="51de4-158">tooenter um corpo de solicitação, alternar toohello **corpo** guia.</span><span class="sxs-lookup"><span data-stu-id="51de4-158">tooenter a request body, switch toohello **Body** tab.</span></span>

<span data-ttu-id="51de4-159">Clique em **Adicionar representação**, comece a digitar o nome do tipo de conteúdo desejado (por exemplo, application/json), selecione-o no hello suspenso e colar Olá desejado exemplo de corpo de solicitação no formato de saudação selecionado na caixa de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="51de4-159">Click **Add Representation**, start typing desired content type name (e.g. application/json), select it in hello drop-down, and paste hello desired request body example in hello selected format into hello text box.</span></span> 

![Corpo da solicitação][api-management-request-body]

<span data-ttu-id="51de4-161">Em toorepresentations adicionais, você também pode especificar uma descrição de texto opcional na Olá **descrição** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="51de4-161">In additional toorepresentations, you can also specify an optional text description in hello **Description** text box.</span></span>

## <span data-ttu-id="51de4-162"><a name="responses"> </a>Respostas</span><span class="sxs-lookup"><span data-stu-id="51de4-162"><a name="responses"> </a>Responses</span></span>
<span data-ttu-id="51de4-163">Exemplos de tooprovide uma boa prática de respostas para todos os códigos de status que pode produzir operação Olá é.</span><span class="sxs-lookup"><span data-stu-id="51de4-163">It is a good practice tooprovide examples of responses for all status codes that hello operation may produce.</span></span> <span data-ttu-id="51de4-164">Cada código de status pode ter mais de um exemplo de corpo de resposta, uma para cada Olá suporte para tipos de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="51de4-164">Each status code may have more than one response body example, one for each of hello supported content types.</span></span> 

<span data-ttu-id="51de4-165">tooadd uma resposta, clique em **adicionar** e comece a digitar o código de status de saudação desejado.</span><span class="sxs-lookup"><span data-stu-id="51de4-165">tooadd a response, click **Add** and start typing hello desired status code.</span></span> <span data-ttu-id="51de4-166">Esse status do exemplo hello código é **200 Okey**.</span><span class="sxs-lookup"><span data-stu-id="51de4-166">In this example hello status code is **200 OK**.</span></span> <span data-ttu-id="51de4-167">Depois que o código de saudação é exibido na lista suspensa hello, selecioná-la e o código de resposta de saudação é criado e adicionado tooyour operação.</span><span class="sxs-lookup"><span data-stu-id="51de4-167">Once hello code is displayed in hello drop-down, select it, and hello response code is created and added tooyour operation.</span></span>

![Código de resposta][api-management-response-code]

<span data-ttu-id="51de4-169">Clique em **Adicionar representação**, comece a digitar o nome de tipo de conteúdo desejado hello (por exemplo, application/json) e, em seguida, selecione no hello lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="51de4-169">Click **Add Representation**, start typing hello desired content type name (e.g. application/json) and then select it in hello drop down.</span></span>

![Tipo de conteúdo do corpo][api-management-response-body-content-type]

<span data-ttu-id="51de4-171">Cole o exemplo de corpo de resposta hello no formato selecionado Olá na caixa de texto de hello.</span><span class="sxs-lookup"><span data-stu-id="51de4-171">Paste hello response body example in hello selected format into hello text box.</span></span> 

![Corpo da resposta][api-management-response-body]

<span data-ttu-id="51de4-173">Se desejar, adicione uma descrição opcional para Olá **descrição** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="51de4-173">If desired, add an optional description into hello **Description** text box.</span></span>

<span data-ttu-id="51de4-174">Após configurar a operação de saudação, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="51de4-174">Once hello operation is configured, click **Save**.</span></span>

## <span data-ttu-id="51de4-175"><a name="next-steps"> </a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="51de4-175"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="51de4-176">Quando as operações de saudação são adicionadas tooan API, o hello próxima etapa é tooassociate hello API com um produto e publicá-lo para que os desenvolvedores podem chamar suas operações.</span><span class="sxs-lookup"><span data-stu-id="51de4-176">Once hello operations are added tooan API, hello next step is tooassociate hello API with a product and publish it so that developers can call its operations.</span></span>

* <span data-ttu-id="51de4-177">[Como toocreate e publicar um produto][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="51de4-177">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
