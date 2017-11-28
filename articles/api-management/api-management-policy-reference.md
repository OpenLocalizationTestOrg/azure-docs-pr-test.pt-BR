---
title: "aaaAzure Referência de política de gerenciamento de API"
description: "Saiba mais sobre Olá de políticas disponíveis tooconfigure gerenciamento de API."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 9d4ac609-b221-4032-93ae-e27a1254d43d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7ee194f4d6f172bf836c789cbe8ab732e18a7e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-policy-reference"></a><span data-ttu-id="57569-103">Referência de políticas do Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="57569-103">Azure API Management Policy Reference</span></span>
<span data-ttu-id="57569-104">Esta seção fornece um índice para diretivas Olá Olá [referência de política de gerenciamento de API][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="57569-104">This section provides an index for hello policies in hello [API Management policy reference][API Management policy reference].</span></span> <span data-ttu-id="57569-105">Para obter informações sobre como adicionar e configurar políticas, consulte [Políticas no Gerenciamento de API do Azure][Policies in API Management].</span><span class="sxs-lookup"><span data-stu-id="57569-105">For information on adding and configuring policies, see [Policies in API Management][Policies in API Management].</span></span>

<span data-ttu-id="57569-106">Expressões de política podem ser usadas como valores de atributo ou texto em qualquer uma das políticas de gerenciamento de API hello, a menos que Olá política especifique o contrário.</span><span class="sxs-lookup"><span data-stu-id="57569-106">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="57569-107">Algumas políticas, como Olá [fluxo de controle] [ Control flow] e [Set variable] [ Set variable] políticas se baseiam em expressões de política.</span><span class="sxs-lookup"><span data-stu-id="57569-107">Some policies such as hello [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="57569-108">Para obter mais informações, consulte [Advanced policies][Advanced policies] (Políticas avançadas) e [Policy expressions][Policy expressions] (Expressões de política)</span><span class="sxs-lookup"><span data-stu-id="57569-108">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions]</span></span>

## <a name="policy-reference-index"></a><span data-ttu-id="57569-109">Índice de referência de política</span><span class="sxs-lookup"><span data-stu-id="57569-109">Policy reference index</span></span>
* <span data-ttu-id="57569-110">[Access restriction policies][Access restriction policies] (Políticas de restrição de acesso)</span><span class="sxs-lookup"><span data-stu-id="57569-110">[Access restriction policies][Access restriction policies]</span></span>
  * <span data-ttu-id="57569-111">[Verificar cabeçalho HTTP][Check HTTP header] – impõe a existência e/ou o valor de um Cabeçalho HTTP.</span><span class="sxs-lookup"><span data-stu-id="57569-111">[Check HTTP header][Check HTTP header] - Enforces existence and/or value of a HTTP Header.</span></span>
  * <span data-ttu-id="57569-112">[Limitar a taxa de chamada por assinatura][Limit call rate by subscription] – previne picos de uso da API limitando a taxa de chamada, baseado em assinatura.</span><span class="sxs-lookup"><span data-stu-id="57569-112">[Limit call rate by subscription][Limit call rate by subscription] - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>
  * <span data-ttu-id="57569-113">[Limitar a taxa de chamada por chave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) - Previne picos de uso da API limitando a taxa de chamada, baseado em chave.</span><span class="sxs-lookup"><span data-stu-id="57569-113">[Limit call rate by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>
  * <span data-ttu-id="57569-114">[Restringir IPs do chamador][Restrict caller IPs] – filtra (permite/nega) chamadas de endereços IP e/ou intervalos de endereços específicos.</span><span class="sxs-lookup"><span data-stu-id="57569-114">[Restrict caller IPs][Restrict caller IPs] - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>
  * <span data-ttu-id="57569-115">[Definir a cota de uso por assinatura] [ Set usage quota by subscription] -permite que você tooenforce uma vida útil ou renovável chamada volume e/ou a largura de banda de cota, em uma base por assinatura.</span><span class="sxs-lookup"><span data-stu-id="57569-115">[Set usage quota by subscription][Set usage quota by subscription] - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>
  * <span data-ttu-id="57569-116">[Definir a cota de uso pela chave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) -permite que você tooenforce uma vida útil ou renovável chamada volume e/ou a largura de banda de cota, em uma base por chave.</span><span class="sxs-lookup"><span data-stu-id="57569-116">[Set usage quota by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>
  * <span data-ttu-id="57569-117">[Validar JWT][Validate JWT] – impõe a existência e a validade de um JWT extraído de um Cabeçalho HTTP ou um parâmetro de consulta especificado.</span><span class="sxs-lookup"><span data-stu-id="57569-117">[Validate JWT][Validate JWT] - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>
* <span data-ttu-id="57569-118">[Advanced policies][Advanced policies] (Políticas avançadas)</span><span class="sxs-lookup"><span data-stu-id="57569-118">[Advanced policies][Advanced policies]</span></span>
  * <span data-ttu-id="57569-119">[Fluxo de controle] [ Control flow] - condicionalmente aplica instruções de política com base nos resultados de saudação da avaliação de saudação de booliano [expressões][expressions].</span><span class="sxs-lookup"><span data-stu-id="57569-119">[Control flow][Control flow] - Conditionally applies policy statements based on hello results of hello evaluation of Boolean [expressions][expressions].</span></span>
  * <span data-ttu-id="57569-120">[Enviar solicitação] [ Forward request] -encaminha o serviço de back-end do hello solicitação toohello.</span><span class="sxs-lookup"><span data-stu-id="57569-120">[Forward request][Forward request] - Forwards hello request toohello backend service.</span></span>
  * <span data-ttu-id="57569-121">[Log tooEvent Hub] [ Log tooEvent Hub] -envia mensagens no destino de mensagem do hello formato especificado tooa definido por um [agente](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entidade.</span><span class="sxs-lookup"><span data-stu-id="57569-121">[Log tooEvent Hub][Log tooEvent Hub] - Sends messages in hello specified format tooa message target defined by a [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entity.</span></span>
  * <span data-ttu-id="57569-122">[Repita](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) -tentativas de execução de saudação colocados declarações de política, se e até Olá condição for atendida.</span><span class="sxs-lookup"><span data-stu-id="57569-122">[Retry](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="57569-123">A execução será repetida em Olá intervalos de tempo especificado e o toohello especificado contagem de repetição.</span><span class="sxs-lookup"><span data-stu-id="57569-123">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>
  * <span data-ttu-id="57569-124">[Retornar a resposta](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) -Olá de execução e retorna de anulações de pipeline da resposta especificada diretamente toohello chamador.</span><span class="sxs-lookup"><span data-stu-id="57569-124">[Return response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span>
  * <span data-ttu-id="57569-125">[Enviar solicitação de uma maneira](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) -envia uma solicitação toohello especificado URL sem aguardar uma resposta.</span><span class="sxs-lookup"><span data-stu-id="57569-125">[Send one way request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>
  * <span data-ttu-id="57569-126">[Enviar solicitação](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) -envia uma solicitação toohello especificou a URL.</span><span class="sxs-lookup"><span data-stu-id="57569-126">[Send request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) - Sends a request toohello specified URL.</span></span>
  * <span data-ttu-id="57569-127">[Definir o método de solicitação](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) -permite que você toochange método de saudação HTTP para uma solicitação.</span><span class="sxs-lookup"><span data-stu-id="57569-127">[Set request method](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>
  * <span data-ttu-id="57569-128">[Definir status](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) -valor especificado de toohello de código de status HTTP de saudação alterações.</span><span class="sxs-lookup"><span data-stu-id="57569-128">[Set status](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>
  * <span data-ttu-id="57569-129">[Definir variável][Set variable] – persiste um valor em uma variável [context][context] nomeada para acesso posterior.</span><span class="sxs-lookup"><span data-stu-id="57569-129">[Set variable][Set variable] - Persist a value in a named [context][context] variable for later access.</span></span>
  * <span data-ttu-id="57569-130">[Rastreamento](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) -adiciona uma cadeia de caracteres de saudação [API Inspetor](api-management-howto-api-inspector.md) saída.</span><span class="sxs-lookup"><span data-stu-id="57569-130">[Trace](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) - Adds a string into hello [API Inspector](api-management-howto-api-inspector.md) output.</span></span>
  * <span data-ttu-id="57569-131">[Aguarde](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - aguarda entre enviar solicitação, obter o valor de cache ou controlar o fluxo políticas toocomplete antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="57569-131">[Wait](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - Waits for enclosed Send request, Get value from cache, or Control flow policies toocomplete before proceeding.</span></span>
* <span data-ttu-id="57569-132">[Authentication policies][Authentication policies] (Políticas de autenticação)</span><span class="sxs-lookup"><span data-stu-id="57569-132">[Authentication policies][Authentication policies]</span></span>
  * <span data-ttu-id="57569-133">[Autenticar com o Básico][Authenticate with Basic] – autenticar com um serviço de back-end usando a autenticação Básica.</span><span class="sxs-lookup"><span data-stu-id="57569-133">[Authenticate with Basic][Authenticate with Basic] - Authenticate with a backend service using Basic authentication.</span></span>
  * <span data-ttu-id="57569-134">[Autenticar com o certificado do cliente][Authenticate with client certificate] – autenticar com um serviço de back-end usando certificados do cliente.</span><span class="sxs-lookup"><span data-stu-id="57569-134">[Authenticate with client certificate][Authenticate with client certificate] - Authenticate with a backend service using client certificates.</span></span>
* <span data-ttu-id="57569-135">[Caching policies][Caching policies] (Políticas de caching)</span><span class="sxs-lookup"><span data-stu-id="57569-135">[Caching policies][Caching policies]</span></span> 
  * <span data-ttu-id="57569-136">[Obter do cache][Get from cache] – executa a pesquisa em cache e retorna uma resposta válida armazenada em cache quando disponível.</span><span class="sxs-lookup"><span data-stu-id="57569-136">[Get from cache][Get from cache] - Perform cache look up and return a valid cached response when available.</span></span>
  * <span data-ttu-id="57569-137">[Armazenar toocache] [ Store toocache] -resposta de Caches de acordo com o toohello especificado a configuração de controle de cache.</span><span class="sxs-lookup"><span data-stu-id="57569-137">[Store toocache][Store toocache] - Caches response according toohello specified cache control configuration.</span></span>
  * <span data-ttu-id="57569-138">[Obter valor do cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) - Recupere um item em cache por chave.</span><span class="sxs-lookup"><span data-stu-id="57569-138">[Get value from cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>
  * <span data-ttu-id="57569-139">[Armazena o valor em cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) -armazenar um item no cache de saudação por chave.</span><span class="sxs-lookup"><span data-stu-id="57569-139">[Store value in cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>
  * <span data-ttu-id="57569-140">[Remova o valor do cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) -remover um item no cache de saudação por chave.</span><span class="sxs-lookup"><span data-stu-id="57569-140">[Remove value from cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>
* <span data-ttu-id="57569-141">[Cross domain policies][Cross domain policies] (Políticas entre domínios)</span><span class="sxs-lookup"><span data-stu-id="57569-141">[Cross domain policies][Cross domain policies]</span></span> 
  * <span data-ttu-id="57569-142">[Permitir chamadas entre domínios] [ Allow cross-domain calls] -torna Olá API acessível de clientes baseados em navegador Microsoft Silverlight e Adobe Flash.</span><span class="sxs-lookup"><span data-stu-id="57569-142">[Allow cross-domain calls][Allow cross-domain calls] - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>
  * <span data-ttu-id="57569-143">[CORS] [ CORS] -adiciona o compartilhamento de recursos entre origens (CORS) suporte para a operação de tooan ou chama um API entre tooallow domínios de clientes baseados em navegador.</span><span class="sxs-lookup"><span data-stu-id="57569-143">[CORS][CORS] - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>
  * <span data-ttu-id="57569-144">[JSONP] [ JSONP] - adiciona JSON com a operação de tooan de suporte de preenchimento (JSONP) ou chama um API entre tooallow domínios de clientes baseados em navegador do JavaScript.</span><span class="sxs-lookup"><span data-stu-id="57569-144">[JSONP][JSONP] - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>
* <span data-ttu-id="57569-145">[Transformation policies][Transformation policies] (Políticas de transformação)</span><span class="sxs-lookup"><span data-stu-id="57569-145">[Transformation policies][Transformation policies]</span></span> 
  * <span data-ttu-id="57569-146">[Converter JSON tooXML] [ Convert JSON tooXML] - converte solicitação ou o corpo da resposta de JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="57569-146">[Convert JSON tooXML][Convert JSON tooXML] - Converts request or response body from JSON tooXML.</span></span>
  * <span data-ttu-id="57569-147">[Converter XML tooJSON] [ Convert XML tooJSON] - converte solicitação ou o corpo da resposta de XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="57569-147">[Convert XML tooJSON][Convert XML tooJSON] - Converts request or response body from XML tooJSON.</span></span>
  * <span data-ttu-id="57569-148">[Localizar e substituir cadeia de caracteres no corpo][Find and replace string in body] – localiza uma subcadeia de caracteres de solicitação ou de resposta e a substitui por outra subcadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="57569-148">[Find and replace string in body][Find and replace string in body] - Finds a request or response substring and replaces it with a different substring.</span></span>
  * <span data-ttu-id="57569-149">[Mascarar URLs no conteúdo] [ Mask URLs in content] -regrava (mascara) links na resposta de saudação do corpo para que eles apontem toohello o link equivalente através do gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="57569-149">[Mask URLs in content][Mask URLs in content] - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>
  * <span data-ttu-id="57569-150">[Configurar o serviço de back-end] [ Set backend service] -altera o serviço de back-end Olá para uma solicitação de entrada.</span><span class="sxs-lookup"><span data-stu-id="57569-150">[Set backend service][Set backend service] - Changes hello backend service for an incoming request.</span></span>
  * <span data-ttu-id="57569-151">[Definir corpo] [ Set body] -define o corpo da mensagem de saudação para solicitações de entrada e saídas.</span><span class="sxs-lookup"><span data-stu-id="57569-151">[Set body][Set body] - Sets hello message body for incoming and outgoing requests.</span></span>
  * <span data-ttu-id="57569-152">[Definir cabeçalho HTTP] [ Set HTTP header] - atribui um cabeçalho de solicitação e/ou resposta do valor tooan existente ou adiciona um novo cabeçalho de solicitação de e/ou resposta.</span><span class="sxs-lookup"><span data-stu-id="57569-152">[Set HTTP header][Set HTTP header] - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>
  * <span data-ttu-id="57569-153">[Definir parâmetro de cadeia de consulta][Set query string parameter] – adiciona, substitui o valor ou exclui parâmetros de cadeias de consulta de solicitação.</span><span class="sxs-lookup"><span data-stu-id="57569-153">[Set query string parameter][Set query string parameter] - Adds, replaces value of, or deletes request query string parameter.</span></span>
  * <span data-ttu-id="57569-154">[Regravar URL] [ Rewrite URL] -converte uma URL de solicitação de forma pública formulário toohello esperada pelo serviço da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="57569-154">[Rewrite URL][Rewrite URL] - Converts a request URL from its public form toohello form expected by hello web service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57569-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="57569-155">Next steps</span></span>
<span data-ttu-id="57569-156">Para obter mais informações sobre expressões de política, consulte Olá vídeo a seguir.</span><span class="sxs-lookup"><span data-stu-id="57569-156">For more information on policy expressions, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Access restriction policies]: https://msdn.microsoft.com/library/azure/dn894078.aspx
[Check HTTP header]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#CheckHTTPHeader
[Limit call rate by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#LimitCallRate
[Restrict caller IPs]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#RestrictCallerIPs
[Set usage quota by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#SetUsageQuota
[Validate JWT]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx
[context]: https://msdn.microsoft.com/library/azure/ea160028-fc04-4782-aa26-4b8329df3448#ContextVariables
[Forward request]: https://msdn.microsoft.com/library/azure/dn894085.aspx#ForwardRequest
[Log tooEvent Hub]: https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub

[Authentication policies]: https://msdn.microsoft.com/library/azure/dn894079.aspx
[Authenticate with Basic]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#Basic
[Authenticate with client certificate]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#ClientCertificate
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx
[Get from cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#GetFromCache
[Store toocache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#StoreToCache

[Cross domain policies]: https://msdn.microsoft.com/library/azure/dn894084.aspx
[Allow cross-domain calls]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#AllowCrossDomainCalls
[CORS]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#CORS
[JSONP]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#JSONP

[Transformation policies]: https://msdn.microsoft.com/library/azure/dn894083.aspx
[Convert JSON tooXML]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertJSONtoXML
[Convert XML tooJSON]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertXMLtoJSON
[Find and replace string in body]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#Findandreplacestringinbody
[Mask URLs in content]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#MaskURLSContent
[Set backend service]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetBackendService
[Set body]: https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBody
[Set HTTP header]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetHTTPheader
[Set query string parameter]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetQueryStringParameter
[Rewrite URL]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#RewriteURL



[Policies in API Management]: api-management-howto-policies.md
[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx

[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx


