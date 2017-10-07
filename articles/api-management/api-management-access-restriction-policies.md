---
title: "políticas de restrição de acesso de gerenciamento de API aaaAzure | Microsoft Docs"
description: "Saiba mais sobre políticas de restrição de acesso de saudação disponíveis para uso no gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 034febe3-465f-4840-9fc6-c448ef520b0f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 0ef368c2781d9a5cf9eaaa41a47489c904ed3198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-access-restriction-policies"></a>Políticas de restrição de acesso do Gerenciamento de API
Este tópico fornece uma referência para Olá políticas de gerenciamento de API a seguir. Para obter mais informações sobre como adicionar e configurar políticas, consulte [Políticas de Gerenciamento de API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="AccessRestrictionPolicies"></a> Políticas de restrição de acesso  
  
-   [Verificar cabeçalho HTTP](api-management-access-restriction-policies.md#CheckHTTPHeader) - Impõe a existência e/ou valor de um cabeçalho HTTP.  
  
-   [Limitar a taxa de chamada por assinatura](api-management-access-restriction-policies.md#LimitCallRate) - Previne picos de uso da API limitando a taxa de chamada, baseado em assinatura.  
  
-   [Limitar a taxa de chamada por chave](#LimitCallRateByKey) - Previne picos de uso da API limitando a taxa de chamada, baseado em chave.  
  
-   [Restringir IP do autor da chamada](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filtra (permite/recusa) chamadas de endereços IP específicos e/ou intervalos de endereços.  
  
-   [Definir a cota de uso por assinatura](api-management-access-restriction-policies.md#SetUsageQuota) -permite que você tooenforce uma vida útil ou renovável chamada volume e/ou a largura de banda de cota, em uma base por assinatura.  
  
-   [Definir a cota de uso pela chave](#SetUsageQuotaByKey) -permite que você tooenforce uma vida útil ou renovável chamada volume e/ou a largura de banda de cota, em uma base por chave.  
  
-   [Validar JWT](api-management-access-restriction-policies.md#ValidateJWT) - Impõe a existência e a validade de JWT extraída de um cabeçalho HTTP especificado ou um parâmetro de consulta especificado.  
  
##  <a name="CheckHTTPHeader"></a> Verificar cabeçalho HTTP  
 Saudação de uso `check-header` tooenforce de política que uma solicitação tem um cabeçalho HTTP especificado. Opcionalmente, você pode verificar toosee se o cabeçalho de saudação tem um valor específico ou para um intervalo de valores permitidos. Se Olá verificação falhar, política de saudação termina o processamento da solicitação e retorna Olá HTTP status código e mensagem de erro especificada por política hello.  
  
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
|valor|Valor do cabeçalho HTTP permitido. Quando forem especificados vários elementos de valor, seleção de saudação é considerada um sucesso se qualquer um dos valores de saudação é uma correspondência.|Não|  
  
### <a name="attributes"></a>Atributos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|failed-check-error-message|Tooreturn de mensagem de erro no corpo de resposta HTTP de saudação se o cabeçalho de saudação não existe ou tem um valor inválido. Esta mensagem deve conter quaisquer caracteres especiais adequadamente seguidos por caracteres de escape.|Sim|N/D|  
|failed-check-httpcode|Tooreturn do código de HTTP Status se o cabeçalho de saudação não existe ou tem um valor inválido.|Sim|N/D|  
|header-name|nome de saudação do hello toocheck do cabeçalho HTTP.|Sim|N/D|  
|ignore-case|Pode ser definido tooTrue ou False. Se o conjunto tooTrue caso é ignorado quando o valor do cabeçalho Olá é comparado com o conjunto de saudação de valores aceitáveis.|Sim|N/D|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** de entrada, de saída  
  
-   **Escopos de política:** global, produto, API, operação  
  
##  <a name="LimitCallRate"></a> Limitar a taxa de chamadas por assinatura  
 Olá `rate-limit` política impede o uso da API picos em uma base por assinatura, limitando Olá chamar tooa taxa especificada número por um período de tempo especificado. Quando essa política é acionada chamador Olá recebe um `429 Too Many Requests` código de status de resposta.  
  
> [!IMPORTANT]
>  Essa política pode ser usada apenas uma vez por cada documento de política.  
>   
>  [Expressões de política](api-management-policy-expressions.md) não pode ser usado em qualquer um dos atributos de política Olá para esta política.  
  
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
|api|Adicione um ou mais desses elementos tooimpose um limite de taxa de chamada nas APIs no produto hello. Limites de taxa de chamadas à API e ao produto são aplicados de forma independente.|Não|  
|operation|Adicione um ou mais desses elementos tooimpose um limite de taxa de chamada nas operações em uma API. Limites de taxa de chamadas à API, operação e produto são aplicados de forma independente.|Não|  
  
### <a name="attributes"></a>Atributos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|name|nome de Olá do hello API para o limite de taxa que tooapply Olá.|Sim|N/D|  
|chamadas|Olá número total máximo de chamadas permitidas durante o intervalo de tempo de saudação especificado no hello `renewal-period`.|Sim|N/D|  
|renewal-period|saudação do período de tempo em segundos após o qual hello cota é redefinida.|Sim|N/D|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** de entrada  
  
-   **Escopos de política:** produto  
  
##  <a name="LimitCallRateByKey"></a> Limitar a taxa de chamadas por chave  
 Olá `rate-limit-by-key` política impede o uso da API picos em uma base por chave limitando Olá chamar tooa taxa especificada número por um período de tempo especificado. chave de saudação pode ter um valor de cadeia de caracteres arbitrária e normalmente é fornecido usando uma expressão de política. Condição de incremento opcional pode ser adicionada toospecify as solicitações que devem ser contadas até o limite de saudação. Quando essa política é acionada chamador Olá recebe um `429 Too Many Requests` código de status de resposta.  
  
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
 Em Olá exemplo a seguir, o limite de taxa de saudação é codificado por endereço IP do chamador Olá.  
  
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
|chamadas|Olá número total máximo de chamadas permitidas durante o intervalo de tempo de saudação especificado no hello `renewal-period`.|Sim|N/D|  
|counter-key|Olá toouse chave para política de limite de taxa de saudação.|Sim|N/D|  
|increment-condition|expressão booleana Hello, especificando se a solicitação Olá deve ser contabilizada em direção a cota de saudação (`true`).|Não|N/D|  
|renewal-period|saudação do período de tempo em segundos após o qual hello cota é redefinida.|Sim|N/D|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** de entrada  
  
-   **Escopos de política:** global, produto, API, operação  
  
##  <a name="RestrictCallerIPs"></a> Restringir IPs do chamador  
 Olá `ip-filter` política filtros de chamadas (permite/recusa) de endereços IP específicos e/ou intervalos de endereços.  
  
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
|endereço|Especifica um único endereço IP no qual toofilter.|Pelo menos um elemento `address` ou `address-range` é necessário.|  
|address-range from="address" to="address"|Especifica um intervalo de endereços IP no qual toofilter.|Pelo menos um elemento `address` ou `address-range` é necessário.|  
  
### <a name="attributes"></a>Atributos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|address-range from="address" to="address"|Um intervalo de IP endereços tooallow ou negar acesso.|Necessário quando hello `address-range` elemento é usado.|N/D|  
|ip-filter action="allow &#124; forbid"|Especifica se chamadas devem ser permitidas ou não para Olá especificado intervalos e endereços IP.|Sim|N/D|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** de entrada  
  
-   **Escopos de política:** global, produto, API, operação  
  
##  <a name="SetUsageQuota"></a> Definir a cota de uso por assinatura  
 Olá `quota` política impõe uma vida útil ou renovável chamada volume e/ou a largura de banda de cota, em uma base por assinatura.  
  
> [!IMPORTANT]
>  Essa política pode ser usada apenas uma vez por cada documento de política.  
>   
>  [Expressões de política](api-management-policy-expressions.md) não pode ser usado em qualquer um dos atributos de política Olá para esta política.  
  
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
|api|Adicione um ou mais desses elementos tooimpose uma cota nas APIs no produto hello. Cotas de API e produto são aplicadas de forma independente.|Não|  
|operation|Adicione um ou mais desses elementos tooimpose uma cota nas operações em uma API. Cotas de operações, APIs e produtos são aplicadas de forma independente.|Não|  
  
### <a name="attributes"></a>Atributos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|name|nome de saudação do hello API ou operação para o qual Olá cota se aplica.|Sim|N/D|  
|largura de banda|Olá número máximo total de quilobytes permitidos durante o intervalo de tempo de saudação especificado no hello `renewal-period`.|`calls` ou `bandwidth` ou ainda ambos juntos devem ser especificados.|N/D|  
|chamadas|Olá número total máximo de chamadas permitidas durante o intervalo de tempo de saudação especificado no hello `renewal-period`.|`calls` ou `bandwidth` ou ainda ambos juntos devem ser especificados.|N/D|  
|renewal-period|saudação do período de tempo em segundos após o qual hello cota é redefinida.|Sim|N/D|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** de entrada  
  
-   **Escopos de política:** produto  
  
##  <a name="SetUsageQuotaByKey"></a> Definir uma cota de uso por chave  
 Olá `quota-by-key` política impõe uma vida útil ou renovável chamada volume e/ou a largura de banda de cota, em uma base por chave. chave de saudação pode ter um valor de cadeia de caracteres arbitrária e normalmente é fornecido usando uma expressão de política. Condição de incremento opcional pode ser adicionada toospecify as solicitações que devem ser contadas em direção a cota de saudação.  
  
 Para obter mais informações e exemplos dessa política, consulte [Limitação de solicitação avançada com o Gerenciamento de API do Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).  
  
> [!IMPORTANT]
>  Essa política pode ser usada apenas uma vez por cada documento de política.  
>   
>  [Expressões de política](api-management-policy-expressions.md) não pode ser usado em qualquer um dos atributos de política Olá para esta política.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a>Exemplo  
 Em Olá exemplo a seguir, cota Olá é inserida pelo endereço IP do chamador hello.  
  
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
|largura de banda|Olá número máximo total de quilobytes permitidos durante o intervalo de tempo de saudação especificado no hello `renewal-period`.|`calls` ou `bandwidth` ou ainda ambos juntos devem ser especificados.|N/D|  
|chamadas|Olá número total máximo de chamadas permitidas durante o intervalo de tempo de saudação especificado no hello `renewal-period`.|`calls` ou `bandwidth` ou ainda ambos juntos devem ser especificados.|N/D|  
|counter-key|Olá toouse chave para a política de cota de saudação.|Sim|N/D|  
|increment-condition|expressão booleana Hello, especificando se a solicitação Olá deve ser contabilizada em direção a cota de saudação (`true`)|Não|N/D|  
|renewal-period|saudação do período de tempo em segundos após o qual hello cota é redefinida.|Sim|N/D|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** de entrada  
  
-   **Escopos de política:** global, produto, API, operação  
  
##  <a name="ValidateJWT"></a> Validar JWT  
 Olá `validate-jwt` política impõe a existência e a validade de um JWT extraído de um determinado cabeçalho HTTP ou um parâmetro de consulta especificado.  
  
> [!IMPORTANT]
>  Olá `validate-jwt` política requer que Olá `exp` declaração registrada é incluído (s) no token JWT hello, a menos que `require-expiration-time` atributo for especificado e definido muito`false`.  
> Olá `validate-jwt` diretiva dá suporte a algoritmos de assinatura HS256 e RS256. Para HS256 chave Olá deve ser fornecido embutido na política de saudação no formulário do hello codificado na base64. RS256 chave Olá tem toobe fornecer por meio de um ponto de extremidade de configuração do Open ID.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<validate-jwt   
    header-name="name of http header containing hello token (use query-parameter-name attribute if hello token is passed in hello URL)"   
    failed-validation-httpcode="http status code tooreturn on failure"   
    failed-validation-error-message="error message tooreturn on failure"   
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
    <claim name="name of hello claim as it appears in hello token" match="all|any">  
      <value>claim value as it is expected tooappear in hello token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of hello configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
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
  
#### <a name="authorize-access-toooperations-based-on-token-claims"></a>Autorizar toooperations de acesso baseado em declarações de token  
 Este exemplo mostra como Olá toouse [validar JWT](api-management-access-restriction-policies.md#ValidateJWT) política toopre-autorizar toooperations de acesso baseado em declarações de token. Para ver uma demonstração de como configurar e usar essa política, consulte [nuvem abrangem episódio 177: mais recursos de gerenciamento de API com Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e Avançar too13:50. Avanço too15:00 toosee políticas de saudação configuradas no editor de diretiva de saudação e, em seguida, too18:50 para ver uma demonstração de como chamar uma operação do portal do desenvolvedor do hello com e sem Olá necessário token de autorização.  
  
```xml  
<!-- Copy hello following snippet into hello inbound section at hello api (or higher) level toopre-authorize access toooperations based on token claims -->  
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
|públicos-alvo|Contém uma lista de declarações de público aceitáveis que podem estar presentes no token de saudação. Se vários valores de público-alvo estiverem presentes, cada valor será tentado até que todos sejam esgotados (nesse caso, a validação falhará) ou até obter êxito. Pelo menos um público-alvo deve ser especificado.|Não|  
|issuer-signing-keys|Uma lista de segurança codificada em Base64 chaves usadas toovalidate assinado tokens. Se várias chaves de segurança estiverem presentes, cada chave será tentada até que todas sejam esgotadas (nesse caso, a validação falhará) ou até obter êxito (útil para substituição de token). Elementos chave têm um recurso opcional `id` toomatch atributo usado contra `kid` de declaração.|Não|  
|emissores|Uma lista de entidades aceitáveis que emitiu o token de saudação. Se vários valores de emissor estiverem presentes, cada valor será tentado até que todos sejam esgotados (nesse caso, a validação falhará) ou até obter êxito.|Não|  
|openid-config|elemento de saudação usado para especificar um compatível com Open ID configuração ponto de extremidade do qual as chaves e o emissor de assinatura pode ser obtido.|Não|  
|required-claims|Contém uma lista de declarações esperadas toobe presente no token Olá para ele toobe considerado válido. Olá quando `match` atributo está definido muito`all` cada valor de declaração na diretiva Olá deve estar presente no token Olá para toosucceed de validação. Olá quando `match` atributo está definido muito`any` pelo menos uma declaração deve estar presente no token Olá para toosucceed de validação.|Não|  
|zumo-master-key|Chave mestra para tokens emitidos pelos Serviços Móveis do Azure|Não|  
  
### <a name="attributes"></a>Atributos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|clock-skew|Período de tempo. Fornece alguma reserva pequena no caso de declaração de expiração do token hello está presente no token hello e passou Olá atual data / hora.|Não|0 segundos|  
|failed-validation-error-message|Tooreturn de mensagem de erro no corpo de resposta HTTP de saudação se Olá JWT não passar na validação. Esta mensagem deve conter quaisquer caracteres especiais adequadamente seguidos por caracteres de escape.|Não|A mensagem de erro padrão depende do problema de validação, por exemplo, "O JWT não está presente."|  
|failed-validation-httpcode|Tooreturn do código de HTTP Status se Olá JWT não passa na validação.|Não|401|  
|header-name|nome de saudação do cabeçalho de saudação HTTP contém Olá token.|`header-name` ou `query-paremeter-name` deve ser especificado; mas não ambos.|N/D|  
|ID|Olá `id` atributo Olá `key` elemento permite toospecify Olá cadeia de caracteres será comparada à `kid` toofind de token (se houver) Olá out Olá toouse de chave apropriado para a validação de assinatura de declaração.|Não|N/D|  
|match|Olá `match` atributo Olá `claim` elemento Especifica se cada valor de declaração na diretiva Olá deve estar presente no token Olá para toosucceed de validação. Os valores possíveis são:<br /><br /> -                          `all`-cada valor de declaração na diretiva Olá deve estar presente no token Olá para toosucceed de validação.<br /><br /> -                          `any`-pelo menos uma declaração de valor deve estar presente no token Olá para toosucceed de validação.|Não|tudo|  
|query-paremeter-name|nome de Olá Olá Olá do parâmetro de consulta contém o token de saudação.|`header-name` ou `query-paremeter-name` deve ser especificado; mas não ambos.|N/D|  
|require-expiration-time|Booliano. Especifica se uma declaração de expiração é necessária no token de saudação.|Não|verdadeiro|
|require-scheme|Olá, por exemplo, o nome do esquema de token Olá, "Portador". Quando esse atributo é definido, política de saudação garantirá que especificado o esquema está presente no valor do cabeçalho de autorização de saudação.|Não|N/D|
|require-signed-tokens|Booliano. Especifica se um token é necessário toobe assinado.|Não|verdadeiro|  
|url|URL ponto de extremidade de configuração de Open ID da qual é possível obter os metadados de configuração de Open ID. Active Directory do Azure use Olá URL a seguir: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituindo o nome do locatário de diretório, por exemplo, `contoso.onmicrosoft.com`.|Sim|N/D|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** de entrada  
  
-   **Escopos de política:** global, produto, API, operação  
  
## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre como trabalhar com políticas, veja [Políticas em Gerenciamento de API](api-management-howto-policies.md).  
