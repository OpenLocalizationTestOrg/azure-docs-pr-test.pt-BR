---
title: "Políticas no Gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba mais sobre as políticas disponíveis para uso no Gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 1cc460cb-8e67-41aa-bc76-bbafc1892798
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 485dc3a87a81dc67f5144596a30d498293d6b76a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-policies"></a><span data-ttu-id="8a187-103">Políticas de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="8a187-103">API Management policies</span></span>
<span data-ttu-id="8a187-104">Esta seção fornece uma referência para as políticas de Gerenciamento de API a seguir.</span><span class="sxs-lookup"><span data-stu-id="8a187-104">This section provides a reference for the following API Management policies.</span></span> <span data-ttu-id="8a187-105">Para obter mais informações sobre como adicionar e configurar políticas, consulte [Políticas de Gerenciamento de API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="8a187-105">For information on adding and configuring policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
  
 <span data-ttu-id="8a187-106">As políticas são um recurso poderoso do sistema que permitem ao editor alterar o comportamento da API por meio de configuração.</span><span class="sxs-lookup"><span data-stu-id="8a187-106">Policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="8a187-107">As políticas são um conjunto de instruções executadas em sequência, no momento da solicitação ou da resposta de uma API.</span><span class="sxs-lookup"><span data-stu-id="8a187-107">Policies are a collection of Statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="8a187-108">Instruções populares incluem a conversão do formato de XML para JSON e limite de taxa de chamada para restringir a quantidade de chamadas recebidas de um desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="8a187-108">Popular Statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer.</span></span> <span data-ttu-id="8a187-109">Muitas políticas estão disponíveis pré-configuradas.</span><span class="sxs-lookup"><span data-stu-id="8a187-109">Many more policies are available out of the box.</span></span>  
  
 <span data-ttu-id="8a187-110">Expressões de política podem ser usadas como valores de atributo ou texto em qualquer uma das políticas de Gerenciamento de API, a menos que a política especifique o contrário.</span><span class="sxs-lookup"><span data-stu-id="8a187-110">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="8a187-111">Algumas políticas, como [Controlar fluxo](api-management-advanced-policies.md#choose) e [Definir variável](api-management-advanced-policies.md#set-variable) se baseiam em expressões de políticas.</span><span class="sxs-lookup"><span data-stu-id="8a187-111">Some policies such as the [Control flow](api-management-advanced-policies.md#choose) and [Set variable](api-management-advanced-policies.md#set-variable) policies are based on policy expressions.</span></span> <span data-ttu-id="8a187-112">Para obter mais informações, confira [Políticas avançadas](api-management-advanced-policies.md#AdvancedPolicies) e [Expressões de política](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="8a187-112">For more information, see [Advanced policies](api-management-advanced-policies.md#AdvancedPolicies) and [Policy expressions](api-management-policy-expressions.md).</span></span>  
  
##  <span data-ttu-id="8a187-113"><a name="ProxyPolicies"></a> Políticas</span><span class="sxs-lookup"><span data-stu-id="8a187-113"><a name="ProxyPolicies"></a> Policies</span></span>  
  
-   [<span data-ttu-id="8a187-114">Políticas de restrição de acesso</span><span class="sxs-lookup"><span data-stu-id="8a187-114">Access restriction policies</span></span>](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   <span data-ttu-id="8a187-115">[Verificar cabeçalho HTTP](api-management-access-restriction-policies.md#CheckHTTPHeader) - Impõe a existência e/ou valor de um cabeçalho HTTP.</span><span class="sxs-lookup"><span data-stu-id="8a187-115">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
    -   <span data-ttu-id="8a187-116">[Limitar a taxa de chamada por assinatura](api-management-access-restriction-policies.md#LimitCallRate) - Previne picos de uso da API limitando a taxa de chamada, baseado em assinatura.</span><span class="sxs-lookup"><span data-stu-id="8a187-116">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="8a187-117">[Limitar a taxa de chamada por chave](api-management-access-restriction-policies.md#LimitCallRateByKey) - Previne picos de uso da API limitando a taxa de chamada, baseado em chave.</span><span class="sxs-lookup"><span data-stu-id="8a187-117">[Limit call rate by key](api-management-access-restriction-policies.md#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="8a187-118">[Restringir IP do autor da chamada](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filtra (permite/recusa) chamadas de endereços IP específicos e/ou intervalos de endereços.</span><span class="sxs-lookup"><span data-stu-id="8a187-118">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
    -   <span data-ttu-id="8a187-119">[Definir a cota de uso por assinatura](api-management-access-restriction-policies.md#SetUsageQuota) - Permite que você aplique uma cota renovável ou permanente de volume de chamada e/ou largura de banda, baseado em assinatura.</span><span class="sxs-lookup"><span data-stu-id="8a187-119">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="8a187-120">[Definir a cota de uso por chave](api-management-access-restriction-policies.md#SetUsageQuotaByKey) - Permite que você aplique uma cota renovável ou permanente de volume de chamada e/ou largura de banda, baseado em chave.</span><span class="sxs-lookup"><span data-stu-id="8a187-120">[Set usage quota by key](api-management-access-restriction-policies.md#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="8a187-121">[Validar JWT](api-management-access-restriction-policies.md#ValidateJWT) - Impõe a existência e a validade de JWT extraída de um cabeçalho HTTP especificado ou um parâmetro de consulta especificado.</span><span class="sxs-lookup"><span data-stu-id="8a187-121">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
-   [<span data-ttu-id="8a187-122">Políticas avançadas</span><span class="sxs-lookup"><span data-stu-id="8a187-122">Advanced policies</span></span>](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   <span data-ttu-id="8a187-123">[Fluxo de controle](api-management-advanced-policies.md#choose): aplica condicionalmente declarações de política com base na avaliação de expressões boolianas.</span><span class="sxs-lookup"><span data-stu-id="8a187-123">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on the evaluation of Boolean expressions.</span></span>  
  
    -   <span data-ttu-id="8a187-124">[Encaminhar solicitação](api-management-advanced-policies.md#ForwardRequest) -Encaminha a solicitação ao serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="8a187-124">[Forward request](api-management-advanced-policies.md#ForwardRequest) - Forwards the request to the backend service.</span></span>  
  
    -   <span data-ttu-id="8a187-125">[Registrar em log no Hub de Eventos](api-management-advanced-policies.md#log-to-eventhub): envia mensagens no formato especificado para um destino de mensagem definido por uma entidade Agente.</span><span class="sxs-lookup"><span data-stu-id="8a187-125">[Log to Event Hub](api-management-advanced-policies.md#log-to-eventhub) - Sends messages in the specified format to a message target defined by a Logger entity.</span></span>  
  
    -   <span data-ttu-id="8a187-126">[Repetir](api-management-advanced-policies.md#Retry) - repete a execução das instruções de política, se e até que a condição seja atendida.</span><span class="sxs-lookup"><span data-stu-id="8a187-126">[Retry](api-management-advanced-policies.md#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="8a187-127">A execução será repetida em intervalos de tempo especificados até e a contagem de repetições especificada.</span><span class="sxs-lookup"><span data-stu-id="8a187-127">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>  
  
    -   <span data-ttu-id="8a187-128">[Retornar resposta](api-management-advanced-policies.md#ReturnResponse) - Anula a execução de pipeline e retorna a resposta especificada diretamente para o autor da chamada.</span><span class="sxs-lookup"><span data-stu-id="8a187-128">[Return response](api-management-advanced-policies.md#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span>  
  
    -   <span data-ttu-id="8a187-129">[Enviar solicitação unidirecional](api-management-advanced-policies.md#SendOneWayRequest) - Envia uma solicitação para a URL especificada sem aguardar uma resposta.</span><span class="sxs-lookup"><span data-stu-id="8a187-129">[Send one way request](api-management-advanced-policies.md#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>  
  
    -   <span data-ttu-id="8a187-130">[Enviar solicitação](api-management-advanced-policies.md#SendRequest) - Envia uma solicitação para a URL especificada.</span><span class="sxs-lookup"><span data-stu-id="8a187-130">[Send request](api-management-advanced-policies.md#SendRequest) - Sends a request to the specified URL.</span></span>  
  
    -   <span data-ttu-id="8a187-131">[Definir variável](api-management-advanced-policies.md#set-variable): persiste um valor em uma variável de contexto nomeada para acesso posterior.</span><span class="sxs-lookup"><span data-stu-id="8a187-131">[Set variable](api-management-advanced-policies.md#set-variable) - Persist a value in a named context variable for later access.</span></span>  
  
    -   <span data-ttu-id="8a187-132">[Definir método de solicitação](api-management-advanced-policies.md#SetRequestMethod) - Permite alterar o método HTTP de uma solicitação.</span><span class="sxs-lookup"><span data-stu-id="8a187-132">[Set request method](api-management-advanced-policies.md#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>  
  
    -   <span data-ttu-id="8a187-133">[Definir código de status](api-management-advanced-policies.md#SetStatus) – altera o código de status de HTTP para o valor especificado.</span><span class="sxs-lookup"><span data-stu-id="8a187-133">[Set status code](api-management-advanced-policies.md#SetStatus) - Changes the HTTP status code to the specified value.</span></span>  
  
    -   <span data-ttu-id="8a187-134">[Rastreamento](api-management-advanced-policies.md#Trace) - adiciona uma cadeia de caracteres para a saída do [Inspetor de API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/).</span><span class="sxs-lookup"><span data-stu-id="8a187-134">[Trace](api-management-advanced-policies.md#Trace) - Adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
    -   <span data-ttu-id="8a187-135">[Aguarde](api-management-advanced-policies.md#Wait): espera pelas políticas [Enviar solicitação](api-management-advanced-policies.md#SendRequest), [Obter valor do cache](api-management-caching-policies.md#GetFromCacheByKey) ou [Fluxo de controle](api-management-advanced-policies.md#choose) incorporadas serem concluídas antes de prosseguir.</span><span class="sxs-lookup"><span data-stu-id="8a187-135">[Wait](api-management-advanced-policies.md#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies to complete before proceeding.</span></span>  
  
-   [<span data-ttu-id="8a187-136">Políticas de autenticação</span><span class="sxs-lookup"><span data-stu-id="8a187-136">Authentication policies</span></span>](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   <span data-ttu-id="8a187-137">[Autenticar com o Basic](api-management-authentication-policies.md#Basic) - Autenticar com um serviço de back-end usando a autenticação Básica.</span><span class="sxs-lookup"><span data-stu-id="8a187-137">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
    -   <span data-ttu-id="8a187-138">[Autenticar com o certificado de cliente](api-management-authentication-policies.md#ClientCertificate) - Autenticar com um serviço de back-end usando certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="8a187-138">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
-   [<span data-ttu-id="8a187-139">Políticas de cache</span><span class="sxs-lookup"><span data-stu-id="8a187-139">Caching policies</span></span>](api-management-caching-policies.md#CachingPolicies)  
  
    -   <span data-ttu-id="8a187-140">[Obter do cache](api-management-caching-policies.md#GetFromCache) - Executa a pesquisa em cache e retorna uma resposta válida armazenada em cache quando uma estiver disponível.</span><span class="sxs-lookup"><span data-stu-id="8a187-140">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached response when available.</span></span>  
  
    -   <span data-ttu-id="8a187-141">[Armazenar em cache](api-management-caching-policies.md#StoreToCache) - Armazena a resposta em cache de acordo com a configuração de controle de cache especificada.</span><span class="sxs-lookup"><span data-stu-id="8a187-141">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches response according to the specified cache control configuration.</span></span>  
  
    -   <span data-ttu-id="8a187-142">[Obter valor do cache](api-management-caching-policies.md#GetFromCacheByKey) - Recupere um item em cache por chave.</span><span class="sxs-lookup"><span data-stu-id="8a187-142">[Get value from cache](api-management-caching-policies.md#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="8a187-143">[Armazenar valor em cache](api-management-caching-policies.md#StoreToCacheByKey) -Armazene um item no cache por chave.</span><span class="sxs-lookup"><span data-stu-id="8a187-143">[Store value in cache](api-management-caching-policies.md#StoreToCacheByKey) - Store an item in the cache by key.</span></span>  
  
    -   <span data-ttu-id="8a187-144">[Remover o valor do cache](api-management-caching-policies.md#RemoveCacheByKey) - remove um item no cache por chave.</span><span class="sxs-lookup"><span data-stu-id="8a187-144">[Remove value from cache](api-management-caching-policies.md#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>  
  
-   [<span data-ttu-id="8a187-145">Políticas entre domínios</span><span class="sxs-lookup"><span data-stu-id="8a187-145">Cross domain policies</span></span>](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   <span data-ttu-id="8a187-146">[Permitir chamadas entre domínios](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Torna a API acessível por meio de clientes Adobe Flash e Microsoft Silverlight baseados em navegadores.</span><span class="sxs-lookup"><span data-stu-id="8a187-146">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
    -   <span data-ttu-id="8a187-147">[CORS](api-management-cross-domain-policies.md#CORS) - Adicionar suporte de compartilhamento de recursos entre origens (CORS) a uma operação ou a uma API para permitir chamadas entre domínios de clientes baseados em navegadores.</span><span class="sxs-lookup"><span data-stu-id="8a187-147">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
    -   <span data-ttu-id="8a187-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adiciona suporte JSON com preenchimento (JSONP) a uma operação ou a uma API para permitir chamadas entre domínios de clientes JavaScript baseados em navegadores.</span><span class="sxs-lookup"><span data-stu-id="8a187-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
-   [<span data-ttu-id="8a187-149">Políticas de transformação</span><span class="sxs-lookup"><span data-stu-id="8a187-149">Transformation policies</span></span>](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   <span data-ttu-id="8a187-150">[Converter JSON para XML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converte o corpo da solicitação ou da resposta de JSON para XML.</span><span class="sxs-lookup"><span data-stu-id="8a187-150">[Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON to XML.</span></span>  
  
    -   <span data-ttu-id="8a187-151">[Converter XML para JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converte o corpo da solicitação ou da resposta de XML para JSON.</span><span class="sxs-lookup"><span data-stu-id="8a187-151">[Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML to JSON.</span></span>  
  
    -   <span data-ttu-id="8a187-152">[Localizar e substituir cadeia no corpo](api-management-transformation-policies.md#Findandreplacestringinbody) - Encontra uma subcadeia de uma solicitação ou resposta e a substitui por outra subcadeia.</span><span class="sxs-lookup"><span data-stu-id="8a187-152">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
    -   <span data-ttu-id="8a187-153">[Mascarar URLs no conteúdo](api-management-transformation-policies.md#MaskURLSContent) – Reescreve (mascara) os links no corpo da resposta, para que eles apontem para o link equivalente por meio do gateway.</span><span class="sxs-lookup"><span data-stu-id="8a187-153">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>  
  
    -   <span data-ttu-id="8a187-154">[Definir o serviço de back-end](api-management-transformation-policies.md#SetBackendService) - Altera o serviço de back-end para uma solicitação de entrada.</span><span class="sxs-lookup"><span data-stu-id="8a187-154">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes the backend service for an incoming request.</span></span>  
  
    -   <span data-ttu-id="8a187-155">[Definir corpo](api-management-transformation-policies.md#SetBody) - Define o corpo da mensagem para solicitações de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="8a187-155">[Set body](api-management-transformation-policies.md#SetBody) - Sets the message body for incoming and outgoing requests.</span></span>  
  
    -   <span data-ttu-id="8a187-156">[Definir cabeçalho HTTP](api-management-transformation-policies.md#SetHTTPheader) - Atribui um valor a uma resposta e/ou cabeçalho de resposta existente ou adiciona uma nova resposta e/ou cabeçalho de resposta.</span><span class="sxs-lookup"><span data-stu-id="8a187-156">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
    -   <span data-ttu-id="8a187-157">[Definir parâmetro de cadeia de consulta](api-management-transformation-policies.md#SetQueryStringParameter) - Adiciona, substitui o valor ou exclui parâmetros de cadeias de consulta de solicitação.</span><span class="sxs-lookup"><span data-stu-id="8a187-157">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
    -   <span data-ttu-id="8a187-158">[Reescrever URL](api-management-transformation-policies.md#RewriteURL) - Converte a URL de uma solicitação de sua forma pública em sua forma esperada pelo serviço Web.</span><span class="sxs-lookup"><span data-stu-id="8a187-158">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form to the form expected by the web service.</span></span>  
  
    -   <span data-ttu-id="8a187-159">[Transformar XML usando um XSLT](api-management-transformation-policies.md#XSLTransform): aplica uma transformação XSL para XML no corpo da solicitação ou da resposta.</span><span class="sxs-lookup"><span data-stu-id="8a187-159">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation to XML in the request or response body.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="8a187-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8a187-160">Next steps</span></span>
<span data-ttu-id="8a187-161">Para saber mais sobre como trabalhar com políticas, veja [Políticas em Gerenciamento de API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="8a187-161">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
