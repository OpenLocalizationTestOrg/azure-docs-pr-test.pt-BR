---
title: "Gerenciamento de API de aaaAzure políticas entre domínios | Microsoft Docs"
description: "Saiba mais sobre Olá políticas entre domínios disponíveis para uso no gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7689d277-8abe-472a-a78c-e6d4bd43455d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: dd5ebfd65b92ebd0c1f589a2bac669a3928d40b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-cross-domain-policies"></a>Políticas entre domínios de Gerenciamento de API
Este tópico fornece uma referência para Olá políticas de gerenciamento de API a seguir. Para obter mais informações sobre como adicionar e configurar políticas, consulte [Políticas de Gerenciamento de API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="CrossDomainPolicies"></a> Políticas entre domínios  
  
-   [Permitir chamadas entre domínios](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -torna Olá API acessível de clientes baseados em navegador Microsoft Silverlight e Adobe Flash.  
  
-   [CORS](api-management-cross-domain-policies.md#CORS) -adiciona o compartilhamento de recursos entre origens (CORS) suporte para a operação de tooan ou chama um API entre tooallow domínios de clientes baseados em navegador.  
  
-   [JSONP](api-management-cross-domain-policies.md#JSONP) - adiciona JSON com a operação de tooan de suporte de preenchimento (JSONP) ou chama um API entre tooallow domínios de clientes baseados em navegador do JavaScript.  
  
##  <a name="AllowCrossDomainCalls"></a> Permitir chamadas entre domínios  
 Saudação de uso `cross-domain` Olá toomake de política API acessível de clientes baseados em navegador Microsoft Silverlight e Adobe Flash.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in hello Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a>Exemplo  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|  
|----------|-----------------|--------------|  
|cross-domain|Elemento raiz. Elementos filho devem estar de acordo com toohello [especificação de arquivo de política entre domínios do Adobe](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).|Sim|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** de entrada  
  
-   **Escopos de política:** global  
  
##  <a name="CORS"></a> CORS  
 Olá `cors` política adiciona o compartilhamento de recursos entre origens (CORS) suporte para a operação de tooan ou chama um API entre tooallow domínios de clientes baseados em navegador.  
  
 CORS permite que um navegador e um servidor toointeract e determinar se as solicitações de tooallow específicas entre origens (ou seja, chamadas XMLHttpRequests feitas do JavaScript em domínios de tooother uma página da web). Isso permite maior flexibilidade do que permitir somente solicitações com a mesma origem, mas é mais seguro do que permitir todas as solicitações entre origens.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<cors allow-credentials="false|true">  
    <allowed-origins>  
        <origin>origin uri</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="number of seconds">  
        <method>http verb</method>  
    </allowed-methods>  
    <allowed-headers>  
        <header>header name</header>  
    </allowed-headers>  
    <expose-headers>  
        <header>header name</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="example"></a>Exemplo  
 Este exemplo demonstra como solicitar toosupport preliminares, como aquelas com cabeçalhos personalizados ou métodos diferentes de GET e POST. cabeçalhos personalizados toosupport e verbos HTTP adicionais, use Olá `allowed-methods` e `allowed-headers` seções, conforme mostrado no exemplo a seguir de saudação.  
  
```xml  
<cors allow-credentials="true">  
    <allowed-origins>  
        <!-- Localhost useful for development -->  
        <origin>http://localhost:8080/</origin>  
        <origin>http://example.com/</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="300">  
        <method>GET</method>  
        <method>POST</method>  
        <method>PATCH</method>  
        <method>DELETE</method>  
    </allowed-methods>  
    <allowed-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
        <header>x-zumo-version</header>  
        <header>x-zumo-auth</header>  
        <header>content-type</header>  
        <header>accept</header>  
    </allowed-headers>  
    <expose-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|cors|Elemento raiz.|Sim|N/D|  
|allowed-origins|Contém `origin` elementos que descrevem a saudação permitida origens para solicitações entre domínios. `allowed-origins`pode conter um único `origin` elemento especifica `*` tooallow qualquer origem ou de um ou mais `origin` elementos que contêm um URI.|Sim|N/D|  
|origin|Olá valor pode ser `*` tooallow todas as origens ou um URI que especifica uma origem única. Olá URI deve incluir um esquema, host e porta.|Sim|Se a porta de saudação for omitida em um URI, porta 80 é usada para HTTP e é usada a porta 443 para HTTPS.|  
|allowed-methods|Esse elemento é necessário se métodos diferentes de GET ou POST forem permitidos. Contém `method` elementos que especificam a saudação suporte para verbos HTTP.|Não|Se esta seção não estiver presente, GET e POST são compatíveis.|  
|estático|Especifica um verbo HTTP.|Pelo menos um `method` elemento é necessário se hello `allowed-methods` seção estiver presente.|N/D|  
|allowed-headers|Esse elemento contém `header` elementos especificando os nomes dos cabeçalhos de saudação que podem ser incluídos na solicitação de saudação.|Não|N/D|  
|expose-headers|Esse elemento contém `header` elementos especificando os nomes dos cabeçalhos de saudação que poderá ser acessados pelo cliente hello.|Não|N/D|  
|cabeçalho|Especifica um nome de cabeçalho.|Pelo menos um `header` elemento é necessário em `allowed-headers` ou `expose-headers` se Olá seção estiver presente.|N/D|  
  
### <a name="attributes"></a>Atributos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|allow-credentials|Olá `Access-Control-Allow-Credentials` cabeçalho de resposta de simulação hello serão toohello defina o valor desse atributo e afeta as credenciais de toosubmit de capacidade do cliente Olá nas solicitações entre domínios.|Não|false|  
|preflight-result-max-age|Olá `Access-Control-Max-Age` cabeçalho de resposta de simulação hello serão toohello defina o valor desse atributo e afeta a resposta de simulação do agente do usuário Olá capacidade toocache.|Não|0|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** de entrada  
  
-   **Escopos de política:** API, operação  
  
##  <a name="JSONP"></a> JSONP  
 Olá `jsonp` política adiciona JSON com preenchimento de operação de tooan de suporte (JSONP) ou um chamadas à API tooallow entre domínios de clientes baseados em navegador do JavaScript. JSONP é um método usado nos dados de toorequest programas JavaScript de um servidor em um domínio diferente. JSONP ignora a limitação de saudação imposta pela maioria dos navegadores da web onde as páginas de acesso a tooweb devem estar no hello mesmo domínio.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a>Exemplo  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 Se você chamar o método hello sem parâmetro de retorno de chamada Olá? cb = XXX retornará JSON simples (sem um invólucro de chamada de função).  
  
 Se você adicionar o parâmetro de retorno de chamada hello `?cb=XXX` ele retornará um resultado JSONP, encapsulamento resultados JSON originais de saudação em torno da função de retorno de chamada hello como`XYZ('<json result goes here>');`  
  
### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|  
|----------|-----------------|--------------|  
|jsonp|Elemento raiz.|Sim|  
  
### <a name="attributes"></a>Atributos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|callback-parameter-name|Olá chamada de função JavaScript entre domínios prefixado com o nome de domínio totalmente qualificado do hello onde hello função reside.|Sim|N/D|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** saída  
  
-   **Escopos de política:** global, produto, API, operação  
  
## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre como trabalhar com políticas, veja [Políticas em Gerenciamento de API](api-management-howto-policies.md).  