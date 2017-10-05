---
title: "Políticas avançadas de Gerenciamento de API do Azure| Microsoft Docs"
description: "Saiba mais sobre as políticas avançadas disponíveis para uso no Gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 8a13348b-7856-428f-8e35-9e4273d94323
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 0c65ac74316421a0258f01143baa25ffecb5be3b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="api-management-advanced-policies"></a><span data-ttu-id="bf7fd-103">Políticas avançadas de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="bf7fd-103">API Management advanced policies</span></span>
<span data-ttu-id="bf7fd-104">Este tópico fornece uma referência para as políticas de Gerenciamento de API a seguir.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="bf7fd-105">Para obter mais informações sobre como adicionar e configurar políticas, consulte [Políticas de Gerenciamento de API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="bf7fd-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="bf7fd-106"><a name="AdvancedPolicies"></a> Políticas avançadas</span><span class="sxs-lookup"><span data-stu-id="bf7fd-106"><a name="AdvancedPolicies"></a> Advanced policies</span></span>  
  
-   <span data-ttu-id="bf7fd-107">[Controlar fluxo](api-management-advanced-policies.md#choose) - Aplica-se condicionalmente a instruções de políticas com base nos resultados da avaliação do booliano [expressions](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="bf7fd-107">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on the results of the evaluation of Boolean [expressions](api-management-policy-expressions.md).</span></span>  
  
-   <span data-ttu-id="bf7fd-108">[Encaminhar solicitação](#ForwardRequest) -Encaminha a solicitação ao serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-108">[Forward request](#ForwardRequest) - Forwards the request to the backend service.</span></span>

-   <span data-ttu-id="bf7fd-109">[Simultaneidade de limite](#LimitConcurrency) - impede que as políticas embutidas sejam executadas mais do que o número especificado de solicitações por vez.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-109">[Limit concurrency](#LimitConcurrency) - Prevents enclosed policies from executing by more than the specified number of requests at a time.</span></span>
  
-   <span data-ttu-id="bf7fd-110">[Registrar no Hub de Eventos](#log-to-eventhub) – envia mensagens no formato especificado para um Hub de Eventos definido por uma entidade Logger.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-110">[Log to Event Hub](#log-to-eventhub) - Sends messages in the specified format to an Event Hub defined by a Logger entity.</span></span> 

-   <span data-ttu-id="bf7fd-111">[Resposta fictícia](#mock-response) – anula a execução de pipeline e retorna uma resposta fictícia diretamente para o chamador.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-111">[Mock response](#mock-response) - Aborts pipeline execution and returns a mocked response directly to the caller.</span></span>
  
-   <span data-ttu-id="bf7fd-112">[Repetir](#Retry) - repete a execução das instruções de política, se e até que a condição seja atendida.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-112">[Retry](#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="bf7fd-113">A execução será repetida em intervalos de tempo especificados até e a contagem de repetições especificada.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-113">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>  
  
-   <span data-ttu-id="bf7fd-114">[Retornar resposta](#ReturnResponse) - Anula a execução de pipeline e retorna a resposta especificada diretamente para o autor da chamada.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-114">[Return response](#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span> 
  
-   <span data-ttu-id="bf7fd-115">[Enviar solicitação unidirecional](#SendOneWayRequest) - Envia uma solicitação para a URL especificada sem aguardar uma resposta.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-115">[Send one way request](#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>  
  
-   <span data-ttu-id="bf7fd-116">[Enviar solicitação](#SendRequest) - Envia uma solicitação para a URL especificada.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-116">[Send request](#SendRequest) - Sends a request to the specified URL.</span></span>  

-   <span data-ttu-id="bf7fd-117">[Definir proxy HTTP](#SetHttpProxy) – permite a você, por meio de um proxy HTTP, reencaminhar solicitações encaminhadas.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-117">[Set HTTP proxy](#SetHttpProxy) - Allows you to route forwarded requests via an HTTP proxy.</span></span>  

-   <span data-ttu-id="bf7fd-118">[Definir método de solicitação](#SetRequestMethod) - Permite alterar o método HTTP de uma solicitação.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-118">[Set request method](#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>  
  
-   <span data-ttu-id="bf7fd-119">[Definir código de status](#SetStatus) – altera o código de status de HTTP para o valor especificado.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-119">[Set status code](#SetStatus) - Changes the HTTP status code to the specified value.</span></span>  
  
-   <span data-ttu-id="bf7fd-120">[Definir variável](api-management-advanced-policies.md#set-variable) – persiste um valor em uma variável de [contexto](api-management-policy-expressions.md#ContextVariables) nomeada para acesso posterior.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-120">[Set variable](api-management-advanced-policies.md#set-variable) - Persists a value in a named [context](api-management-policy-expressions.md#ContextVariables) variable for later access.</span></span>  

-   <span data-ttu-id="bf7fd-121">[Rastreamento](#Trace) - adiciona uma cadeia de caracteres para a saída do [Inspetor de API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/).</span><span class="sxs-lookup"><span data-stu-id="bf7fd-121">[Trace](#Trace) - Adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
-   <span data-ttu-id="bf7fd-122">[Aguardar](#Wait) – aguarda a conclusão das políticas [Enviar solicitação](api-management-advanced-policies.md#SendRequest), [Obter valor do cache](api-management-caching-policies.md#GetFromCacheByKey) ou [Controlar fluxo](api-management-advanced-policies.md#choose) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-122">[Wait](#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies to complete before proceeding.</span></span>  
  
##  <span data-ttu-id="bf7fd-123"><a name="choose"></a> Controlar fluxo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-123"><a name="choose"></a> Control flow</span></span>  
 <span data-ttu-id="bf7fd-124">A política `choose` aplica declarações de política embutidas com base no resultado da avaliação de expressões boolianas, semelhantes a um if-then-else ou a um constructo de opção em uma linguagem de programação.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-124">The `choose` policy applies enclosed policy statements based on the outcome of evaluation of Boolean expressions, similar to an if-then-else or a switch construct in a programming language.</span></span>  
  
###  <span data-ttu-id="bf7fd-125"><a name="ChoosePolicyStatement"></a> Declaração de política</span><span class="sxs-lookup"><span data-stu-id="bf7fd-125"><a name="ChoosePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<choose>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements to be applied if the above condition is true  -->  
    </when>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements to be applied if the above condition is true  -->  
    </when>   
    <otherwise>   
        <!— one or more policy statements to be applied if none of the above conditions are true  -->  
</otherwise>   
</choose>  
```  
  
 <span data-ttu-id="bf7fd-126">A política de fluxo de controle deve conter pelo menos um elemento `<when/>`.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-126">The control flow policy must contain at least one `<when/>` element.</span></span> <span data-ttu-id="bf7fd-127">O elemento `<otherwise/>` é opcional.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-127">The `<otherwise/>` element is optional.</span></span> <span data-ttu-id="bf7fd-128">As condições nos elementos `<when/>` são avaliadas na ordem de aparecimento na política.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-128">Conditions in `<when/>` elements are evaluated in order of their appearance within the policy.</span></span> <span data-ttu-id="bf7fd-129">As declarações de política incluídas dentro do primeiro elemento `<when/>` com atributo de condição igual a `true` serão aplicadas.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-129">Policy statement(s) enclosed within the first `<when/>` element with condition attribute equals `true` will be applied.</span></span> <span data-ttu-id="bf7fd-130">As políticas incluídas dentro do elemento `<otherwise/>`, se estiverem presentes, serão aplicadas se todos os atributos de condição do elemento `<when/>` forem `false`.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-130">Policies enclosed within the `<otherwise/>` element, if present, will be applied if all of the `<when/>` element condition attributes are `false`.</span></span>  
  
### <a name="examples"></a><span data-ttu-id="bf7fd-131">Exemplos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-131">Examples</span></span>  
  
####  <span data-ttu-id="bf7fd-132"><a name="ChooseExample"></a> Exemplo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-132"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="bf7fd-133">O exemplo a seguir demonstra uma política [set-variable](api-management-advanced-policies.md#set-variable) e duas políticas de fluxo de controle.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-133">The following example demonstrates a [set-variable](api-management-advanced-policies.md#set-variable) policy and two control flow policies.</span></span>  
  
 <span data-ttu-id="bf7fd-134">A política de definir variável está na seção de entrada e cria uma variável de [contexto](api-management-policy-expressions.md#ContextVariables) booliana `isMobile` que será definida como true se o cabeçalho da solicitação `User-Agent` contiver o texto `iPad` ou `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-134">The set variable policy is in the inbound section and creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set to true if the `User-Agent` request header contains the text `iPad` or `iPhone`.</span></span>  
  
 <span data-ttu-id="bf7fd-135">A primeira política de fluxo de controle também está na seção de entrada e aplica condicionalmente uma de duas políticas [Definir parâmetro de cadeia de caracteres de consulta](api-management-transformation-policies.md#SetQueryStringParameter) dependendo do valor da variável de contexto `isMobile`.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-135">The first control flow policy is also in the inbound section, and conditionally applies one of two [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policies depending on the value of the `isMobile` context variable.</span></span>  
  
 <span data-ttu-id="bf7fd-136">A segunda política de fluxo de controle está na seção de saída e aplica condicionalmente a política [Converter XML para JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) quando `isMobile` é definida como `true`.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-136">The second control flow policy is in the outbound section and conditionally applies the [Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) policy when `isMobile` is set to `true`.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <set-variable name="isMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
        <base />  
        <choose>  
            <when condition="@(context.Variables.GetValueOrDefault<bool>("isMobile"))">  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>true</value>  
                </set-query-parameter>  
            </when>  
            <otherwise>  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>false</value>  
                </set-query-parameter>  
            </otherwise>  
        </choose>  
    </inbound>  
    <outbound>  
        <base />  
        <choose>  
            <when condition="@(context.GetValueOrDefault<bool>("isMobile"))">  
                <xml-to-json kind="direct" apply="always" consider-accept-header="false"/>  
            </when>  
        </choose>  
    </outbound>  
</policies>  
```  
  
#### <a name="example"></a><span data-ttu-id="bf7fd-137">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-137">Example</span></span>  
 <span data-ttu-id="bf7fd-138">Este exemplo mostra como executar a filtragem de conteúdo removendo elementos de dados da resposta recebida do serviço de back-end ao usar o produto `Starter`.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-138">This example shows how to perform content filtering by removing data elements from the response received from the backend service when using the `Starter` product.</span></span> <span data-ttu-id="bf7fd-139">Para ver uma demonstração da configuração e do uso dessa política, consulte [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Abordagem da Nuvem Episódio 177: Mais Recursos de Gerenciamento de API com Vlad Vinogradsky) e avance para 34:30.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-139">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 34:30.</span></span> <span data-ttu-id="bf7fd-140">Inicie em 31:50 para uma visão geral da [API da Previsão de Céu Escuro](https://developer.forecast.io/) usada para esta demonstração.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-140">Start  at 31:50 to see an overview of [The Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into the outbound section to remove a number of data elements from the response received from the backend service based on the name of the api product -->  
<choose>  
  <when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals("Starter"))">  
    <set-body>@{  
        var response = context.Response.Body.As<JObject>();  
        foreach (var key in new [] {"minutely", "hourly", "daily", "flags"}) {  
          response.Property (key).Remove ();  
        }  
        return response.ToString();  
      }  
    </set-body>  
  </when>  
</choose>  
```  
  
### <a name="elements"></a><span data-ttu-id="bf7fd-141">Elementos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-141">Elements</span></span>  
  
|<span data-ttu-id="bf7fd-142">Elemento</span><span class="sxs-lookup"><span data-stu-id="bf7fd-142">Element</span></span>|<span data-ttu-id="bf7fd-143">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-143">Description</span></span>|<span data-ttu-id="bf7fd-144">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-144">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf7fd-145">choose</span><span class="sxs-lookup"><span data-stu-id="bf7fd-145">choose</span></span>|<span data-ttu-id="bf7fd-146">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-146">Root element.</span></span>|<span data-ttu-id="bf7fd-147">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-147">Yes</span></span>|  
|<span data-ttu-id="bf7fd-148">when</span><span class="sxs-lookup"><span data-stu-id="bf7fd-148">when</span></span>|<span data-ttu-id="bf7fd-149">A condição a ser usada para as partes `if` ou `ifelse` da política `choose`.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-149">The condition to use for the `if` or `ifelse` parts of the `choose` policy.</span></span> <span data-ttu-id="bf7fd-150">Se política `choose` tiver várias seções `when`, elas serão avaliadas sequencialmente.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-150">If the `choose` policy has multiple `when` sections, they are evaluated sequentially.</span></span> <span data-ttu-id="bf7fd-151">Uma vez que o `condition` de um elemento when é avaliado como `true`, nenhuma outra condição `when` é avaliada.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-151">Once the `condition` of a when element evaluates to `true`, no further `when` conditions are evaluated.</span></span>|<span data-ttu-id="bf7fd-152">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-152">Yes</span></span>|  
|<span data-ttu-id="bf7fd-153">otherwise</span><span class="sxs-lookup"><span data-stu-id="bf7fd-153">otherwise</span></span>|<span data-ttu-id="bf7fd-154">Contém o trecho de código da política a ser usado se nenhuma das condições `when` for avaliada como `true`.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-154">Contains the policy snippet to be used if none of the `when` conditions evaluate to `true`.</span></span>|<span data-ttu-id="bf7fd-155">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-155">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf7fd-156">Atributos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-156">Attributes</span></span>  
  
|<span data-ttu-id="bf7fd-157">Atributo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-157">Attribute</span></span>|<span data-ttu-id="bf7fd-158">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-158">Description</span></span>|<span data-ttu-id="bf7fd-159">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-159">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="bf7fd-160">condition="Boolean expression &#124; Boolean constant"</span><span class="sxs-lookup"><span data-stu-id="bf7fd-160">condition="Boolean expression &#124; Boolean constant"</span></span>|<span data-ttu-id="bf7fd-161">A constante ou expressão booliana a ser avaliada quando a declaração de política contendo `when` é avaliada.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-161">The Boolean expression or constant to evaluated when the containing `when` policy statement is evaluated.</span></span>|<span data-ttu-id="bf7fd-162">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-162">Yes</span></span>|  
  
###  <span data-ttu-id="bf7fd-163"><a name="ChooseUsage"></a> Uso</span><span class="sxs-lookup"><span data-stu-id="bf7fd-163"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="bf7fd-164">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-164">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf7fd-165">**Seções da política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="bf7fd-165">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bf7fd-166">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-166">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bf7fd-167"><a name="ForwardRequest"></a> Encaminhar solicitação</span><span class="sxs-lookup"><span data-stu-id="bf7fd-167"><a name="ForwardRequest"></a> Forward request</span></span>  
 <span data-ttu-id="bf7fd-168">A política `forward-request` encaminha a solicitação de entrada para o serviço de back-end especificado na variável de [contexto](api-management-policy-expressions.md#ContextVariables) de solicitação.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-168">The `forward-request` policy forwards the incoming request to the backend service specified in the request [context](api-management-policy-expressions.md#ContextVariables).</span></span> <span data-ttu-id="bf7fd-169">A URL do serviço de back-end é especificada nas [configurações](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) de API e pode ser alterada usando a política [definir o serviço de back-end](api-management-transformation-policies.md).</span><span class="sxs-lookup"><span data-stu-id="bf7fd-169">The backend service URL is specified in the API  [settings](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) and can be changed using the [set backend service](api-management-transformation-policies.md) policy.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="bf7fd-170">A remoção dessa política resulta na solicitação não ser encaminhada para o serviço de back-end e as políticas na seção de saída serem avaliadas imediatamente após a conclusão bem-sucedida das políticas na seção de entrada.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-170">Removing this policy results in the request not being forwarded to the backend service and the policies in the outbound section are evaluated immediately upon the successful completion of the policies in the inbound section.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bf7fd-171">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="bf7fd-171">Policy statement</span></span>  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a><span data-ttu-id="bf7fd-172">Exemplos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-172">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="bf7fd-173">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-173">Example</span></span>  
 <span data-ttu-id="bf7fd-174">A política de nível de API a seguir encaminha todas as solicitações para o serviço de back-end com um intervalo de tempo limite de 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-174">The following API level policy forwards all requests to the backend service with a timeout interval of 60 seconds.</span></span>  
  
```xml  
<!-- api level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="60"/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="bf7fd-175">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-175">Example</span></span>  
 <span data-ttu-id="bf7fd-176">Esta política de nível de operação usa o elemento `base` para herdar a política de back-end do escopo de nível de API pai.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-176">This operation level policy uses the `base` element to inherit the backend policy from the parent API level scope.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <base/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="bf7fd-177">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-177">Example</span></span>  
 <span data-ttu-id="bf7fd-178">Essa política de nível de operação explicitamente encaminha todas as solicitações para o serviço de back-end com um tempo limite de 120 e não herda a política de back-end do nível da API pai.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-178">This operation level policy explicitly forwards all requests to the backend service with a timeout of 120 and does not inherit the parent API level backend policy.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="120"/>   
        <!-- effective policy. note the absence of <base/> -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="bf7fd-179">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-179">Example</span></span>  
 <span data-ttu-id="bf7fd-180">Essa política de nível de operação não encaminha solicitações para o serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-180">This operation level policy does not forward requests to the backend service.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <!-- no forwarding to backend -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="bf7fd-181">Elementos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-181">Elements</span></span>  
  
|<span data-ttu-id="bf7fd-182">Elemento</span><span class="sxs-lookup"><span data-stu-id="bf7fd-182">Element</span></span>|<span data-ttu-id="bf7fd-183">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-183">Description</span></span>|<span data-ttu-id="bf7fd-184">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-184">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf7fd-185">forward-request</span><span class="sxs-lookup"><span data-stu-id="bf7fd-185">forward-request</span></span>|<span data-ttu-id="bf7fd-186">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-186">Root element.</span></span>|<span data-ttu-id="bf7fd-187">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-187">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf7fd-188">Atributos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-188">Attributes</span></span>  
  
|<span data-ttu-id="bf7fd-189">Atributo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-189">Attribute</span></span>|<span data-ttu-id="bf7fd-190">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-190">Description</span></span>|<span data-ttu-id="bf7fd-191">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-191">Required</span></span>|<span data-ttu-id="bf7fd-192">Padrão</span><span class="sxs-lookup"><span data-stu-id="bf7fd-192">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bf7fd-193">timeout="integer"</span><span class="sxs-lookup"><span data-stu-id="bf7fd-193">timeout="integer"</span></span>|<span data-ttu-id="bf7fd-194">O intervalo de tempo limite em segundos antes de a chamada para o serviço de back-end falhar.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-194">The timeout interval in seconds before the call to the backend service fails.</span></span>|<span data-ttu-id="bf7fd-195">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-195">No</span></span>|<span data-ttu-id="bf7fd-196">Sem tempo limite</span><span class="sxs-lookup"><span data-stu-id="bf7fd-196">No timeout</span></span>|  
|<span data-ttu-id="bf7fd-197">follow-redirects="true &#124; false"</span><span class="sxs-lookup"><span data-stu-id="bf7fd-197">follow-redirects="true &#124; false"</span></span>|<span data-ttu-id="bf7fd-198">Especifica se os redirecionamentos do serviço de back-end são seguidos pelo gateway ou retornados ao chamador.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-198">Specifies whether redirects from the backend service are followed by the gateway or returned to the caller.</span></span>|<span data-ttu-id="bf7fd-199">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-199">No</span></span>|<span data-ttu-id="bf7fd-200">false</span><span class="sxs-lookup"><span data-stu-id="bf7fd-200">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bf7fd-201">Uso</span><span class="sxs-lookup"><span data-stu-id="bf7fd-201">Usage</span></span>  
 <span data-ttu-id="bf7fd-202">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-202">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf7fd-203">**Seções de política:** back-end</span><span class="sxs-lookup"><span data-stu-id="bf7fd-203">**Policy sections:** backend</span></span>  
  
-   <span data-ttu-id="bf7fd-204">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-204">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bf7fd-205"><a name="LimitConcurrency"></a> Simultaneidade de limite</span><span class="sxs-lookup"><span data-stu-id="bf7fd-205"><a name="LimitConcurrency"></a> Limit concurrency</span></span>  
 <span data-ttu-id="bf7fd-206">A política `limit-concurrency` impede que as políticas embutidas sejam executadas mais do que o número especificado de solicitações em um determinado momento.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-206">The `limit-concurrency` policy prevents enclosed policies from executing by more than the specified number of requests at a given time.</span></span> <span data-ttu-id="bf7fd-207">Ao exceder o limite, novas solicitações são adicionadas a uma fila, até que o comprimento máximo da fila seja atingido.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-207">Upon exceeding the threshold, new requests are added to a queue, until the maximum queue length is achieved.</span></span> <span data-ttu-id="bf7fd-208">Quando a fila atinge seu máximo, novas solicitações falham imediatamente.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-208">Upon queue exhaustion, new requests will fail immediately.</span></span>
  
###  <span data-ttu-id="bf7fd-209"><a name="LimitConcurrencyStatement"></a> Declaração de política</span><span class="sxs-lookup"><span data-stu-id="bf7fd-209"><a name="LimitConcurrencyStatement"></a> Policy statement</span></span>  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a><span data-ttu-id="bf7fd-210">Exemplos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-210">Examples</span></span>  
  
####  <span data-ttu-id="bf7fd-211"><a name="ChooseExample"></a> Exemplo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-211"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="bf7fd-212">O exemplo a seguir demonstra como limitar o número de solicitações encaminhadas a um back-end com base no valor de uma variável de contexto.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-212">The following example demonstrates how to limit number of requests forwarded to a backend based on the value of a context variable.</span></span>
 
```xml  
<policies>
  <inbound>…</inbound>
  <backend>
    <limit-concurrency key="@((string)context.Variables["connectionId"])" max-count="3" timeout="60">
      <forward-request timeout="120"/>
    <limit-concurrency/>
  </backend>
  <outbound>…</outbound>
</policies>
```

### <a name="elements"></a><span data-ttu-id="bf7fd-213">Elementos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-213">Elements</span></span>  
  
|<span data-ttu-id="bf7fd-214">Elemento</span><span class="sxs-lookup"><span data-stu-id="bf7fd-214">Element</span></span>|<span data-ttu-id="bf7fd-215">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-215">Description</span></span>|<span data-ttu-id="bf7fd-216">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-216">Required</span></span>|  
|-------------|-----------------|--------------|    
|<span data-ttu-id="bf7fd-217">limit-concurrency</span><span class="sxs-lookup"><span data-stu-id="bf7fd-217">limit-concurrency</span></span>|<span data-ttu-id="bf7fd-218">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-218">Root element.</span></span>|<span data-ttu-id="bf7fd-219">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf7fd-220">Atributos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-220">Attributes</span></span>  
  
|<span data-ttu-id="bf7fd-221">Atributo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-221">Attribute</span></span>|<span data-ttu-id="bf7fd-222">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-222">Description</span></span>|<span data-ttu-id="bf7fd-223">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-223">Required</span></span>|<span data-ttu-id="bf7fd-224">Padrão</span><span class="sxs-lookup"><span data-stu-id="bf7fd-224">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="bf7fd-225">chave</span><span class="sxs-lookup"><span data-stu-id="bf7fd-225">key</span></span>|<span data-ttu-id="bf7fd-226">Uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-226">A string.</span></span> <span data-ttu-id="bf7fd-227">Expressão permitida.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-227">Expression allowed.</span></span> <span data-ttu-id="bf7fd-228">Especifica o escopo de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-228">Specifies the concurrency scope.</span></span> <span data-ttu-id="bf7fd-229">Pode ser compartilhado por várias políticas.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-229">Can be shared by multiple policies.</span></span>|<span data-ttu-id="bf7fd-230">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-230">Yes</span></span>|<span data-ttu-id="bf7fd-231">N/D</span><span class="sxs-lookup"><span data-stu-id="bf7fd-231">N/A</span></span>|  
|<span data-ttu-id="bf7fd-232">max-count</span><span class="sxs-lookup"><span data-stu-id="bf7fd-232">max-count</span></span>|<span data-ttu-id="bf7fd-233">Um inteiro.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-233">An integer.</span></span> <span data-ttu-id="bf7fd-234">Especifica um número máximo de solicitações que são permitidas para inserir a política.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-234">Specifies a maximum number of requests that are allowed to enter the policy.</span></span>|<span data-ttu-id="bf7fd-235">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-235">Yes</span></span>|<span data-ttu-id="bf7fd-236">N/D</span><span class="sxs-lookup"><span data-stu-id="bf7fd-236">N/A</span></span>|  
|<span data-ttu-id="bf7fd-237">Tempo limite</span><span class="sxs-lookup"><span data-stu-id="bf7fd-237">timeout</span></span>|<span data-ttu-id="bf7fd-238">Um inteiro.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-238">An integer.</span></span> <span data-ttu-id="bf7fd-239">Expressão permitida.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-239">Expression allowed.</span></span> <span data-ttu-id="bf7fd-240">Especifica o número de segundos que uma solicitação deve esperar para inserir um escopo antes de falhar com "403 Muitas solicitações"</span><span class="sxs-lookup"><span data-stu-id="bf7fd-240">Specifies the number of seconds a request should wait to enter a scope before failing with "403 Too Many Requests"</span></span>|<span data-ttu-id="bf7fd-241">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-241">No</span></span>|<span data-ttu-id="bf7fd-242">Infinito</span><span class="sxs-lookup"><span data-stu-id="bf7fd-242">Infinity</span></span>|  
|<span data-ttu-id="bf7fd-243">max-queue-length</span><span class="sxs-lookup"><span data-stu-id="bf7fd-243">max-queue-length</span></span>|<span data-ttu-id="bf7fd-244">Um inteiro.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-244">An integer.</span></span> <span data-ttu-id="bf7fd-245">Expressão permitida.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-245">Expression allowed.</span></span> <span data-ttu-id="bf7fd-246">Especifica o comprimento máximo da fila.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-246">Specifies the maximum queue length.</span></span> <span data-ttu-id="bf7fd-247">Solicitações de entrada que tentarem inserir essa política serão encerradas com "403 Muitas solicitações" assim que a fila atingir seu comprimento máximo.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-247">Incoming requests trying to enter this policy will be terminated with “403 Too Many Requests” immediately when the queue is exhausted.</span></span>|<span data-ttu-id="bf7fd-248">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-248">No</span></span>|<span data-ttu-id="bf7fd-249">Infinito</span><span class="sxs-lookup"><span data-stu-id="bf7fd-249">Infinity</span></span>|  
  
###  <span data-ttu-id="bf7fd-250"><a name="ChooseUsage"></a> Uso</span><span class="sxs-lookup"><span data-stu-id="bf7fd-250"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="bf7fd-251">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-251">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf7fd-252">**Seções da política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="bf7fd-252">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bf7fd-253">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-253">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="bf7fd-254"><a name="log-to-eventhub"></a> Registrar no Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-254"><a name="log-to-eventhub"></a> Log to Event Hub</span></span>  
 <span data-ttu-id="bf7fd-255">A política `log-to-eventhub` envia mensagens no formato especificado para um Hub de Eventos definido por uma entidade Logger.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-255">The `log-to-eventhub` policy sends messages in the specified format to an Event Hub defined by a Logger entity.</span></span> <span data-ttu-id="bf7fd-256">Como o nome sugere, a política é usada para salvar informações de contexto de solicitação ou de resposta solicitadas para a análise online ou offline.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-256">As its name implies, the policy is used for saving selected request or response context information for online or offline analysis.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="bf7fd-257">Para obter um guia passo a passo sobre como configurar um hub de eventos e registrar eventos, consulte [Como registrar eventos em log para Hubs de Eventos do Azure no Gerenciamento de API](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="bf7fd-257">For a step-by-step guide on configuring an event hub and logging events, see [How to log API Management events with Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bf7fd-258">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="bf7fd-258">Policy statement</span></span>  
  
```xml  
<log-to-eventhub logger-id="id of the logger entity" partition-id="index of the partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string to be logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a><span data-ttu-id="bf7fd-259">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-259">Example</span></span>  
 <span data-ttu-id="bf7fd-260">Qualquer cadeia de caracteres pode ser usada como o valor a ser registrado em Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-260">Any string can be used as the value to be logged in Event Hubs.</span></span> <span data-ttu-id="bf7fd-261">Neste exemplo, a data e hora, nome do serviço de implantação, a ID de solicitação, endereço IP e o nome da operação para todas as chamadas de entrada são registrados no agente do hub de eventos registrado com a ID `contoso-logger`.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-261">In this example the date and time, deployment service name, request id, ip address, and operation name for all inbound calls are logged to the event hub Logger registered with the `contoso-logger` id.</span></span>  
  
```xml  
<policies>  
  <inbound>  
    <log-to-eventhub logger-id ='contoso-logger'>  
      @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name) )   
    </log-to-eventhub>  
  </inbound>  
  <outbound>          
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="bf7fd-262">Elementos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-262">Elements</span></span>  
  
|<span data-ttu-id="bf7fd-263">Elemento</span><span class="sxs-lookup"><span data-stu-id="bf7fd-263">Element</span></span>|<span data-ttu-id="bf7fd-264">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-264">Description</span></span>|<span data-ttu-id="bf7fd-265">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-265">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf7fd-266">log-to-eventhub</span><span class="sxs-lookup"><span data-stu-id="bf7fd-266">log-to-eventhub</span></span>|<span data-ttu-id="bf7fd-267">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-267">Root element.</span></span> <span data-ttu-id="bf7fd-268">O valor desse elemento é a cadeia de caracteres a ser registrada no seu hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-268">The value of this element is the string to log to your event hub.</span></span>|<span data-ttu-id="bf7fd-269">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-269">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf7fd-270">Atributos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-270">Attributes</span></span>  
  
|<span data-ttu-id="bf7fd-271">Atributo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-271">Attribute</span></span>|<span data-ttu-id="bf7fd-272">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-272">Description</span></span>|<span data-ttu-id="bf7fd-273">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-273">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="bf7fd-274">logger-id</span><span class="sxs-lookup"><span data-stu-id="bf7fd-274">logger-id</span></span>|<span data-ttu-id="bf7fd-275">A ID do agente registrada com o serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-275">The id of the Logger registered with your API Management service.</span></span>|<span data-ttu-id="bf7fd-276">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-276">Yes</span></span>|  
|<span data-ttu-id="bf7fd-277">partition-id</span><span class="sxs-lookup"><span data-stu-id="bf7fd-277">partition-id</span></span>|<span data-ttu-id="bf7fd-278">Especifica o índice da partição em que as mensagens são enviadas.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-278">Specifies the index of the partition where messages are sent.</span></span>|<span data-ttu-id="bf7fd-279">Opcional.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-279">Optional.</span></span> <span data-ttu-id="bf7fd-280">Esse atributo não poderá ser usado se `partition-key` for usado.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-280">This attribute may not be used if `partition-key` is used.</span></span>|  
|<span data-ttu-id="bf7fd-281">partition-key</span><span class="sxs-lookup"><span data-stu-id="bf7fd-281">partition-key</span></span>|<span data-ttu-id="bf7fd-282">Especifica o valor usado para a atribuição de partição quando as mensagens são enviadas.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-282">Specifies the value used for partition assignment when messages are sent.</span></span>|<span data-ttu-id="bf7fd-283">Opcional.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-283">Optional.</span></span> <span data-ttu-id="bf7fd-284">Esse atributo não poderá ser usado se `partition-id` for usado.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-284">This attribute may not be used if `partition-id` is used.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bf7fd-285">Uso</span><span class="sxs-lookup"><span data-stu-id="bf7fd-285">Usage</span></span>  
 <span data-ttu-id="bf7fd-286">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-286">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf7fd-287">**Seções da política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="bf7fd-287">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bf7fd-288">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-288">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="bf7fd-289"><a name="mock-response"></a> Resposta fictícia</span><span class="sxs-lookup"><span data-stu-id="bf7fd-289"><a name="mock-response"></a> Mock response</span></span>  
<span data-ttu-id="bf7fd-290">O `mock-response`, como o nome indica, é usado para simular APIs e operações.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-290">The `mock-response`, as the name implies, is used to mock APIs and operations.</span></span> <span data-ttu-id="bf7fd-291">Ele anula a execução normal de pipeline e retorna uma resposta fictícia ao chamador.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-291">It aborts normal pipeline execution and returns a mocked response to the caller.</span></span> <span data-ttu-id="bf7fd-292">A política sempre tenta retornar respostas da mais alta fidelidade.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-292">The policy always tries to return responses of highest fidelity.</span></span> <span data-ttu-id="bf7fd-293">Ela prefere exemplos de conteúdo de resposta, sempre que disponíveis.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-293">It prefers response content examples, whenever available.</span></span> <span data-ttu-id="bf7fd-294">Ela gera respostas de exemplo com base em esquemas, quando esquemas são fornecidos e exemplos não são fornecidos.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-294">It generates sample responses from schemas, when schemas are provided and examples are not.</span></span> <span data-ttu-id="bf7fd-295">Se não forem encontrados exemplos nem esquemas, serão retornadas respostas sem conteúdo.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-295">If neither examples or schemas are found, responses with no content are returned.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="bf7fd-296">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="bf7fd-296">Policy statement</span></span>  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="bf7fd-297">Exemplos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-297">Examples</span></span>  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, the content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, the content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a><span data-ttu-id="bf7fd-298">Elementos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-298">Elements</span></span>  
  
|<span data-ttu-id="bf7fd-299">Elemento</span><span class="sxs-lookup"><span data-stu-id="bf7fd-299">Element</span></span>|<span data-ttu-id="bf7fd-300">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-300">Description</span></span>|<span data-ttu-id="bf7fd-301">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-301">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf7fd-302">mock-response</span><span class="sxs-lookup"><span data-stu-id="bf7fd-302">mock-response</span></span>|<span data-ttu-id="bf7fd-303">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-303">Root element.</span></span>|<span data-ttu-id="bf7fd-304">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-304">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf7fd-305">Atributos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-305">Attributes</span></span>  
  
|<span data-ttu-id="bf7fd-306">Atributo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-306">Attribute</span></span>|<span data-ttu-id="bf7fd-307">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-307">Description</span></span>|<span data-ttu-id="bf7fd-308">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-308">Required</span></span>|<span data-ttu-id="bf7fd-309">Padrão</span><span class="sxs-lookup"><span data-stu-id="bf7fd-309">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="bf7fd-310">status-code</span><span class="sxs-lookup"><span data-stu-id="bf7fd-310">status-code</span></span>|<span data-ttu-id="bf7fd-311">Especifica o código de status da resposta e é usado para selecionar o exemplo ou o esquema correspondente.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-311">Specifies response status code and is used to select corresponding example or schema.</span></span>|<span data-ttu-id="bf7fd-312">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-312">No</span></span>|<span data-ttu-id="bf7fd-313">200</span><span class="sxs-lookup"><span data-stu-id="bf7fd-313">200</span></span>|  
|<span data-ttu-id="bf7fd-314">content-type</span><span class="sxs-lookup"><span data-stu-id="bf7fd-314">content-type</span></span>|<span data-ttu-id="bf7fd-315">Especifica o valor de cabeçalho da resposta `Content-Type` e é usado para selecionar o exemplo ou o esquema correspondente.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-315">Specifies `Content-Type` response header value and is used to select corresponding example or schema.</span></span>|<span data-ttu-id="bf7fd-316">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-316">No</span></span>|<span data-ttu-id="bf7fd-317">Nenhum</span><span class="sxs-lookup"><span data-stu-id="bf7fd-317">None</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bf7fd-318">Uso</span><span class="sxs-lookup"><span data-stu-id="bf7fd-318">Usage</span></span>  
 <span data-ttu-id="bf7fd-319">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-319">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf7fd-320">**Seções de política:** de entrada, de saída, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="bf7fd-320">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="bf7fd-321">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-321">**Policy scopes:** all scopes</span></span>

##  <span data-ttu-id="bf7fd-322"><a name="Retry"></a> Repetir</span><span class="sxs-lookup"><span data-stu-id="bf7fd-322"><a name="Retry"></a> Retry</span></span>  
 <span data-ttu-id="bf7fd-323">A política `retry` executa suas políticas filho uma vez e tenta realizar sua execução novamente até `condition` da nova tentativa se tornar `false` ou `count` da nova tentativa ser esgotada.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-323">The             `retry` policy executes its child policies once and then retries their execution until the retry `condition` becomes            `false` or retry            `count` is exhausted.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bf7fd-324">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="bf7fd-324">Policy statement</span></span>  
  
```xml  
  
<retry  
    condition="boolean expression or literal"  
    count="number of retry attempts"  
    interval="retry interval in seconds"  
    max-interval="maximum retry interval in seconds"  
    delta="retry interval delta in seconds"  
    first-fast-retry="boolean expression or literal">  
        <!-- One or more child policies. No restrictions -->  
</retry>  
  
```  
  
### <a name="example"></a><span data-ttu-id="bf7fd-325">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-325">Example</span></span>  
 <span data-ttu-id="bf7fd-326">No exemplo a seguir o encaminhamento de solicitação será repetido até dez vezes usando o algoritmo de nova tentativa exponencial.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-326">In the following example request forewarding is retried up to ten times using exponential retry algorithm.</span></span> <span data-ttu-id="bf7fd-327">Uma vez que `first-fast-retry` é definido como false, todas novas tentativas estão sujeitas ao algoritmo de nova tentativa exponencial.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-327">Since                    `first-fast-retry` is set to false, all retry attempts are subject to the exponsntial retry algorithm.</span></span>  
  
```xml  
  
<retry  
    condition="@(context.Response.StatusCode == 500)"  
    count="10"  
    interval="10"  
    max-interval="100"  
    delta="10"  
    first-fast-retry="false">  
        <forward-request />  
</retry>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="bf7fd-328">Elementos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-328">Elements</span></span>  
  
|<span data-ttu-id="bf7fd-329">Elemento</span><span class="sxs-lookup"><span data-stu-id="bf7fd-329">Element</span></span>|<span data-ttu-id="bf7fd-330">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-330">Description</span></span>|<span data-ttu-id="bf7fd-331">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-331">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf7fd-332">tentar novamente</span><span class="sxs-lookup"><span data-stu-id="bf7fd-332">retry</span></span>|<span data-ttu-id="bf7fd-333">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-333">Root element.</span></span> <span data-ttu-id="bf7fd-334">Pode conter quaisquer outras políticas como seus elementos filho.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-334">May contain any other policies as its child elements.</span></span>|<span data-ttu-id="bf7fd-335">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-335">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf7fd-336">Atributos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-336">Attributes</span></span>  
  
|<span data-ttu-id="bf7fd-337">Atributo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-337">Attribute</span></span>|<span data-ttu-id="bf7fd-338">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-338">Description</span></span>|<span data-ttu-id="bf7fd-339">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-339">Required</span></span>|<span data-ttu-id="bf7fd-340">Padrão</span><span class="sxs-lookup"><span data-stu-id="bf7fd-340">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bf7fd-341">condition</span><span class="sxs-lookup"><span data-stu-id="bf7fd-341">condition</span></span>|<span data-ttu-id="bf7fd-342">Uma [expressão](api-management-policy-expressions.md) ou literal booliano especificando se as novas tentativas devem ser paradas (`false`) ou continuadas (`true`).</span><span class="sxs-lookup"><span data-stu-id="bf7fd-342">A boolean literal or [expression](api-management-policy-expressions.md) specifying if retries should be stopped (`false`) or continued (`true`).</span></span>|<span data-ttu-id="bf7fd-343">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-343">Yes</span></span>|<span data-ttu-id="bf7fd-344">N/D</span><span class="sxs-lookup"><span data-stu-id="bf7fd-344">N/A</span></span>|  
|<span data-ttu-id="bf7fd-345">count</span><span class="sxs-lookup"><span data-stu-id="bf7fd-345">count</span></span>|<span data-ttu-id="bf7fd-346">Um número positivo que especifica o número máximo de novas tentativas a serem realizadas.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-346">A positive number specifying the maximum number of retries to attempt.</span></span>|<span data-ttu-id="bf7fd-347">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-347">Yes</span></span>|<span data-ttu-id="bf7fd-348">N/D</span><span class="sxs-lookup"><span data-stu-id="bf7fd-348">N/A</span></span>|  
|<span data-ttu-id="bf7fd-349">intervalo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-349">interval</span></span>|<span data-ttu-id="bf7fd-350">Um número positivo, em segundos, que especifica o intervalo de espera entre as novas tentativas.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-350">A positive number in seconds specifying the wait interval between the retry attempts.</span></span>|<span data-ttu-id="bf7fd-351">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-351">Yes</span></span>|<span data-ttu-id="bf7fd-352">N/D</span><span class="sxs-lookup"><span data-stu-id="bf7fd-352">N/A</span></span>|  
|<span data-ttu-id="bf7fd-353">max-interval</span><span class="sxs-lookup"><span data-stu-id="bf7fd-353">max-interval</span></span>|<span data-ttu-id="bf7fd-354">Um número positivo, em segundos, que especifica o intervalo de espera máximo entre as novas tentativas.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-354">A positive number in seconds specifying the maximum wait interval between the retry attempts.</span></span> <span data-ttu-id="bf7fd-355">Ele é usado para implementar um algoritmo de nova tentativa exponencial.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-355">It is used to implement an exponential retry algorithm.</span></span>|<span data-ttu-id="bf7fd-356">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-356">No</span></span>|<span data-ttu-id="bf7fd-357">N/D</span><span class="sxs-lookup"><span data-stu-id="bf7fd-357">N/A</span></span>|  
|<span data-ttu-id="bf7fd-358">delta</span><span class="sxs-lookup"><span data-stu-id="bf7fd-358">delta</span></span>|<span data-ttu-id="bf7fd-359">Um número positivo, em segundos, que especifica o incremento do intervalo de espera.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-359">A positive number in seconds specifying the wait interval increment.</span></span> <span data-ttu-id="bf7fd-360">Ele é usado para implementar algoritmos de nova tentativa exponenciais e lineares.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-360">It is used to implement the linear and exponential retry algorithms.</span></span>|<span data-ttu-id="bf7fd-361">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-361">No</span></span>|<span data-ttu-id="bf7fd-362">N/D</span><span class="sxs-lookup"><span data-stu-id="bf7fd-362">N/A</span></span>|  
|<span data-ttu-id="bf7fd-363">first-fast-retry</span><span class="sxs-lookup"><span data-stu-id="bf7fd-363">first-fast-retry</span></span>|<span data-ttu-id="bf7fd-364">Se definido como `true`, a primeira nova tentativa será realizada imediatamente.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-364">If set to                                    `true` , the first retry attempt is performed immediately.</span></span>|<span data-ttu-id="bf7fd-365">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-365">No</span></span>|`false`|  
  
> [!NOTE]
>  <span data-ttu-id="bf7fd-366">Quando apenas `interval` for especificado, novas tentativas de intervalo **fixo** serão realizadas.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-366">When only the `interval` is specified, **fixed** interval retries are performed.</span></span>  
>  <span data-ttu-id="bf7fd-367">Quando apenas `interval` e `delta` forem especificados, um algoritmo de nova tentativa de intervalo **linear** será usado, em que o tempo de espera entre as novas tentativas é calculado de acordo com a seguinte fórmula – `interval + (count - 1)*delta`.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-367">When only the `interval` and `delta` are specified, a **linear** interval retry algorithm is used, where wait time between retries is calculated according the following formula - `interval + (count - 1)*delta`.</span></span>  
>  <span data-ttu-id="bf7fd-368">Quando `interval`, `max-interval` e `delta` forem especificados, o algoritmo de nova tentativa de intervalo **exponencial** será aplicado, em que o tempo de espera entre as novas tentativas aumenta exponencialmente do valor de `interval` até o valor de `max-interval` de acordo com a seguinte fórmula – `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-368">When the `interval`, `max-interval` and `delta` are specified, **exponential** interval retry algorithm is applied, where the wait time between the retries is growing exponentially from the value of `interval` to the value `max-interval` according to the following forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span></span>  
  
### <a name="usage"></a><span data-ttu-id="bf7fd-369">Uso</span><span class="sxs-lookup"><span data-stu-id="bf7fd-369">Usage</span></span>  
 <span data-ttu-id="bf7fd-370">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-370">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span> <span data-ttu-id="bf7fd-371">Observe que as restrições de uso de política filho serão herdadas por essa política.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-371">Note that child policy usage restrictions will be inherited by this policy.</span></span>  
  
-   <span data-ttu-id="bf7fd-372">**Seções da política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="bf7fd-372">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bf7fd-373">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-373">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bf7fd-374"><a name="ReturnResponse"></a> Retornar resposta</span><span class="sxs-lookup"><span data-stu-id="bf7fd-374"><a name="ReturnResponse"></a> Return response</span></span>  
 <span data-ttu-id="bf7fd-375">A política `return-response` anula a execução do pipeline e retorna uma resposta padrão ou personalizada para o chamador.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-375">The `return-response` policy aborts pipeline execution and returns either a default or custom response to the caller.</span></span> <span data-ttu-id="bf7fd-376">A resposta padrão é `200 OK` sem corpo.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-376">Default response is `200 OK` with no body.</span></span> <span data-ttu-id="bf7fd-377">A resposta personalizada pode ser especificada por meio de declarações de política ou variável de contexto.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-377">Custom response can be specified via a context variable or policy statements.</span></span> <span data-ttu-id="bf7fd-378">Quando ambas são fornecidas, a resposta contida na variável de contexto é modificada pelas instruções de política antes de ser retornada para o chamador.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-378">When both are provided, the response contained within the context variable is modified by the policy statements before being returned to the caller.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bf7fd-379">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="bf7fd-379">Policy statement</span></span>  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a><span data-ttu-id="bf7fd-380">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-380">Example</span></span>  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="bf7fd-381">Elementos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-381">Elements</span></span>  
  
|<span data-ttu-id="bf7fd-382">Elemento</span><span class="sxs-lookup"><span data-stu-id="bf7fd-382">Element</span></span>|<span data-ttu-id="bf7fd-383">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-383">Description</span></span>|<span data-ttu-id="bf7fd-384">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-384">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf7fd-385">return-response</span><span class="sxs-lookup"><span data-stu-id="bf7fd-385">return-response</span></span>|<span data-ttu-id="bf7fd-386">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-386">Root element.</span></span>|<span data-ttu-id="bf7fd-387">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-387">Yes</span></span>|  
|<span data-ttu-id="bf7fd-388">set-header</span><span class="sxs-lookup"><span data-stu-id="bf7fd-388">set-header</span></span>|<span data-ttu-id="bf7fd-389">Uma declaração de política [set-header](api-management-transformation-policies.md#SetHTTPheader).</span><span class="sxs-lookup"><span data-stu-id="bf7fd-389">A [set-header](api-management-transformation-policies.md#SetHTTPheader) policy statement.</span></span>|<span data-ttu-id="bf7fd-390">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-390">No</span></span>|  
|<span data-ttu-id="bf7fd-391">set-body</span><span class="sxs-lookup"><span data-stu-id="bf7fd-391">set-body</span></span>|<span data-ttu-id="bf7fd-392">Uma declaração de política [set-body](api-management-transformation-policies.md#SetBody).</span><span class="sxs-lookup"><span data-stu-id="bf7fd-392">A [set-body](api-management-transformation-policies.md#SetBody) policy statement.</span></span>|<span data-ttu-id="bf7fd-393">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-393">No</span></span>|  
|<span data-ttu-id="bf7fd-394">set-status</span><span class="sxs-lookup"><span data-stu-id="bf7fd-394">set-status</span></span>|<span data-ttu-id="bf7fd-395">Uma declaração de política [set-status](api-management-advanced-policies.md#SetStatus).</span><span class="sxs-lookup"><span data-stu-id="bf7fd-395">A [set-status](api-management-advanced-policies.md#SetStatus) policy statement.</span></span>|<span data-ttu-id="bf7fd-396">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-396">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf7fd-397">Atributos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-397">Attributes</span></span>  
  
|<span data-ttu-id="bf7fd-398">Atributo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-398">Attribute</span></span>|<span data-ttu-id="bf7fd-399">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-399">Description</span></span>|<span data-ttu-id="bf7fd-400">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-400">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="bf7fd-401">response-variable-name</span><span class="sxs-lookup"><span data-stu-id="bf7fd-401">response-variable-name</span></span>|<span data-ttu-id="bf7fd-402">O nome da variável de contexto referenciada de, por exemplo, uma política [send-request](api-management-advanced-policies.md#SendRequest) upstream e que contém um objeto `Response`</span><span class="sxs-lookup"><span data-stu-id="bf7fd-402">The name of the context variable referenced from, for example, an upstream [send-request](api-management-advanced-policies.md#SendRequest) policy and containing a `Response` object</span></span>|<span data-ttu-id="bf7fd-403">Opcional.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-403">Optional.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bf7fd-404">Uso</span><span class="sxs-lookup"><span data-stu-id="bf7fd-404">Usage</span></span>  
 <span data-ttu-id="bf7fd-405">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-405">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf7fd-406">**Seções da política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="bf7fd-406">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bf7fd-407">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-407">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bf7fd-408"><a name="SendOneWayRequest"></a> Enviar solicitação unidirecional</span><span class="sxs-lookup"><span data-stu-id="bf7fd-408"><a name="SendOneWayRequest"></a> Send one way request</span></span>  
 <span data-ttu-id="bf7fd-409">A política `send-one-way-request` envia a solicitação fornecida para a URL especificada sem aguardar uma resposta.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-409">The `send-one-way-request` policy sends the provided request to the specified URL without waiting for a response.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bf7fd-410">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="bf7fd-410">Policy statement</span></span>  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="bf7fd-411">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-411">Example</span></span>  
 <span data-ttu-id="bf7fd-412">Essa política de exemplo mostra um exemplo de uso da política `send-one-way-request` para enviar uma mensagem para uma sala de chat do Slack se o código de resposta HTTP for maior ou igual a 500.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-412">This sample policy shows an example of using the `send-one-way-request` policy to send a message to a Slack chat room if the HTTP response code is greater than or equal to 500.</span></span> <span data-ttu-id="bf7fd-413">Para obter mais informações sobre esse exemplo, consulte [Uso dos serviços externos do serviço de Gerenciamento de API do Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="bf7fd-413">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="bf7fd-414">Elementos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-414">Elements</span></span>  
  
|<span data-ttu-id="bf7fd-415">Elemento</span><span class="sxs-lookup"><span data-stu-id="bf7fd-415">Element</span></span>|<span data-ttu-id="bf7fd-416">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-416">Description</span></span>|<span data-ttu-id="bf7fd-417">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-417">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf7fd-418">send-one-way-request</span><span class="sxs-lookup"><span data-stu-id="bf7fd-418">send-one-way-request</span></span>|<span data-ttu-id="bf7fd-419">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-419">Root element.</span></span>|<span data-ttu-id="bf7fd-420">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-420">Yes</span></span>|  
|<span data-ttu-id="bf7fd-421">url</span><span class="sxs-lookup"><span data-stu-id="bf7fd-421">url</span></span>|<span data-ttu-id="bf7fd-422">A URL da solicitação.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-422">The URL of the request.</span></span>|<span data-ttu-id="bf7fd-423">Não se mode=copy, caso contrário, sim.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-423">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="bf7fd-424">estático</span><span class="sxs-lookup"><span data-stu-id="bf7fd-424">method</span></span>|<span data-ttu-id="bf7fd-425">O método HTTP para a solicitação.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-425">The HTTP method for the request.</span></span>|<span data-ttu-id="bf7fd-426">Não se mode=copy, caso contrário, sim.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-426">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="bf7fd-427">cabeçalho</span><span class="sxs-lookup"><span data-stu-id="bf7fd-427">header</span></span>|<span data-ttu-id="bf7fd-428">Cabeçalho da solicitação.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-428">Request header.</span></span> <span data-ttu-id="bf7fd-429">Use vários elementos de cabeçalho para vários cabeçalhos de solicitação.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-429">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="bf7fd-430">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-430">No</span></span>|  
|<span data-ttu-id="bf7fd-431">corpo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-431">body</span></span>|<span data-ttu-id="bf7fd-432">O corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-432">The request body.</span></span>|<span data-ttu-id="bf7fd-433">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-433">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf7fd-434">Atributos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-434">Attributes</span></span>  
  
|<span data-ttu-id="bf7fd-435">Atributo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-435">Attribute</span></span>|<span data-ttu-id="bf7fd-436">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-436">Description</span></span>|<span data-ttu-id="bf7fd-437">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-437">Required</span></span>|<span data-ttu-id="bf7fd-438">Padrão</span><span class="sxs-lookup"><span data-stu-id="bf7fd-438">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bf7fd-439">mode="string"</span><span class="sxs-lookup"><span data-stu-id="bf7fd-439">mode="string"</span></span>|<span data-ttu-id="bf7fd-440">Determina se esta é uma nova solicitação ou uma cópia da solicitação atual.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-440">Determines whether this is a new request or a copy of the current request.</span></span> <span data-ttu-id="bf7fd-441">No modo de saída, mode=copy não inicializa o corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-441">In outbound mode, mode=copy does not initialize the request body.</span></span>|<span data-ttu-id="bf7fd-442">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-442">No</span></span>|<span data-ttu-id="bf7fd-443">Novo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-443">New</span></span>|  
|<span data-ttu-id="bf7fd-444">name</span><span class="sxs-lookup"><span data-stu-id="bf7fd-444">name</span></span>|<span data-ttu-id="bf7fd-445">Especifica o nome do cabeçalho a ser definido.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-445">Specifies the name of the header to be set.</span></span>|<span data-ttu-id="bf7fd-446">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-446">Yes</span></span>|<span data-ttu-id="bf7fd-447">N/D</span><span class="sxs-lookup"><span data-stu-id="bf7fd-447">N/A</span></span>|  
|<span data-ttu-id="bf7fd-448">exists-action</span><span class="sxs-lookup"><span data-stu-id="bf7fd-448">exists-action</span></span>|<span data-ttu-id="bf7fd-449">Especifica a ação a ser adotada quando o cabeçalho já foi especificado.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-449">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="bf7fd-450">Este atributo deve ter um dos valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-450">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="bf7fd-451">– override – substitui o valor do cabeçalho existente.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-451">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="bf7fd-452">– skip – não substitui o valor do cabeçalho existente.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-452">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="bf7fd-453">– append – acrescenta o valor ao valor do cabeçalho existente.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-453">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="bf7fd-454">– delete – remove o cabeçalho da solicitação.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-454">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="bf7fd-455">Quando definido como `override`, listar diversas entradas com o mesmo nome faz com que o cabeçalho seja definido de acordo com todas as entradas (que serão listadas várias vezes); somente valores listados serão definidos no resultado.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-455">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="bf7fd-456">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-456">No</span></span>|<span data-ttu-id="bf7fd-457">override</span><span class="sxs-lookup"><span data-stu-id="bf7fd-457">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bf7fd-458">Uso</span><span class="sxs-lookup"><span data-stu-id="bf7fd-458">Usage</span></span>  
 <span data-ttu-id="bf7fd-459">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-459">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf7fd-460">**Seções da política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="bf7fd-460">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bf7fd-461">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-461">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bf7fd-462"><a name="SendRequest"></a> Enviar solicitação</span><span class="sxs-lookup"><span data-stu-id="bf7fd-462"><a name="SendRequest"></a> Send request</span></span>  
 <span data-ttu-id="bf7fd-463">A política `send-request` envia a solicitação fornecida para a URL especificada, aguardando não mais do que o valor de tempo limite definido.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-463">The `send-request` policy sends the provided request to the specified URL, waiting no longer than the set timeout value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bf7fd-464">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="bf7fd-464">Policy statement</span></span>  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="bf7fd-465">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-465">Example</span></span>  
 <span data-ttu-id="bf7fd-466">Este exemplo mostra uma maneira de verificar um token de referência com um servidor de autorização.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-466">This example shows one way to verify a reference token with an authorization server.</span></span> <span data-ttu-id="bf7fd-467">Para obter mais informações sobre esse exemplo, consulte [Uso dos serviços externos do serviço de Gerenciamento de API do Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="bf7fd-467">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<inbound>  
  <!-- Extract Token from Authorization header parameter -->  
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />  
  
  <!-- Send request to Token Server to validate token (see RFC 7662) -->  
  <send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">  
    <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>  
    <set-method>POST</set-method>  
    <set-header name="Authorization" exists-action="override">  
      <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>  
    </set-header>  
    <set-header name="Content-Type" exists-action="override">  
      <value>application/x-www-form-urlencoded</value>  
    </set-header>  
    <set-body>@($"token={(string)context.Variables["token"]}")</set-body>  
  </send-request>  
  
  <choose>  
        <!-- Check active property in response -->  
        <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
            <!-- Return 401 Unauthorized with http-problem payload -->  
            <return-response response-variable-name="existing response variable">  
                <set-status code="401" reason="Unauthorized" />  
                <set-header name="WWW-Authenticate" exists-action="override">  
                    <value>Bearer error="invalid_token"</value>  
                </set-header>  
            </return-response>  
        </when>  
    </choose>  
  <base />  
</inbound>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="bf7fd-468">Elementos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-468">Elements</span></span>  
  
|<span data-ttu-id="bf7fd-469">Elemento</span><span class="sxs-lookup"><span data-stu-id="bf7fd-469">Element</span></span>|<span data-ttu-id="bf7fd-470">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-470">Description</span></span>|<span data-ttu-id="bf7fd-471">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-471">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf7fd-472">send-request</span><span class="sxs-lookup"><span data-stu-id="bf7fd-472">send-request</span></span>|<span data-ttu-id="bf7fd-473">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-473">Root element.</span></span>|<span data-ttu-id="bf7fd-474">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-474">Yes</span></span>|  
|<span data-ttu-id="bf7fd-475">url</span><span class="sxs-lookup"><span data-stu-id="bf7fd-475">url</span></span>|<span data-ttu-id="bf7fd-476">A URL da solicitação.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-476">The URL of the request.</span></span>|<span data-ttu-id="bf7fd-477">Não se mode=copy, caso contrário, sim.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-477">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="bf7fd-478">estático</span><span class="sxs-lookup"><span data-stu-id="bf7fd-478">method</span></span>|<span data-ttu-id="bf7fd-479">O método HTTP para a solicitação.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-479">The HTTP method for the request.</span></span>|<span data-ttu-id="bf7fd-480">Não se mode=copy, caso contrário, sim.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-480">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="bf7fd-481">cabeçalho</span><span class="sxs-lookup"><span data-stu-id="bf7fd-481">header</span></span>|<span data-ttu-id="bf7fd-482">Cabeçalho da solicitação.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-482">Request header.</span></span> <span data-ttu-id="bf7fd-483">Use vários elementos de cabeçalho para vários cabeçalhos de solicitação.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-483">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="bf7fd-484">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-484">No</span></span>|  
|<span data-ttu-id="bf7fd-485">corpo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-485">body</span></span>|<span data-ttu-id="bf7fd-486">O corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-486">The request body.</span></span>|<span data-ttu-id="bf7fd-487">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-487">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf7fd-488">Atributos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-488">Attributes</span></span>  
  
|<span data-ttu-id="bf7fd-489">Atributo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-489">Attribute</span></span>|<span data-ttu-id="bf7fd-490">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-490">Description</span></span>|<span data-ttu-id="bf7fd-491">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-491">Required</span></span>|<span data-ttu-id="bf7fd-492">Padrão</span><span class="sxs-lookup"><span data-stu-id="bf7fd-492">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bf7fd-493">mode="string"</span><span class="sxs-lookup"><span data-stu-id="bf7fd-493">mode="string"</span></span>|<span data-ttu-id="bf7fd-494">Determina se esta é uma nova solicitação ou uma cópia da solicitação atual.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-494">Determines whether this is a new request or a copy of the current request.</span></span> <span data-ttu-id="bf7fd-495">No modo de saída, mode=copy não inicializa o corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-495">In outbound mode, mode=copy does not initialize the request body.</span></span>|<span data-ttu-id="bf7fd-496">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-496">No</span></span>|<span data-ttu-id="bf7fd-497">Novo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-497">New</span></span>|  
|<span data-ttu-id="bf7fd-498">response-variable-name="string"</span><span class="sxs-lookup"><span data-stu-id="bf7fd-498">response-variable-name="string"</span></span>|<span data-ttu-id="bf7fd-499">Se não estiver presente, `context.Response` será usado.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-499">If not present, `context.Response` is used.</span></span>|<span data-ttu-id="bf7fd-500">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-500">No</span></span>|<span data-ttu-id="bf7fd-501">N/D</span><span class="sxs-lookup"><span data-stu-id="bf7fd-501">N/A</span></span>|  
|<span data-ttu-id="bf7fd-502">timeout="integer"</span><span class="sxs-lookup"><span data-stu-id="bf7fd-502">timeout="integer"</span></span>|<span data-ttu-id="bf7fd-503">O intervalo de tempo limite em segundos antes de a chamada para a URL falhar.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-503">The timeout interval in seconds before the call to the URL fails.</span></span>|<span data-ttu-id="bf7fd-504">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-504">No</span></span>|<span data-ttu-id="bf7fd-505">60</span><span class="sxs-lookup"><span data-stu-id="bf7fd-505">60</span></span>|  
|<span data-ttu-id="bf7fd-506">ignore-error</span><span class="sxs-lookup"><span data-stu-id="bf7fd-506">ignore-error</span></span>|<span data-ttu-id="bf7fd-507">Se for true e a solicitação resultar em um erro:</span><span class="sxs-lookup"><span data-stu-id="bf7fd-507">If true and the request results in an error:</span></span><br /><br /> <span data-ttu-id="bf7fd-508">– Se response-variable-name tiver sido especificado, ele conterá um valor nulo.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-508">-   If response-variable-name was specified it will contain a null value.</span></span><br /><span data-ttu-id="bf7fd-509">– Se response-variable-name não tiver sido especificado, context.Request não será atualizado.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-509">-   If response-variable-name was not specified, context.Request will not be updated.</span></span>|<span data-ttu-id="bf7fd-510">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-510">No</span></span>|<span data-ttu-id="bf7fd-511">false</span><span class="sxs-lookup"><span data-stu-id="bf7fd-511">false</span></span>|  
|<span data-ttu-id="bf7fd-512">name</span><span class="sxs-lookup"><span data-stu-id="bf7fd-512">name</span></span>|<span data-ttu-id="bf7fd-513">Especifica o nome do cabeçalho a ser definido.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-513">Specifies the name of the header to be set.</span></span>|<span data-ttu-id="bf7fd-514">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-514">Yes</span></span>|<span data-ttu-id="bf7fd-515">N/D</span><span class="sxs-lookup"><span data-stu-id="bf7fd-515">N/A</span></span>|  
|<span data-ttu-id="bf7fd-516">exists-action</span><span class="sxs-lookup"><span data-stu-id="bf7fd-516">exists-action</span></span>|<span data-ttu-id="bf7fd-517">Especifica a ação a ser adotada quando o cabeçalho já foi especificado.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-517">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="bf7fd-518">Este atributo deve ter um dos valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-518">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="bf7fd-519">– override – substitui o valor do cabeçalho existente.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-519">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="bf7fd-520">– skip – não substitui o valor do cabeçalho existente.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-520">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="bf7fd-521">– append – acrescenta o valor ao valor do cabeçalho existente.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-521">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="bf7fd-522">– delete – remove o cabeçalho da solicitação.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-522">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="bf7fd-523">Quando definido como `override`, listar diversas entradas com o mesmo nome faz com que o cabeçalho seja definido de acordo com todas as entradas (que serão listadas várias vezes); somente valores listados serão definidos no resultado.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-523">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="bf7fd-524">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-524">No</span></span>|<span data-ttu-id="bf7fd-525">override</span><span class="sxs-lookup"><span data-stu-id="bf7fd-525">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bf7fd-526">Uso</span><span class="sxs-lookup"><span data-stu-id="bf7fd-526">Usage</span></span>  
 <span data-ttu-id="bf7fd-527">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-527">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf7fd-528">**Seções da política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="bf7fd-528">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bf7fd-529">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-529">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bf7fd-530"><a name="SetHttpProxy"></a> Definir proxy HTTP</span><span class="sxs-lookup"><span data-stu-id="bf7fd-530"><a name="SetHttpProxy"></a> Set HTTP proxy</span></span>  
 <span data-ttu-id="bf7fd-531">A política `proxy` permite reencaminhar, por meio de um proxy HTTP, as solicitações encaminhadas aos back-ends.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-531">The `proxy` policy allows you to route requests forwarded to backends via an HTTP proxy.</span></span> <span data-ttu-id="bf7fd-532">Entre o gateway e o proxy, há suporte apenas para HTTP (e não para HTTPS).</span><span class="sxs-lookup"><span data-stu-id="bf7fd-532">Only HTTP (not HTTPS) is supported between the gateway and the proxy.</span></span> <span data-ttu-id="bf7fd-533">Somente autenticação básica e NTLM.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-533">Basic and NTLM authentication only.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="bf7fd-534">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="bf7fd-534">Policy statement</span></span>  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="bf7fd-535">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-535">Example</span></span>  
<span data-ttu-id="bf7fd-536">Observe o uso de [propriedades](api-management-howto-properties.md) como valores de nome de usuário e senha para evitar armazenar informações confidenciais no documento de política.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-536">Note the use of [properties](api-management-howto-properties.md) as values of the username and password to avoid storing sensitive information in the policy document.</span></span>  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a><span data-ttu-id="bf7fd-537">Elementos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-537">Elements</span></span>  
  
|<span data-ttu-id="bf7fd-538">Elemento</span><span class="sxs-lookup"><span data-stu-id="bf7fd-538">Element</span></span>|<span data-ttu-id="bf7fd-539">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-539">Description</span></span>|<span data-ttu-id="bf7fd-540">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-540">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf7fd-541">proxy</span><span class="sxs-lookup"><span data-stu-id="bf7fd-541">proxy</span></span>|<span data-ttu-id="bf7fd-542">Elemento raiz</span><span class="sxs-lookup"><span data-stu-id="bf7fd-542">Root element</span></span>|<span data-ttu-id="bf7fd-543">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-543">Yes</span></span>|  

### <a name="attributes"></a><span data-ttu-id="bf7fd-544">Atributos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-544">Attributes</span></span>  
  
|<span data-ttu-id="bf7fd-545">Atributo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-545">Attribute</span></span>|<span data-ttu-id="bf7fd-546">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-546">Description</span></span>|<span data-ttu-id="bf7fd-547">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-547">Required</span></span>|<span data-ttu-id="bf7fd-548">Padrão</span><span class="sxs-lookup"><span data-stu-id="bf7fd-548">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bf7fd-549">url="string"</span><span class="sxs-lookup"><span data-stu-id="bf7fd-549">url="string"</span></span>|<span data-ttu-id="bf7fd-550">URL do proxy no formato http://host:porta.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-550">Proxy URL in the form of http://host:port.</span></span>|<span data-ttu-id="bf7fd-551">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-551">Yes</span></span>|<span data-ttu-id="bf7fd-552">N/D </span><span class="sxs-lookup"><span data-stu-id="bf7fd-552">N/A</span></span>|  
|<span data-ttu-id="bf7fd-553">username="string"</span><span class="sxs-lookup"><span data-stu-id="bf7fd-553">username="string"</span></span>|<span data-ttu-id="bf7fd-554">Nome de usuário a ser usado para autenticação com o proxy.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-554">Username to be used for authentication with the proxy.</span></span>|<span data-ttu-id="bf7fd-555">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-555">No</span></span>|<span data-ttu-id="bf7fd-556">N/D </span><span class="sxs-lookup"><span data-stu-id="bf7fd-556">N/A</span></span>|  
|<span data-ttu-id="bf7fd-557">password="string"</span><span class="sxs-lookup"><span data-stu-id="bf7fd-557">password="string"</span></span>|<span data-ttu-id="bf7fd-558">Senha a ser usada para autenticação com o proxy.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-558">Password to be used for authentication with the proxy.</span></span>|<span data-ttu-id="bf7fd-559">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-559">No</span></span>|<span data-ttu-id="bf7fd-560">N/D </span><span class="sxs-lookup"><span data-stu-id="bf7fd-560">N/A</span></span>|  

### <a name="usage"></a><span data-ttu-id="bf7fd-561">Uso</span><span class="sxs-lookup"><span data-stu-id="bf7fd-561">Usage</span></span>  
 <span data-ttu-id="bf7fd-562">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-562">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf7fd-563">**Seções de política:** de entrada</span><span class="sxs-lookup"><span data-stu-id="bf7fd-563">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="bf7fd-564">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-564">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="bf7fd-565"><a name="SetRequestMethod"></a> Definir método de solicitação</span><span class="sxs-lookup"><span data-stu-id="bf7fd-565"><a name="SetRequestMethod"></a> Set request method</span></span>  
 <span data-ttu-id="bf7fd-566">A política `set-method` permite alterar o método de solicitação HTTP de uma solicitação.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-566">The `set-method` policy allows you to change the HTTP request method for a request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bf7fd-567">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="bf7fd-567">Policy statement</span></span>  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a><span data-ttu-id="bf7fd-568">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-568">Example</span></span>  
 <span data-ttu-id="bf7fd-569">Essa política de exemplo que usa a política `set-method` mostra um exemplo de envio de uma mensagem para uma sala de chat do Slack se o código de resposta HTTP for maior ou igual a 500.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-569">This sample policy that uses the `set-method` policy shows an example of sending a message to a Slack chat room if the HTTP response code is greater than or equal to 500.</span></span> <span data-ttu-id="bf7fd-570">Para obter mais informações sobre esse exemplo, consulte [Uso dos serviços externos do serviço de Gerenciamento de API do Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="bf7fd-570">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="bf7fd-571">Elementos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-571">Elements</span></span>  
  
|<span data-ttu-id="bf7fd-572">Elemento</span><span class="sxs-lookup"><span data-stu-id="bf7fd-572">Element</span></span>|<span data-ttu-id="bf7fd-573">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-573">Description</span></span>|<span data-ttu-id="bf7fd-574">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-574">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf7fd-575">set-method</span><span class="sxs-lookup"><span data-stu-id="bf7fd-575">set-method</span></span>|<span data-ttu-id="bf7fd-576">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-576">Root element.</span></span> <span data-ttu-id="bf7fd-577">O valor do elemento especifica o método HTTP.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-577">The value of the element specifies the HTTP method.</span></span>|<span data-ttu-id="bf7fd-578">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-578">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bf7fd-579">Uso</span><span class="sxs-lookup"><span data-stu-id="bf7fd-579">Usage</span></span>  
 <span data-ttu-id="bf7fd-580">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-580">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf7fd-581">**Seções de política:** entrada, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="bf7fd-581">**Policy sections:** inbound, on-error</span></span>  
  
-   <span data-ttu-id="bf7fd-582">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-582">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bf7fd-583"><a name="SetStatus"></a> Definir código de status</span><span class="sxs-lookup"><span data-stu-id="bf7fd-583"><a name="SetStatus"></a> Set status code</span></span>  
 <span data-ttu-id="bf7fd-584">A política `set-status` define o código de status HTTP para o valor especificado.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-584">The `set-status` policy sets the HTTP status code to the specified value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bf7fd-585">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="bf7fd-585">Policy statement</span></span>  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a><span data-ttu-id="bf7fd-586">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-586">Example</span></span>  
 <span data-ttu-id="bf7fd-587">Este exemplo mostra como retornar uma resposta 401, se o token de autorização for inválido.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-587">This example shows how to return a 401 response if the authorization token is invalid.</span></span> <span data-ttu-id="bf7fd-588">Para obter mais informações, consulte [Uso dos serviços externos do serviço de Gerenciamento de API do Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span><span class="sxs-lookup"><span data-stu-id="bf7fd-588">For more information, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span></span>  
  
```xml  
<choose>  
  <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
    <return-response response-variable-name="existing response variable">  
      <set-status code="401" reason="Unauthorized" />  
      <set-header name="WWW-Authenticate" exists-action="override">  
        <value>Bearer error="invalid_token"</value>  
      </set-header>  
    </return-response>  
  </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="bf7fd-589">Elementos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-589">Elements</span></span>  
  
|<span data-ttu-id="bf7fd-590">Elemento</span><span class="sxs-lookup"><span data-stu-id="bf7fd-590">Element</span></span>|<span data-ttu-id="bf7fd-591">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-591">Description</span></span>|<span data-ttu-id="bf7fd-592">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-592">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf7fd-593">set-status</span><span class="sxs-lookup"><span data-stu-id="bf7fd-593">set-status</span></span>|<span data-ttu-id="bf7fd-594">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-594">Root element.</span></span>|<span data-ttu-id="bf7fd-595">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-595">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf7fd-596">Atributos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-596">Attributes</span></span>  
  
|<span data-ttu-id="bf7fd-597">Atributo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-597">Attribute</span></span>|<span data-ttu-id="bf7fd-598">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-598">Description</span></span>|<span data-ttu-id="bf7fd-599">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-599">Required</span></span>|<span data-ttu-id="bf7fd-600">Padrão</span><span class="sxs-lookup"><span data-stu-id="bf7fd-600">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bf7fd-601">code="integer"</span><span class="sxs-lookup"><span data-stu-id="bf7fd-601">code="integer"</span></span>|<span data-ttu-id="bf7fd-602">O código de status HTTP a ser retornado.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-602">The HTTP status code to return.</span></span>|<span data-ttu-id="bf7fd-603">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-603">Yes</span></span>|<span data-ttu-id="bf7fd-604">N/D</span><span class="sxs-lookup"><span data-stu-id="bf7fd-604">N/A</span></span>|  
|<span data-ttu-id="bf7fd-605">reason="string"</span><span class="sxs-lookup"><span data-stu-id="bf7fd-605">reason="string"</span></span>|<span data-ttu-id="bf7fd-606">Uma descrição do motivo para retornar o código de status.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-606">A description of the reason for returning the status code.</span></span>|<span data-ttu-id="bf7fd-607">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-607">Yes</span></span>|<span data-ttu-id="bf7fd-608">N/D</span><span class="sxs-lookup"><span data-stu-id="bf7fd-608">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bf7fd-609">Uso</span><span class="sxs-lookup"><span data-stu-id="bf7fd-609">Usage</span></span>  
 <span data-ttu-id="bf7fd-610">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-610">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf7fd-611">**Seções de política:** saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="bf7fd-611">**Policy sections:** outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bf7fd-612">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-612">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="bf7fd-613"><a name="set-variable"></a> Definir variável</span><span class="sxs-lookup"><span data-stu-id="bf7fd-613"><a name="set-variable"></a> Set variable</span></span>  
 <span data-ttu-id="bf7fd-614">A política `set-variable` declara uma variável de [contexto](api-management-policy-expressions.md#ContextVariables) e atribui a ela um valor especificado por meio de uma [expressão](api-management-policy-expressions.md) ou literal de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-614">The `set-variable` policy declares a [context](api-management-policy-expressions.md#ContextVariables) variable and assigns it a value specified via an [expression](api-management-policy-expressions.md) or a string literal.</span></span> <span data-ttu-id="bf7fd-615">Se a expressão contiver um literal ele será convertido em uma cadeia de caracteres e o tipo do valor será `System.String`.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-615">if the expression contains a literal it will be converted to a string and the type of the value will be `System.String`.</span></span>  
  
###  <span data-ttu-id="bf7fd-616"><a name="set-variablePolicyStatement"></a> Declaração de política</span><span class="sxs-lookup"><span data-stu-id="bf7fd-616"><a name="set-variablePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <span data-ttu-id="bf7fd-617"><a name="set-variableExample"></a> Exemplo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-617"><a name="set-variableExample"></a> Example</span></span>  
 <span data-ttu-id="bf7fd-618">O exemplo a seguir demonstra uma política de definir a variável na seção de entrada.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-618">The following example demonstrates a set variable policy in the inbound section.</span></span> <span data-ttu-id="bf7fd-619">Essa política de definir variável cria uma variável de [contexto](api-management-policy-expressions.md#ContextVariables) booliana `isMobile` que será definida como true se o cabeçalho da solicitação `User-Agent` contiver o texto `iPad` ou `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-619">This set variable policy creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set to true if the `User-Agent` request header contains the text `iPad` or `iPhone`.</span></span>  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a><span data-ttu-id="bf7fd-620">Elementos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-620">Elements</span></span>  
  
|<span data-ttu-id="bf7fd-621">Elemento</span><span class="sxs-lookup"><span data-stu-id="bf7fd-621">Element</span></span>|<span data-ttu-id="bf7fd-622">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-622">Description</span></span>|<span data-ttu-id="bf7fd-623">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-623">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf7fd-624">set-variable</span><span class="sxs-lookup"><span data-stu-id="bf7fd-624">set-variable</span></span>|<span data-ttu-id="bf7fd-625">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-625">Root element.</span></span>|<span data-ttu-id="bf7fd-626">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-626">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf7fd-627">Atributos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-627">Attributes</span></span>  
  
|<span data-ttu-id="bf7fd-628">Atributo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-628">Attribute</span></span>|<span data-ttu-id="bf7fd-629">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-629">Description</span></span>|<span data-ttu-id="bf7fd-630">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-630">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="bf7fd-631">name</span><span class="sxs-lookup"><span data-stu-id="bf7fd-631">name</span></span>|<span data-ttu-id="bf7fd-632">O nome da variável.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-632">The name of the variable.</span></span>|<span data-ttu-id="bf7fd-633">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-633">Yes</span></span>|  
|<span data-ttu-id="bf7fd-634">valor</span><span class="sxs-lookup"><span data-stu-id="bf7fd-634">value</span></span>|<span data-ttu-id="bf7fd-635">O valor da variável.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-635">The value of the variable.</span></span> <span data-ttu-id="bf7fd-636">Isso pode ser uma expressão ou um valor literal.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-636">This can be an expression or a literal value.</span></span>|<span data-ttu-id="bf7fd-637">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-637">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bf7fd-638">Uso</span><span class="sxs-lookup"><span data-stu-id="bf7fd-638">Usage</span></span>  
 <span data-ttu-id="bf7fd-639">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-639">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf7fd-640">**Seções da política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="bf7fd-640">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bf7fd-641">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-641">**Policy scopes:** all scopes</span></span>  
  
###  <span data-ttu-id="bf7fd-642"><a name="set-variableAllowedTypes"></a> Tipos permitidos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-642"><a name="set-variableAllowedTypes"></a> Allowed types</span></span>  
 <span data-ttu-id="bf7fd-643">As expressões usadas na política `set-variable` devem retornar um dos seguintes tipos básicos.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-643">Expressions used in the `set-variable` policy must return one of the following basic types.</span></span>  
  
-   <span data-ttu-id="bf7fd-644">System.Boolean</span><span class="sxs-lookup"><span data-stu-id="bf7fd-644">System.Boolean</span></span>  
  
-   <span data-ttu-id="bf7fd-645">System.SByte</span><span class="sxs-lookup"><span data-stu-id="bf7fd-645">System.SByte</span></span>  
  
-   <span data-ttu-id="bf7fd-646">System.Byte</span><span class="sxs-lookup"><span data-stu-id="bf7fd-646">System.Byte</span></span>  
  
-   <span data-ttu-id="bf7fd-647">System.UInt16</span><span class="sxs-lookup"><span data-stu-id="bf7fd-647">System.UInt16</span></span>  
  
-   <span data-ttu-id="bf7fd-648">System.UInt32</span><span class="sxs-lookup"><span data-stu-id="bf7fd-648">System.UInt32</span></span>  
  
-   <span data-ttu-id="bf7fd-649">System.UInt64</span><span class="sxs-lookup"><span data-stu-id="bf7fd-649">System.UInt64</span></span>  
  
-   <span data-ttu-id="bf7fd-650">System.Int16</span><span class="sxs-lookup"><span data-stu-id="bf7fd-650">System.Int16</span></span>  
  
-   <span data-ttu-id="bf7fd-651">System.Int32</span><span class="sxs-lookup"><span data-stu-id="bf7fd-651">System.Int32</span></span>  
  
-   <span data-ttu-id="bf7fd-652">System.Int64</span><span class="sxs-lookup"><span data-stu-id="bf7fd-652">System.Int64</span></span>  
  
-   <span data-ttu-id="bf7fd-653">System.Decimal</span><span class="sxs-lookup"><span data-stu-id="bf7fd-653">System.Decimal</span></span>  
  
-   <span data-ttu-id="bf7fd-654">System.Single</span><span class="sxs-lookup"><span data-stu-id="bf7fd-654">System.Single</span></span>  
  
-   <span data-ttu-id="bf7fd-655">System.Double</span><span class="sxs-lookup"><span data-stu-id="bf7fd-655">System.Double</span></span>  
  
-   <span data-ttu-id="bf7fd-656">System.Guid</span><span class="sxs-lookup"><span data-stu-id="bf7fd-656">System.Guid</span></span>  
  
-   <span data-ttu-id="bf7fd-657">System.String</span><span class="sxs-lookup"><span data-stu-id="bf7fd-657">System.String</span></span>  
  
-   <span data-ttu-id="bf7fd-658">System.Char</span><span class="sxs-lookup"><span data-stu-id="bf7fd-658">System.Char</span></span>  
  
-   <span data-ttu-id="bf7fd-659">System.DateTime</span><span class="sxs-lookup"><span data-stu-id="bf7fd-659">System.DateTime</span></span>  
  
-   <span data-ttu-id="bf7fd-660">System.TimeSpan</span><span class="sxs-lookup"><span data-stu-id="bf7fd-660">System.TimeSpan</span></span>  
  
-   <span data-ttu-id="bf7fd-661">System.Byte?</span><span class="sxs-lookup"><span data-stu-id="bf7fd-661">System.Byte?</span></span>  
  
-   <span data-ttu-id="bf7fd-662">System.UInt16?</span><span class="sxs-lookup"><span data-stu-id="bf7fd-662">System.UInt16?</span></span>  
  
-   <span data-ttu-id="bf7fd-663">System.UInt32?</span><span class="sxs-lookup"><span data-stu-id="bf7fd-663">System.UInt32?</span></span>  
  
-   <span data-ttu-id="bf7fd-664">System.UInt64?</span><span class="sxs-lookup"><span data-stu-id="bf7fd-664">System.UInt64?</span></span>  
  
-   <span data-ttu-id="bf7fd-665">System.Int16?</span><span class="sxs-lookup"><span data-stu-id="bf7fd-665">System.Int16?</span></span>  
  
-   <span data-ttu-id="bf7fd-666">System.Int32?</span><span class="sxs-lookup"><span data-stu-id="bf7fd-666">System.Int32?</span></span>  
  
-   <span data-ttu-id="bf7fd-667">System.Int64?</span><span class="sxs-lookup"><span data-stu-id="bf7fd-667">System.Int64?</span></span>  
  
-   <span data-ttu-id="bf7fd-668">System.Decimal?</span><span class="sxs-lookup"><span data-stu-id="bf7fd-668">System.Decimal?</span></span>  
  
-   <span data-ttu-id="bf7fd-669">System.Single?</span><span class="sxs-lookup"><span data-stu-id="bf7fd-669">System.Single?</span></span>  
  
-   <span data-ttu-id="bf7fd-670">System.Double?</span><span class="sxs-lookup"><span data-stu-id="bf7fd-670">System.Double?</span></span>  
  
-   <span data-ttu-id="bf7fd-671">System.Guid?</span><span class="sxs-lookup"><span data-stu-id="bf7fd-671">System.Guid?</span></span>  
  
-   <span data-ttu-id="bf7fd-672">System.String?</span><span class="sxs-lookup"><span data-stu-id="bf7fd-672">System.String?</span></span>  
  
-   <span data-ttu-id="bf7fd-673">System.Char?</span><span class="sxs-lookup"><span data-stu-id="bf7fd-673">System.Char?</span></span>  
  
-   <span data-ttu-id="bf7fd-674">System.DateTime?</span><span class="sxs-lookup"><span data-stu-id="bf7fd-674">System.DateTime?</span></span>  

##  <span data-ttu-id="bf7fd-675"><a name="Trace"></a> Rastreamento</span><span class="sxs-lookup"><span data-stu-id="bf7fd-675"><a name="Trace"></a> Trace</span></span>  
 <span data-ttu-id="bf7fd-676">A política `trace` adiciona uma cadeia de caracteres à saída do [Inspetor de API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/).</span><span class="sxs-lookup"><span data-stu-id="bf7fd-676">The             `trace` policy adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span> <span data-ttu-id="bf7fd-677">A política será executada somente quando o rastreamento for disparado, ou seja, o cabeçalho de solicitação `Ocp-Apim-Trace` está presente e definido como `true` e o cabeçalho de solicitação `Ocp-Apim-Subscription-Key` está presente e contém uma chave válida associada à conta do administrador.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-677">The policy will execute only when tracing is triggered, i.e. `Ocp-Apim-Trace` request header is present and set to `true` and `Ocp-Apim-Subscription-Key` request header is present and holds a valid key associated with the admin account.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bf7fd-678">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="bf7fd-678">Policy statement</span></span>  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="bf7fd-679">Elementos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-679">Elements</span></span>  
  
|<span data-ttu-id="bf7fd-680">Elemento</span><span class="sxs-lookup"><span data-stu-id="bf7fd-680">Element</span></span>|<span data-ttu-id="bf7fd-681">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-681">Description</span></span>|<span data-ttu-id="bf7fd-682">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-682">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf7fd-683">trace</span><span class="sxs-lookup"><span data-stu-id="bf7fd-683">trace</span></span>|<span data-ttu-id="bf7fd-684">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-684">Root element.</span></span>|<span data-ttu-id="bf7fd-685">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-685">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf7fd-686">Atributos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-686">Attributes</span></span>  
  
|<span data-ttu-id="bf7fd-687">Atributo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-687">Attribute</span></span>|<span data-ttu-id="bf7fd-688">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-688">Description</span></span>|<span data-ttu-id="bf7fd-689">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-689">Required</span></span>|<span data-ttu-id="bf7fd-690">Padrão</span><span class="sxs-lookup"><span data-stu-id="bf7fd-690">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bf7fd-691">fonte</span><span class="sxs-lookup"><span data-stu-id="bf7fd-691">source</span></span>|<span data-ttu-id="bf7fd-692">Literal de cadeia de caracteres significativo para o visualizador de rastreamento e especificando a fonte da mensagem.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-692">String literal meaningful to the trace viewer and specifying the source of the message.</span></span>|<span data-ttu-id="bf7fd-693">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-693">Yes</span></span>|<span data-ttu-id="bf7fd-694">N/D</span><span class="sxs-lookup"><span data-stu-id="bf7fd-694">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bf7fd-695">Uso</span><span class="sxs-lookup"><span data-stu-id="bf7fd-695">Usage</span></span>  
 <span data-ttu-id="bf7fd-696">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-696">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="bf7fd-697">**Seções da política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="bf7fd-697">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="bf7fd-698">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-698">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="bf7fd-699"><a name="Wait"></a> Aguardar</span><span class="sxs-lookup"><span data-stu-id="bf7fd-699"><a name="Wait"></a> Wait</span></span>  
 <span data-ttu-id="bf7fd-700">A política `wait` executa suas políticas filho imediatas em paralelo e aguarda que todas ou uma das políticas filho imediatas sejam concluídas antes de ser concluída.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-700">The `wait` policy executes its immediate child policies in parallel, and waits for either all or one of its immediate child policies to complete before it completes.</span></span> <span data-ttu-id="bf7fd-701">A política de espera pode ter como suas políticas de filho imediatas as políticas de [Enviar solicitação](api-management-advanced-policies.md#SendRequest), [Obter valor do cache](api-management-caching-policies.md#GetFromCacheByKey) e [Controlar fluxo](api-management-advanced-policies.md#choose).</span><span class="sxs-lookup"><span data-stu-id="bf7fd-701">The wait policy can have as its immediate child policies [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), and [Control flow](api-management-advanced-policies.md#choose) policies.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="bf7fd-702">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="bf7fd-702">Policy statement</span></span>  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a><span data-ttu-id="bf7fd-703">Exemplo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-703">Example</span></span>  
 <span data-ttu-id="bf7fd-704">No exemplo a seguir há duas políticas `choose` como políticas filho imediatas da política `wait`.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-704">In the following example there are two `choose` policies as immediate child policies of the `wait` policy.</span></span> <span data-ttu-id="bf7fd-705">Cada uma dessas políticas `choose` executadas em paralelo.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-705">Each of these `choose` policies executes in parallel.</span></span> <span data-ttu-id="bf7fd-706">Cada política `choose` tenta recuperar um valor em cache.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-706">Each `choose` policy attempts to retrieve a cached value.</span></span> <span data-ttu-id="bf7fd-707">Se houver uma perda no cache, um serviço de back-end será chamado para fornecer o valor.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-707">If there is a cache miss, a backend service is called to provide the value.</span></span> <span data-ttu-id="bf7fd-708">Neste exemplo a política `wait` não é concluída até todas as políticas filho imediatas serem concluídas, porque o atributo `for` está definido como `all`.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-708">In this example the `wait` policy does not complete until all of its immediate child policies complete, because the `for` attribute is set to `all`.</span></span>   <span data-ttu-id="bf7fd-709">Neste exemplo as variáveis de contexto (`execute-branch-one`, `value-one`, `execute-branch-two` e `value-two`) são declaradas fora do escopo desta política de exemplo.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-709">In this example the context variables (`execute-branch-one`, `value-one`, `execute-branch-two`, and `value-two`) are declared outside of the scope of this example policy.</span></span>  
  
```xml  
<wait for="all">  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-one="])">  
      <cache-lookup-value key="key-one" variable-name="value-one" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-one="))">  
          <send-request mode="new" response-variable-name="value-one">  
            <set-url>https://backend-one</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-two="])">  
      <cache-lookup-value key="key-two" variable-name="value-two" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-two="))">  
          <send-request mode="new" response-variable-name="value-two">  
            <set-url>https://backend-two</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
</wait>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="bf7fd-710">Elementos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-710">Elements</span></span>  
  
|<span data-ttu-id="bf7fd-711">Elemento</span><span class="sxs-lookup"><span data-stu-id="bf7fd-711">Element</span></span>|<span data-ttu-id="bf7fd-712">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-712">Description</span></span>|<span data-ttu-id="bf7fd-713">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-713">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="bf7fd-714">wait</span><span class="sxs-lookup"><span data-stu-id="bf7fd-714">wait</span></span>|<span data-ttu-id="bf7fd-715">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-715">Root element.</span></span> <span data-ttu-id="bf7fd-716">Pode conter como elementos filho somente as políticas `send-request`, `cache-lookup-value` e `choose`.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-716">May contain as child elements only `send-request`, `cache-lookup-value`, and `choose` policies.</span></span>|<span data-ttu-id="bf7fd-717">Sim</span><span class="sxs-lookup"><span data-stu-id="bf7fd-717">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="bf7fd-718">Atributos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-718">Attributes</span></span>  
  
|<span data-ttu-id="bf7fd-719">Atributo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-719">Attribute</span></span>|<span data-ttu-id="bf7fd-720">Descrição</span><span class="sxs-lookup"><span data-stu-id="bf7fd-720">Description</span></span>|<span data-ttu-id="bf7fd-721">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="bf7fd-721">Required</span></span>|<span data-ttu-id="bf7fd-722">Padrão</span><span class="sxs-lookup"><span data-stu-id="bf7fd-722">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="bf7fd-723">for</span><span class="sxs-lookup"><span data-stu-id="bf7fd-723">for</span></span>|<span data-ttu-id="bf7fd-724">Determina se a política `wait` aguarda todas as políticas filho imediatas a serem concluídas ou apenas uma.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-724">Determines whether the `wait` policy waits for all immediate child policies to be completed or just one.</span></span> <span data-ttu-id="bf7fd-725">Valores permitidos são:</span><span class="sxs-lookup"><span data-stu-id="bf7fd-725">Allowed values are:</span></span><br /><br /> <span data-ttu-id="bf7fd-726">-   `all` – aguarda todas as políticas filho imediatas serem concluídas</span><span class="sxs-lookup"><span data-stu-id="bf7fd-726">-   `all` - wait for all immediate child policies to complete</span></span><br /><span data-ttu-id="bf7fd-727">– any – aguarda qualquer política filho imediata ser concluída.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-727">-   any - wait for any immediate child policy to complete.</span></span> <span data-ttu-id="bf7fd-728">Concluída a primeira política filho imediata, a política `wait` é concluída e a execução de qualquer outra política filho imediata é encerrada.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-728">Once the first immediate child policy has completed, the `wait` policy completes and execution of any other immediate child policies is terminated.</span></span>|<span data-ttu-id="bf7fd-729">Não</span><span class="sxs-lookup"><span data-stu-id="bf7fd-729">No</span></span>|<span data-ttu-id="bf7fd-730">tudo</span><span class="sxs-lookup"><span data-stu-id="bf7fd-730">all</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="bf7fd-731">Uso</span><span class="sxs-lookup"><span data-stu-id="bf7fd-731">Usage</span></span>  
 <span data-ttu-id="bf7fd-732">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="bf7fd-732">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="bf7fd-733">**Seções de política:** entrada, saída, back-end</span><span class="sxs-lookup"><span data-stu-id="bf7fd-733">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="bf7fd-734">**Escopos da política:**todos os escopos</span><span class="sxs-lookup"><span data-stu-id="bf7fd-734">**Policy scopes:**all scopes</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="bf7fd-735">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bf7fd-735">Next steps</span></span>
<span data-ttu-id="bf7fd-736">Para obter mais informações sobre como trabalhar com políticas, consulte:</span><span class="sxs-lookup"><span data-stu-id="bf7fd-736">For more information working with policies, see:</span></span>
-   [<span data-ttu-id="bf7fd-737">Políticas no Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="bf7fd-737">Policies in API Management</span></span>](api-management-howto-policies.md) 
-   [<span data-ttu-id="bf7fd-738">Expressões de política</span><span class="sxs-lookup"><span data-stu-id="bf7fd-738">Policy expressions</span></span>](api-management-policy-expressions.md)
