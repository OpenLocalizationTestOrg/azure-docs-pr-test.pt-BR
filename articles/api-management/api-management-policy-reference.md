---
title: "Referência de políticas do Gerenciamento de API do Azure"
description: "Saiba mais sobre as políticas disponíveis para configurar o Gerenciamento de API."
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
ms.openlocfilehash: adc0c4415e10ddd0b4994cecef17f026546e91a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-api-management-policy-reference"></a><span data-ttu-id="3b444-103">Referência de políticas do Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="3b444-103">Azure API Management Policy Reference</span></span>
<span data-ttu-id="3b444-104">Esta seção fornece um índice para as políticas na [referência de política de Gerenciamento de API][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="3b444-104">This section provides an index for the policies in the [API Management policy reference][API Management policy reference].</span></span> <span data-ttu-id="3b444-105">Para obter informações sobre como adicionar e configurar políticas, consulte [Políticas no Gerenciamento de API do Azure][Policies in API Management].</span><span class="sxs-lookup"><span data-stu-id="3b444-105">For information on adding and configuring policies, see [Policies in API Management][Policies in API Management].</span></span>

<span data-ttu-id="3b444-106">Expressões de política podem ser usadas como valores de atributo ou texto em qualquer uma das políticas de Gerenciamento de API, a menos que a política especifique o contrário.</span><span class="sxs-lookup"><span data-stu-id="3b444-106">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="3b444-107">Algumas políticas como [Controlar fluxo][Control flow] e [Definir variável][Set variable] baseiam-se em expressões de políticas.</span><span class="sxs-lookup"><span data-stu-id="3b444-107">Some policies such as the [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="3b444-108">Para obter mais informações, consulte [Advanced policies][Advanced policies] (Políticas avançadas) e [Policy expressions][Policy expressions] (Expressões de política)</span><span class="sxs-lookup"><span data-stu-id="3b444-108">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions]</span></span>

## <a name="policy-reference-index"></a><span data-ttu-id="3b444-109">Índice de referência de política</span><span class="sxs-lookup"><span data-stu-id="3b444-109">Policy reference index</span></span>
* <span data-ttu-id="3b444-110">[Access restriction policies][Access restriction policies] (Políticas de restrição de acesso)</span><span class="sxs-lookup"><span data-stu-id="3b444-110">[Access restriction policies][Access restriction policies]</span></span>
  * <span data-ttu-id="3b444-111">[Verificar cabeçalho HTTP][Check HTTP header] – impõe a existência e/ou o valor de um Cabeçalho HTTP.</span><span class="sxs-lookup"><span data-stu-id="3b444-111">[Check HTTP header][Check HTTP header] - Enforces existence and/or value of a HTTP Header.</span></span>
  * <span data-ttu-id="3b444-112">[Limitar a taxa de chamada por assinatura][Limit call rate by subscription] – previne picos de uso da API limitando a taxa de chamada, baseado em assinatura.</span><span class="sxs-lookup"><span data-stu-id="3b444-112">[Limit call rate by subscription][Limit call rate by subscription] - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>
  * <span data-ttu-id="3b444-113">[Limitar a taxa de chamada por chave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) - Previne picos de uso da API limitando a taxa de chamada, baseado em chave.</span><span class="sxs-lookup"><span data-stu-id="3b444-113">[Limit call rate by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>
  * <span data-ttu-id="3b444-114">[Restringir IPs do chamador][Restrict caller IPs] – filtra (permite/nega) chamadas de endereços IP e/ou intervalos de endereços específicos.</span><span class="sxs-lookup"><span data-stu-id="3b444-114">[Restrict caller IPs][Restrict caller IPs] - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>
  * <span data-ttu-id="3b444-115">[Definir cota de uso por assinatura][Set usage quota by subscription] – permite impor uma cota renovável ou de tempo de vida de volume de chamadas e/ou largura de banda, baseado em assinatura.</span><span class="sxs-lookup"><span data-stu-id="3b444-115">[Set usage quota by subscription][Set usage quota by subscription] - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>
  * <span data-ttu-id="3b444-116">[Definir a cota de uso por chave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) - Permite que você aplique uma cota renovável ou permanente de volume de chamada e/ou largura de banda, baseado em chave.</span><span class="sxs-lookup"><span data-stu-id="3b444-116">[Set usage quota by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>
  * <span data-ttu-id="3b444-117">[Validar JWT][Validate JWT] – impõe a existência e a validade de um JWT extraído de um Cabeçalho HTTP ou um parâmetro de consulta especificado.</span><span class="sxs-lookup"><span data-stu-id="3b444-117">[Validate JWT][Validate JWT] - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>
* <span data-ttu-id="3b444-118">[Advanced policies][Advanced policies] (Políticas avançadas)</span><span class="sxs-lookup"><span data-stu-id="3b444-118">[Advanced policies][Advanced policies]</span></span>
  * <span data-ttu-id="3b444-119">[Controlar fluxo][Control flow] – aplica condicionalmente instruções de política com base nos resultados da avaliação de [expressões][expressions] boolianas.</span><span class="sxs-lookup"><span data-stu-id="3b444-119">[Control flow][Control flow] - Conditionally applies policy statements based on the results of the evaluation of Boolean [expressions][expressions].</span></span>
  * <span data-ttu-id="3b444-120">[Encaminhar solicitação][Forward request] – encaminha a solicitação ao serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="3b444-120">[Forward request][Forward request] - Forwards the request to the backend service.</span></span>
  * <span data-ttu-id="3b444-121">[Registrar no Hub de Eventos][Log to Event Hub] – envia mensagens no formato especificado para um destino de mensagem definido por uma entidade [Agente](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger).</span><span class="sxs-lookup"><span data-stu-id="3b444-121">[Log to Event Hub][Log to Event Hub] - Sends messages in the specified format to a message target defined by a [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entity.</span></span>
  * <span data-ttu-id="3b444-122">[Repetir](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) - repete a execução das instruções de política, se e até que a condição seja atendida.</span><span class="sxs-lookup"><span data-stu-id="3b444-122">[Retry](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="3b444-123">A execução será repetida em intervalos de tempo especificados até e a contagem de repetições especificada.</span><span class="sxs-lookup"><span data-stu-id="3b444-123">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>
  * <span data-ttu-id="3b444-124">[Retornar resposta](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) - Anula a execução de pipeline e retorna a resposta especificada diretamente para o autor da chamada.</span><span class="sxs-lookup"><span data-stu-id="3b444-124">[Return response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span>
  * <span data-ttu-id="3b444-125">[Enviar solicitação unidirecional](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) - Envia uma solicitação para a URL especificada sem aguardar uma resposta.</span><span class="sxs-lookup"><span data-stu-id="3b444-125">[Send one way request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>
  * <span data-ttu-id="3b444-126">[Enviar solicitação](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) - Envia uma solicitação para a URL especificada.</span><span class="sxs-lookup"><span data-stu-id="3b444-126">[Send request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) - Sends a request to the specified URL.</span></span>
  * <span data-ttu-id="3b444-127">[Definir método de solicitação](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) - Permite alterar o método HTTP de uma solicitação.</span><span class="sxs-lookup"><span data-stu-id="3b444-127">[Set request method](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>
  * <span data-ttu-id="3b444-128">[Definir status](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) - Altera o código de status de HTTP para o valor especificado.</span><span class="sxs-lookup"><span data-stu-id="3b444-128">[Set status](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) - Changes the HTTP status code to the specified value.</span></span>
  * <span data-ttu-id="3b444-129">[Definir variável][Set variable] – persiste um valor em uma variável [context][context] nomeada para acesso posterior.</span><span class="sxs-lookup"><span data-stu-id="3b444-129">[Set variable][Set variable] - Persist a value in a named [context][context] variable for later access.</span></span>
  * <span data-ttu-id="3b444-130">[Rastreamento](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) - adiciona uma cadeia de caracteres para a saída do [Inspetor de API](api-management-howto-api-inspector.md).</span><span class="sxs-lookup"><span data-stu-id="3b444-130">[Trace](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) - Adds a string into the [API Inspector](api-management-howto-api-inspector.md) output.</span></span>
  * <span data-ttu-id="3b444-131">[Aguardar](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - Aguarda a conclusão da solicitação de Envio embutida, Obtenção do valor do cache ou Controle de políticas de fluxo antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="3b444-131">[Wait](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - Waits for enclosed Send request, Get value from cache, or Control flow policies to complete before proceeding.</span></span>
* <span data-ttu-id="3b444-132">[Authentication policies][Authentication policies] (Políticas de autenticação)</span><span class="sxs-lookup"><span data-stu-id="3b444-132">[Authentication policies][Authentication policies]</span></span>
  * <span data-ttu-id="3b444-133">[Autenticar com o Básico][Authenticate with Basic] – autenticar com um serviço de back-end usando a autenticação Básica.</span><span class="sxs-lookup"><span data-stu-id="3b444-133">[Authenticate with Basic][Authenticate with Basic] - Authenticate with a backend service using Basic authentication.</span></span>
  * <span data-ttu-id="3b444-134">[Autenticar com o certificado do cliente][Authenticate with client certificate] – autenticar com um serviço de back-end usando certificados do cliente.</span><span class="sxs-lookup"><span data-stu-id="3b444-134">[Authenticate with client certificate][Authenticate with client certificate] - Authenticate with a backend service using client certificates.</span></span>
* <span data-ttu-id="3b444-135">[Caching policies][Caching policies] (Políticas de caching)</span><span class="sxs-lookup"><span data-stu-id="3b444-135">[Caching policies][Caching policies]</span></span> 
  * <span data-ttu-id="3b444-136">[Obter do cache][Get from cache] – executa a pesquisa em cache e retorna uma resposta válida armazenada em cache quando disponível.</span><span class="sxs-lookup"><span data-stu-id="3b444-136">[Get from cache][Get from cache] - Perform cache look up and return a valid cached response when available.</span></span>
  * <span data-ttu-id="3b444-137">[Armazenar em cache][Store to cache] – armazena a resposta em cache de acordo com a configuração de controle de cache especificada.</span><span class="sxs-lookup"><span data-stu-id="3b444-137">[Store to cache][Store to cache] - Caches response according to the specified cache control configuration.</span></span>
  * <span data-ttu-id="3b444-138">[Obter valor do cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) - Recupere um item em cache por chave.</span><span class="sxs-lookup"><span data-stu-id="3b444-138">[Get value from cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>
  * <span data-ttu-id="3b444-139">[Armazenar valor em cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) -Armazene um item no cache por chave.</span><span class="sxs-lookup"><span data-stu-id="3b444-139">[Store value in cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) - Store an item in the cache by key.</span></span>
  * <span data-ttu-id="3b444-140">[Remover o valor do cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) - remove um item no cache por chave.</span><span class="sxs-lookup"><span data-stu-id="3b444-140">[Remove value from cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>
* <span data-ttu-id="3b444-141">[Cross domain policies][Cross domain policies] (Políticas entre domínios)</span><span class="sxs-lookup"><span data-stu-id="3b444-141">[Cross domain policies][Cross domain policies]</span></span> 
  * <span data-ttu-id="3b444-142">[Permitir chamadas entre domínios][Allow cross-domain calls] – torna a API acessível por meio de clientes Adobe Flash e Microsoft Silverlight baseados em navegador.</span><span class="sxs-lookup"><span data-stu-id="3b444-142">[Allow cross-domain calls][Allow cross-domain calls] - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>
  * <span data-ttu-id="3b444-143">[CORS][CORS] – adiciona suporte do CORS (compartilhamento de recurso entre origens) a uma operação ou API para permitir chamadas entre domínios de clientes baseados em navegador.</span><span class="sxs-lookup"><span data-stu-id="3b444-143">[CORS][CORS] - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>
  * <span data-ttu-id="3b444-144">[JSONP][JSONP] – adiciona suporte do JSON com preenchimento (JSONP) a uma operação ou API para permitir chamadas entre domínios de clientes JavaScript baseados em navegador.</span><span class="sxs-lookup"><span data-stu-id="3b444-144">[JSONP][JSONP] - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>
* <span data-ttu-id="3b444-145">[Transformation policies][Transformation policies] (Políticas de transformação)</span><span class="sxs-lookup"><span data-stu-id="3b444-145">[Transformation policies][Transformation policies]</span></span> 
  * <span data-ttu-id="3b444-146">[Converter JSON para XML][Convert JSON to XML] – converte o corpo da solicitação ou da resposta de JSON para XML.</span><span class="sxs-lookup"><span data-stu-id="3b444-146">[Convert JSON to XML][Convert JSON to XML] - Converts request or response body from JSON to XML.</span></span>
  * <span data-ttu-id="3b444-147">[Converter XML para JSON][Convert XML to JSON] – converte o corpo da solicitação ou da resposta de XML para JSON.</span><span class="sxs-lookup"><span data-stu-id="3b444-147">[Convert XML to JSON][Convert XML to JSON] - Converts request or response body from XML to JSON.</span></span>
  * <span data-ttu-id="3b444-148">[Localizar e substituir cadeia de caracteres no corpo][Find and replace string in body] – localiza uma subcadeia de caracteres de solicitação ou de resposta e a substitui por outra subcadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="3b444-148">[Find and replace string in body][Find and replace string in body] - Finds a request or response substring and replaces it with a different substring.</span></span>
  * <span data-ttu-id="3b444-149">[Mascarar URLs no conteúdo][Mask URLs in content] – reescreve (mascara) os links no corpo da resposta para que eles apontem para o link equivalente por meio do gateway.</span><span class="sxs-lookup"><span data-stu-id="3b444-149">[Mask URLs in content][Mask URLs in content] - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>
  * <span data-ttu-id="3b444-150">[Definir serviço de back-end][Set backend service] – altera o serviço de back-end de uma solicitação de entrada.</span><span class="sxs-lookup"><span data-stu-id="3b444-150">[Set backend service][Set backend service] - Changes the backend service for an incoming request.</span></span>
  * <span data-ttu-id="3b444-151">[Definir corpo][Set body] – define o corpo da mensagem de solicitações de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="3b444-151">[Set body][Set body] - Sets the message body for incoming and outgoing requests.</span></span>
  * <span data-ttu-id="3b444-152">[Definir cabeçalho HTTP][Set HTTP header] – atribui um valor a um cabeçalho de resposta e/ou solicitação existente ou adiciona um novo cabeçalho de resposta e/ou solicitação.</span><span class="sxs-lookup"><span data-stu-id="3b444-152">[Set HTTP header][Set HTTP header] - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>
  * <span data-ttu-id="3b444-153">[Definir parâmetro de cadeia de consulta][Set query string parameter] – adiciona, substitui o valor ou exclui parâmetros de cadeias de consulta de solicitação.</span><span class="sxs-lookup"><span data-stu-id="3b444-153">[Set query string parameter][Set query string parameter] - Adds, replaces value of, or deletes request query string parameter.</span></span>
  * <span data-ttu-id="3b444-154">[Reescrever URL][Rewrite URL] – converte a URL de uma solicitação de sua forma pública para a forma esperada pelo serviço Web.</span><span class="sxs-lookup"><span data-stu-id="3b444-154">[Rewrite URL][Rewrite URL] - Converts a request URL from its public form to the form expected by the web service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b444-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3b444-155">Next steps</span></span>
<span data-ttu-id="3b444-156">Para obter mais informações sobre expressões de política, consulte o vídeo a seguir.</span><span class="sxs-lookup"><span data-stu-id="3b444-156">For more information on policy expressions, see the following video.</span></span>

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
[Log to Event Hub]: https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub

[Authentication policies]: https://msdn.microsoft.com/library/azure/dn894079.aspx
[Authenticate with Basic]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#Basic
[Authenticate with client certificate]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#ClientCertificate
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx
[Get from cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#GetFromCache
[Store to cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#StoreToCache

[Cross domain policies]: https://msdn.microsoft.com/library/azure/dn894084.aspx
[Allow cross-domain calls]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#AllowCrossDomainCalls
[CORS]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#CORS
[JSONP]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#JSONP

[Transformation policies]: https://msdn.microsoft.com/library/azure/dn894083.aspx
[Convert JSON to XML]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertJSONtoXML
[Convert XML to JSON]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertXMLtoJSON
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


