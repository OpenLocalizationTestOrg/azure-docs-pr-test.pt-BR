---
title: "políticas de gerenciamento de API aaaAzure | Microsoft Docs"
description: "Saiba mais sobre políticas de saudação disponíveis para uso no gerenciamento de API do Azure."
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
ms.openlocfilehash: 1c468ff37d73359f1dd694b91e20c2ca04f8934e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-policies"></a><span data-ttu-id="b1f21-103">Políticas de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="b1f21-103">API Management policies</span></span>
<span data-ttu-id="b1f21-104">Esta seção fornece uma referência para Olá políticas de gerenciamento de API a seguir.</span><span class="sxs-lookup"><span data-stu-id="b1f21-104">This section provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="b1f21-105">Para obter mais informações sobre como adicionar e configurar políticas, consulte [Políticas de Gerenciamento de API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="b1f21-105">For information on adding and configuring policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
  
 <span data-ttu-id="b1f21-106">As políticas são um recurso poderoso do sistema Olá que permitem que o publicador Olá toochange comportamento de saudação do hello API por meio da configuração.</span><span class="sxs-lookup"><span data-stu-id="b1f21-106">Policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="b1f21-107">As políticas são um conjunto de instruções que são executadas sequencialmente na solicitação de saudação ou resposta de uma API.</span><span class="sxs-lookup"><span data-stu-id="b1f21-107">Policies are a collection of Statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="b1f21-108">As instruções populares incluem conversão de formato de XML tooJSON e limitando toorestrict Olá quantidade de chamadas de entrada de um desenvolvedor de taxa de chamada.</span><span class="sxs-lookup"><span data-stu-id="b1f21-108">Popular Statements include format conversion from XML tooJSON and call rate limiting toorestrict hello amount of incoming calls from a developer.</span></span> <span data-ttu-id="b1f21-109">Muitas outras políticas estão disponíveis sem a necessidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="b1f21-109">Many more policies are available out of hello box.</span></span>  
  
 <span data-ttu-id="b1f21-110">Expressões de política podem ser usadas como valores de atributo ou texto em qualquer uma das políticas de gerenciamento de API hello, a menos que Olá política especifique o contrário.</span><span class="sxs-lookup"><span data-stu-id="b1f21-110">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="b1f21-111">Algumas políticas, como Olá [fluxo de controle](api-management-advanced-policies.md#choose) e [Set variable](api-management-advanced-policies.md#set-variable) políticas se baseiam em expressões de política.</span><span class="sxs-lookup"><span data-stu-id="b1f21-111">Some policies such as hello [Control flow](api-management-advanced-policies.md#choose) and [Set variable](api-management-advanced-policies.md#set-variable) policies are based on policy expressions.</span></span> <span data-ttu-id="b1f21-112">Para obter mais informações, confira [Políticas avançadas](api-management-advanced-policies.md#AdvancedPolicies) e [Expressões de política](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="b1f21-112">For more information, see [Advanced policies](api-management-advanced-policies.md#AdvancedPolicies) and [Policy expressions](api-management-policy-expressions.md).</span></span>  
  
##  <span data-ttu-id="b1f21-113"><a name="ProxyPolicies"></a> Políticas</span><span class="sxs-lookup"><span data-stu-id="b1f21-113"><a name="ProxyPolicies"></a> Policies</span></span>  
  
-   [<span data-ttu-id="b1f21-114">Políticas de restrição de acesso</span><span class="sxs-lookup"><span data-stu-id="b1f21-114">Access restriction policies</span></span>](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   <span data-ttu-id="b1f21-115">[Verificar cabeçalho HTTP](api-management-access-restriction-policies.md#CheckHTTPHeader) - Impõe a existência e/ou valor de um cabeçalho HTTP.</span><span class="sxs-lookup"><span data-stu-id="b1f21-115">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
    -   <span data-ttu-id="b1f21-116">[Limitar a taxa de chamada por assinatura](api-management-access-restriction-policies.md#LimitCallRate) - Previne picos de uso da API limitando a taxa de chamada, baseado em assinatura.</span><span class="sxs-lookup"><span data-stu-id="b1f21-116">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="b1f21-117">[Limitar a taxa de chamada por chave](api-management-access-restriction-policies.md#LimitCallRateByKey) - Previne picos de uso da API limitando a taxa de chamada, baseado em chave.</span><span class="sxs-lookup"><span data-stu-id="b1f21-117">[Limit call rate by key](api-management-access-restriction-policies.md#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="b1f21-118">[Restringir IP do autor da chamada](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filtra (permite/recusa) chamadas de endereços IP específicos e/ou intervalos de endereços.</span><span class="sxs-lookup"><span data-stu-id="b1f21-118">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
    -   <span data-ttu-id="b1f21-119">[Definir a cota de uso por assinatura](api-management-access-restriction-policies.md#SetUsageQuota) -permite que você tooenforce uma vida útil ou renovável chamada volume e/ou a largura de banda de cota, em uma base por assinatura.</span><span class="sxs-lookup"><span data-stu-id="b1f21-119">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="b1f21-120">[Definir a cota de uso pela chave](api-management-access-restriction-policies.md#SetUsageQuotaByKey) -permite que você tooenforce uma vida útil ou renovável chamada volume e/ou a largura de banda de cota, em uma base por chave.</span><span class="sxs-lookup"><span data-stu-id="b1f21-120">[Set usage quota by key](api-management-access-restriction-policies.md#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="b1f21-121">[Validar JWT](api-management-access-restriction-policies.md#ValidateJWT) - Impõe a existência e a validade de JWT extraída de um cabeçalho HTTP especificado ou um parâmetro de consulta especificado.</span><span class="sxs-lookup"><span data-stu-id="b1f21-121">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
-   [<span data-ttu-id="b1f21-122">Políticas avançadas</span><span class="sxs-lookup"><span data-stu-id="b1f21-122">Advanced policies</span></span>](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   <span data-ttu-id="b1f21-123">[Fluxo de controle](api-management-advanced-policies.md#choose) - condicionalmente aplica instruções de política com base na avaliação de saudação de expressões Boolianas.</span><span class="sxs-lookup"><span data-stu-id="b1f21-123">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on hello evaluation of Boolean expressions.</span></span>  
  
    -   <span data-ttu-id="b1f21-124">[Enviar solicitação](api-management-advanced-policies.md#ForwardRequest) -encaminha o serviço de back-end do hello solicitação toohello.</span><span class="sxs-lookup"><span data-stu-id="b1f21-124">[Forward request](api-management-advanced-policies.md#ForwardRequest) - Forwards hello request toohello backend service.</span></span>  
  
    -   <span data-ttu-id="b1f21-125">[Log tooEvent Hub](api-management-advanced-policies.md#log-to-eventhub) -envia mensagens no destino de mensagem hello formato especificado tooa definido por uma entidade de agente de log.</span><span class="sxs-lookup"><span data-stu-id="b1f21-125">[Log tooEvent Hub](api-management-advanced-policies.md#log-to-eventhub) - Sends messages in hello specified format tooa message target defined by a Logger entity.</span></span>  
  
    -   <span data-ttu-id="b1f21-126">[Repita](api-management-advanced-policies.md#Retry) -tentativas de execução de saudação colocados declarações de política, se e até Olá condição for atendida.</span><span class="sxs-lookup"><span data-stu-id="b1f21-126">[Retry](api-management-advanced-policies.md#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="b1f21-127">A execução será repetida em Olá intervalos de tempo especificado e o toohello especificado contagem de repetição.</span><span class="sxs-lookup"><span data-stu-id="b1f21-127">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>  
  
    -   <span data-ttu-id="b1f21-128">[Retornar a resposta](api-management-advanced-policies.md#ReturnResponse) -Olá de execução e retorna de anulações de pipeline da resposta especificada diretamente toohello chamador.</span><span class="sxs-lookup"><span data-stu-id="b1f21-128">[Return response](api-management-advanced-policies.md#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span>  
  
    -   <span data-ttu-id="b1f21-129">[Enviar solicitação de uma maneira](api-management-advanced-policies.md#SendOneWayRequest) -envia uma solicitação toohello especificado URL sem aguardar uma resposta.</span><span class="sxs-lookup"><span data-stu-id="b1f21-129">[Send one way request](api-management-advanced-policies.md#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>  
  
    -   <span data-ttu-id="b1f21-130">[Enviar solicitação](api-management-advanced-policies.md#SendRequest) -envia uma solicitação toohello especificou a URL.</span><span class="sxs-lookup"><span data-stu-id="b1f21-130">[Send request](api-management-advanced-policies.md#SendRequest) - Sends a request toohello specified URL.</span></span>  
  
    -   <span data-ttu-id="b1f21-131">[Definir variável](api-management-advanced-policies.md#set-variable): persiste um valor em uma variável de contexto nomeada para acesso posterior.</span><span class="sxs-lookup"><span data-stu-id="b1f21-131">[Set variable](api-management-advanced-policies.md#set-variable) - Persist a value in a named context variable for later access.</span></span>  
  
    -   <span data-ttu-id="b1f21-132">[Definir o método de solicitação](api-management-advanced-policies.md#SetRequestMethod) -permite que você toochange método de saudação HTTP para uma solicitação.</span><span class="sxs-lookup"><span data-stu-id="b1f21-132">[Set request method](api-management-advanced-policies.md#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>  
  
    -   <span data-ttu-id="b1f21-133">[Definir o código de status](api-management-advanced-policies.md#SetStatus) -valor especificado de toohello de código de status HTTP de saudação alterações.</span><span class="sxs-lookup"><span data-stu-id="b1f21-133">[Set status code](api-management-advanced-policies.md#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>  
  
    -   <span data-ttu-id="b1f21-134">[Rastreamento](api-management-advanced-policies.md#Trace) -adiciona uma cadeia de caracteres de saudação [API Inspetor](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) saída.</span><span class="sxs-lookup"><span data-stu-id="b1f21-134">[Trace](api-management-advanced-policies.md#Trace) - Adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
    -   <span data-ttu-id="b1f21-135">[Aguarde](api-management-advanced-policies.md#Wait) -aguarda para colocados [solicitação de envio](api-management-advanced-policies.md#SendRequest), [obter o valor de cache](api-management-caching-policies.md#GetFromCacheByKey), ou [fluxo de controle](api-management-advanced-policies.md#choose) toocomplete políticas antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="b1f21-135">[Wait](api-management-advanced-policies.md#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies toocomplete before proceeding.</span></span>  
  
-   [<span data-ttu-id="b1f21-136">Políticas de autenticação</span><span class="sxs-lookup"><span data-stu-id="b1f21-136">Authentication policies</span></span>](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   <span data-ttu-id="b1f21-137">[Autenticar com o Basic](api-management-authentication-policies.md#Basic) - Autenticar com um serviço de back-end usando a autenticação Básica.</span><span class="sxs-lookup"><span data-stu-id="b1f21-137">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
    -   <span data-ttu-id="b1f21-138">[Autenticar com o certificado de cliente](api-management-authentication-policies.md#ClientCertificate) - Autenticar com um serviço de back-end usando certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="b1f21-138">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
-   [<span data-ttu-id="b1f21-139">Políticas de cache</span><span class="sxs-lookup"><span data-stu-id="b1f21-139">Caching policies</span></span>](api-management-caching-policies.md#CachingPolicies)  
  
    -   <span data-ttu-id="b1f21-140">[Obter do cache](api-management-caching-policies.md#GetFromCache) - Executa a pesquisa em cache e retorna uma resposta válida armazenada em cache quando uma estiver disponível.</span><span class="sxs-lookup"><span data-stu-id="b1f21-140">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached response when available.</span></span>  
  
    -   <span data-ttu-id="b1f21-141">[Armazenar toocache](api-management-caching-policies.md#StoreToCache) -resposta de Caches de acordo com o toohello especificado a configuração de controle de cache.</span><span class="sxs-lookup"><span data-stu-id="b1f21-141">[Store toocache](api-management-caching-policies.md#StoreToCache) - Caches response according toohello specified cache control configuration.</span></span>  
  
    -   <span data-ttu-id="b1f21-142">[Obter valor do cache](api-management-caching-policies.md#GetFromCacheByKey) - Recupere um item em cache por chave.</span><span class="sxs-lookup"><span data-stu-id="b1f21-142">[Get value from cache](api-management-caching-policies.md#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="b1f21-143">[Armazena o valor em cache](api-management-caching-policies.md#StoreToCacheByKey) -armazenar um item no cache de saudação por chave.</span><span class="sxs-lookup"><span data-stu-id="b1f21-143">[Store value in cache](api-management-caching-policies.md#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>  
  
    -   <span data-ttu-id="b1f21-144">[Remova o valor do cache](api-management-caching-policies.md#RemoveCacheByKey) -remover um item no cache de saudação por chave.</span><span class="sxs-lookup"><span data-stu-id="b1f21-144">[Remove value from cache](api-management-caching-policies.md#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>  
  
-   [<span data-ttu-id="b1f21-145">Políticas entre domínios</span><span class="sxs-lookup"><span data-stu-id="b1f21-145">Cross domain policies</span></span>](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   <span data-ttu-id="b1f21-146">[Permitir chamadas entre domínios](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -torna Olá API acessível de clientes baseados em navegador Microsoft Silverlight e Adobe Flash.</span><span class="sxs-lookup"><span data-stu-id="b1f21-146">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
    -   <span data-ttu-id="b1f21-147">[CORS](api-management-cross-domain-policies.md#CORS) -adiciona o compartilhamento de recursos entre origens (CORS) suporte para a operação de tooan ou chama um API entre tooallow domínios de clientes baseados em navegador.</span><span class="sxs-lookup"><span data-stu-id="b1f21-147">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
    -   <span data-ttu-id="b1f21-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - adiciona JSON com a operação de tooan de suporte de preenchimento (JSONP) ou chama um API entre tooallow domínios de clientes baseados em navegador do JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b1f21-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
-   [<span data-ttu-id="b1f21-149">Políticas de transformação</span><span class="sxs-lookup"><span data-stu-id="b1f21-149">Transformation policies</span></span>](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   <span data-ttu-id="b1f21-150">[Converter JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - converte solicitação ou o corpo da resposta de JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="b1f21-150">[Convert JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON tooXML.</span></span>  
  
    -   <span data-ttu-id="b1f21-151">[Converter XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - converte solicitação ou o corpo da resposta de XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="b1f21-151">[Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML tooJSON.</span></span>  
  
    -   <span data-ttu-id="b1f21-152">[Localizar e substituir cadeia no corpo](api-management-transformation-policies.md#Findandreplacestringinbody) - Encontra uma subcadeia de uma solicitação ou resposta e a substitui por outra subcadeia.</span><span class="sxs-lookup"><span data-stu-id="b1f21-152">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
    -   <span data-ttu-id="b1f21-153">[Mascarar URLs no conteúdo](api-management-transformation-policies.md#MaskURLSContent) -regrava (mascara) links na resposta de saudação do corpo para que eles apontem toohello o link equivalente através do gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="b1f21-153">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>  
  
    -   <span data-ttu-id="b1f21-154">[Configurar o serviço de back-end](api-management-transformation-policies.md#SetBackendService) -altera o serviço de back-end Olá para uma solicitação de entrada.</span><span class="sxs-lookup"><span data-stu-id="b1f21-154">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes hello backend service for an incoming request.</span></span>  
  
    -   <span data-ttu-id="b1f21-155">[Definir corpo](api-management-transformation-policies.md#SetBody) -define o corpo da mensagem de saudação para solicitações de entrada e saídas.</span><span class="sxs-lookup"><span data-stu-id="b1f21-155">[Set body](api-management-transformation-policies.md#SetBody) - Sets hello message body for incoming and outgoing requests.</span></span>  
  
    -   <span data-ttu-id="b1f21-156">[Definir cabeçalho HTTP](api-management-transformation-policies.md#SetHTTPheader) - atribui um cabeçalho de solicitação e/ou resposta do valor tooan existente ou adiciona um novo cabeçalho de solicitação de e/ou resposta.</span><span class="sxs-lookup"><span data-stu-id="b1f21-156">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
    -   <span data-ttu-id="b1f21-157">[Definir parâmetro de cadeia de consulta](api-management-transformation-policies.md#SetQueryStringParameter) - Adiciona, substitui o valor ou exclui parâmetros de cadeias de consulta de solicitação.</span><span class="sxs-lookup"><span data-stu-id="b1f21-157">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
    -   <span data-ttu-id="b1f21-158">[Regravar URL](api-management-transformation-policies.md#RewriteURL) -converte uma URL de solicitação de forma pública formulário toohello esperada pelo serviço da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="b1f21-158">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form toohello form expected by hello web service.</span></span>  
  
    -   <span data-ttu-id="b1f21-159">[Transformar XML usando um XSLT](api-management-transformation-policies.md#XSLTransform) -aplica-se um tooXML de transformação XSL no corpo de solicitação ou resposta hello.</span><span class="sxs-lookup"><span data-stu-id="b1f21-159">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="b1f21-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b1f21-160">Next steps</span></span>
<span data-ttu-id="b1f21-161">Para saber mais sobre como trabalhar com políticas, veja [Políticas em Gerenciamento de API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="b1f21-161">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
