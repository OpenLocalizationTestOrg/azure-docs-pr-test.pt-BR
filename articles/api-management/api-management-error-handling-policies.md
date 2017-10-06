---
title: "aaaError tratamento nas políticas de gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba como Olá a toorespond tooerror condições que podem ocorrer durante o processamento de solicitações no gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 3c777964-02b2-4f55-8731-8c3bd3c0ae27
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 002c65f21e763fd644da61b6a11685ffd97488c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="error-handling-in-api-management-policies"></a>Tratamento de erro em políticas de Gerenciamento de API
Gerenciamento de API do Azure permite que os editores toorespond tooerror condições que podem ocorrer durante o processamento de saudação do proxy de toohello solicitações, fornecendo um `ProxyError` objeto. Olá `ProxyError` objeto é acessado por meio de saudação [contexto. LastError](api-management-policy-expressions.md#ContextVariables) propriedade e pode ser usado pelas políticas de saudação `on-error` seção da política. Este tópico fornece uma referência para o erro Olá manipulação de recursos no gerenciamento de API do Azure.  
  
## <a name="error-handling-in-api-management"></a>Tratamento de erro no Gerenciamento de API  
 Políticas de gerenciamento de API do Azure são divididas em `inbound`, `backend`, `outbound`, e `on-error` seções, conforme mostrado no exemplo a seguir de saudação.  
  
```xml  
<policies>  
  <inbound>  
    <!-- statements toobe applied toohello request go here -->  
  </inbound>  
  <backend>  
    <!-- statements toobe applied before hello request is   
         forwarded toohello backend service go here -->  
    </backend>  
    <outbound>  
      <!-- statements toobe applied toohello response go here -->  
    </outbound>  
    <on-error>  
        <!-- statements toobe applied if there is an error   
             condition go here -->  
  </on-error>  
</policies>  
```  
  
 Durante o processamento de saudação de uma solicitação, etapas internas são executadas juntamente com as políticas que estão no escopo de solicitação de saudação. Se ocorrer um erro, o processamento imediatamente salta toohello `on-error` seção da política. Olá `on-error` seção política pode ser usada em qualquer escopo e editores de API podem configurar o comportamento personalizado, como hubs de tooevent Olá erro de log ou criar um novo chamador de toohello de tooreturn de resposta.  
  
> [!NOTE]
>  Olá `on-error` seção não está presente nas políticas por padrão. Olá tooadd `on-error` seção política tooa, procurar política toohello desejado no editor de diretiva de saudação e adicioná-lo. Para informações sobre como configurar políticas, consulte [Políticas do Gerenciamento de API](https://azure.microsoft.com/documentation/articles/api-management-howto-policies/).  
>   
>  Se não houver nenhuma seção `on-error`, os chamadores receberão mensagens de resposta HTTP 400 ou 500 se ocorrer uma condição de erro.  
  
### <a name="policies-allowed-in-on-error"></a>Políticas permitidas em caso de erro  
 Olá políticas a seguir podem ser usadas em Olá `on-error` seção da política.  
  
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
 Quando ocorre um erro e controle salta toohello `on-error` seção de política, o erro Olá é armazenado em [contexto. LastError](api-management-policy-expressions.md#ContextVariables) propriedade que pode ser acessada por diretivas em Olá `on-error` seção e tem Olá propriedades a seguir.  
  
|Nome|Tipo|Descrição|Obrigatório|  
|----------|----------|-----------------|--------------|  
|Fonte|string|Elemento de saudação nomes onde ocorreu o erro de saudação. Pode ser o nome de uma etapa do pipeline interno ou política.|Sim|  
|Motivo|string|Código de erro amigável para computadores, que pode ser usado no tratamento de erro.|Não|  
|Mensagem|string|Descrição de erro legível por humanos.|Sim|  
|Escopo|string|Nome do escopo de saudação onde ocorreu erro de saudação e pode ser "global", "produto", "api" ou "operação"|Não|  
|Seção|string|Nome da seção em que o erro ocorreu e pode ser "inbound", "backend", "outbound" ou "on-error".|Não|  
|Caminho|string|Especifica a política aninhada, por exemplo, "choose[3]/when[2]".|Não|  
|PolicyId|string|Valor de saudação `id` atributo, se especificado pelo cliente hello, na política de saudação onde ocorreu o erro|Não|  
  
> [!NOTE]
>  Todas as políticas têm um recurso opcional `id` atributos que podem ser adicionados como elemento raiz de toohello da política de saudação. Se esse atributo estiver presente em uma política quando ocorre uma condição de erro, valor de saudação do atributo Olá pode ser recuperado usando Olá `context.LastError.PolicyId` propriedade.  
  
## <a name="predefined-errors-for-built-in-steps"></a>Erros predefinidos para etapas internas  
 Olá erros a seguir são predefinidos para condições de erro que podem ocorrer durante a avaliação da saudação das etapas de processamento interno.  
  
|Fonte|Condição|Motivo|Mensagem|  
|------------|---------------|------------|-------------|  
|configuração|URI não corresponde tooany Api ou operação|OperationNotFound|Não é possível toomatch entrada solicitação tooan a operação.|  
|autorização|Chave de assinatura não fornecida|SubscriptionKeyNotFound|Acesso negado devido a chave de assinatura toomissing. Certifique-se de chave de assinatura tooinclude ao fazer solicitações toothis API.|  
|autorização|O valor chave e assinatura é inválido|SubscriptionKeyInvalid|Acesso negado devido a chave de assinatura tooinvalid. Verifique se tooprovide uma chave válida para uma assinatura ativa.|  
  
## <a name="predefined-errors-for-policies"></a>Erros predefinidos para políticas  
 Olá erros a seguir são predefinidos para condições de erro que podem ocorrer durante a avaliação da política.  
  
|Fonte|Condição|Motivo|Mensagem|  
|------------|---------------|------------|-------------|  
|rate-limit|Limite de taxa excedido|RateLimitExceeded|O limite da taxa foi excedido|  
|quota|Cota excedida|QuotaExceeded|Fora da cota do volume de chamada. A cota será reposta em xx:xx:xx. – ou – Sem cota de largura de banda. A cota será reposta em xx:xx:xx.|  
|jsonp|O valor do parâmetro de retorno de chamada é inválido (contém caracteres errados)|CallbackParameterInvalid|O valor do parâmetro de retorno de chamada {callback-parameter-name} não é um identificador JavaScript válido.|  
|ip-filter|IP de chamador tooparse com falha de solicitação|FailedToParseCallerIP|Falha ao endereço IP tooestablish chamador hello. Acesso negado.|  
|ip-filter|O IP do chamador não está na lista de permissões|CallerIpNotAllowed|O endereço IP do chamador {ip-address} não é permitido. Acesso negado.|  
|ip-filter|O IP do chamador está na lista de bloqueios|CallerIpBlocked|O endereço IP do chamador está bloqueado. Acesso negado.|  
|check-header|O cabeçalho necessário não é apresentado ou o valor está ausente|HeaderNotFound|Cabeçalho {nome do cabeçalho} não foi encontrado na solicitação de saudação. Acesso negado.|  
|check-header|O cabeçalho necessário não é apresentado ou o valor está ausente|HeaderValueNotAllowed|O valor do cabeçalho {header-name} de {header-value} não é permitido. Acesso negado.|  
|validate-jwt|O token Jwt está ausente na solicitação|TokenNotFound|JWT não encontrado na solicitação de saudação. Acesso negado.|  
|validate-jwt|Falha na validação da assinatura|TokenSignatureInvalid|<mensagem da biblioteca jwt\>. Acesso negado.|  
|validate-jwt|Público-alvo inválido|TokenAudienceNotAllowed|<mensagem da biblioteca jwt\>. Acesso negado.|  
|validate-jwt|Emissor inválido|TokenIssuerNotAllowed|<mensagem da biblioteca jwt\>. Acesso negado.|  
|validate-jwt|Token expirado|TokenExpired|<mensagem da biblioteca jwt\>. Acesso negado.|  
|validate-jwt|A chave de assinatura não foi resolvida por ID|TokenSignatureKeyNotFound|<mensagem da biblioteca jwt\>. Acesso negado.|  
|validate-jwt|As declarações necessárias estão ausentes no token|TokenClaimNotFound|Token de JWT está faltando Olá declarações a seguir: < c1\>, < c2\>,... Acesso negado.|  
|validate-jwt|Incompatibilidade de valores de declaração|TokenClaimValueNotAllowed|O valor da declaração {claim-name} de {claim-value} não é permitido. Acesso negado.|  
|validate-jwt|Outras falhas de validação|JwtInvalid|<mensagem da biblioteca jwt\>|

## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre como trabalhar com políticas, veja [Políticas em Gerenciamento de API](api-management-howto-policies.md).  