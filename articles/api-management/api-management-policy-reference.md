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
# <a name="azure-api-management-policy-reference"></a>Referência de políticas do Gerenciamento de API do Azure
Esta seção fornece um índice para diretivas Olá Olá [referência de política de gerenciamento de API][API Management policy reference]. Para obter informações sobre como adicionar e configurar políticas, consulte [Políticas no Gerenciamento de API do Azure][Policies in API Management].

Expressões de política podem ser usadas como valores de atributo ou texto em qualquer uma das políticas de gerenciamento de API hello, a menos que Olá política especifique o contrário. Algumas políticas, como Olá [fluxo de controle] [ Control flow] e [Set variable] [ Set variable] políticas se baseiam em expressões de política. Para obter mais informações, consulte [Advanced policies][Advanced policies] (Políticas avançadas) e [Policy expressions][Policy expressions] (Expressões de política)

## <a name="policy-reference-index"></a>Índice de referência de política
* [Access restriction policies][Access restriction policies] (Políticas de restrição de acesso)
  * [Verificar cabeçalho HTTP][Check HTTP header] – impõe a existência e/ou o valor de um Cabeçalho HTTP.
  * [Limitar a taxa de chamada por assinatura][Limit call rate by subscription] – previne picos de uso da API limitando a taxa de chamada, baseado em assinatura.
  * [Limitar a taxa de chamada por chave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) - Previne picos de uso da API limitando a taxa de chamada, baseado em chave.
  * [Restringir IPs do chamador][Restrict caller IPs] – filtra (permite/nega) chamadas de endereços IP e/ou intervalos de endereços específicos.
  * [Definir a cota de uso por assinatura] [ Set usage quota by subscription] -permite que você tooenforce uma vida útil ou renovável chamada volume e/ou a largura de banda de cota, em uma base por assinatura.
  * [Definir a cota de uso pela chave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) -permite que você tooenforce uma vida útil ou renovável chamada volume e/ou a largura de banda de cota, em uma base por chave.
  * [Validar JWT][Validate JWT] – impõe a existência e a validade de um JWT extraído de um Cabeçalho HTTP ou um parâmetro de consulta especificado.
* [Advanced policies][Advanced policies] (Políticas avançadas)
  * [Fluxo de controle] [ Control flow] - condicionalmente aplica instruções de política com base nos resultados de saudação da avaliação de saudação de booliano [expressões][expressions].
  * [Enviar solicitação] [ Forward request] -encaminha o serviço de back-end do hello solicitação toohello.
  * [Log tooEvent Hub] [ Log tooEvent Hub] -envia mensagens no destino de mensagem do hello formato especificado tooa definido por um [agente](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entidade.
  * [Repita](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) -tentativas de execução de saudação colocados declarações de política, se e até Olá condição for atendida. A execução será repetida em Olá intervalos de tempo especificado e o toohello especificado contagem de repetição.
  * [Retornar a resposta](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) -Olá de execução e retorna de anulações de pipeline da resposta especificada diretamente toohello chamador.
  * [Enviar solicitação de uma maneira](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) -envia uma solicitação toohello especificado URL sem aguardar uma resposta.
  * [Enviar solicitação](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) -envia uma solicitação toohello especificou a URL.
  * [Definir o método de solicitação](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) -permite que você toochange método de saudação HTTP para uma solicitação.
  * [Definir status](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) -valor especificado de toohello de código de status HTTP de saudação alterações.
  * [Definir variável][Set variable] – persiste um valor em uma variável [context][context] nomeada para acesso posterior.
  * [Rastreamento](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) -adiciona uma cadeia de caracteres de saudação [API Inspetor](api-management-howto-api-inspector.md) saída.
  * [Aguarde](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - aguarda entre enviar solicitação, obter o valor de cache ou controlar o fluxo políticas toocomplete antes de continuar.
* [Authentication policies][Authentication policies] (Políticas de autenticação)
  * [Autenticar com o Básico][Authenticate with Basic] – autenticar com um serviço de back-end usando a autenticação Básica.
  * [Autenticar com o certificado do cliente][Authenticate with client certificate] – autenticar com um serviço de back-end usando certificados do cliente.
* [Caching policies][Caching policies] (Políticas de caching) 
  * [Obter do cache][Get from cache] – executa a pesquisa em cache e retorna uma resposta válida armazenada em cache quando disponível.
  * [Armazenar toocache] [ Store toocache] -resposta de Caches de acordo com o toohello especificado a configuração de controle de cache.
  * [Obter valor do cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) - Recupere um item em cache por chave.
  * [Armazena o valor em cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) -armazenar um item no cache de saudação por chave.
  * [Remova o valor do cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) -remover um item no cache de saudação por chave.
* [Cross domain policies][Cross domain policies] (Políticas entre domínios) 
  * [Permitir chamadas entre domínios] [ Allow cross-domain calls] -torna Olá API acessível de clientes baseados em navegador Microsoft Silverlight e Adobe Flash.
  * [CORS] [ CORS] -adiciona o compartilhamento de recursos entre origens (CORS) suporte para a operação de tooan ou chama um API entre tooallow domínios de clientes baseados em navegador.
  * [JSONP] [ JSONP] - adiciona JSON com a operação de tooan de suporte de preenchimento (JSONP) ou chama um API entre tooallow domínios de clientes baseados em navegador do JavaScript.
* [Transformation policies][Transformation policies] (Políticas de transformação) 
  * [Converter JSON tooXML] [ Convert JSON tooXML] - converte solicitação ou o corpo da resposta de JSON tooXML.
  * [Converter XML tooJSON] [ Convert XML tooJSON] - converte solicitação ou o corpo da resposta de XML tooJSON.
  * [Localizar e substituir cadeia de caracteres no corpo][Find and replace string in body] – localiza uma subcadeia de caracteres de solicitação ou de resposta e a substitui por outra subcadeia de caracteres.
  * [Mascarar URLs no conteúdo] [ Mask URLs in content] -regrava (mascara) links na resposta de saudação do corpo para que eles apontem toohello o link equivalente através do gateway de saudação.
  * [Configurar o serviço de back-end] [ Set backend service] -altera o serviço de back-end Olá para uma solicitação de entrada.
  * [Definir corpo] [ Set body] -define o corpo da mensagem de saudação para solicitações de entrada e saídas.
  * [Definir cabeçalho HTTP] [ Set HTTP header] - atribui um cabeçalho de solicitação e/ou resposta do valor tooan existente ou adiciona um novo cabeçalho de solicitação de e/ou resposta.
  * [Definir parâmetro de cadeia de consulta][Set query string parameter] – adiciona, substitui o valor ou exclui parâmetros de cadeias de consulta de solicitação.
  * [Regravar URL] [ Rewrite URL] -converte uma URL de solicitação de forma pública formulário toohello esperada pelo serviço da web de saudação.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre expressões de política, consulte Olá vídeo a seguir.

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


