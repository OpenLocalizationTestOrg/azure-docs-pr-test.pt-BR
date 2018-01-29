---
title: "Tratamento de erro em políticas de Gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba como responder às condições de erro que podem ocorrer durante o processamento de solicitações no Gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 3c777964-02b2-4f55-8731-8c3bd3c0ae27
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2017
ms.author: apimpm
ms.openlocfilehash: 6bc71c0745493d52128553a78a31c45a3bca30f8
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2017
---
# <a name="error-handling-in-api-management-policies"></a>Tratamento de erro em políticas de Gerenciamento de API
O Gerenciamento de API do Azure permite que os editores respondam a condições de erro que podem ocorrer durante o processamento de solicitações para o proxy fornecendo um objeto `ProxyError`. O objeto `ProxyError` é acessado por meio da propriedade [context.LastError](api-management-policy-expressions.md#ContextVariables) e pode ser usado por políticas na seção da política `on-error`. Este tópico fornece uma referência para os recursos de tratamento de erro no Gerenciamento de API do Azure.  
  
## <a name="error-handling-in-api-management"></a>Tratamento de erro no Gerenciamento de API  
 As políticas no Gerenciamento de API do Azure são divididas nas seções `inbound`, `backend`, `outbound` e `on-error` conforme mostrado no exemplo a seguir.  
  
```xml  
<policies>  
  <inbound>  
    <!-- statements to be applied to the request go here -->  
  </inbound>  
  <backend>  
    <!-- statements to be applied before the request is   
         forwarded to the backend service go here -->  
    </backend>  
    <outbound>  
      <!-- statements to be applied to the response go here -->  
    </outbound>  
    <on-error>  
        <!-- statements to be applied if there is an error   
             condition go here -->  
  </on-error>  
</policies>  
```  
  
 Durante o processamento de uma solicitação, etapas internas são executadas juntamente com todas as políticas que estão no escopo da solicitação. Se ocorre um erro, o processamento imediatamente salta para a seção da política `on-error`. A seção da política `on-error` pode ser usada em qualquer escopo e os editores de API podem configurar o comportamento personalizado como registro do erro em hubs de eventos ou a criação de uma nova resposta para retornar ao chamador.  
  
> [!NOTE]
>  A seção `on-error` não está presente nas políticas por padrão. Para adicionar a seção `on-error` a uma política, navegue até a política desejada no editor de políticas e adicione-a. Para informações sobre como configurar políticas, consulte [Políticas do Gerenciamento de API](https://azure.microsoft.com/documentation/articles/api-management-howto-policies/).  
>   
>  Se não houver nenhuma seção `on-error`, os chamadores receberão mensagens de resposta HTTP 400 ou 500 se ocorrer uma condição de erro.  
  
### <a name="policies-allowed-in-on-error"></a>Políticas permitidas em caso de erro  
 As políticas a seguir podem ser usadas na seção da política `on-error`.  
  
-   [choose](api-management-advanced-policies.md#choose)  
-   [set-variable](api-management-advanced-policies.md#set-variable)  
-   [find-and-replace](api-management-transformation-policies.md#Findandreplacestringinbody)  
-   [return-response](api-management-advanced-policies.md#ReturnResponse)  
-   [set-header](api-management-transformation-policies.md#SetHTTPheader)  
-   [set-method](api-management-advanced-policies.md#SetRequestMethod)  
-   [set-status](api-management-advanced-policies.md#SetStatus)  
-   [send-request](api-management-advanced-policies.md#SendRequest)  
-   [send-one-way-request](api-management-advanced-policies.md#SendOneWayRequest)  
-   [log-to-eventhub](api-management-advanced-policies.md#log-to-eventhub)  
-   [json-to-xml](api-management-transformation-policies.md#ConvertJSONtoXML)  
-   [xml-to-json](api-management-transformation-policies.md#ConvertXMLtoJSON)  
  
## <a name="lasterror"></a>LastError  
 Quando ocorre um erro e o controle salta para a seção da política `on-error`, o erro é armazenado na propriedade [context.LastError](api-management-policy-expressions.md#ContextVariables), que pode ser acessada por políticas na seção `on-error` e tem as seguintes propriedades.  
  
|Nome|Tipo|Descrição|Obrigatório|  
|----------|----------|-----------------|--------------|  
|Fonte|string|Indica o elemento em que ocorreu o erro. Pode ser o nome de uma etapa do pipeline interno ou política.|Sim|  
|Motivo|string|Código de erro amigável para computadores, que pode ser usado no tratamento de erro.|Não|  
|Mensagem|string|Descrição de erro legível por humanos.|Sim|  
|Escopo|string|Nome do escopo em que ocorreu o erro e pode ser um dos "global", "produto", "api" ou "operação"|Não|  
|Seção|string|Nome da seção em que o erro ocorreu e pode ser "inbound", "backend", "outbound" ou "on-error".|Não|  
|Caminho|string|Especifica a política aninhada, por exemplo, "choose[3]/when[2]".|Não|  
|PolicyId|string|O valor do atributo `id`, se especificado pelo cliente, na política em que ocorreu o erro|Não|  
  
> [!NOTE]
>  Todas as políticas têm um atributo `id` opcional que pode ser adicionado ao elemento raiz da política. Se esse atributo estiver presente em uma política quando ocorrer uma condição de erro, o valor do atributo poderá ser recuperado usando a propriedade `context.LastError.PolicyId`.  
  
## <a name="predefined-errors-for-built-in-steps"></a>Erros predefinidos para etapas internas  
 Os erros a seguir são predefinidos para condições de erro que podem ocorrer durante a avaliação das etapas de processamento interno.  
  
|Fonte|Condição|Motivo|Mensagem|  
|------------|---------------|------------|-------------|  
|configuração|O URI não corresponde a nenhuma API ou operação|OperationNotFound|Não é possível corresponder a solicitação recebida a uma operação.|  
|autorização|Chave de assinatura não fornecida|SubscriptionKeyNotFound|Acesso negado devido à ausência da chave de assinatura. Certifique-se de incluir a chave de assinatura ao fazer solicitações para esta API.|  
|autorização|O valor chave e assinatura é inválido|SubscriptionKeyInvalid|Acesso negado devido à chave de assinatura inválida. Certifique-se de fornecer uma chave válida para uma assinatura ativa.|  
  
## <a name="predefined-errors-for-policies"></a>Erros predefinidos para políticas  
 Os erros a seguir são predefinidos para condições de erro que podem ocorrer durante a avaliação da política.  
  
|Fonte|Condição|Motivo|Mensagem|  
|------------|---------------|------------|-------------|  
|rate-limit|Limite de taxa excedido|RateLimitExceeded|O limite da taxa foi excedido|  
|quota|Cota excedida|QuotaExceeded|Fora da cota do volume de chamada. A cota será reposta em xx:xx:xx. – ou – Sem cota de largura de banda. A cota será reposta em xx:xx:xx.|  
|jsonp|O valor do parâmetro de retorno de chamada é inválido (contém caracteres errados)|CallbackParameterInvalid|O valor do parâmetro de retorno de chamada {callback-parameter-name} não é um identificador JavaScript válido.|  
|ip-filter|Falha ao analisar o IP do chamador da solicitação|FailedToParseCallerIP|Falha ao estabelecer o endereço IP para o chamador. Acesso negado.|  
|ip-filter|O IP do chamador não está na lista de permissões|CallerIpNotAllowed|O endereço IP do chamador {ip-address} não é permitido. Acesso negado.|  
|ip-filter|O IP do chamador está na lista de bloqueios|CallerIpBlocked|O endereço IP do chamador está bloqueado. Acesso negado.|  
|check-header|O cabeçalho necessário não é apresentado ou o valor está ausente|HeaderNotFound|O cabeçalho {header-name} não foi encontrado na solicitação. Acesso negado.|  
|check-header|O cabeçalho necessário não é apresentado ou o valor está ausente|HeaderValueNotAllowed|O valor do cabeçalho {header-name} de {header-value} não é permitido. Acesso negado.|  
|validate-jwt|O token Jwt está ausente na solicitação|TokenNotFound|JWT não encontrado na solicitação. Acesso negado.|  
|validate-jwt|Falha na validação da assinatura|TokenSignatureInvalid|<mensagem da biblioteca jwt\>. Acesso negado.|  
|validate-jwt|Público-alvo inválido|TokenAudienceNotAllowed|<mensagem da biblioteca jwt\>. Acesso negado.|  
|validate-jwt|Emissor inválido|TokenIssuerNotAllowed|<mensagem da biblioteca jwt\>. Acesso negado.|  
|validate-jwt|Token expirado|TokenExpired|<mensagem da biblioteca jwt\>. Acesso negado.|  
|validate-jwt|A chave de assinatura não foi resolvida por ID|TokenSignatureKeyNotFound|<mensagem da biblioteca jwt\>. Acesso negado.|  
|validate-jwt|As declarações necessárias estão ausentes no token|TokenClaimNotFound|O token JWT não tem as seguintes declarações: <c1\>, <c2\>, … Acesso negado.|  
|validate-jwt|Incompatibilidade de valores de declaração|TokenClaimValueNotAllowed|O valor da declaração {claim-name} de {claim-value} não é permitido. Acesso negado.|  
|validate-jwt|Outras falhas de validação|JwtInvalid|<mensagem da biblioteca jwt\>|

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como trabalhar com políticas, consulte:

+ [Políticas no Gerenciamento de API](api-management-howto-policies.md)
+ [Transformar APIs](transform-api.md)
+ [Referência de Política](api-management-policy-reference.md) para uma lista completa das instruções de política e suas configurações
+ [Exemplos de política](policy-samples.md)   