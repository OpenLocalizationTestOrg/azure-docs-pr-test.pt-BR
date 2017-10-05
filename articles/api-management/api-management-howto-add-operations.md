---
title: "Como adicionar operações a uma API no Gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba como adicionar operações a uma API no Gerenciamento de API do Azure."
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
ms.openlocfilehash: 105fc51c2d1152a40a5757985da47330e0b7b8cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-operations-to-an-api-in-azure-api-management"></a><span data-ttu-id="2b99c-103">Como adicionar operações a uma API no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="2b99c-103">How to add operations to an API in Azure API Management</span></span>
<span data-ttu-id="2b99c-104">Antes que uma API no Gerenciamento de API possa ser usada, as operações devem ser adicionadas.</span><span class="sxs-lookup"><span data-stu-id="2b99c-104">Before an API in API Management can be used, operations must be added.</span></span> <span data-ttu-id="2b99c-105">Este guia mostra como adicionar e configurar tipos diferentes de operações para uma API em Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="2b99c-105">This guide shows how to add and configure different types of operations to an API in API Management.</span></span>

## <span data-ttu-id="2b99c-106"><a name="add-operation"> </a>Adicionar uma operação</span><span class="sxs-lookup"><span data-stu-id="2b99c-106"><a name="add-operation"> </a>Add an operation</span></span>
<span data-ttu-id="2b99c-107">Operações são adicionadas e configuradas em uma API no Portal do editor.</span><span class="sxs-lookup"><span data-stu-id="2b99c-107">Operations are added and configured to an API in the publisher portal.</span></span> <span data-ttu-id="2b99c-108">Para acessar o portal do editor, clique em **Portal do editor** no Portal do Azure para acessar o serviço Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="2b99c-108">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Portal do editor][api-management-management-console]

> <span data-ttu-id="2b99c-110">Se ainda não criou uma instância de serviço de Gerenciamento de API, confira [Criar uma instância de serviço de Gerenciamento de API][Create an API Management service instance] no tutorial [Introdução ao Gerenciamento de API do Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="2b99c-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="2b99c-111">Selecione a API desejada no Portal do editor e então selecione a guia **Operações** .</span><span class="sxs-lookup"><span data-stu-id="2b99c-111">Select the desired API in the publisher portal and then select the **Operations** tab.</span></span> 

![Operações][api-management-operations]

<span data-ttu-id="2b99c-113">Clique em **Adicionar operação** para adicionar uma nova operação.</span><span class="sxs-lookup"><span data-stu-id="2b99c-113">Click **Add Operation** to add a new operation.</span></span> <span data-ttu-id="2b99c-114">A janela **Nova operação** será exibida e a guia **Assinatura** será selecionada por padrão.</span><span class="sxs-lookup"><span data-stu-id="2b99c-114">The **New operation** will be displayed and the **Signature** tab will be selected by default.</span></span>

![Adicionar operação][api-management-add-operation]

<span data-ttu-id="2b99c-116">Especifique o **verbo HTTP** escolhendo na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="2b99c-116">Specify the **HTTP verb** by choosing from the drop-down list.</span></span>

![Método HTTP][api-management-http-method]

<a name="url-template"></a>

<span data-ttu-id="2b99c-118">Defina o modelo do URL digitando um fragmento de URL consistindo de um ou mais segmentos de caminho URL e nenhum ou mais parâmetros de cadeia de consulta.</span><span class="sxs-lookup"><span data-stu-id="2b99c-118">Define the URL template by typing in a URL fragment consisting of one or more URL path segments and zero or more query string parameters.</span></span> <span data-ttu-id="2b99c-119">O modelo do URL, anexado ao URL base da API, identifica uma única operação HTTP.</span><span class="sxs-lookup"><span data-stu-id="2b99c-119">The URL template, appended to the base URL of the API, identifies a single HTTP operation.</span></span> <span data-ttu-id="2b99c-120">Ele pode conter uma ou mais partes variáveis nomeadas que são identificadas por chaves.</span><span class="sxs-lookup"><span data-stu-id="2b99c-120">It may contain one or more named variable parts that are identified by curly braces.</span></span> <span data-ttu-id="2b99c-121">Essas partes variáveis se chamam parâmetros de modelo, que são valores atribuídos dinamicamente e extraídos do URL da solicitação quando a solicitação está sendo processada pela plataforma de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="2b99c-121">These variable parts are called template parameters and are dynamically assigned values extracted from the request's URL when the request is being processed by the API Management platform.</span></span>

> <span data-ttu-id="2b99c-122">O modelo de URL pode incluir padrões curingas.</span><span class="sxs-lookup"><span data-stu-id="2b99c-122">The URL template can include wildcard patterns.</span></span> <span data-ttu-id="2b99c-123">Por exemplo, especificar `/*` encaminha todas as solicitações para esse método HTTP para o serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="2b99c-123">For example, specifying `/*` will forward all requests for that HTTP method to the back end service.</span></span>

![Modelo do URL][api-management-url-template]

<a name="rewrite-url-template"></a>

<span data-ttu-id="2b99c-125">Se desejar, especifique **Reescrever modelo de URL**.</span><span class="sxs-lookup"><span data-stu-id="2b99c-125">If desired, specify the **Rewrite URL template**.</span></span> <span data-ttu-id="2b99c-126">Isso permite que você use o modelo de URL padrão para processar solicitações de entrada no front-end, enquanto chama o back-end por meio de um URL convertido de acordo com o modelo reescrito.</span><span class="sxs-lookup"><span data-stu-id="2b99c-126">This allows you to use the standard URL template for processing incoming requests on the front-end, while calling the back-end via a converted URL according to the rewrite template.</span></span> <span data-ttu-id="2b99c-127">Os parâmetros de modelo do modelo de URL devem ser usados no modelo reescrito.</span><span class="sxs-lookup"><span data-stu-id="2b99c-127">Template parameters from the URL template should be used in the rewrite template.</span></span> <span data-ttu-id="2b99c-128">O exemplo a seguir mostra como o tipo de conteúdo codificado como um segmento de caminho no serviço Web do exemplo anterior pode ser fornecido como parâmetro de consulta na API publicada por meio da plataforma de Gerenciamento de API usando os modelos de URL.</span><span class="sxs-lookup"><span data-stu-id="2b99c-128">The following example shows how content type encoded as path segment in the web service from the previous example can be provided as a query parameter in the API published via the API Management platform using the URL templates.</span></span>

![Modelo de URL reescrito][api-management-url-template-rewrite]

<span data-ttu-id="2b99c-130">Quem chamar a operação utilizará o formato `/customers?customerid=ALFKI` e ele será mapeado para `/Customers('ALFKI')` quando o serviço de back-end for invocado.</span><span class="sxs-lookup"><span data-stu-id="2b99c-130">Callers to the operation will use the format `/customers?customerid=ALFKI` and this will be mapped to `/Customers('ALFKI')` when the back-end service is invoked.</span></span>

<span data-ttu-id="2b99c-131">O Nome de **exibição** e a **Descrição** oferecem uma descrição da operação e são usados para fornecer documentação aos desenvolvedores que utilizam essa API no portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="2b99c-131">**Display** name and **Description** provide a description of the operation and are used to provide documentation to the developers using this API in the developer portal.</span></span>

![Descrição][api-management-description]

<span data-ttu-id="2b99c-133">A descrição da operação pode ser especificada como texto sem formatação ou HTML na caixa de texto **Descrição** .</span><span class="sxs-lookup"><span data-stu-id="2b99c-133">The operation description can be specified as plain text or HTML in the **Description** text box.</span></span>

## <span data-ttu-id="2b99c-134"><a name="operation-caching"> </a>Cache da operação</span><span class="sxs-lookup"><span data-stu-id="2b99c-134"><a name="operation-caching"> </a>Operation caching</span></span>
<span data-ttu-id="2b99c-135">O cache de respostas reduz a latência percebida pelos consumidores da API, reduz a largura de banda e diminui a carga no serviço Web HTTP que está implementando a API.</span><span class="sxs-lookup"><span data-stu-id="2b99c-135">Response caching reduces latency perceived by the API consumers, lowers bandwidth consumption and decreases the load on the HTTP web service implementing the API.</span></span> 

<span data-ttu-id="2b99c-136">Para habilitar o cache para a operação de modo fácil e rápido, selecione a guia **Caching** e marque a caixa de seleção **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="2b99c-136">To easily and quickly enable caching for the operation, select the **Caching** tab and check the **Enable** checkbox.</span></span>

![Cache][api-management-caching-tab]

<span data-ttu-id="2b99c-138">**Duração** especifica o período de tempo durante o qual a resposta da operação permanece armazenada em cache.</span><span class="sxs-lookup"><span data-stu-id="2b99c-138">**Duration** specifies the time period during which the operation response remains in the cache.</span></span> <span data-ttu-id="2b99c-139">O valor padrão é 3.600 segundos, ou uma hora.</span><span class="sxs-lookup"><span data-stu-id="2b99c-139">The default value is 3600 seconds or 1 hour.</span></span>

<span data-ttu-id="2b99c-140">Chaves de cache são usadas para diferenciar as respostas, de modo que a resposta correspondente a cada chave de cache diferente tenha seu próprio valor em cache separado.</span><span class="sxs-lookup"><span data-stu-id="2b99c-140">Cache keys are used to differentiate between responses so that the response corresponding to each different cache key will get its own separate cached value.</span></span> <span data-ttu-id="2b99c-141">Outra opção é inserir parâmetros de cadeia de consulta específicos e/ou cabeçalhos HTTP a serem utilizados para computar valores de chave de cache nas caixas de texto **Variar de acordo com os parâmetros da cadeia de consulta** e **Variar de acordo com cabeçalhos**.</span><span class="sxs-lookup"><span data-stu-id="2b99c-141">Optionally, enter specific query string parameters and/or HTTP headers to be used in computing cache key values in the **Vary by query string parameters** and **Vary by headers** text boxes respectively.</span></span> <span data-ttu-id="2b99c-142">Quando nenhum é especificado, o URL de solicitação completo e os seguintes valores de cabeçalho HTTP são usados para gerar a chave de cache: **Accept** e **Accept-Charset**.</span><span class="sxs-lookup"><span data-stu-id="2b99c-142">When none are specified, full request URL and the following HTTP header values are used in cache key generation: **Accept** and **Accept-Charset**.</span></span>

> <span data-ttu-id="2b99c-143">Para obter mais informações sobre cache e políticas de cache, consulte [Como armazenar em cache os resultados de operações no Gerenciamento de API do Azure][How to cache operation results in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="2b99c-143">For more information on caching and caching policies, see [How to cache operation results in Azure API Management][How to cache operation results in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="2b99c-144"><a name="request-parameters"> </a>Parâmetros da solicitação</span><span class="sxs-lookup"><span data-stu-id="2b99c-144"><a name="request-parameters"> </a>Request parameters</span></span>
<span data-ttu-id="2b99c-145">Os parâmetros da operação são gerenciados na guia Parâmetros.</span><span class="sxs-lookup"><span data-stu-id="2b99c-145">Operation parameters are managed on the Parameters tab.</span></span> <span data-ttu-id="2b99c-146">Parâmetros especificados no **Modelo do URL**, na guia **Assinatura**, são adicionados automaticamente e somente podem ser alterados editando o modelo do URL.</span><span class="sxs-lookup"><span data-stu-id="2b99c-146">Parameters specified in the **URL Template** on the **Signature** tab are added automatically and can be changed only by editing the URL template.</span></span> <span data-ttu-id="2b99c-147">Parâmetros adicionais podem ser inseridos manualmente.</span><span class="sxs-lookup"><span data-stu-id="2b99c-147">Additional parameters can be entered manually.</span></span>

<span data-ttu-id="2b99c-148">Para adicionar um novo parâmetro de consulta, clique em **Adicionar parâmetro de consulta** e insira as informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="2b99c-148">To add a new query parameter, click **Add Query Parameter** and enter the following information:</span></span>

* <span data-ttu-id="2b99c-149">**Nome** - nome do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="2b99c-149">**Name** - parameter name.</span></span>
* <span data-ttu-id="2b99c-150">**Descrição** - uma breve descrição do parâmetro (opcional).</span><span class="sxs-lookup"><span data-stu-id="2b99c-150">**Description** - a brief description of the parameter (optional).</span></span>
* <span data-ttu-id="2b99c-151">**Tipo** - tipo do parâmetro, selecionado no menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="2b99c-151">**Type** - parameter type, selected in the drop down.</span></span>
* <span data-ttu-id="2b99c-152">**Valores** - valores que podem ser atribuídos a esse parâmetro.</span><span class="sxs-lookup"><span data-stu-id="2b99c-152">**Values** - values that can be assigned to this parameter.</span></span> <span data-ttu-id="2b99c-153">Um dos valores pode ser marcado como padrão (opcional).</span><span class="sxs-lookup"><span data-stu-id="2b99c-153">One of the values can be marked as default (optional).</span></span>
* <span data-ttu-id="2b99c-154">**Obrigatório** - faça com que o parâmetro seja obrigatório marcando a caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="2b99c-154">**Required** - make the parameter mandatory by checking the checkbox.</span></span> 

![Parâmetros da solicitação][api-management-request-parameters]

## <span data-ttu-id="2b99c-156"><a name="request-body"> </a>Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="2b99c-156"><a name="request-body"> </a>Request body</span></span>
<span data-ttu-id="2b99c-157">Se a operação permitir (por exemplo, PUT, POST) e precisar de um corpo, você poderá fornecer um exemplo dele em todos os formatos de representação com suporte (por exemplo, json, XML).</span><span class="sxs-lookup"><span data-stu-id="2b99c-157">If the operation allows (e.g. PUT, POST) and requires a body you may provide an example of it in all of the supported representation formats (e.g. json, XML).</span></span> 

> <span data-ttu-id="2b99c-158">O corpo da solicitação é usado somente para fins de documentação e não é validado.</span><span class="sxs-lookup"><span data-stu-id="2b99c-158">The request body is used for documentation purposes only and is not validated.</span></span>
> 
> 

<span data-ttu-id="2b99c-159">Para inserir um corpo de solicitação, vá até a guia **Corpo** .</span><span class="sxs-lookup"><span data-stu-id="2b99c-159">To enter a request body, switch to the **Body** tab.</span></span>

<span data-ttu-id="2b99c-160">Clique em **Adicionar representação**, comece a digitar o nome do tipo de conteúdo desejado (por exemplo, aplicativo/json), selecione-o no menu suspenso e cole o exemplo de corpo de solicitação desejado, no formato selecionado, na caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="2b99c-160">Click **Add Representation**, start typing desired content type name (e.g. application/json), select it in the drop-down, and paste the desired request body example in the selected format into the text box.</span></span> 

![Corpo da solicitação][api-management-request-body]

<span data-ttu-id="2b99c-162">Além de representações, você também pode especificar um texto de descrição opcional na caixa de texto **Descrição** .</span><span class="sxs-lookup"><span data-stu-id="2b99c-162">In additional to representations, you can also specify an optional text description in the **Description** text box.</span></span>

## <span data-ttu-id="2b99c-163"><a name="responses"> </a>Respostas</span><span class="sxs-lookup"><span data-stu-id="2b99c-163"><a name="responses"> </a>Responses</span></span>
<span data-ttu-id="2b99c-164">É uma prática recomendável fornecer exemplos de respostas para todos os códigos de status que a operação possa produzir.</span><span class="sxs-lookup"><span data-stu-id="2b99c-164">It is a good practice to provide examples of responses for all status codes that the operation may produce.</span></span> <span data-ttu-id="2b99c-165">Cada código de status pode ter mais de um exemplo de corpo de resposta, um para cada um dos tipos de conteúdos com suporte.</span><span class="sxs-lookup"><span data-stu-id="2b99c-165">Each status code may have more than one response body example, one for each of the supported content types.</span></span> 

<span data-ttu-id="2b99c-166">Para adicionar uma resposta, clique em **Adicionar** e comece a digitar o código de status desejado.</span><span class="sxs-lookup"><span data-stu-id="2b99c-166">To add a response, click **Add** and start typing the desired status code.</span></span> <span data-ttu-id="2b99c-167">Neste exemplo, o código de status é **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="2b99c-167">In this example the status code is **200 OK**.</span></span> <span data-ttu-id="2b99c-168">Quando o código for exibido no menu suspenso, selecione-o e o código de resposta será criado e adicionado à sua operação.</span><span class="sxs-lookup"><span data-stu-id="2b99c-168">Once the code is displayed in the drop-down, select it, and the response code is created and added to your operation.</span></span>

![Código de resposta][api-management-response-code]

<span data-ttu-id="2b99c-170">Clique em **Adicionar representação**, comece a digitar o nome do tipo de conteúdo desejado (por exemplo, aplicativo/json) e selecione-o no menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="2b99c-170">Click **Add Representation**, start typing the desired content type name (e.g. application/json) and then select it in the drop down.</span></span>

![Tipo de conteúdo do corpo][api-management-response-body-content-type]

<span data-ttu-id="2b99c-172">Copie o exemplo de corpo de resposta no formato selecionado na caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="2b99c-172">Paste the response body example in the selected format into the text box.</span></span> 

![Corpo da resposta][api-management-response-body]

<span data-ttu-id="2b99c-174">Se desejar, adicione uma descrição opcional na caixa de texto **Descrição** .</span><span class="sxs-lookup"><span data-stu-id="2b99c-174">If desired, add an optional description into the **Description** text box.</span></span>

<span data-ttu-id="2b99c-175">Após configurar a operação, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2b99c-175">Once the operation is configured, click **Save**.</span></span>

## <span data-ttu-id="2b99c-176"><a name="next-steps"> </a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2b99c-176"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="2b99c-177">Após as operações serem adicionadas a uma API, a próxima etapa é associar a API a um produto e publicá-la para que os desenvolvedores possam chamar suas operações.</span><span class="sxs-lookup"><span data-stu-id="2b99c-177">Once the operations are added to an API, the next step is to associate the API with a product and publish it so that developers can call its operations.</span></span>

* <span data-ttu-id="2b99c-178">[Como criar e publicar um produto][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="2b99c-178">[How to create and publish a product][How to create and publish a product]</span></span>

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

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to cache operation results in Azure API Management]: api-management-howto-cache.md
