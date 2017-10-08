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
# <a name="api-management-policies"></a>Políticas de Gerenciamento de API
Esta seção fornece uma referência para Olá políticas de gerenciamento de API a seguir. Para obter mais informações sobre como adicionar e configurar políticas, consulte [Políticas de Gerenciamento de API](api-management-howto-policies.md).  
  
 As políticas são um recurso poderoso do sistema Olá que permitem que o publicador Olá toochange comportamento de saudação do hello API por meio da configuração. As políticas são um conjunto de instruções que são executadas sequencialmente na solicitação de saudação ou resposta de uma API. As instruções populares incluem conversão de formato de XML tooJSON e limitando toorestrict Olá quantidade de chamadas de entrada de um desenvolvedor de taxa de chamada. Muitas outras políticas estão disponíveis sem a necessidade de saudação.  
  
 Expressões de política podem ser usadas como valores de atributo ou texto em qualquer uma das políticas de gerenciamento de API hello, a menos que Olá política especifique o contrário. Algumas políticas, como Olá [fluxo de controle](api-management-advanced-policies.md#choose) e [Set variable](api-management-advanced-policies.md#set-variable) políticas se baseiam em expressões de política. Para obter mais informações, confira [Políticas avançadas](api-management-advanced-policies.md#AdvancedPolicies) e [Expressões de política](api-management-policy-expressions.md).  
  
##  <a name="ProxyPolicies"></a> Políticas  
  
-   [Políticas de restrição de acesso](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   [Verificar cabeçalho HTTP](api-management-access-restriction-policies.md#CheckHTTPHeader) - Impõe a existência e/ou valor de um cabeçalho HTTP.  
  
    -   [Limitar a taxa de chamada por assinatura](api-management-access-restriction-policies.md#LimitCallRate) - Previne picos de uso da API limitando a taxa de chamada, baseado em assinatura.  
  
    -   [Limitar a taxa de chamada por chave](api-management-access-restriction-policies.md#LimitCallRateByKey) - Previne picos de uso da API limitando a taxa de chamada, baseado em chave.  
  
    -   [Restringir IP do autor da chamada](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filtra (permite/recusa) chamadas de endereços IP específicos e/ou intervalos de endereços.  
  
    -   [Definir a cota de uso por assinatura](api-management-access-restriction-policies.md#SetUsageQuota) -permite que você tooenforce uma vida útil ou renovável chamada volume e/ou a largura de banda de cota, em uma base por assinatura.  
  
    -   [Definir a cota de uso pela chave](api-management-access-restriction-policies.md#SetUsageQuotaByKey) -permite que você tooenforce uma vida útil ou renovável chamada volume e/ou a largura de banda de cota, em uma base por chave.  
  
    -   [Validar JWT](api-management-access-restriction-policies.md#ValidateJWT) - Impõe a existência e a validade de JWT extraída de um cabeçalho HTTP especificado ou um parâmetro de consulta especificado.  
  
-   [Políticas avançadas](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   [Fluxo de controle](api-management-advanced-policies.md#choose) - condicionalmente aplica instruções de política com base na avaliação de saudação de expressões Boolianas.  
  
    -   [Enviar solicitação](api-management-advanced-policies.md#ForwardRequest) -encaminha o serviço de back-end do hello solicitação toohello.  
  
    -   [Log tooEvent Hub](api-management-advanced-policies.md#log-to-eventhub) -envia mensagens no destino de mensagem hello formato especificado tooa definido por uma entidade de agente de log.  
  
    -   [Repita](api-management-advanced-policies.md#Retry) -tentativas de execução de saudação colocados declarações de política, se e até Olá condição for atendida. A execução será repetida em Olá intervalos de tempo especificado e o toohello especificado contagem de repetição.  
  
    -   [Retornar a resposta](api-management-advanced-policies.md#ReturnResponse) -Olá de execução e retorna de anulações de pipeline da resposta especificada diretamente toohello chamador.  
  
    -   [Enviar solicitação de uma maneira](api-management-advanced-policies.md#SendOneWayRequest) -envia uma solicitação toohello especificado URL sem aguardar uma resposta.  
  
    -   [Enviar solicitação](api-management-advanced-policies.md#SendRequest) -envia uma solicitação toohello especificou a URL.  
  
    -   [Definir variável](api-management-advanced-policies.md#set-variable): persiste um valor em uma variável de contexto nomeada para acesso posterior.  
  
    -   [Definir o método de solicitação](api-management-advanced-policies.md#SetRequestMethod) -permite que você toochange método de saudação HTTP para uma solicitação.  
  
    -   [Definir o código de status](api-management-advanced-policies.md#SetStatus) -valor especificado de toohello de código de status HTTP de saudação alterações.  
  
    -   [Rastreamento](api-management-advanced-policies.md#Trace) -adiciona uma cadeia de caracteres de saudação [API Inspetor](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) saída.  
  
    -   [Aguarde](api-management-advanced-policies.md#Wait) -aguarda para colocados [solicitação de envio](api-management-advanced-policies.md#SendRequest), [obter o valor de cache](api-management-caching-policies.md#GetFromCacheByKey), ou [fluxo de controle](api-management-advanced-policies.md#choose) toocomplete políticas antes de continuar.  
  
-   [Políticas de autenticação](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   [Autenticar com o Basic](api-management-authentication-policies.md#Basic) - Autenticar com um serviço de back-end usando a autenticação Básica.  
  
    -   [Autenticar com o certificado de cliente](api-management-authentication-policies.md#ClientCertificate) - Autenticar com um serviço de back-end usando certificados de cliente.  
  
-   [Políticas de cache](api-management-caching-policies.md#CachingPolicies)  
  
    -   [Obter do cache](api-management-caching-policies.md#GetFromCache) - Executa a pesquisa em cache e retorna uma resposta válida armazenada em cache quando uma estiver disponível.  
  
    -   [Armazenar toocache](api-management-caching-policies.md#StoreToCache) -resposta de Caches de acordo com o toohello especificado a configuração de controle de cache.  
  
    -   [Obter valor do cache](api-management-caching-policies.md#GetFromCacheByKey) - Recupere um item em cache por chave.  
  
    -   [Armazena o valor em cache](api-management-caching-policies.md#StoreToCacheByKey) -armazenar um item no cache de saudação por chave.  
  
    -   [Remova o valor do cache](api-management-caching-policies.md#RemoveCacheByKey) -remover um item no cache de saudação por chave.  
  
-   [Políticas entre domínios](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   [Permitir chamadas entre domínios](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -torna Olá API acessível de clientes baseados em navegador Microsoft Silverlight e Adobe Flash.  
  
    -   [CORS](api-management-cross-domain-policies.md#CORS) -adiciona o compartilhamento de recursos entre origens (CORS) suporte para a operação de tooan ou chama um API entre tooallow domínios de clientes baseados em navegador.  
  
    -   [JSONP](api-management-cross-domain-policies.md#JSONP) - adiciona JSON com a operação de tooan de suporte de preenchimento (JSONP) ou chama um API entre tooallow domínios de clientes baseados em navegador do JavaScript.  
  
-   [Políticas de transformação](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   [Converter JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - converte solicitação ou o corpo da resposta de JSON tooXML.  
  
    -   [Converter XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - converte solicitação ou o corpo da resposta de XML tooJSON.  
  
    -   [Localizar e substituir cadeia no corpo](api-management-transformation-policies.md#Findandreplacestringinbody) - Encontra uma subcadeia de uma solicitação ou resposta e a substitui por outra subcadeia.  
  
    -   [Mascarar URLs no conteúdo](api-management-transformation-policies.md#MaskURLSContent) -regrava (mascara) links na resposta de saudação do corpo para que eles apontem toohello o link equivalente através do gateway de saudação.  
  
    -   [Configurar o serviço de back-end](api-management-transformation-policies.md#SetBackendService) -altera o serviço de back-end Olá para uma solicitação de entrada.  
  
    -   [Definir corpo](api-management-transformation-policies.md#SetBody) -define o corpo da mensagem de saudação para solicitações de entrada e saídas.  
  
    -   [Definir cabeçalho HTTP](api-management-transformation-policies.md#SetHTTPheader) - atribui um cabeçalho de solicitação e/ou resposta do valor tooan existente ou adiciona um novo cabeçalho de solicitação de e/ou resposta.  
  
    -   [Definir parâmetro de cadeia de consulta](api-management-transformation-policies.md#SetQueryStringParameter) - Adiciona, substitui o valor ou exclui parâmetros de cadeias de consulta de solicitação.  
  
    -   [Regravar URL](api-management-transformation-policies.md#RewriteURL) -converte uma URL de solicitação de forma pública formulário toohello esperada pelo serviço da web de saudação.  
  
    -   [Transformar XML usando um XSLT](api-management-transformation-policies.md#XSLTransform) -aplica-se um tooXML de transformação XSL no corpo de solicitação ou resposta hello.  
  
## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre como trabalhar com políticas, veja [Políticas em Gerenciamento de API](api-management-howto-policies.md).  
