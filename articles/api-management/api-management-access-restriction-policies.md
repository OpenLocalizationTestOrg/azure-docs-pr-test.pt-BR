---
title: "Políticas de restrição de acesso do Gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba mais sobre as políticas de restrição de acesso disponíveis para uso no Gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 034febe3-465f-4840-9fc6-c448ef520b0f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2017
ms.author: apimpm
ms.openlocfilehash: f9872ee033d8c0bed215f8b37d64395e5dcd534c
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2017
---
# <a name="api-management-access-restriction-policies"></a>Políticas de restrição de acesso do Gerenciamento de API
Este tópico fornece uma referência para as políticas de Gerenciamento de API a seguir. Para obter mais informações sobre como adicionar e configurar políticas, consulte [Políticas de Gerenciamento de API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="AccessRestrictionPolicies"></a> Políticas de restrição de acesso  
  
-   [Verificar cabeçalho HTTP](api-management-access-restriction-policies.md#CheckHTTPHeader) - Impõe a existência e/ou valor de um cabeçalho HTTP.  
-   [Limitar a taxa de chamada por assinatura](api-management-access-restriction-policies.md#LimitCallRate) - Previne picos de uso da API limitando a taxa de chamada, baseado em assinatura.  
-   [Limitar a taxa de chamada por chave](#LimitCallRateByKey) - Previne picos de uso da API limitando a taxa de chamada, baseado em chave.  
-   [Restringir IP do autor da chamada](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filtra (permite/recusa) chamadas de endereços IP específicos e/ou intervalos de endereços.  
-   [Definir a cota de uso por assinatura](api-management-access-restriction-policies.md#SetUsageQuota) - Permite que você aplique uma cota renovável ou permanente de volume de chamada e/ou largura de banda, baseado em assinatura.  
-   [Definir a cota de uso por chave](#SetUsageQuotaByKey) - Permite que você aplique uma cota renovável ou permanente de volume de chamada e/ou largura de banda, baseado em chave.  
-   [Validar JWT](api-management-access-restriction-policies.md#ValidateJWT) - Impõe a existência e a validade de JWT extraída de um cabeçalho HTTP especificado ou um parâmetro de consulta especificado.  
  
##  <a name="CheckHTTPHeader"></a> Verificar cabeçalho HTTP  
 Use a política `check-header` para impor que uma solicitação tem um cabeçalho HTTP especificado. Você pode, opcionalmente, verificar se o cabeçalho tem um valor específico ou procurar um intervalo de valores permitidos. Se a verificação falhar, a política encerrará o processamento da solicitação e retornará a mensagem de erro e código de status HTTP especificada pela política.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a>Exemplo  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|  
|----------|-----------------|--------------|  
|check-header|Elemento raiz.|Sim|  
|valor|Valor do cabeçalho HTTP permitido. Quando vários elementos de valor são especificados, a verificação é considerada um sucesso se qualquer um dos valores é uma correspondência.|Não|  
  
### <a name="attributes"></a>Atributos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|failed-check-error-message|A mensagem de erro para retornar no corpo da resposta HTTP se o cabeçalho não existe ou tem um valor inválido. Esta mensagem deve conter quaisquer caracteres especiais adequadamente seguidos por caracteres de escape.|Sim|N/D|  
|failed-check-httpcode|O código de status HTTP para retornar se o cabeçalho não existir ou tiver um valor inválido.|Sim|N/D|  
|header-name|O nome do cabeçalho HTTP para verificar.|Sim|N/D|  
|ignore-case|Pode ser definido como True ou False. Se definido como True, maiúsculas e minúsculas são ignoradas quando o valor do cabeçalho é comparado com o conjunto de valores aceitáveis.|Sim|N/D|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.  
  
-   **Seções de política:** de entrada, de saída  
  
-   **Escopos de política:** global, produto, API, operação  
  
##  <a name="LimitCallRate"></a> Limitar a taxa de chamadas por assinatura  
 A política `rate-limit` impede picos de uso da API para cada assinatura, limitando a taxa de chamadas para um número especificado por um período de tempo especificado. Quando essa política é disparada, o chamador recebe um código de status de resposta `429 Too Many Requests`.  
  
> [!IMPORTANT]
>  Essa política pode ser usada apenas uma vez por cada documento de política.  
>   
>  As [expressões de política](api-management-policy-expressions.md) não podem ser usadas em nenhum dos atributos de política para essa política.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a>Exemplo  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit calls="20" renewal-period="90" />  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|  
|----------|-----------------|--------------|  
|set-limit|Elemento raiz.|Sim|  
|api|Adicione um ou mais desses elementos para impor um limite de taxa de chamadas para as APIs dentro do produto. Limites de taxa de chamadas à API e ao produto são aplicados de forma independente.|Não|  
|operation|Adicione um ou mais desses elementos para impor um limite de taxa de chamadas para as operações dentro de uma API. Limites de taxa de chamadas à API, operação e produto são aplicados de forma independente.|Não|  
  
### <a name="attributes"></a>Atributos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|name|O nome da API para a qual aplicar o limite de taxa.|Sim|N/D|  
|chamadas|O número total máximo de chamadas permitidas durante o intervalo de tempo especificado no `renewal-period`.|Sim|N/D|  
|renewal-period|O período de tempo, em segundos, durante o qual uma cota reinicia.|Sim|N/D|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.  
  
-   **Seções de política:** de entrada  
  
-   **Escopos de política:** produto  
  
##  <a name="LimitCallRateByKey"></a> Limitar a taxa de chamadas por chave  
 A política `rate-limit-by-key` impede picos de uso da API para cada chave, limitando a taxa de chamadas para um número especificado por um período de tempo especificado. A chave pode ter um valor de cadeia de caracteres arbitrária e geralmente é fornecida usando uma expressão de política. A condição de incremento opcional pode ser adicionada para especificar quais solicitações devem ser contadas para obtenção do limite. Quando essa política é disparada, o chamador recebe um código de status de resposta `429 Too Many Requests`.  
  
 Para obter mais informações e exemplos dessa política, consulte [Limitação de solicitação avançada com o Gerenciamento de API do Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).  
  
> [!IMPORTANT]
>  Essa política pode ser usada apenas uma vez por cada documento de política.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a>Exemplo  
 No exemplo a seguir, o limite de taxa é codificado pelo endereço IP do chamador.  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit-by-key  calls="10"  
              renewal-period="60"  
              increment-condition="@(context.Response.StatusCode == 200)"  
              counter-key="@(context.Request.IpAddress)"/>  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|  
|----------|-----------------|--------------|  
|set-limit|Elemento raiz.|Sim|  
  
### <a name="attributes"></a>Atributos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|chamadas|O número total máximo de chamadas permitidas durante o intervalo de tempo especificado no `renewal-period`.|Sim|N/D|  
|counter-key|A chave a ser usada para a política de limite de taxa.|Sim|N/D|  
|increment-condition|A expressão booliana que especifica se a solicitação deve ser contabilizada para a cota (`true`).|Não|N/D|  
|renewal-period|O período de tempo, em segundos, durante o qual uma cota reinicia.|Sim|N/D|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.  
  
-   **Seções de política:** de entrada  
  
-   **Escopos de política:** global, produto, API, operação  
  
##  <a name="RestrictCallerIPs"></a> Restringir IPs do chamador  
 A política `ip-filter` filtra (permite/recusa) chamadas de endereços IP específicos e/ou intervalos de endereços.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a>Exemplo  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|  
|----------|-----------------|--------------|  
|ip-filter|Elemento raiz.|Sim|  
|endereço|Especifica um único endereço IP no qual filtrar.|Pelo menos um elemento `address` ou `address-range` é necessário.|  
|address-range from="address" to="address"|Especifica um intervalo de endereços IP nos quais filtrar.|Pelo menos um elemento `address` ou `address-range` é necessário.|  
  
### <a name="attributes"></a>Atributos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|address-range from="address" to="address"|Um intervalo de endereços IP aos quais o acesso será permitido ou negado.|Necessário quando o elemento `address-range` é usado.|N/D|  
|ip-filter action="allow &#124; forbid"|Especifica se chamadas para os endereços IP e intervalos de endereços IP especificados devem ou não ser permitidas.|Sim|N/D|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.  
  
-   **Seções de política:** de entrada  
-   **Escopos de política:** global, produto, API, operação  
  
##  <a name="SetUsageQuota"></a> Definir a cota de uso por assinatura  
 A política `quota` impõe uma cota renovável ou de tempo de vida de volume de chamadas e/ou largura de banda, para cada assinatura.  
  
> [!IMPORTANT]
>  Essa política pode ser usada apenas uma vez por cada documento de política.  
>   
>  As [expressões de política](api-management-policy-expressions.md) não podem ser usadas em nenhum dos atributos de política para essa política.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a>Exemplo  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota calls="10000" bandwidth="40000" renewal-period="3600" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|  
|----------|-----------------|--------------|  
|quota|Elemento raiz.|Sim|  
|api|Adicione um ou mais desses elementos para impor uma cota para as APIs dentro do produto. Cotas de API e produto são aplicadas de forma independente.|Não|  
|operation|Adicione um ou mais desses elementos para impor uma cota para as operações dentro de uma API. Cotas de operações, APIs e produtos são aplicadas de forma independente.|Não|  
  
### <a name="attributes"></a>Atributos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|name|O nome da API ou operação à qual a cota se aplica.|Sim|N/D|  
|largura de banda|O número total máximo de kilobytes permitidos durante o intervalo de tempo especificado no `renewal-period`.|`calls` ou `bandwidth` ou ainda ambos juntos devem ser especificados.|N/D|  
|chamadas|O número total máximo de chamadas permitidas durante o intervalo de tempo especificado no `renewal-period`.|`calls` ou `bandwidth` ou ainda ambos juntos devem ser especificados.|N/D|  
|renewal-period|O período de tempo, em segundos, durante o qual uma cota reinicia.|Sim|N/D|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.  
  
-   **Seções de política:** de entrada  
-   **Escopos de política:** produto  
  
##  <a name="SetUsageQuotaByKey"></a> Definir uma cota de uso por chave  
 A política `quota-by-key` impõe uma cota renovável ou de tempo de vida de volume de chamadas e/ou largura de banda, para cada chave. A chave pode ter um valor de cadeia de caracteres arbitrária e geralmente é fornecida usando uma expressão de política. A condição de incremento opcional pode ser adicionada para especificar quais solicitações devem ser contadas para obtenção da cota.  
  
 Para obter mais informações e exemplos dessa política, consulte [Limitação de solicitação avançada com o Gerenciamento de API do Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).  
  
> [!IMPORTANT]
>  Essa política pode ser usada apenas uma vez por cada documento de política.  
>   
>  As [expressões de política](api-management-policy-expressions.md) não podem ser usadas em nenhum dos atributos de política para essa política.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a>Exemplo  
 No exemplo a seguir, a cota é codificada pelo endereço IP do chamador.  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota-by-key calls="10000" bandwidth="40000" renewal-period="3600"  
                      increment-condition="@(context.Response.StatusCode >= 200 && context.Response.StatusCode < 400)"  
                      counter-key="@(context.Request.IpAddress)" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|  
|----------|-----------------|--------------|  
|quota|Elemento raiz.|Sim|  
  
### <a name="attributes"></a>Atributos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|largura de banda|O número total máximo de kilobytes permitidos durante o intervalo de tempo especificado no `renewal-period`.|`calls` ou `bandwidth` ou ainda ambos juntos devem ser especificados.|N/D|  
|chamadas|O número total máximo de chamadas permitidas durante o intervalo de tempo especificado no `renewal-period`.|`calls` ou `bandwidth` ou ainda ambos juntos devem ser especificados.|N/D|  
|counter-key|A chave a ser usada para a política de cota.|Sim|N/D|  
|increment-condition|A expressão booliana que especifica se a solicitação deve ser contabilizada para a cota (`true`)|Não|N/D|  
|renewal-period|O período de tempo, em segundos, durante o qual uma cota reinicia.|Sim|N/D|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.  
  
-   **Seções de política:** de entrada  
-   **Escopos de política:** global, produto, API, operação  
  
##  <a name="ValidateJWT"></a> Validar JWT  
 A política `validate-jwt` impõe a existência e a validade de um JWT extraído de um Cabeçalho HTTP ou um parâmetro de consulta especificado.  
  
> [!IMPORTANT]
>  A política `validate-jwt` requer que a declaração registrada `exp` seja incluída no token JWT, a menos que o atributo `require-expiration-time` seja especificado e definido como `false`.  
> A política `validate-jwt` dá suporte aos algoritmos de assinatura HS256 e RS256. Para HS256, a chave deve ser fornecida embutida na política no formato codificado em base64. Para RS256, a chave deve ser fornecida por meio de um ponto de extremidade de configuração de Open ID.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<validate-jwt   
    header-name="name of http header containing the token (use query-parameter-name attribute if the token is passed in the URL)"   
    failed-validation-httpcode="http status code to return on failure"   
    failed-validation-error-message="error message to return on failure"   
    require-expiration-time="true|false"
    require-scheme="scheme"
    require-signed-tokens="true|false"   
    clock-skew="allowed clock skew in seconds">  
  <issuer-signing-keys>  
    <key>base64 encoded signing key</key>  
    <!-- if there are multiple keys, then add additional key elements -->  
  </issuer-signing-keys>  
  <audiences>  
    <audience>audience string</audience>  
    <!-- if there are multiple possible audiences, then add additional audience elements -->  
  </audiences>  
  <issuers>  
    <issuer>issuer string</issuer>  
    <!-- if there are multiple possible issuers, then add additional issuer elements -->  
  </issuers>  
  <required-claims>  
    <claim name="name of the claim as it appears in the token" match="all|any" separator="separator character in a multi-valued claim">
      <value>claim value as it is expected to appear in the token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of the configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a>Exemplos  
  
#### <a name="azure-mobile-services-token-validation"></a>Validação de token de Serviços Móveis do Azure  
  
```xml  
<validate-jwt header-name="x-zumo-auth" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Supplied access token is invalid.">  
    <issuers>  
        <issuer>urn:microsoft:windows-azure:zumo</issuer>  
    </issuers>  
    <audiences>  
        <audience>Facebook</audience>  
    </audiences>  
    <issuer-signing-keys>  
        <zumo-master-key id="0">insert key here</zumo-master-key>  
    </issuer-signing-keys>  
</validate-jwt>  
```  
  
#### <a name="azure-active-directory-token-validation"></a>Validação de token do Azure Active Directory  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration" />  
    <audiences>
        <audience>25eef6e4-c905-4a07-8eb4-0d08d5df8b3f</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  

  
#### <a name="azure-active-directory-b2c-token-validation"></a>Validação de token do Azure Active Directory B2C  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/tfp/contoso.onmicrosoft.com/b2c_1_signin/v2.0/.well-known/openid-configuration" />
    <audiences>
        <audience>d313c4e4-de5f-4197-9470-e509a2f0b806</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  
  
#### <a name="authorize-access-to-operations-based-on-token-claims"></a>Autorizar o acesso para operações baseadas em declarações de token  
 Este exemplo mostra como usar a política [Validar JWT](api-management-access-restriction-policies.md#ValidateJWT) para pré-autorizar o acesso a operações baseadas em declarações de token. Para ver uma demonstração da configuração e do uso dessa política, consulte [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Abordagem da Nuvem Episódio 177: Mais Recursos de Gerenciamento de API com Vlad Vinogradsky) e avance para 13:50. Avance para 15:00 para ver as diretivas configuradas no editor de diretiva e, em seguida, 18:50 para uma demonstração de como chamar uma operação do portal do desenvolvedor com e sem o token de autorização necessário.  
  
```xml  
<!-- Copy the following snippet into the inbound section at the api (or higher) level to pre-authorize access to operations based on token claims -->  
<set-variable name="signingKey" value="insert signing key here" />  
<choose>  
  <when condition="@(context.Request.Method.Equals("patch",StringComparison.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="edit">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <when condition="@(new [] {"post", "put"}.Contains(context.Request.Method,StringComparer.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="create">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <otherwise>  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
    </validate-jwt>  
  </otherwise>  
</choose>  
```  
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descrição|Obrigatório|  
|-------------|-----------------|--------------|  
|validate-jwt|Elemento raiz.|Sim|  
|públicos-alvo|Contém uma lista de declarações de público-alvo aceitáveis que podem estar presentes no token. Se vários valores de público-alvo estiverem presentes, cada valor será tentado até que todos sejam esgotados (nesse caso, a validação falhará) ou até obter êxito. Pelo menos um público-alvo deve ser especificado.|Não|  
|issuer-signing-keys|Uma lista de chaves de segurança codificadas em Base64 usadas para validar tokens assinados. Se várias chaves de segurança estiverem presentes, cada chave será tentada até que todas sejam esgotadas (nesse caso, a validação falhará) ou até obter êxito (útil para substituição de token). Elementos-chave têm um atributo `id` opcional usado para correspondência com a declaração `kid`.|Não|  
|emissores|Uma lista de entidades aceitáveis que emitiram o token. Se vários valores de emissor estiverem presentes, cada valor será tentado até que todos sejam esgotados (nesse caso, a validação falhará) ou até obter êxito.|Não|  
|openid-config|O elemento usado para especificar um ponto de extremidade de configuração de Open ID em conformidade do qual chaves de assinatura e emissor podem ser obtidos.|Não|  
|required-claims|Contém uma lista de declarações cuja presença é esperada no token para que ele possa ser considerado válido. Quando o atributo `match` é definido como `all`, cada valor de declaração na política deve estar presente no token para que a validação seja bem-sucedida. Quando o atributo `match` é definido como `any`, pelo menos uma declaração deve estar presente no token para que a validação seja bem-sucedida.|Não|  
|zumo-master-key|Chave mestra para tokens emitidos pelos Serviços Móveis do Azure|Não|  
  
### <a name="attributes"></a>Atributos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|clock-skew|Período de tempo. Fornece alguma pequena reserva caso a declaração de expiração do token esteja presente no token e seja após a data/hora atual.|Não|0 segundos|  
|failed-validation-error-message|Mensagem de erro para retornar no corpo da resposta HTTP se o JWT não passar na validação. Esta mensagem deve conter quaisquer caracteres especiais adequadamente seguidos por caracteres de escape.|Não|A mensagem de erro padrão depende do problema de validação, por exemplo, "O JWT não está presente."|  
|failed-validation-httpcode|O código de status HTTP para retornar se o JWT não passar na validação.|Não|401|  
|header-name|O nome do cabeçalho HTTP contendo o token.|`header-name` ou `query-paremeter-name` deve ser especificado; mas não ambos.|N/D|  
|ID|O atributo `id` no elemento `key` permite que você especifique a cadeia de caracteres cuja correspondência será verificada em relação à declaração `kid` no token (se presente) para descobrir a chave apropriada a ser usada para validação de assinatura.|Não|N/D|  
|match|O atributo `match` no elemento `claim` especifica se todos os valores de declaração na política devem estar presentes no token para que a validação seja bem-sucedida. Os valores possíveis são:<br /><br /> -                          `all` – todos os valores de declaração na política devem estar presentes no token para que a validação seja bem-sucedida.<br /><br /> -                          `any` – pelo menos um valor de declaração na política deve estar presente no token para que a validação seja bem-sucedida.|Não|tudo|  
|query-paremeter-name|O nome do parâmetro de consulta que contém o token.|`header-name` ou `query-paremeter-name` deve ser especificado; mas não ambos.|N/D|  
|require-expiration-time|Booliano. Especifica se uma declaração de expiração é necessária no token.|Não|verdadeiro|
|require-scheme|O nome do esquema do token, por exemplo, "Portador". Quando esse atributo for definido, a política garantirá que o esquema especificado esteja presente no valor do cabeçalho de Autorização.|Não|N/D|
|require-signed-tokens|Booliano. Especifica se é necessário que um determinado token seja assinado.|Não|verdadeiro|  
|separador|Cadeia de caracteres. Especifica um separador (por exemplo, ",") a ser usado para extrair um conjunto de valores de uma declaração com valores múltiplos.|Não|N/D| 
|url|URL ponto de extremidade de configuração de Open ID da qual é possível obter os metadados de configuração de Open ID. Para o Azure Active Directory, use a seguinte URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituindo o seu nome de locatário do diretório, por exemplo, `contoso.onmicrosoft.com`.|Sim|N/D|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.  
  
-   **Seções de política:** de entrada  
-   **Escopos de política:** global, produto, API, operação  
  
## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como trabalhar com políticas, consulte:

+ [Políticas no Gerenciamento de API](api-management-howto-policies.md)
+ [Transformar APIs](transform-api.md)
+ [Referência de Política](api-management-policy-reference.md) para uma lista completa das instruções de política e suas configurações
+ [Exemplos de política](policy-samples.md)   