---
title: "políticas de gerenciamento de API de cache do aaaAzure | Microsoft Docs"
description: "Saiba mais sobre Olá cache políticas disponíveis para uso no gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 8147199c-24d8-439f-b2a9-da28a70a890c
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: bd6b0721945609b28dbf6e7ef0631979c08c8c65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-caching-policies"></a>Políticas de cache do Gerenciamento de API
Este tópico fornece uma referência para Olá políticas de gerenciamento de API a seguir. Para obter mais informações sobre como adicionar e configurar políticas, consulte [Políticas de Gerenciamento de API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="CachingPolicies"></a> Políticas de cache  
  
-   Resposta das políticas de cache  
  
    -   [Obter do cache](api-management-caching-policies.md#GetFromCache): executa a pesquisa em cache e retorna uma resposta válida armazenada em cache quando disponível.  
  
    -   [Armazenar toocache](api-management-caching-policies.md#StoreToCache) - respostas de Caches de acordo com o toohello configuração de controle de cache especificado.  
  
-   Valor das políticas de cache  
  
    -   [Obter valor do cache](#GetFromCacheByKey) - Recupere um item em cache por chave.  
  
    -   [Armazena o valor em cache](#StoreToCacheByKey) -armazenar um item no cache de saudação por chave.  
  
    -   [Remova o valor do cache](#RemoveCacheByKey) -remover um item no cache de saudação por chave.  
  
##  <a name="GetFromCache"></a> Obter do cache  
 Saudação de uso `cache-lookup` cache da política de tooperform pesquisar e retornar uma resposta válida de cache quando disponível. Esta política deve ser aplicada em casos nos quais o conteúdo da resposta permanece estático por um período de tempo. O cache de resposta reduz a largura de banda e requisitos de processamento impostos Olá back-end da web server e reduz a latência percebida pelos consumidores de API.  
  
> [!NOTE]
>  Essa diretiva deve ter um correspondente [toocache repositório](api-management-caching-policies.md#StoreToCache) política.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression tooevaluate)">  
  <vary-by-header>Accept</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Accept-Charset</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Authorization</vary-by-header>  
  <!-- should be present when allow-authorized-response-caching is "true"-->  
  <vary-by-header>header name</vary-by-header>  
  <!-- optional, can repeated several times -->  
  <vary-by-query-parameter>parameter name</vary-by-query-parameter>  
  <!-- optional, can repeated several times -->  
</cache-lookup>  
```  
  
### <a name="examples"></a>Exemplos  
  
#### <a name="example"></a>Exemplo  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="none" must-revalidate="true">  
            <vary-by-query-parameter>version</vary-by-query-parameter>  
        </cache-lookup>           
    </inbound>  
    <outbound>  
        <cache-store duration="seconds" />  
        <base />          
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a>Exemplo usando expressões de política  
 Este exemplo mostra como resposta de gerenciamento de API tootooconfigure cache duração que corresponde ao Olá cache de resposta do serviço de back-end Olá conforme especificado pelas Olá feito do serviço `Cache-Control` diretiva. Para ver uma demonstração de como configurar e usar essa política, consulte [nuvem abrangem episódio 177: mais recursos de gerenciamento de API com Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e Avançar too25:25.  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 Para obter mais informações, veja [Expressões de política](api-management-policy-expressions.md) e [Variável de contexto](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|  
|----------|-----------------|--------------|  
|cache-lookup|Elemento raiz.|Sim|  
|vary-by-header|Inicie o cache de respostas por valor de cabeçalho especificado, como Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.|Não|  
|vary-by-query-parameter|Inicie o cache de respostas de acordo com o valor dos parâmetros de consulta especificados. Insira somente um ou múltiplos parâmetros. Use ponto e vírgula como um separador. Se nenhum for especificado, todos os parâmetros de consulta serão usados.|Não|  
  
### <a name="attributes"></a>Atributos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|allow-private-response-caching|Quando definido muito`true`, permite armazenar em cache de solicitações que contêm um cabeçalho de autorização.|Não|false|  
|downstream-caching-type|Esse atributo deve ser definido como tooone de saudação valores a seguir.<br /><br /> -   none: o cache downstream não é permitido.<br />-   private: o cache downstream privado é permitido.<br />-   public: o cache downstream privado e compartilhado é permitido.|Não|nenhum|  
|must-revalidate|Quando o cache downstream é habilitado esse atributo ativa ou desativa a saudação `must-revalidate` diretiva de controle de cache em respostas de gateway.|Não|verdadeiro|  
|vary-by-developer|Definir muito`true` respostas toocache por chave de desenvolvedor.|Não|false|  
|vary-by-developer-groups|Definir muito`true` respostas toocache por função de usuário.|Não|false|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** de entrada  
  
-   **Escopos de política:** API, operação, produto  
  
##  <a name="StoreToCache"></a>Repositório toocache  
 Olá `cache-store` especificado de respostas de caches de política toohello de acordo com as configurações de cache. Esta política deve ser aplicada em casos nos quais o conteúdo da resposta permanece estático por um período de tempo. O cache de resposta reduz a largura de banda e requisitos de processamento impostos Olá back-end da web server e reduz a latência percebida pelos consumidores de API.  
  
> [!NOTE]
>  Esta política deve ter uma política [Obter do cache](api-management-caching-policies.md#GetFromCache) correspondente.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a>Exemplos  
  
#### <a name="example"></a>Exemplo  
  
```xml  
<policies>  
    <inbound>  
        <base />  
          <cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false">  
                <vary-by-query-parameter>parameter name</vary-by-query-parameter> <!-- optional, can repeated several times -->  
        </cache-lookup>  
    </inbound>  
    <outbound>  
        <base />  
            <cache-store duration="3600" />  
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a>Exemplo usando expressões de política  
 Este exemplo mostra como resposta de gerenciamento de API tootooconfigure cache duração que corresponde ao Olá cache de resposta do serviço de back-end Olá conforme especificado pelas Olá feito do serviço `Cache-Control` diretiva. Para ver uma demonstração de como configurar e usar essa política, consulte [nuvem abrangem episódio 177: mais recursos de gerenciamento de API com Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e Avançar too25:25.  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 Para obter mais informações, veja [Expressões de política](api-management-policy-expressions.md) e [Variável de contexto](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|  
|----------|-----------------|--------------|  
|cache-store|Elemento raiz.|Sim|  
  
### <a name="attributes"></a>Atributos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|duration|Tempo de vida de saudação armazenados em cache as entradas, especificadas em segundos.|Sim|N/D|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** saída  
  
-   **Escopos de política:** API, operação, produto  
  
##  <a name="GetFromCacheByKey"></a> Obter valor do cache  
 Saudação de uso `cache-lookup-value` política tooperform pesquisa de cache por chave e retornam um valor armazenado em cache. chave de saudação pode ter um valor de cadeia de caracteres arbitrária e normalmente é fornecido usando uma expressão de política.  
  
> [!NOTE]
>  É necessário ter uma política correspondente de [Armazenar valor em cache](#StoreToCacheByKey).  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value toouse if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a>Exemplo  
 Para saber mais e obter exemplos dessa política, veja [Cache personalizado no Gerenciamento de API do Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|  
|----------|-----------------|--------------|  
|cache-lookup-value|Elemento raiz.|Sim|  
  
### <a name="attributes"></a>Atributos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|default-value|Um valor que será atribuído toohello variável se a pesquisa de chave de cache Olá resultou em um erro. Se esse atributo não for especificado, `null` é atribuído.|Não|`null`|  
|chave|Toouse de valor de chave na pesquisa de saudação do cache.|Sim|N/D|  
|variable-name|Nome da saudação [variável de contexto](api-management-policy-expressions.md#ContextVariables) Olá pesquisado o valor será atribuído, se a pesquisa for bem-sucedida. Se a pesquisa resulta em um erro, variável Olá será atribuído valor Olá Olá `default-value` atributo ou `null`, se hello `default-value` atributo for omitido.|Sim|N/D|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções da política:** entrada, saída, back-end, em caso de erro  
  
-   **Escopos de política:** global, API, operação, produto  
  
##  <a name="StoreToCacheByKey"></a> Armazenar valor em cache  
 Olá `cache-store-value` executa o armazenamento em cache por chave. chave de saudação pode ter um valor de cadeia de caracteres arbitrária e normalmente é fornecido usando uma expressão de política.  
  
> [!NOTE]
>  Esta política deve ter uma política [Obter valor do cache](#GetFromCacheByKey) correspondente.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<cache-store-value key="cache key value" value="value toocache" duration="seconds" />  
```  
  
### <a name="example"></a>Exemplo  
 Para saber mais e obter exemplos dessa política, veja [Cache personalizado no Gerenciamento de API do Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|  
|----------|-----------------|--------------|  
|cache-store-value|Elemento raiz.|Sim|  
  
### <a name="attributes"></a>Atributos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|duration|Valor serão armazenadas em cache para Olá fornecido valor de duração, especificado em segundos.|Sim|N/D|  
|chave|Valor de chave saudação do cache será armazenado em.|Sim|N/D|  
|valor|Olá toobe de valor armazenado em cache.|Sim|N/D|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções da política:** entrada, saída, back-end, em caso de erro  
  
-   **Escopos de política:** global, API, operação, produto  
  
###  <a name="RemoveCacheByKey"></a> Remover valor do cache  
 Olá `cache-remove-value` exclui um item em cache identificado por sua chave. chave de saudação pode ter um valor de cadeia de caracteres arbitrária e normalmente é fornecido usando uma expressão de política.  
  
#### <a name="policy-statement"></a>Declaração de política  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a>Exemplo  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|  
|----------|-----------------|--------------|  
|cache-remove-value|Elemento raiz.|Sim|  
  
#### <a name="attributes"></a>Atributos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|chave|chave de saudação do hello previamente armazenados em cache toobe valor removido do cache de saudação.|Sim|N/D|  
  
#### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .  
  
-   **Seções da política:** entrada, saída, back-end, em caso de erro  
  
-   **Escopos de política:** global, API, operação, produto  
  

## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre como trabalhar com políticas, veja [Políticas em Gerenciamento de API](api-management-howto-policies.md).  