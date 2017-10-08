---
title: "aaaAzure políticas avançadas de gerenciamento de API | Microsoft Docs"
description: "Saiba mais sobre Olá avançadas de políticas disponíveis para uso no gerenciamento de API do Azure."
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
ms.openlocfilehash: 8245e7a4c9d432b7b4d362192e357829fcabad55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-advanced-policies"></a><span data-ttu-id="585eb-103">Políticas avançadas de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="585eb-103">API Management advanced policies</span></span>
<span data-ttu-id="585eb-104">Este tópico fornece uma referência para Olá políticas de gerenciamento de API a seguir.</span><span class="sxs-lookup"><span data-stu-id="585eb-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="585eb-105">Para obter mais informações sobre como adicionar e configurar políticas, consulte [Políticas de Gerenciamento de API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="585eb-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="585eb-106"><a name="AdvancedPolicies"></a> Políticas avançadas</span><span class="sxs-lookup"><span data-stu-id="585eb-106"><a name="AdvancedPolicies"></a> Advanced policies</span></span>  
  
-   <span data-ttu-id="585eb-107">[Fluxo de controle](api-management-advanced-policies.md#choose) - condicionalmente aplica instruções de política com base nos resultados de saudação da avaliação de saudação de booliano [expressões](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="585eb-107">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on hello results of hello evaluation of Boolean [expressions](api-management-policy-expressions.md).</span></span>  
  
-   <span data-ttu-id="585eb-108">[Enviar solicitação](#ForwardRequest) -encaminha o serviço de back-end do hello solicitação toohello.</span><span class="sxs-lookup"><span data-stu-id="585eb-108">[Forward request](#ForwardRequest) - Forwards hello request toohello backend service.</span></span>

-   <span data-ttu-id="585eb-109">[Limite a simultaneidade](#LimitConcurrency) -impede entre as políticas de execução por mais de Olá quantidade especificada de solicitações por vez.</span><span class="sxs-lookup"><span data-stu-id="585eb-109">[Limit concurrency](#LimitConcurrency) - Prevents enclosed policies from executing by more than hello specified number of requests at a time.</span></span>
  
-   <span data-ttu-id="585eb-110">[Log tooEvent Hub](#log-to-eventhub) -envia mensagens de saudação especificado tooan formato Hub de eventos definido por uma entidade de agente de log.</span><span class="sxs-lookup"><span data-stu-id="585eb-110">[Log tooEvent Hub](#log-to-eventhub) - Sends messages in hello specified format tooan Event Hub defined by a Logger entity.</span></span> 

-   <span data-ttu-id="585eb-111">[Resposta de simulação](#mock-response) -anulações de pipeline de execução e retorna uma resposta fictícias diretamente toohello chamador.</span><span class="sxs-lookup"><span data-stu-id="585eb-111">[Mock response](#mock-response) - Aborts pipeline execution and returns a mocked response directly toohello caller.</span></span>
  
-   <span data-ttu-id="585eb-112">[Repita](#Retry) -tentativas de execução de saudação colocados declarações de política, se e até Olá condição for atendida.</span><span class="sxs-lookup"><span data-stu-id="585eb-112">[Retry](#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="585eb-113">A execução será repetida em Olá intervalos de tempo especificado e o toohello especificado contagem de repetição.</span><span class="sxs-lookup"><span data-stu-id="585eb-113">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>  
  
-   <span data-ttu-id="585eb-114">[Retornar a resposta](#ReturnResponse) -Olá de execução e retorna de anulações de pipeline da resposta especificada diretamente toohello chamador.</span><span class="sxs-lookup"><span data-stu-id="585eb-114">[Return response](#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span> 
  
-   <span data-ttu-id="585eb-115">[Enviar solicitação de uma maneira](#SendOneWayRequest) -envia uma solicitação toohello especificado URL sem aguardar uma resposta.</span><span class="sxs-lookup"><span data-stu-id="585eb-115">[Send one way request](#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>  
  
-   <span data-ttu-id="585eb-116">[Enviar solicitação](#SendRequest) -envia uma solicitação toohello especificou a URL.</span><span class="sxs-lookup"><span data-stu-id="585eb-116">[Send request](#SendRequest) - Sends a request toohello specified URL.</span></span>  

-   <span data-ttu-id="585eb-117">[Definir o proxy HTTP](#SetHttpProxy) -permite solicitações de tooroute encaminhado por meio de um proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="585eb-117">[Set HTTP proxy](#SetHttpProxy) - Allows you tooroute forwarded requests via an HTTP proxy.</span></span>  

-   <span data-ttu-id="585eb-118">[Definir o método de solicitação](#SetRequestMethod) -permite que você toochange método de saudação HTTP para uma solicitação.</span><span class="sxs-lookup"><span data-stu-id="585eb-118">[Set request method](#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>  
  
-   <span data-ttu-id="585eb-119">[Definir o código de status](#SetStatus) -valor especificado de toohello de código de status HTTP de saudação alterações.</span><span class="sxs-lookup"><span data-stu-id="585eb-119">[Set status code](#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>  
  
-   <span data-ttu-id="585eb-120">[Definir variável](api-management-advanced-policies.md#set-variable) – persiste um valor em uma variável de [contexto](api-management-policy-expressions.md#ContextVariables) nomeada para acesso posterior.</span><span class="sxs-lookup"><span data-stu-id="585eb-120">[Set variable](api-management-advanced-policies.md#set-variable) - Persists a value in a named [context](api-management-policy-expressions.md#ContextVariables) variable for later access.</span></span>  

-   <span data-ttu-id="585eb-121">[Rastreamento](#Trace) -adiciona uma cadeia de caracteres de saudação [API Inspetor](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) saída.</span><span class="sxs-lookup"><span data-stu-id="585eb-121">[Trace](#Trace) - Adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
-   <span data-ttu-id="585eb-122">[Aguarde](#Wait) -aguarda para colocados [solicitação de envio](api-management-advanced-policies.md#SendRequest), [obter o valor de cache](api-management-caching-policies.md#GetFromCacheByKey), ou [fluxo de controle](api-management-advanced-policies.md#choose) toocomplete políticas antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="585eb-122">[Wait](#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies toocomplete before proceeding.</span></span>  
  
##  <span data-ttu-id="585eb-123"><a name="choose"></a> Controlar fluxo</span><span class="sxs-lookup"><span data-stu-id="585eb-123"><a name="choose"></a> Control flow</span></span>  
 <span data-ttu-id="585eb-124">Olá `choose` política se aplica a política anexada construir instruções com base no resultado de saudação da avaliação de expressões Boolianas, semelhante tooan if-then-else ou uma opção em uma linguagem de programação.</span><span class="sxs-lookup"><span data-stu-id="585eb-124">hello `choose` policy applies enclosed policy statements based on hello outcome of evaluation of Boolean expressions, similar tooan if-then-else or a switch construct in a programming language.</span></span>  
  
###  <span data-ttu-id="585eb-125"><a name="ChoosePolicyStatement"></a> Declaração de política</span><span class="sxs-lookup"><span data-stu-id="585eb-125"><a name="ChoosePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<choose>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <otherwise>   
        <!— one or more policy statements toobe applied if none of hello above conditions are true  -->  
</otherwise>   
</choose>  
```  
  
 <span data-ttu-id="585eb-126">Olá política de controle de fluxo deve conter pelo menos um `<when/>` elemento.</span><span class="sxs-lookup"><span data-stu-id="585eb-126">hello control flow policy must contain at least one `<when/>` element.</span></span> <span data-ttu-id="585eb-127">Olá `<otherwise/>` elemento é opcional.</span><span class="sxs-lookup"><span data-stu-id="585eb-127">hello `<otherwise/>` element is optional.</span></span> <span data-ttu-id="585eb-128">Condições no `<when/>` elementos são avaliados na ordem de sua aparência na política de saudação.</span><span class="sxs-lookup"><span data-stu-id="585eb-128">Conditions in `<when/>` elements are evaluated in order of their appearance within hello policy.</span></span> <span data-ttu-id="585eb-129">Declarações de política em Olá primeiro `<when/>` elemento com atributo de condição é igual a `true` será aplicada.</span><span class="sxs-lookup"><span data-stu-id="585eb-129">Policy statement(s) enclosed within hello first `<when/>` element with condition attribute equals `true` will be applied.</span></span> <span data-ttu-id="585eb-130">Políticas entre Olá `<otherwise/>` elemento, se houver, será aplicado se todos os de saudação `<when/>` são atributos do elemento condição `false`.</span><span class="sxs-lookup"><span data-stu-id="585eb-130">Policies enclosed within hello `<otherwise/>` element, if present, will be applied if all of hello `<when/>` element condition attributes are `false`.</span></span>  
  
### <a name="examples"></a><span data-ttu-id="585eb-131">Exemplos</span><span class="sxs-lookup"><span data-stu-id="585eb-131">Examples</span></span>  
  
####  <span data-ttu-id="585eb-132"><a name="ChooseExample"></a> Exemplo</span><span class="sxs-lookup"><span data-stu-id="585eb-132"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="585eb-133">Olá exemplo a seguir demonstra um [variável definida](api-management-advanced-policies.md#set-variable) duas políticas de fluxo de controle e de política.</span><span class="sxs-lookup"><span data-stu-id="585eb-133">hello following example demonstrates a [set-variable](api-management-advanced-policies.md#set-variable) policy and two control flow policies.</span></span>  
  
 <span data-ttu-id="585eb-134">Olá definir variável política está em Olá seção de entrada e cria um `isMobile` booliano [contexto](api-management-policy-expressions.md#ContextVariables) variável definida tootrue se hello `User-Agent` solicitação cabeçalho contém o texto de saudação `iPad` ou `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="585eb-134">hello set variable policy is in hello inbound section and creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set tootrue if hello `User-Agent` request header contains hello text `iPad` or `iPhone`.</span></span>  
  
 <span data-ttu-id="585eb-135">Olá primeira política de fluxo de controle também está em Olá seção de entrada e aplica condicionalmente uma de duas [definir parâmetro de cadeia de caracteres de consulta](api-management-transformation-policies.md#SetQueryStringParameter) políticas dependendo do valor Olá Olá `isMobile` variável de contexto.</span><span class="sxs-lookup"><span data-stu-id="585eb-135">hello first control flow policy is also in hello inbound section, and conditionally applies one of two [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policies depending on hello value of hello `isMobile` context variable.</span></span>  
  
 <span data-ttu-id="585eb-136">política de fluxo de controle de segundo Hello está na seção de saída de hello e aplica condicionalmente Olá [converter XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) política quando `isMobile` está definido muito`true`.</span><span class="sxs-lookup"><span data-stu-id="585eb-136">hello second control flow policy is in hello outbound section and conditionally applies hello [Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) policy when `isMobile` is set too`true`.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="585eb-137">Exemplo</span><span class="sxs-lookup"><span data-stu-id="585eb-137">Example</span></span>  
 <span data-ttu-id="585eb-138">Este exemplo mostra como tooperform a filtragem de conteúdo removendo elementos de dados de resposta de saudação foi recebida do serviço de back-end Olá Olá `Starter` produto.</span><span class="sxs-lookup"><span data-stu-id="585eb-138">This example shows how tooperform content filtering by removing data elements from hello response received from hello backend service when using hello `Starter` product.</span></span> <span data-ttu-id="585eb-139">Para ver uma demonstração de como configurar e usar essa política, consulte [nuvem abrangem episódio 177: mais recursos de gerenciamento de API com Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e Avançar too34:30.</span><span class="sxs-lookup"><span data-stu-id="585eb-139">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too34:30.</span></span> <span data-ttu-id="585eb-140">Iniciar em 31:50 toosee uma visão geral de [Olá escuro API de previsão Sky](https://developer.forecast.io/) usado para esta demonstração.</span><span class="sxs-lookup"><span data-stu-id="585eb-140">Start  at 31:50 toosee an overview of [hello Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into hello outbound section tooremove a number of data elements from hello response received from hello backend service based on hello name of hello api product -->  
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
  
### <a name="elements"></a><span data-ttu-id="585eb-141">Elementos</span><span class="sxs-lookup"><span data-stu-id="585eb-141">Elements</span></span>  
  
|<span data-ttu-id="585eb-142">Elemento</span><span class="sxs-lookup"><span data-stu-id="585eb-142">Element</span></span>|<span data-ttu-id="585eb-143">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-143">Description</span></span>|<span data-ttu-id="585eb-144">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-144">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="585eb-145">choose</span><span class="sxs-lookup"><span data-stu-id="585eb-145">choose</span></span>|<span data-ttu-id="585eb-146">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="585eb-146">Root element.</span></span>|<span data-ttu-id="585eb-147">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-147">Yes</span></span>|  
|<span data-ttu-id="585eb-148">when</span><span class="sxs-lookup"><span data-stu-id="585eb-148">when</span></span>|<span data-ttu-id="585eb-149">Olá toouse condição para Olá `if` ou `ifelse` partes da saudação `choose` política.</span><span class="sxs-lookup"><span data-stu-id="585eb-149">hello condition toouse for hello `if` or `ifelse` parts of hello `choose` policy.</span></span> <span data-ttu-id="585eb-150">Se hello `choose` política tem vários `when` seções, elas serão avaliadas sequencialmente.</span><span class="sxs-lookup"><span data-stu-id="585eb-150">If hello `choose` policy has multiple `when` sections, they are evaluated sequentially.</span></span> <span data-ttu-id="585eb-151">Uma vez Olá `condition` de um quando o elemento avalia muito`true`, nenhuma outra `when` condições são avaliadas.</span><span class="sxs-lookup"><span data-stu-id="585eb-151">Once hello `condition` of a when element evaluates too`true`, no further `when` conditions are evaluated.</span></span>|<span data-ttu-id="585eb-152">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-152">Yes</span></span>|  
|<span data-ttu-id="585eb-153">otherwise</span><span class="sxs-lookup"><span data-stu-id="585eb-153">otherwise</span></span>|<span data-ttu-id="585eb-154">Contém Olá política trecho toobe usado se nenhum Olá `when` condições muito avaliar`true`.</span><span class="sxs-lookup"><span data-stu-id="585eb-154">Contains hello policy snippet toobe used if none of hello `when` conditions evaluate too`true`.</span></span>|<span data-ttu-id="585eb-155">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-155">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="585eb-156">Atributos</span><span class="sxs-lookup"><span data-stu-id="585eb-156">Attributes</span></span>  
  
|<span data-ttu-id="585eb-157">Atributo</span><span class="sxs-lookup"><span data-stu-id="585eb-157">Attribute</span></span>|<span data-ttu-id="585eb-158">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-158">Description</span></span>|<span data-ttu-id="585eb-159">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-159">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="585eb-160">condition="Boolean expression &#124; Boolean constant"</span><span class="sxs-lookup"><span data-stu-id="585eb-160">condition="Boolean expression &#124; Boolean constant"</span></span>|<span data-ttu-id="585eb-161">expressão booleana Hello ou constante tooevaluated quando Olá contendo `when` declaração da política é avaliada.</span><span class="sxs-lookup"><span data-stu-id="585eb-161">hello Boolean expression or constant tooevaluated when hello containing `when` policy statement is evaluated.</span></span>|<span data-ttu-id="585eb-162">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-162">Yes</span></span>|  
  
###  <span data-ttu-id="585eb-163"><a name="ChooseUsage"></a> Uso</span><span class="sxs-lookup"><span data-stu-id="585eb-163"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="585eb-164">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="585eb-164">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="585eb-165">**Seções da política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="585eb-165">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="585eb-166">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="585eb-166">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="585eb-167"><a name="ForwardRequest"></a> Encaminhar solicitação</span><span class="sxs-lookup"><span data-stu-id="585eb-167"><a name="ForwardRequest"></a> Forward request</span></span>  
 <span data-ttu-id="585eb-168">Olá `forward-request` política encaminha Olá entrada solicitação toohello serviço back-end especificado na solicitação de saudação [contexto](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="585eb-168">hello `forward-request` policy forwards hello incoming request toohello backend service specified in hello request [context](api-management-policy-expressions.md#ContextVariables).</span></span> <span data-ttu-id="585eb-169">Olá URL de serviço de back-end é especificado em Olá API [configurações](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) e pode ser alterado usando Olá [Configurar serviço de back-end](api-management-transformation-policies.md) política.</span><span class="sxs-lookup"><span data-stu-id="585eb-169">hello backend service URL is specified in hello API  [settings](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) and can be changed using hello [set backend service](api-management-transformation-policies.md) policy.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="585eb-170">Remover esta política resulta em solicitação Olá não está sendo encaminhada políticas de serviço e hello de back-end de toohello na seção de saída Olá é avaliadas imediatamente após a conclusão bem-sucedida de saudação de políticas do Olá Olá seção de entrada.</span><span class="sxs-lookup"><span data-stu-id="585eb-170">Removing this policy results in hello request not being forwarded toohello backend service and hello policies in hello outbound section are evaluated immediately upon hello successful completion of hello policies in hello inbound section.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="585eb-171">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="585eb-171">Policy statement</span></span>  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a><span data-ttu-id="585eb-172">Exemplos</span><span class="sxs-lookup"><span data-stu-id="585eb-172">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="585eb-173">Exemplo</span><span class="sxs-lookup"><span data-stu-id="585eb-173">Example</span></span>  
 <span data-ttu-id="585eb-174">Olá seguinte política de nível de API encaminha todas as solicitações de serviço de back-end toohello com um intervalo de tempo limite de 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="585eb-174">hello following API level policy forwards all requests toohello backend service with a timeout interval of 60 seconds.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="585eb-175">Exemplo</span><span class="sxs-lookup"><span data-stu-id="585eb-175">Example</span></span>  
 <span data-ttu-id="585eb-176">Esta política de nível de operação usa Olá `base` política de back-end do elemento tooinherit saudação do escopo de nível de API do pai de saudação.</span><span class="sxs-lookup"><span data-stu-id="585eb-176">This operation level policy uses hello `base` element tooinherit hello backend policy from hello parent API level scope.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="585eb-177">Exemplo</span><span class="sxs-lookup"><span data-stu-id="585eb-177">Example</span></span>  
 <span data-ttu-id="585eb-178">Essa política de nível de operação explicitamente encaminha todas as solicitações toohello back-end de serviço com um tempo limite de 120 e não herda pai Olá política de nível de back-end de API.</span><span class="sxs-lookup"><span data-stu-id="585eb-178">This operation level policy explicitly forwards all requests toohello backend service with a timeout of 120 and does not inherit hello parent API level backend policy.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="120"/>   
        <!-- effective policy. note hello absence of <base/> -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="585eb-179">Exemplo</span><span class="sxs-lookup"><span data-stu-id="585eb-179">Example</span></span>  
 <span data-ttu-id="585eb-180">Essa política de nível de operação não encaminhar solicitações de serviço de back-end toohello.</span><span class="sxs-lookup"><span data-stu-id="585eb-180">This operation level policy does not forward requests toohello backend service.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <!-- no forwarding toobackend -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="585eb-181">Elementos</span><span class="sxs-lookup"><span data-stu-id="585eb-181">Elements</span></span>  
  
|<span data-ttu-id="585eb-182">Elemento</span><span class="sxs-lookup"><span data-stu-id="585eb-182">Element</span></span>|<span data-ttu-id="585eb-183">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-183">Description</span></span>|<span data-ttu-id="585eb-184">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-184">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="585eb-185">forward-request</span><span class="sxs-lookup"><span data-stu-id="585eb-185">forward-request</span></span>|<span data-ttu-id="585eb-186">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="585eb-186">Root element.</span></span>|<span data-ttu-id="585eb-187">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-187">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="585eb-188">Atributos</span><span class="sxs-lookup"><span data-stu-id="585eb-188">Attributes</span></span>  
  
|<span data-ttu-id="585eb-189">Atributo</span><span class="sxs-lookup"><span data-stu-id="585eb-189">Attribute</span></span>|<span data-ttu-id="585eb-190">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-190">Description</span></span>|<span data-ttu-id="585eb-191">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-191">Required</span></span>|<span data-ttu-id="585eb-192">Padrão</span><span class="sxs-lookup"><span data-stu-id="585eb-192">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="585eb-193">timeout="integer"</span><span class="sxs-lookup"><span data-stu-id="585eb-193">timeout="integer"</span></span>|<span data-ttu-id="585eb-194">intervalo de tempo limite de saudação em segundos antes que o serviço de back-end do hello chamada toohello falha.</span><span class="sxs-lookup"><span data-stu-id="585eb-194">hello timeout interval in seconds before hello call toohello backend service fails.</span></span>|<span data-ttu-id="585eb-195">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-195">No</span></span>|<span data-ttu-id="585eb-196">Sem tempo limite</span><span class="sxs-lookup"><span data-stu-id="585eb-196">No timeout</span></span>|  
|<span data-ttu-id="585eb-197">follow-redirects="true &#124; false"</span><span class="sxs-lookup"><span data-stu-id="585eb-197">follow-redirects="true &#124; false"</span></span>|<span data-ttu-id="585eb-198">Especifica se os redirecionamentos de serviço de back-end de saudação são seguidos pelo gateway de saudação ou retornados toohello chamador.</span><span class="sxs-lookup"><span data-stu-id="585eb-198">Specifies whether redirects from hello backend service are followed by hello gateway or returned toohello caller.</span></span>|<span data-ttu-id="585eb-199">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-199">No</span></span>|<span data-ttu-id="585eb-200">false</span><span class="sxs-lookup"><span data-stu-id="585eb-200">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="585eb-201">Uso</span><span class="sxs-lookup"><span data-stu-id="585eb-201">Usage</span></span>  
 <span data-ttu-id="585eb-202">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="585eb-202">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="585eb-203">**Seções de política:** back-end</span><span class="sxs-lookup"><span data-stu-id="585eb-203">**Policy sections:** backend</span></span>  
  
-   <span data-ttu-id="585eb-204">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="585eb-204">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="585eb-205"><a name="LimitConcurrency"></a> Simultaneidade de limite</span><span class="sxs-lookup"><span data-stu-id="585eb-205"><a name="LimitConcurrency"></a> Limit concurrency</span></span>  
 <span data-ttu-id="585eb-206">Olá `limit-concurrency` política impede entre as políticas de execução por mais de Olá quantidade especificada de solicitações em um determinado momento.</span><span class="sxs-lookup"><span data-stu-id="585eb-206">hello `limit-concurrency` policy prevents enclosed policies from executing by more than hello specified number of requests at a given time.</span></span> <span data-ttu-id="585eb-207">Ao exceder o limite de hello, novas solicitações são adicionadas tooa fila, até que o comprimento máximo da fila de saudação é obtido.</span><span class="sxs-lookup"><span data-stu-id="585eb-207">Upon exceeding hello threshold, new requests are added tooa queue, until hello maximum queue length is achieved.</span></span> <span data-ttu-id="585eb-208">Quando a fila atinge seu máximo, novas solicitações falham imediatamente.</span><span class="sxs-lookup"><span data-stu-id="585eb-208">Upon queue exhaustion, new requests will fail immediately.</span></span>
  
###  <span data-ttu-id="585eb-209"><a name="LimitConcurrencyStatement"></a> Declaração de política</span><span class="sxs-lookup"><span data-stu-id="585eb-209"><a name="LimitConcurrencyStatement"></a> Policy statement</span></span>  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a><span data-ttu-id="585eb-210">Exemplos</span><span class="sxs-lookup"><span data-stu-id="585eb-210">Examples</span></span>  
  
####  <span data-ttu-id="585eb-211"><a name="ChooseExample"></a> Exemplo</span><span class="sxs-lookup"><span data-stu-id="585eb-211"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="585eb-212">Olá exemplo a seguir demonstra como o número de solicitações toolimit encaminhado tooa back-end com base no valor de saudação de uma variável de contexto.</span><span class="sxs-lookup"><span data-stu-id="585eb-212">hello following example demonstrates how toolimit number of requests forwarded tooa backend based on hello value of a context variable.</span></span>
 
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

### <a name="elements"></a><span data-ttu-id="585eb-213">Elementos</span><span class="sxs-lookup"><span data-stu-id="585eb-213">Elements</span></span>  
  
|<span data-ttu-id="585eb-214">Elemento</span><span class="sxs-lookup"><span data-stu-id="585eb-214">Element</span></span>|<span data-ttu-id="585eb-215">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-215">Description</span></span>|<span data-ttu-id="585eb-216">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-216">Required</span></span>|  
|-------------|-----------------|--------------|    
|<span data-ttu-id="585eb-217">limit-concurrency</span><span class="sxs-lookup"><span data-stu-id="585eb-217">limit-concurrency</span></span>|<span data-ttu-id="585eb-218">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="585eb-218">Root element.</span></span>|<span data-ttu-id="585eb-219">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="585eb-220">Atributos</span><span class="sxs-lookup"><span data-stu-id="585eb-220">Attributes</span></span>  
  
|<span data-ttu-id="585eb-221">Atributo</span><span class="sxs-lookup"><span data-stu-id="585eb-221">Attribute</span></span>|<span data-ttu-id="585eb-222">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-222">Description</span></span>|<span data-ttu-id="585eb-223">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-223">Required</span></span>|<span data-ttu-id="585eb-224">Padrão</span><span class="sxs-lookup"><span data-stu-id="585eb-224">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="585eb-225">chave</span><span class="sxs-lookup"><span data-stu-id="585eb-225">key</span></span>|<span data-ttu-id="585eb-226">Uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="585eb-226">A string.</span></span> <span data-ttu-id="585eb-227">Expressão permitida.</span><span class="sxs-lookup"><span data-stu-id="585eb-227">Expression allowed.</span></span> <span data-ttu-id="585eb-228">Especifica o escopo de simultaneidade hello.</span><span class="sxs-lookup"><span data-stu-id="585eb-228">Specifies hello concurrency scope.</span></span> <span data-ttu-id="585eb-229">Pode ser compartilhado por várias políticas.</span><span class="sxs-lookup"><span data-stu-id="585eb-229">Can be shared by multiple policies.</span></span>|<span data-ttu-id="585eb-230">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-230">Yes</span></span>|<span data-ttu-id="585eb-231">N/D</span><span class="sxs-lookup"><span data-stu-id="585eb-231">N/A</span></span>|  
|<span data-ttu-id="585eb-232">max-count</span><span class="sxs-lookup"><span data-stu-id="585eb-232">max-count</span></span>|<span data-ttu-id="585eb-233">Um inteiro.</span><span class="sxs-lookup"><span data-stu-id="585eb-233">An integer.</span></span> <span data-ttu-id="585eb-234">Especifica um número máximo de solicitações permitido tooenter política de saudação.</span><span class="sxs-lookup"><span data-stu-id="585eb-234">Specifies a maximum number of requests that are allowed tooenter hello policy.</span></span>|<span data-ttu-id="585eb-235">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-235">Yes</span></span>|<span data-ttu-id="585eb-236">N/D</span><span class="sxs-lookup"><span data-stu-id="585eb-236">N/A</span></span>|  
|<span data-ttu-id="585eb-237">Tempo limite</span><span class="sxs-lookup"><span data-stu-id="585eb-237">timeout</span></span>|<span data-ttu-id="585eb-238">Um inteiro.</span><span class="sxs-lookup"><span data-stu-id="585eb-238">An integer.</span></span> <span data-ttu-id="585eb-239">Expressão permitida.</span><span class="sxs-lookup"><span data-stu-id="585eb-239">Expression allowed.</span></span> <span data-ttu-id="585eb-240">Especifica o número de saudação de segundos que uma solicitação deve esperar tooenter antes de falhar com um escopo de "403 muito muitas solicitações"</span><span class="sxs-lookup"><span data-stu-id="585eb-240">Specifies hello number of seconds a request should wait tooenter a scope before failing with "403 Too Many Requests"</span></span>|<span data-ttu-id="585eb-241">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-241">No</span></span>|<span data-ttu-id="585eb-242">Infinito</span><span class="sxs-lookup"><span data-stu-id="585eb-242">Infinity</span></span>|  
|<span data-ttu-id="585eb-243">max-queue-length</span><span class="sxs-lookup"><span data-stu-id="585eb-243">max-queue-length</span></span>|<span data-ttu-id="585eb-244">Um inteiro.</span><span class="sxs-lookup"><span data-stu-id="585eb-244">An integer.</span></span> <span data-ttu-id="585eb-245">Expressão permitida.</span><span class="sxs-lookup"><span data-stu-id="585eb-245">Expression allowed.</span></span> <span data-ttu-id="585eb-246">Especifica o comprimento máximo da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="585eb-246">Specifies hello maximum queue length.</span></span> <span data-ttu-id="585eb-247">Solicitações de entrada tentar tooenter essa política será encerrada com "403 muito muitas solicitações" imediatamente quando a fila de saudação é esgotada.</span><span class="sxs-lookup"><span data-stu-id="585eb-247">Incoming requests trying tooenter this policy will be terminated with “403 Too Many Requests” immediately when hello queue is exhausted.</span></span>|<span data-ttu-id="585eb-248">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-248">No</span></span>|<span data-ttu-id="585eb-249">Infinito</span><span class="sxs-lookup"><span data-stu-id="585eb-249">Infinity</span></span>|  
  
###  <span data-ttu-id="585eb-250"><a name="ChooseUsage"></a> Uso</span><span class="sxs-lookup"><span data-stu-id="585eb-250"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="585eb-251">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="585eb-251">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="585eb-252">**Seções da política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="585eb-252">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="585eb-253">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="585eb-253">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="585eb-254"><a name="log-to-eventhub"></a>Log tooEvent Hub</span><span class="sxs-lookup"><span data-stu-id="585eb-254"><a name="log-to-eventhub"></a> Log tooEvent Hub</span></span>  
 <span data-ttu-id="585eb-255">Olá `log-to-eventhub` política envia mensagens de saudação especificado formato tooan Hub de eventos definidos por uma entidade de agente de log.</span><span class="sxs-lookup"><span data-stu-id="585eb-255">hello `log-to-eventhub` policy sends messages in hello specified format tooan Event Hub defined by a Logger entity.</span></span> <span data-ttu-id="585eb-256">Como o nome sugere, política de saudação é usada para salvar selecionadas informações de contexto de solicitação ou resposta para a análise online ou offline.</span><span class="sxs-lookup"><span data-stu-id="585eb-256">As its name implies, hello policy is used for saving selected request or response context information for online or offline analysis.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="585eb-257">Para um guia passo a passo sobre como configurar um hub de eventos e log de eventos, consulte [como toolog eventos de gerenciamento de API com Hubs de eventos do Azure](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="585eb-257">For a step-by-step guide on configuring an event hub and logging events, see [How toolog API Management events with Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="585eb-258">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="585eb-258">Policy statement</span></span>  
  
```xml  
<log-to-eventhub logger-id="id of hello logger entity" partition-id="index of hello partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string toobe logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a><span data-ttu-id="585eb-259">Exemplo</span><span class="sxs-lookup"><span data-stu-id="585eb-259">Example</span></span>  
 <span data-ttu-id="585eb-260">Qualquer cadeia de caracteres pode ser usada como Olá valor toobe registrado em Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="585eb-260">Any string can be used as hello value toobe logged in Event Hubs.</span></span> <span data-ttu-id="585eb-261">Neste exemplo hello data e hora, o nome do serviço de implantação, o id da solicitação, o endereço ip e o nome da operação para todas as chamadas de entrada são hub de eventos registrados toohello agente registrado com hello `contoso-logger` id.</span><span class="sxs-lookup"><span data-stu-id="585eb-261">In this example hello date and time, deployment service name, request id, ip address, and operation name for all inbound calls are logged toohello event hub Logger registered with hello `contoso-logger` id.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="585eb-262">Elementos</span><span class="sxs-lookup"><span data-stu-id="585eb-262">Elements</span></span>  
  
|<span data-ttu-id="585eb-263">Elemento</span><span class="sxs-lookup"><span data-stu-id="585eb-263">Element</span></span>|<span data-ttu-id="585eb-264">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-264">Description</span></span>|<span data-ttu-id="585eb-265">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-265">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="585eb-266">log-to-eventhub</span><span class="sxs-lookup"><span data-stu-id="585eb-266">log-to-eventhub</span></span>|<span data-ttu-id="585eb-267">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="585eb-267">Root element.</span></span> <span data-ttu-id="585eb-268">valor Olá desse elemento é o hub de eventos do hello cadeia de caracteres toolog tooyour.</span><span class="sxs-lookup"><span data-stu-id="585eb-268">hello value of this element is hello string toolog tooyour event hub.</span></span>|<span data-ttu-id="585eb-269">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-269">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="585eb-270">Atributos</span><span class="sxs-lookup"><span data-stu-id="585eb-270">Attributes</span></span>  
  
|<span data-ttu-id="585eb-271">Atributo</span><span class="sxs-lookup"><span data-stu-id="585eb-271">Attribute</span></span>|<span data-ttu-id="585eb-272">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-272">Description</span></span>|<span data-ttu-id="585eb-273">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-273">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="585eb-274">logger-id</span><span class="sxs-lookup"><span data-stu-id="585eb-274">logger-id</span></span>|<span data-ttu-id="585eb-275">id de saudação do hello agente registrado com o serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="585eb-275">hello id of hello Logger registered with your API Management service.</span></span>|<span data-ttu-id="585eb-276">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-276">Yes</span></span>|  
|<span data-ttu-id="585eb-277">partition-id</span><span class="sxs-lookup"><span data-stu-id="585eb-277">partition-id</span></span>|<span data-ttu-id="585eb-278">Especifica o índice de saudação da partição Olá onde as mensagens são enviadas.</span><span class="sxs-lookup"><span data-stu-id="585eb-278">Specifies hello index of hello partition where messages are sent.</span></span>|<span data-ttu-id="585eb-279">Opcional.</span><span class="sxs-lookup"><span data-stu-id="585eb-279">Optional.</span></span> <span data-ttu-id="585eb-280">Esse atributo não poderá ser usado se `partition-key` for usado.</span><span class="sxs-lookup"><span data-stu-id="585eb-280">This attribute may not be used if `partition-key` is used.</span></span>|  
|<span data-ttu-id="585eb-281">partition-key</span><span class="sxs-lookup"><span data-stu-id="585eb-281">partition-key</span></span>|<span data-ttu-id="585eb-282">Especifica o valor de saudação usado para atribuição de partição quando as mensagens são enviadas.</span><span class="sxs-lookup"><span data-stu-id="585eb-282">Specifies hello value used for partition assignment when messages are sent.</span></span>|<span data-ttu-id="585eb-283">Opcional.</span><span class="sxs-lookup"><span data-stu-id="585eb-283">Optional.</span></span> <span data-ttu-id="585eb-284">Esse atributo não poderá ser usado se `partition-id` for usado.</span><span class="sxs-lookup"><span data-stu-id="585eb-284">This attribute may not be used if `partition-id` is used.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="585eb-285">Uso</span><span class="sxs-lookup"><span data-stu-id="585eb-285">Usage</span></span>  
 <span data-ttu-id="585eb-286">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="585eb-286">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="585eb-287">**Seções da política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="585eb-287">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="585eb-288">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="585eb-288">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="585eb-289"><a name="mock-response"></a> Resposta fictícia</span><span class="sxs-lookup"><span data-stu-id="585eb-289"><a name="mock-response"></a> Mock response</span></span>  
<span data-ttu-id="585eb-290">Olá `mock-response`, como nome de saudação implica, é usado toomock APIs e operações.</span><span class="sxs-lookup"><span data-stu-id="585eb-290">hello `mock-response`, as hello name implies, is used toomock APIs and operations.</span></span> <span data-ttu-id="585eb-291">Ele anula a execução do pipeline normal e retorna um chamador de toohello resposta fictícios.</span><span class="sxs-lookup"><span data-stu-id="585eb-291">It aborts normal pipeline execution and returns a mocked response toohello caller.</span></span> <span data-ttu-id="585eb-292">política de saudação sempre tenta tooreturn respostas de maior fidelidade.</span><span class="sxs-lookup"><span data-stu-id="585eb-292">hello policy always tries tooreturn responses of highest fidelity.</span></span> <span data-ttu-id="585eb-293">Ela prefere exemplos de conteúdo de resposta, sempre que disponíveis.</span><span class="sxs-lookup"><span data-stu-id="585eb-293">It prefers response content examples, whenever available.</span></span> <span data-ttu-id="585eb-294">Ela gera respostas de exemplo com base em esquemas, quando esquemas são fornecidos e exemplos não são fornecidos.</span><span class="sxs-lookup"><span data-stu-id="585eb-294">It generates sample responses from schemas, when schemas are provided and examples are not.</span></span> <span data-ttu-id="585eb-295">Se não forem encontrados exemplos nem esquemas, serão retornadas respostas sem conteúdo.</span><span class="sxs-lookup"><span data-stu-id="585eb-295">If neither examples or schemas are found, responses with no content are returned.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="585eb-296">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="585eb-296">Policy statement</span></span>  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="585eb-297">Exemplos</span><span class="sxs-lookup"><span data-stu-id="585eb-297">Examples</span></span>  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, hello content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, hello content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a><span data-ttu-id="585eb-298">Elementos</span><span class="sxs-lookup"><span data-stu-id="585eb-298">Elements</span></span>  
  
|<span data-ttu-id="585eb-299">Elemento</span><span class="sxs-lookup"><span data-stu-id="585eb-299">Element</span></span>|<span data-ttu-id="585eb-300">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-300">Description</span></span>|<span data-ttu-id="585eb-301">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-301">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="585eb-302">mock-response</span><span class="sxs-lookup"><span data-stu-id="585eb-302">mock-response</span></span>|<span data-ttu-id="585eb-303">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="585eb-303">Root element.</span></span>|<span data-ttu-id="585eb-304">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-304">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="585eb-305">Atributos</span><span class="sxs-lookup"><span data-stu-id="585eb-305">Attributes</span></span>  
  
|<span data-ttu-id="585eb-306">Atributo</span><span class="sxs-lookup"><span data-stu-id="585eb-306">Attribute</span></span>|<span data-ttu-id="585eb-307">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-307">Description</span></span>|<span data-ttu-id="585eb-308">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-308">Required</span></span>|<span data-ttu-id="585eb-309">Padrão</span><span class="sxs-lookup"><span data-stu-id="585eb-309">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="585eb-310">status-code</span><span class="sxs-lookup"><span data-stu-id="585eb-310">status-code</span></span>|<span data-ttu-id="585eb-311">Especifica o código de status de resposta e é exemplo correspondente tooselect usado ou esquema.</span><span class="sxs-lookup"><span data-stu-id="585eb-311">Specifies response status code and is used tooselect corresponding example or schema.</span></span>|<span data-ttu-id="585eb-312">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-312">No</span></span>|<span data-ttu-id="585eb-313">200</span><span class="sxs-lookup"><span data-stu-id="585eb-313">200</span></span>|  
|<span data-ttu-id="585eb-314">content-type</span><span class="sxs-lookup"><span data-stu-id="585eb-314">content-type</span></span>|<span data-ttu-id="585eb-315">Especifica `Content-Type` valor do cabeçalho de resposta e exemplo correspondente tooselect usado ou esquema.</span><span class="sxs-lookup"><span data-stu-id="585eb-315">Specifies `Content-Type` response header value and is used tooselect corresponding example or schema.</span></span>|<span data-ttu-id="585eb-316">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-316">No</span></span>|<span data-ttu-id="585eb-317">Nenhum</span><span class="sxs-lookup"><span data-stu-id="585eb-317">None</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="585eb-318">Uso</span><span class="sxs-lookup"><span data-stu-id="585eb-318">Usage</span></span>  
 <span data-ttu-id="585eb-319">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="585eb-319">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="585eb-320">**Seções de política:** de entrada, de saída, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="585eb-320">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="585eb-321">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="585eb-321">**Policy scopes:** all scopes</span></span>

##  <span data-ttu-id="585eb-322"><a name="Retry"></a> Repetir</span><span class="sxs-lookup"><span data-stu-id="585eb-322"><a name="Retry"></a> Retry</span></span>  
 <span data-ttu-id="585eb-323">Olá `retry` política suas diretivas de filho é executado uma vez e, em seguida, tenta novamente sua execução até repetição Olá `condition` se torna `false` ou repita `count` está esgotada.</span><span class="sxs-lookup"><span data-stu-id="585eb-323">hello             `retry` policy executes its child policies once and then retries their execution until hello retry `condition` becomes            `false` or retry            `count` is exhausted.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="585eb-324">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="585eb-324">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="585eb-325">Exemplo</span><span class="sxs-lookup"><span data-stu-id="585eb-325">Example</span></span>  
 <span data-ttu-id="585eb-326">Em Olá forewarding de solicitação de exemplo a seguir é repetida backup tooten usando algoritmo de repetição exponencial.</span><span class="sxs-lookup"><span data-stu-id="585eb-326">In hello following example request forewarding is retried up tooten times using exponential retry algorithm.</span></span> <span data-ttu-id="585eb-327">Como `first-fast-retry` é definido como toofalse, todas as tentativas de repetição são algoritmo toohello exponsntial tente novamente.</span><span class="sxs-lookup"><span data-stu-id="585eb-327">Since                    `first-fast-retry` is set toofalse, all retry attempts are subject toohello exponsntial retry algorithm.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="585eb-328">Elementos</span><span class="sxs-lookup"><span data-stu-id="585eb-328">Elements</span></span>  
  
|<span data-ttu-id="585eb-329">Elemento</span><span class="sxs-lookup"><span data-stu-id="585eb-329">Element</span></span>|<span data-ttu-id="585eb-330">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-330">Description</span></span>|<span data-ttu-id="585eb-331">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-331">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="585eb-332">tentar novamente</span><span class="sxs-lookup"><span data-stu-id="585eb-332">retry</span></span>|<span data-ttu-id="585eb-333">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="585eb-333">Root element.</span></span> <span data-ttu-id="585eb-334">Pode conter quaisquer outras políticas como seus elementos filho.</span><span class="sxs-lookup"><span data-stu-id="585eb-334">May contain any other policies as its child elements.</span></span>|<span data-ttu-id="585eb-335">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-335">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="585eb-336">Atributos</span><span class="sxs-lookup"><span data-stu-id="585eb-336">Attributes</span></span>  
  
|<span data-ttu-id="585eb-337">Atributo</span><span class="sxs-lookup"><span data-stu-id="585eb-337">Attribute</span></span>|<span data-ttu-id="585eb-338">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-338">Description</span></span>|<span data-ttu-id="585eb-339">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-339">Required</span></span>|<span data-ttu-id="585eb-340">Padrão</span><span class="sxs-lookup"><span data-stu-id="585eb-340">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="585eb-341">condition</span><span class="sxs-lookup"><span data-stu-id="585eb-341">condition</span></span>|<span data-ttu-id="585eb-342">Uma [expressão](api-management-policy-expressions.md) ou literal booliano especificando se as novas tentativas devem ser paradas (`false`) ou continuadas (`true`).</span><span class="sxs-lookup"><span data-stu-id="585eb-342">A boolean literal or [expression](api-management-policy-expressions.md) specifying if retries should be stopped (`false`) or continued (`true`).</span></span>|<span data-ttu-id="585eb-343">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-343">Yes</span></span>|<span data-ttu-id="585eb-344">N/D</span><span class="sxs-lookup"><span data-stu-id="585eb-344">N/A</span></span>|  
|<span data-ttu-id="585eb-345">count</span><span class="sxs-lookup"><span data-stu-id="585eb-345">count</span></span>|<span data-ttu-id="585eb-346">Um número positivo que especifica o número máximo de saudação do tooattempt de novas tentativas.</span><span class="sxs-lookup"><span data-stu-id="585eb-346">A positive number specifying hello maximum number of retries tooattempt.</span></span>|<span data-ttu-id="585eb-347">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-347">Yes</span></span>|<span data-ttu-id="585eb-348">N/D</span><span class="sxs-lookup"><span data-stu-id="585eb-348">N/A</span></span>|  
|<span data-ttu-id="585eb-349">intervalo</span><span class="sxs-lookup"><span data-stu-id="585eb-349">interval</span></span>|<span data-ttu-id="585eb-350">Um número positivo, em segundos, especificando o intervalo de espera de saudação entre as tentativas de repetição de saudação.</span><span class="sxs-lookup"><span data-stu-id="585eb-350">A positive number in seconds specifying hello wait interval between hello retry attempts.</span></span>|<span data-ttu-id="585eb-351">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-351">Yes</span></span>|<span data-ttu-id="585eb-352">N/D</span><span class="sxs-lookup"><span data-stu-id="585eb-352">N/A</span></span>|  
|<span data-ttu-id="585eb-353">max-interval</span><span class="sxs-lookup"><span data-stu-id="585eb-353">max-interval</span></span>|<span data-ttu-id="585eb-354">Um número positivo, em segundos, especificando o intervalo de espera máximo Olá entre as tentativas de repetição de saudação.</span><span class="sxs-lookup"><span data-stu-id="585eb-354">A positive number in seconds specifying hello maximum wait interval between hello retry attempts.</span></span> <span data-ttu-id="585eb-355">É usado tooimplement um algoritmo de repetição exponencial.</span><span class="sxs-lookup"><span data-stu-id="585eb-355">It is used tooimplement an exponential retry algorithm.</span></span>|<span data-ttu-id="585eb-356">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-356">No</span></span>|<span data-ttu-id="585eb-357">N/D</span><span class="sxs-lookup"><span data-stu-id="585eb-357">N/A</span></span>|  
|<span data-ttu-id="585eb-358">delta</span><span class="sxs-lookup"><span data-stu-id="585eb-358">delta</span></span>|<span data-ttu-id="585eb-359">Um número positivo em segundos para especificar o incremento de intervalo de espera de saudação.</span><span class="sxs-lookup"><span data-stu-id="585eb-359">A positive number in seconds specifying hello wait interval increment.</span></span> <span data-ttu-id="585eb-360">É usado tooimplement Olá repetição linear e exponencial algoritmos.</span><span class="sxs-lookup"><span data-stu-id="585eb-360">It is used tooimplement hello linear and exponential retry algorithms.</span></span>|<span data-ttu-id="585eb-361">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-361">No</span></span>|<span data-ttu-id="585eb-362">N/D</span><span class="sxs-lookup"><span data-stu-id="585eb-362">N/A</span></span>|  
|<span data-ttu-id="585eb-363">first-fast-retry</span><span class="sxs-lookup"><span data-stu-id="585eb-363">first-fast-retry</span></span>|<span data-ttu-id="585eb-364">Se definir muito `true` , Olá primeira tentativa de repetição é executada imediatamente.</span><span class="sxs-lookup"><span data-stu-id="585eb-364">If set too                                   `true` , hello first retry attempt is performed immediately.</span></span>|<span data-ttu-id="585eb-365">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-365">No</span></span>|`false`|  
  
> [!NOTE]
>  <span data-ttu-id="585eb-366">Quando apenas Olá `interval` for especificado, **fixa** tentativas de intervalo são executadas.</span><span class="sxs-lookup"><span data-stu-id="585eb-366">When only hello `interval` is specified, **fixed** interval retries are performed.</span></span>  
>  <span data-ttu-id="585eb-367">Quando apenas Olá `interval` e `delta` forem especificados, um **linear** é usado pelo algoritmo de nova tentativa de intervalo em que o tempo de espera entre as repetições é Olá calculada de acordo seguinte fórmula - `interval + (count - 1)*delta`.</span><span class="sxs-lookup"><span data-stu-id="585eb-367">When only hello `interval` and `delta` are specified, a **linear** interval retry algorithm is used, where wait time between retries is calculated according hello following formula - `interval + (count - 1)*delta`.</span></span>  
>  <span data-ttu-id="585eb-368">Olá quando `interval`, `max-interval` e `delta` forem especificados, **exponencial** algoritmo de nova tentativa de intervalo é aplicado, onde o tempo de espera de saudação entre repetições Olá está aumentando exponencialmente do valor de saudação do `interval`valor toohello `max-interval` de acordo com o seguinte toohello forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span><span class="sxs-lookup"><span data-stu-id="585eb-368">When hello `interval`, `max-interval` and `delta` are specified, **exponential** interval retry algorithm is applied, where hello wait time between hello retries is growing exponentially from hello value of `interval` toohello value `max-interval` according toohello following forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span></span>  
  
### <a name="usage"></a><span data-ttu-id="585eb-369">Uso</span><span class="sxs-lookup"><span data-stu-id="585eb-369">Usage</span></span>  
 <span data-ttu-id="585eb-370">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="585eb-370">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span> <span data-ttu-id="585eb-371">Observe que as restrições de uso de política filho serão herdadas por essa política.</span><span class="sxs-lookup"><span data-stu-id="585eb-371">Note that child policy usage restrictions will be inherited by this policy.</span></span>  
  
-   <span data-ttu-id="585eb-372">**Seções da política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="585eb-372">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="585eb-373">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="585eb-373">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="585eb-374"><a name="ReturnResponse"></a> Retornar resposta</span><span class="sxs-lookup"><span data-stu-id="585eb-374"><a name="ReturnResponse"></a> Return response</span></span>  
 <span data-ttu-id="585eb-375">Olá `return-response` política anula a execução do pipeline e retorna um padrão ou o chamador de toohello de resposta personalizada.</span><span class="sxs-lookup"><span data-stu-id="585eb-375">hello `return-response` policy aborts pipeline execution and returns either a default or custom response toohello caller.</span></span> <span data-ttu-id="585eb-376">A resposta padrão é `200 OK` sem corpo.</span><span class="sxs-lookup"><span data-stu-id="585eb-376">Default response is `200 OK` with no body.</span></span> <span data-ttu-id="585eb-377">A resposta personalizada pode ser especificada por meio de declarações de política ou variável de contexto.</span><span class="sxs-lookup"><span data-stu-id="585eb-377">Custom response can be specified via a context variable or policy statements.</span></span> <span data-ttu-id="585eb-378">Quando ambos são fornecidas, resposta Olá contida na variável de contexto de saudação é modificada por declarações de política de saudação antes de serem retornados toohello chamador.</span><span class="sxs-lookup"><span data-stu-id="585eb-378">When both are provided, hello response contained within hello context variable is modified by hello policy statements before being returned toohello caller.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="585eb-379">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="585eb-379">Policy statement</span></span>  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a><span data-ttu-id="585eb-380">Exemplo</span><span class="sxs-lookup"><span data-stu-id="585eb-380">Example</span></span>  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="585eb-381">Elementos</span><span class="sxs-lookup"><span data-stu-id="585eb-381">Elements</span></span>  
  
|<span data-ttu-id="585eb-382">Elemento</span><span class="sxs-lookup"><span data-stu-id="585eb-382">Element</span></span>|<span data-ttu-id="585eb-383">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-383">Description</span></span>|<span data-ttu-id="585eb-384">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-384">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="585eb-385">return-response</span><span class="sxs-lookup"><span data-stu-id="585eb-385">return-response</span></span>|<span data-ttu-id="585eb-386">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="585eb-386">Root element.</span></span>|<span data-ttu-id="585eb-387">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-387">Yes</span></span>|  
|<span data-ttu-id="585eb-388">set-header</span><span class="sxs-lookup"><span data-stu-id="585eb-388">set-header</span></span>|<span data-ttu-id="585eb-389">Uma declaração de política [set-header](api-management-transformation-policies.md#SetHTTPheader).</span><span class="sxs-lookup"><span data-stu-id="585eb-389">A [set-header](api-management-transformation-policies.md#SetHTTPheader) policy statement.</span></span>|<span data-ttu-id="585eb-390">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-390">No</span></span>|  
|<span data-ttu-id="585eb-391">set-body</span><span class="sxs-lookup"><span data-stu-id="585eb-391">set-body</span></span>|<span data-ttu-id="585eb-392">Uma declaração de política [set-body](api-management-transformation-policies.md#SetBody).</span><span class="sxs-lookup"><span data-stu-id="585eb-392">A [set-body](api-management-transformation-policies.md#SetBody) policy statement.</span></span>|<span data-ttu-id="585eb-393">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-393">No</span></span>|  
|<span data-ttu-id="585eb-394">set-status</span><span class="sxs-lookup"><span data-stu-id="585eb-394">set-status</span></span>|<span data-ttu-id="585eb-395">Uma declaração de política [set-status](api-management-advanced-policies.md#SetStatus).</span><span class="sxs-lookup"><span data-stu-id="585eb-395">A [set-status](api-management-advanced-policies.md#SetStatus) policy statement.</span></span>|<span data-ttu-id="585eb-396">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-396">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="585eb-397">Atributos</span><span class="sxs-lookup"><span data-stu-id="585eb-397">Attributes</span></span>  
  
|<span data-ttu-id="585eb-398">Atributo</span><span class="sxs-lookup"><span data-stu-id="585eb-398">Attribute</span></span>|<span data-ttu-id="585eb-399">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-399">Description</span></span>|<span data-ttu-id="585eb-400">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-400">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="585eb-401">response-variable-name</span><span class="sxs-lookup"><span data-stu-id="585eb-401">response-variable-name</span></span>|<span data-ttu-id="585eb-402">Hello nome de variável de contexto Olá referenciado, por exemplo, um upstream [solicitação de envio](api-management-advanced-policies.md#SendRequest) política e que contém um `Response` objeto</span><span class="sxs-lookup"><span data-stu-id="585eb-402">hello name of hello context variable referenced from, for example, an upstream [send-request](api-management-advanced-policies.md#SendRequest) policy and containing a `Response` object</span></span>|<span data-ttu-id="585eb-403">Opcional.</span><span class="sxs-lookup"><span data-stu-id="585eb-403">Optional.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="585eb-404">Uso</span><span class="sxs-lookup"><span data-stu-id="585eb-404">Usage</span></span>  
 <span data-ttu-id="585eb-405">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="585eb-405">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="585eb-406">**Seções da política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="585eb-406">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="585eb-407">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="585eb-407">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="585eb-408"><a name="SendOneWayRequest"></a> Enviar solicitação unidirecional</span><span class="sxs-lookup"><span data-stu-id="585eb-408"><a name="SendOneWayRequest"></a> Send one way request</span></span>  
 <span data-ttu-id="585eb-409">Olá `send-one-way-request` política envia a solicitação de saudação fornecida toohello especificada URL sem aguardar uma resposta.</span><span class="sxs-lookup"><span data-stu-id="585eb-409">hello `send-one-way-request` policy sends hello provided request toohello specified URL without waiting for a response.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="585eb-410">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="585eb-410">Policy statement</span></span>  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="585eb-411">Exemplo</span><span class="sxs-lookup"><span data-stu-id="585eb-411">Example</span></span>  
 <span data-ttu-id="585eb-412">Essa política de exemplo mostra um exemplo do uso de saudação `send-one-way-request` política toosend uma mensagem tooa atraso salas de chat se Olá código de resposta HTTP for too500 maior que ou igual.</span><span class="sxs-lookup"><span data-stu-id="585eb-412">This sample policy shows an example of using hello `send-one-way-request` policy toosend a message tooa Slack chat room if hello HTTP response code is greater than or equal too500.</span></span> <span data-ttu-id="585eb-413">Para obter mais informações sobre esse exemplo, consulte [usando serviços externos de saudação serviço de gerenciamento do Azure API](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="585eb-413">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="585eb-414">Elementos</span><span class="sxs-lookup"><span data-stu-id="585eb-414">Elements</span></span>  
  
|<span data-ttu-id="585eb-415">Elemento</span><span class="sxs-lookup"><span data-stu-id="585eb-415">Element</span></span>|<span data-ttu-id="585eb-416">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-416">Description</span></span>|<span data-ttu-id="585eb-417">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-417">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="585eb-418">send-one-way-request</span><span class="sxs-lookup"><span data-stu-id="585eb-418">send-one-way-request</span></span>|<span data-ttu-id="585eb-419">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="585eb-419">Root element.</span></span>|<span data-ttu-id="585eb-420">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-420">Yes</span></span>|  
|<span data-ttu-id="585eb-421">url</span><span class="sxs-lookup"><span data-stu-id="585eb-421">url</span></span>|<span data-ttu-id="585eb-422">Olá URL de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="585eb-422">hello URL of hello request.</span></span>|<span data-ttu-id="585eb-423">Não se mode=copy, caso contrário, sim.</span><span class="sxs-lookup"><span data-stu-id="585eb-423">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="585eb-424">estático</span><span class="sxs-lookup"><span data-stu-id="585eb-424">method</span></span>|<span data-ttu-id="585eb-425">o método HTTP para solicitação de saudação do Hello.</span><span class="sxs-lookup"><span data-stu-id="585eb-425">hello HTTP method for hello request.</span></span>|<span data-ttu-id="585eb-426">Não se mode=copy, caso contrário, sim.</span><span class="sxs-lookup"><span data-stu-id="585eb-426">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="585eb-427">cabeçalho</span><span class="sxs-lookup"><span data-stu-id="585eb-427">header</span></span>|<span data-ttu-id="585eb-428">Cabeçalho da solicitação.</span><span class="sxs-lookup"><span data-stu-id="585eb-428">Request header.</span></span> <span data-ttu-id="585eb-429">Use vários elementos de cabeçalho para vários cabeçalhos de solicitação.</span><span class="sxs-lookup"><span data-stu-id="585eb-429">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="585eb-430">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-430">No</span></span>|  
|<span data-ttu-id="585eb-431">body</span><span class="sxs-lookup"><span data-stu-id="585eb-431">body</span></span>|<span data-ttu-id="585eb-432">corpo da solicitação Hello.</span><span class="sxs-lookup"><span data-stu-id="585eb-432">hello request body.</span></span>|<span data-ttu-id="585eb-433">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-433">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="585eb-434">Atributos</span><span class="sxs-lookup"><span data-stu-id="585eb-434">Attributes</span></span>  
  
|<span data-ttu-id="585eb-435">Atributo</span><span class="sxs-lookup"><span data-stu-id="585eb-435">Attribute</span></span>|<span data-ttu-id="585eb-436">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-436">Description</span></span>|<span data-ttu-id="585eb-437">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-437">Required</span></span>|<span data-ttu-id="585eb-438">Padrão</span><span class="sxs-lookup"><span data-stu-id="585eb-438">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="585eb-439">mode="string"</span><span class="sxs-lookup"><span data-stu-id="585eb-439">mode="string"</span></span>|<span data-ttu-id="585eb-440">Determina se esta é uma nova solicitação ou uma cópia da solicitação atual hello.</span><span class="sxs-lookup"><span data-stu-id="585eb-440">Determines whether this is a new request or a copy of hello current request.</span></span> <span data-ttu-id="585eb-441">No modo de saída, modo = cópia não inicializar o corpo da solicitação hello.</span><span class="sxs-lookup"><span data-stu-id="585eb-441">In outbound mode, mode=copy does not initialize hello request body.</span></span>|<span data-ttu-id="585eb-442">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-442">No</span></span>|<span data-ttu-id="585eb-443">Novo</span><span class="sxs-lookup"><span data-stu-id="585eb-443">New</span></span>|  
|<span data-ttu-id="585eb-444">name</span><span class="sxs-lookup"><span data-stu-id="585eb-444">name</span></span>|<span data-ttu-id="585eb-445">Especifica o nome de saudação do hello cabeçalho toobe conjunto.</span><span class="sxs-lookup"><span data-stu-id="585eb-445">Specifies hello name of hello header toobe set.</span></span>|<span data-ttu-id="585eb-446">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-446">Yes</span></span>|<span data-ttu-id="585eb-447">N/D</span><span class="sxs-lookup"><span data-stu-id="585eb-447">N/A</span></span>|  
|<span data-ttu-id="585eb-448">exists-action</span><span class="sxs-lookup"><span data-stu-id="585eb-448">exists-action</span></span>|<span data-ttu-id="585eb-449">Especifica qual ação tootake quando Olá cabeçalho já está especificado.</span><span class="sxs-lookup"><span data-stu-id="585eb-449">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="585eb-450">Esse atributo deve ter uma saudação valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="585eb-450">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="585eb-451">-valor de substituição - substitui saudação do cabeçalho existente hello.</span><span class="sxs-lookup"><span data-stu-id="585eb-451">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="585eb-452">-Ignorar - não substitui o valor do cabeçalho existente hello.</span><span class="sxs-lookup"><span data-stu-id="585eb-452">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="585eb-453">-Acrescentar - acrescenta Olá valor toohello valor do cabeçalho existente.</span><span class="sxs-lookup"><span data-stu-id="585eb-453">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="585eb-454">-delete - remove o cabeçalho de saudação da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="585eb-454">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="585eb-455">Quando definido muito`override` alistando várias entradas com hello mesmo nome resultados no cabeçalho Olá sendo conjunto acordo tooall entradas (que serão listadas várias vezes); somente os valores listados serão definidos no resultado de saudação.</span><span class="sxs-lookup"><span data-stu-id="585eb-455">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="585eb-456">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-456">No</span></span>|<span data-ttu-id="585eb-457">override</span><span class="sxs-lookup"><span data-stu-id="585eb-457">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="585eb-458">Uso</span><span class="sxs-lookup"><span data-stu-id="585eb-458">Usage</span></span>  
 <span data-ttu-id="585eb-459">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="585eb-459">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="585eb-460">**Seções da política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="585eb-460">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="585eb-461">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="585eb-461">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="585eb-462"><a name="SendRequest"></a> Enviar solicitação</span><span class="sxs-lookup"><span data-stu-id="585eb-462"><a name="SendRequest"></a> Send request</span></span>  
 <span data-ttu-id="585eb-463">Olá `send-request` política envia a solicitação de saudação fornecida toohello especificou a URL, esperando não mais que Olá define valor de tempo limite.</span><span class="sxs-lookup"><span data-stu-id="585eb-463">hello `send-request` policy sends hello provided request toohello specified URL, waiting no longer than hello set timeout value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="585eb-464">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="585eb-464">Policy statement</span></span>  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="585eb-465">Exemplo</span><span class="sxs-lookup"><span data-stu-id="585eb-465">Example</span></span>  
 <span data-ttu-id="585eb-466">Este exemplo mostra uma maneira tooverify um token de referência com um servidor de autorização.</span><span class="sxs-lookup"><span data-stu-id="585eb-466">This example shows one way tooverify a reference token with an authorization server.</span></span> <span data-ttu-id="585eb-467">Para obter mais informações sobre esse exemplo, consulte [usando serviços externos de saudação serviço de gerenciamento do Azure API](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="585eb-467">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<inbound>  
  <!-- Extract Token from Authorization header parameter -->  
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />  
  
  <!-- Send request tooToken Server toovalidate token (see RFC 7662) -->  
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
  
### <a name="elements"></a><span data-ttu-id="585eb-468">Elementos</span><span class="sxs-lookup"><span data-stu-id="585eb-468">Elements</span></span>  
  
|<span data-ttu-id="585eb-469">Elemento</span><span class="sxs-lookup"><span data-stu-id="585eb-469">Element</span></span>|<span data-ttu-id="585eb-470">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-470">Description</span></span>|<span data-ttu-id="585eb-471">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-471">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="585eb-472">send-request</span><span class="sxs-lookup"><span data-stu-id="585eb-472">send-request</span></span>|<span data-ttu-id="585eb-473">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="585eb-473">Root element.</span></span>|<span data-ttu-id="585eb-474">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-474">Yes</span></span>|  
|<span data-ttu-id="585eb-475">url</span><span class="sxs-lookup"><span data-stu-id="585eb-475">url</span></span>|<span data-ttu-id="585eb-476">Olá URL de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="585eb-476">hello URL of hello request.</span></span>|<span data-ttu-id="585eb-477">Não se mode=copy, caso contrário, sim.</span><span class="sxs-lookup"><span data-stu-id="585eb-477">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="585eb-478">estático</span><span class="sxs-lookup"><span data-stu-id="585eb-478">method</span></span>|<span data-ttu-id="585eb-479">o método HTTP para solicitação de saudação do Hello.</span><span class="sxs-lookup"><span data-stu-id="585eb-479">hello HTTP method for hello request.</span></span>|<span data-ttu-id="585eb-480">Não se mode=copy, caso contrário, sim.</span><span class="sxs-lookup"><span data-stu-id="585eb-480">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="585eb-481">cabeçalho</span><span class="sxs-lookup"><span data-stu-id="585eb-481">header</span></span>|<span data-ttu-id="585eb-482">Cabeçalho da solicitação.</span><span class="sxs-lookup"><span data-stu-id="585eb-482">Request header.</span></span> <span data-ttu-id="585eb-483">Use vários elementos de cabeçalho para vários cabeçalhos de solicitação.</span><span class="sxs-lookup"><span data-stu-id="585eb-483">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="585eb-484">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-484">No</span></span>|  
|<span data-ttu-id="585eb-485">body</span><span class="sxs-lookup"><span data-stu-id="585eb-485">body</span></span>|<span data-ttu-id="585eb-486">corpo da solicitação Hello.</span><span class="sxs-lookup"><span data-stu-id="585eb-486">hello request body.</span></span>|<span data-ttu-id="585eb-487">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-487">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="585eb-488">Atributos</span><span class="sxs-lookup"><span data-stu-id="585eb-488">Attributes</span></span>  
  
|<span data-ttu-id="585eb-489">Atributo</span><span class="sxs-lookup"><span data-stu-id="585eb-489">Attribute</span></span>|<span data-ttu-id="585eb-490">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-490">Description</span></span>|<span data-ttu-id="585eb-491">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-491">Required</span></span>|<span data-ttu-id="585eb-492">Padrão</span><span class="sxs-lookup"><span data-stu-id="585eb-492">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="585eb-493">mode="string"</span><span class="sxs-lookup"><span data-stu-id="585eb-493">mode="string"</span></span>|<span data-ttu-id="585eb-494">Determina se esta é uma nova solicitação ou uma cópia da solicitação atual hello.</span><span class="sxs-lookup"><span data-stu-id="585eb-494">Determines whether this is a new request or a copy of hello current request.</span></span> <span data-ttu-id="585eb-495">No modo de saída, modo = cópia não inicializar o corpo da solicitação hello.</span><span class="sxs-lookup"><span data-stu-id="585eb-495">In outbound mode, mode=copy does not initialize hello request body.</span></span>|<span data-ttu-id="585eb-496">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-496">No</span></span>|<span data-ttu-id="585eb-497">Novo</span><span class="sxs-lookup"><span data-stu-id="585eb-497">New</span></span>|  
|<span data-ttu-id="585eb-498">response-variable-name="string"</span><span class="sxs-lookup"><span data-stu-id="585eb-498">response-variable-name="string"</span></span>|<span data-ttu-id="585eb-499">Se não estiver presente, `context.Response` será usado.</span><span class="sxs-lookup"><span data-stu-id="585eb-499">If not present, `context.Response` is used.</span></span>|<span data-ttu-id="585eb-500">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-500">No</span></span>|<span data-ttu-id="585eb-501">N/D</span><span class="sxs-lookup"><span data-stu-id="585eb-501">N/A</span></span>|  
|<span data-ttu-id="585eb-502">timeout="integer"</span><span class="sxs-lookup"><span data-stu-id="585eb-502">timeout="integer"</span></span>|<span data-ttu-id="585eb-503">intervalo de tempo limite de saudação em segundos, antes da chamada de saudação toohello URL falhará.</span><span class="sxs-lookup"><span data-stu-id="585eb-503">hello timeout interval in seconds before hello call toohello URL fails.</span></span>|<span data-ttu-id="585eb-504">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-504">No</span></span>|<span data-ttu-id="585eb-505">60</span><span class="sxs-lookup"><span data-stu-id="585eb-505">60</span></span>|  
|<span data-ttu-id="585eb-506">ignore-error</span><span class="sxs-lookup"><span data-stu-id="585eb-506">ignore-error</span></span>|<span data-ttu-id="585eb-507">Se true e hello resulta em um erro de solicitação:</span><span class="sxs-lookup"><span data-stu-id="585eb-507">If true and hello request results in an error:</span></span><br /><br /> <span data-ttu-id="585eb-508">– Se response-variable-name tiver sido especificado, ele conterá um valor nulo.</span><span class="sxs-lookup"><span data-stu-id="585eb-508">-   If response-variable-name was specified it will contain a null value.</span></span><br /><span data-ttu-id="585eb-509">– Se response-variable-name não tiver sido especificado, context.Request não será atualizado.</span><span class="sxs-lookup"><span data-stu-id="585eb-509">-   If response-variable-name was not specified, context.Request will not be updated.</span></span>|<span data-ttu-id="585eb-510">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-510">No</span></span>|<span data-ttu-id="585eb-511">false</span><span class="sxs-lookup"><span data-stu-id="585eb-511">false</span></span>|  
|<span data-ttu-id="585eb-512">name</span><span class="sxs-lookup"><span data-stu-id="585eb-512">name</span></span>|<span data-ttu-id="585eb-513">Especifica o nome de saudação do hello cabeçalho toobe conjunto.</span><span class="sxs-lookup"><span data-stu-id="585eb-513">Specifies hello name of hello header toobe set.</span></span>|<span data-ttu-id="585eb-514">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-514">Yes</span></span>|<span data-ttu-id="585eb-515">N/D</span><span class="sxs-lookup"><span data-stu-id="585eb-515">N/A</span></span>|  
|<span data-ttu-id="585eb-516">exists-action</span><span class="sxs-lookup"><span data-stu-id="585eb-516">exists-action</span></span>|<span data-ttu-id="585eb-517">Especifica qual ação tootake quando Olá cabeçalho já está especificado.</span><span class="sxs-lookup"><span data-stu-id="585eb-517">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="585eb-518">Esse atributo deve ter uma saudação valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="585eb-518">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="585eb-519">-valor de substituição - substitui saudação do cabeçalho existente hello.</span><span class="sxs-lookup"><span data-stu-id="585eb-519">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="585eb-520">-Ignorar - não substitui o valor do cabeçalho existente hello.</span><span class="sxs-lookup"><span data-stu-id="585eb-520">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="585eb-521">-Acrescentar - acrescenta Olá valor toohello valor do cabeçalho existente.</span><span class="sxs-lookup"><span data-stu-id="585eb-521">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="585eb-522">-delete - remove o cabeçalho de saudação da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="585eb-522">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="585eb-523">Quando definido muito`override` alistando várias entradas com hello mesmo nome resultados no cabeçalho Olá sendo conjunto acordo tooall entradas (que serão listadas várias vezes); somente os valores listados serão definidos no resultado de saudação.</span><span class="sxs-lookup"><span data-stu-id="585eb-523">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="585eb-524">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-524">No</span></span>|<span data-ttu-id="585eb-525">override</span><span class="sxs-lookup"><span data-stu-id="585eb-525">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="585eb-526">Uso</span><span class="sxs-lookup"><span data-stu-id="585eb-526">Usage</span></span>  
 <span data-ttu-id="585eb-527">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="585eb-527">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="585eb-528">**Seções da política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="585eb-528">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="585eb-529">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="585eb-529">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="585eb-530"><a name="SetHttpProxy"></a> Definir proxy HTTP</span><span class="sxs-lookup"><span data-stu-id="585eb-530"><a name="SetHttpProxy"></a> Set HTTP proxy</span></span>  
 <span data-ttu-id="585eb-531">Olá `proxy` política permite que você tooroute solicitações encaminhadas toobackends por meio de um proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="585eb-531">hello `proxy` policy allows you tooroute requests forwarded toobackends via an HTTP proxy.</span></span> <span data-ttu-id="585eb-532">HTTP (não HTTPS) tem suporte entre o gateway hello e proxy hello.</span><span class="sxs-lookup"><span data-stu-id="585eb-532">Only HTTP (not HTTPS) is supported between hello gateway and hello proxy.</span></span> <span data-ttu-id="585eb-533">Somente autenticação básica e NTLM.</span><span class="sxs-lookup"><span data-stu-id="585eb-533">Basic and NTLM authentication only.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="585eb-534">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="585eb-534">Policy statement</span></span>  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="585eb-535">Exemplo</span><span class="sxs-lookup"><span data-stu-id="585eb-535">Example</span></span>  
<span data-ttu-id="585eb-536">Observe o uso de saudação do [propriedades](api-management-howto-properties.md) como valores de saudação username e password tooavoid armazenar informações confidenciais no documento de política de saudação.</span><span class="sxs-lookup"><span data-stu-id="585eb-536">Note hello use of [properties](api-management-howto-properties.md) as values of hello username and password tooavoid storing sensitive information in hello policy document.</span></span>  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a><span data-ttu-id="585eb-537">Elementos</span><span class="sxs-lookup"><span data-stu-id="585eb-537">Elements</span></span>  
  
|<span data-ttu-id="585eb-538">Elemento</span><span class="sxs-lookup"><span data-stu-id="585eb-538">Element</span></span>|<span data-ttu-id="585eb-539">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-539">Description</span></span>|<span data-ttu-id="585eb-540">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-540">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="585eb-541">proxy</span><span class="sxs-lookup"><span data-stu-id="585eb-541">proxy</span></span>|<span data-ttu-id="585eb-542">Elemento raiz</span><span class="sxs-lookup"><span data-stu-id="585eb-542">Root element</span></span>|<span data-ttu-id="585eb-543">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-543">Yes</span></span>|  

### <a name="attributes"></a><span data-ttu-id="585eb-544">Atributos</span><span class="sxs-lookup"><span data-stu-id="585eb-544">Attributes</span></span>  
  
|<span data-ttu-id="585eb-545">Atributo</span><span class="sxs-lookup"><span data-stu-id="585eb-545">Attribute</span></span>|<span data-ttu-id="585eb-546">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-546">Description</span></span>|<span data-ttu-id="585eb-547">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-547">Required</span></span>|<span data-ttu-id="585eb-548">Padrão</span><span class="sxs-lookup"><span data-stu-id="585eb-548">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="585eb-549">url="string"</span><span class="sxs-lookup"><span data-stu-id="585eb-549">url="string"</span></span>|<span data-ttu-id="585eb-550">URL do proxy no formulário de saudação do http://host:port.</span><span class="sxs-lookup"><span data-stu-id="585eb-550">Proxy URL in hello form of http://host:port.</span></span>|<span data-ttu-id="585eb-551">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-551">Yes</span></span>|<span data-ttu-id="585eb-552">N/D </span><span class="sxs-lookup"><span data-stu-id="585eb-552">N/A</span></span>|  
|<span data-ttu-id="585eb-553">username="string"</span><span class="sxs-lookup"><span data-stu-id="585eb-553">username="string"</span></span>|<span data-ttu-id="585eb-554">Toobe nome de usuário usado para autenticação com o proxy de saudação.</span><span class="sxs-lookup"><span data-stu-id="585eb-554">Username toobe used for authentication with hello proxy.</span></span>|<span data-ttu-id="585eb-555">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-555">No</span></span>|<span data-ttu-id="585eb-556">N/D </span><span class="sxs-lookup"><span data-stu-id="585eb-556">N/A</span></span>|  
|<span data-ttu-id="585eb-557">password="string"</span><span class="sxs-lookup"><span data-stu-id="585eb-557">password="string"</span></span>|<span data-ttu-id="585eb-558">Toobe senha usado para autenticação com o proxy de saudação.</span><span class="sxs-lookup"><span data-stu-id="585eb-558">Password toobe used for authentication with hello proxy.</span></span>|<span data-ttu-id="585eb-559">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-559">No</span></span>|<span data-ttu-id="585eb-560">N/D </span><span class="sxs-lookup"><span data-stu-id="585eb-560">N/A</span></span>|  

### <a name="usage"></a><span data-ttu-id="585eb-561">Uso</span><span class="sxs-lookup"><span data-stu-id="585eb-561">Usage</span></span>  
 <span data-ttu-id="585eb-562">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="585eb-562">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="585eb-563">**Seções de política:** de entrada</span><span class="sxs-lookup"><span data-stu-id="585eb-563">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="585eb-564">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="585eb-564">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="585eb-565"><a name="SetRequestMethod"></a> Definir método de solicitação</span><span class="sxs-lookup"><span data-stu-id="585eb-565"><a name="SetRequestMethod"></a> Set request method</span></span>  
 <span data-ttu-id="585eb-566">Olá `set-method` política permite que você toochange método de solicitação Olá HTTP para uma solicitação.</span><span class="sxs-lookup"><span data-stu-id="585eb-566">hello `set-method` policy allows you toochange hello HTTP request method for a request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="585eb-567">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="585eb-567">Policy statement</span></span>  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a><span data-ttu-id="585eb-568">Exemplo</span><span class="sxs-lookup"><span data-stu-id="585eb-568">Example</span></span>  
 <span data-ttu-id="585eb-569">Essa política de exemplo que usa Olá `set-method` política mostra um exemplo de enviar uma mensagem tooa atraso sala de bate-papo se Olá código de resposta HTTP for maior que ou igual too500.</span><span class="sxs-lookup"><span data-stu-id="585eb-569">This sample policy that uses hello `set-method` policy shows an example of sending a message tooa Slack chat room if hello HTTP response code is greater than or equal too500.</span></span> <span data-ttu-id="585eb-570">Para obter mais informações sobre esse exemplo, consulte [usando serviços externos de saudação serviço de gerenciamento do Azure API](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="585eb-570">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="585eb-571">Elementos</span><span class="sxs-lookup"><span data-stu-id="585eb-571">Elements</span></span>  
  
|<span data-ttu-id="585eb-572">Elemento</span><span class="sxs-lookup"><span data-stu-id="585eb-572">Element</span></span>|<span data-ttu-id="585eb-573">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-573">Description</span></span>|<span data-ttu-id="585eb-574">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-574">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="585eb-575">set-method</span><span class="sxs-lookup"><span data-stu-id="585eb-575">set-method</span></span>|<span data-ttu-id="585eb-576">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="585eb-576">Root element.</span></span> <span data-ttu-id="585eb-577">valor de saudação do elemento de saudação especifica o método HTTP de saudação.</span><span class="sxs-lookup"><span data-stu-id="585eb-577">hello value of hello element specifies hello HTTP method.</span></span>|<span data-ttu-id="585eb-578">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-578">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="585eb-579">Uso</span><span class="sxs-lookup"><span data-stu-id="585eb-579">Usage</span></span>  
 <span data-ttu-id="585eb-580">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="585eb-580">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="585eb-581">**Seções de política:** entrada, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="585eb-581">**Policy sections:** inbound, on-error</span></span>  
  
-   <span data-ttu-id="585eb-582">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="585eb-582">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="585eb-583"><a name="SetStatus"></a> Definir código de status</span><span class="sxs-lookup"><span data-stu-id="585eb-583"><a name="SetStatus"></a> Set status code</span></span>  
 <span data-ttu-id="585eb-584">Olá `set-status` toohello de código de status do política conjuntos Olá HTTP especificou um valor.</span><span class="sxs-lookup"><span data-stu-id="585eb-584">hello `set-status` policy sets hello HTTP status code toohello specified value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="585eb-585">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="585eb-585">Policy statement</span></span>  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a><span data-ttu-id="585eb-586">Exemplo</span><span class="sxs-lookup"><span data-stu-id="585eb-586">Example</span></span>  
 <span data-ttu-id="585eb-587">Este exemplo mostra como tooreturn uma resposta 401, se o token de autorização de saudação é inválido.</span><span class="sxs-lookup"><span data-stu-id="585eb-587">This example shows how tooreturn a 401 response if hello authorization token is invalid.</span></span> <span data-ttu-id="585eb-588">Para obter mais informações, consulte [usando serviços externos de saudação serviço de gerenciamento de API do Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span><span class="sxs-lookup"><span data-stu-id="585eb-588">For more information, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="585eb-589">Elementos</span><span class="sxs-lookup"><span data-stu-id="585eb-589">Elements</span></span>  
  
|<span data-ttu-id="585eb-590">Elemento</span><span class="sxs-lookup"><span data-stu-id="585eb-590">Element</span></span>|<span data-ttu-id="585eb-591">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-591">Description</span></span>|<span data-ttu-id="585eb-592">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-592">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="585eb-593">set-status</span><span class="sxs-lookup"><span data-stu-id="585eb-593">set-status</span></span>|<span data-ttu-id="585eb-594">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="585eb-594">Root element.</span></span>|<span data-ttu-id="585eb-595">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-595">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="585eb-596">Atributos</span><span class="sxs-lookup"><span data-stu-id="585eb-596">Attributes</span></span>  
  
|<span data-ttu-id="585eb-597">Atributo</span><span class="sxs-lookup"><span data-stu-id="585eb-597">Attribute</span></span>|<span data-ttu-id="585eb-598">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-598">Description</span></span>|<span data-ttu-id="585eb-599">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-599">Required</span></span>|<span data-ttu-id="585eb-600">Padrão</span><span class="sxs-lookup"><span data-stu-id="585eb-600">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="585eb-601">code="integer"</span><span class="sxs-lookup"><span data-stu-id="585eb-601">code="integer"</span></span>|<span data-ttu-id="585eb-602">Olá HTTP tooreturn de código de status.</span><span class="sxs-lookup"><span data-stu-id="585eb-602">hello HTTP status code tooreturn.</span></span>|<span data-ttu-id="585eb-603">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-603">Yes</span></span>|<span data-ttu-id="585eb-604">N/D</span><span class="sxs-lookup"><span data-stu-id="585eb-604">N/A</span></span>|  
|<span data-ttu-id="585eb-605">reason="string"</span><span class="sxs-lookup"><span data-stu-id="585eb-605">reason="string"</span></span>|<span data-ttu-id="585eb-606">Uma descrição do motivo Olá para retornar o código de status de saudação.</span><span class="sxs-lookup"><span data-stu-id="585eb-606">A description of hello reason for returning hello status code.</span></span>|<span data-ttu-id="585eb-607">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-607">Yes</span></span>|<span data-ttu-id="585eb-608">N/D</span><span class="sxs-lookup"><span data-stu-id="585eb-608">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="585eb-609">Uso</span><span class="sxs-lookup"><span data-stu-id="585eb-609">Usage</span></span>  
 <span data-ttu-id="585eb-610">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="585eb-610">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="585eb-611">**Seções de política:** saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="585eb-611">**Policy sections:** outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="585eb-612">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="585eb-612">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="585eb-613"><a name="set-variable"></a> Definir variável</span><span class="sxs-lookup"><span data-stu-id="585eb-613"><a name="set-variable"></a> Set variable</span></span>  
 <span data-ttu-id="585eb-614">Olá `set-variable` política declara um [contexto](api-management-policy-expressions.md#ContextVariables) variável e atribui um valor especificado por meio de um [expressão](api-management-policy-expressions.md) ou um literal de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="585eb-614">hello `set-variable` policy declares a [context](api-management-policy-expressions.md#ContextVariables) variable and assigns it a value specified via an [expression](api-management-policy-expressions.md) or a string literal.</span></span> <span data-ttu-id="585eb-615">Se a expressão de saudação contém um literal, ele será convertido tooa tipo de cadeia de caracteres e hello do valor de saudação será `System.String`.</span><span class="sxs-lookup"><span data-stu-id="585eb-615">if hello expression contains a literal it will be converted tooa string and hello type of hello value will be `System.String`.</span></span>  
  
###  <span data-ttu-id="585eb-616"><a name="set-variablePolicyStatement"></a> Declaração de política</span><span class="sxs-lookup"><span data-stu-id="585eb-616"><a name="set-variablePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <span data-ttu-id="585eb-617"><a name="set-variableExample"></a> Exemplo</span><span class="sxs-lookup"><span data-stu-id="585eb-617"><a name="set-variableExample"></a> Example</span></span>  
 <span data-ttu-id="585eb-618">Olá, exemplo a seguir demonstra uma política de variável definida no hello seção de entrada.</span><span class="sxs-lookup"><span data-stu-id="585eb-618">hello following example demonstrates a set variable policy in hello inbound section.</span></span> <span data-ttu-id="585eb-619">Essa política de variável de conjunto cria uma `isMobile` booliano [contexto](api-management-policy-expressions.md#ContextVariables) variável definida tootrue se hello `User-Agent` solicitação cabeçalho contém o texto de saudação `iPad` ou `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="585eb-619">This set variable policy creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set tootrue if hello `User-Agent` request header contains hello text `iPad` or `iPhone`.</span></span>  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a><span data-ttu-id="585eb-620">Elementos</span><span class="sxs-lookup"><span data-stu-id="585eb-620">Elements</span></span>  
  
|<span data-ttu-id="585eb-621">Elemento</span><span class="sxs-lookup"><span data-stu-id="585eb-621">Element</span></span>|<span data-ttu-id="585eb-622">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-622">Description</span></span>|<span data-ttu-id="585eb-623">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-623">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="585eb-624">set-variable</span><span class="sxs-lookup"><span data-stu-id="585eb-624">set-variable</span></span>|<span data-ttu-id="585eb-625">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="585eb-625">Root element.</span></span>|<span data-ttu-id="585eb-626">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-626">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="585eb-627">Atributos</span><span class="sxs-lookup"><span data-stu-id="585eb-627">Attributes</span></span>  
  
|<span data-ttu-id="585eb-628">Atributo</span><span class="sxs-lookup"><span data-stu-id="585eb-628">Attribute</span></span>|<span data-ttu-id="585eb-629">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-629">Description</span></span>|<span data-ttu-id="585eb-630">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-630">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="585eb-631">name</span><span class="sxs-lookup"><span data-stu-id="585eb-631">name</span></span>|<span data-ttu-id="585eb-632">nome de saudação da variável de saudação.</span><span class="sxs-lookup"><span data-stu-id="585eb-632">hello name of hello variable.</span></span>|<span data-ttu-id="585eb-633">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-633">Yes</span></span>|  
|<span data-ttu-id="585eb-634">valor</span><span class="sxs-lookup"><span data-stu-id="585eb-634">value</span></span>|<span data-ttu-id="585eb-635">valor de saudação da variável de saudação.</span><span class="sxs-lookup"><span data-stu-id="585eb-635">hello value of hello variable.</span></span> <span data-ttu-id="585eb-636">Isso pode ser uma expressão ou um valor literal.</span><span class="sxs-lookup"><span data-stu-id="585eb-636">This can be an expression or a literal value.</span></span>|<span data-ttu-id="585eb-637">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-637">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="585eb-638">Uso</span><span class="sxs-lookup"><span data-stu-id="585eb-638">Usage</span></span>  
 <span data-ttu-id="585eb-639">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="585eb-639">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="585eb-640">**Seções da política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="585eb-640">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="585eb-641">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="585eb-641">**Policy scopes:** all scopes</span></span>  
  
###  <span data-ttu-id="585eb-642"><a name="set-variableAllowedTypes"></a> Tipos permitidos</span><span class="sxs-lookup"><span data-stu-id="585eb-642"><a name="set-variableAllowedTypes"></a> Allowed types</span></span>  
 <span data-ttu-id="585eb-643">As expressões usadas em Olá `set-variable` política deve retornar um dos seguintes tipos básicos de saudação.</span><span class="sxs-lookup"><span data-stu-id="585eb-643">Expressions used in hello `set-variable` policy must return one of hello following basic types.</span></span>  
  
-   <span data-ttu-id="585eb-644">System.Boolean</span><span class="sxs-lookup"><span data-stu-id="585eb-644">System.Boolean</span></span>  
  
-   <span data-ttu-id="585eb-645">System.SByte</span><span class="sxs-lookup"><span data-stu-id="585eb-645">System.SByte</span></span>  
  
-   <span data-ttu-id="585eb-646">System.Byte</span><span class="sxs-lookup"><span data-stu-id="585eb-646">System.Byte</span></span>  
  
-   <span data-ttu-id="585eb-647">System.UInt16</span><span class="sxs-lookup"><span data-stu-id="585eb-647">System.UInt16</span></span>  
  
-   <span data-ttu-id="585eb-648">System.UInt32</span><span class="sxs-lookup"><span data-stu-id="585eb-648">System.UInt32</span></span>  
  
-   <span data-ttu-id="585eb-649">System.UInt64</span><span class="sxs-lookup"><span data-stu-id="585eb-649">System.UInt64</span></span>  
  
-   <span data-ttu-id="585eb-650">System.Int16</span><span class="sxs-lookup"><span data-stu-id="585eb-650">System.Int16</span></span>  
  
-   <span data-ttu-id="585eb-651">System.Int32</span><span class="sxs-lookup"><span data-stu-id="585eb-651">System.Int32</span></span>  
  
-   <span data-ttu-id="585eb-652">System.Int64</span><span class="sxs-lookup"><span data-stu-id="585eb-652">System.Int64</span></span>  
  
-   <span data-ttu-id="585eb-653">System.Decimal</span><span class="sxs-lookup"><span data-stu-id="585eb-653">System.Decimal</span></span>  
  
-   <span data-ttu-id="585eb-654">System.Single</span><span class="sxs-lookup"><span data-stu-id="585eb-654">System.Single</span></span>  
  
-   <span data-ttu-id="585eb-655">System.Double</span><span class="sxs-lookup"><span data-stu-id="585eb-655">System.Double</span></span>  
  
-   <span data-ttu-id="585eb-656">System.Guid</span><span class="sxs-lookup"><span data-stu-id="585eb-656">System.Guid</span></span>  
  
-   <span data-ttu-id="585eb-657">System.String</span><span class="sxs-lookup"><span data-stu-id="585eb-657">System.String</span></span>  
  
-   <span data-ttu-id="585eb-658">System.Char</span><span class="sxs-lookup"><span data-stu-id="585eb-658">System.Char</span></span>  
  
-   <span data-ttu-id="585eb-659">System.DateTime</span><span class="sxs-lookup"><span data-stu-id="585eb-659">System.DateTime</span></span>  
  
-   <span data-ttu-id="585eb-660">System.TimeSpan</span><span class="sxs-lookup"><span data-stu-id="585eb-660">System.TimeSpan</span></span>  
  
-   <span data-ttu-id="585eb-661">System.Byte?</span><span class="sxs-lookup"><span data-stu-id="585eb-661">System.Byte?</span></span>  
  
-   <span data-ttu-id="585eb-662">System.UInt16?</span><span class="sxs-lookup"><span data-stu-id="585eb-662">System.UInt16?</span></span>  
  
-   <span data-ttu-id="585eb-663">System.UInt32?</span><span class="sxs-lookup"><span data-stu-id="585eb-663">System.UInt32?</span></span>  
  
-   <span data-ttu-id="585eb-664">System.UInt64?</span><span class="sxs-lookup"><span data-stu-id="585eb-664">System.UInt64?</span></span>  
  
-   <span data-ttu-id="585eb-665">System.Int16?</span><span class="sxs-lookup"><span data-stu-id="585eb-665">System.Int16?</span></span>  
  
-   <span data-ttu-id="585eb-666">System.Int32?</span><span class="sxs-lookup"><span data-stu-id="585eb-666">System.Int32?</span></span>  
  
-   <span data-ttu-id="585eb-667">System.Int64?</span><span class="sxs-lookup"><span data-stu-id="585eb-667">System.Int64?</span></span>  
  
-   <span data-ttu-id="585eb-668">System.Decimal?</span><span class="sxs-lookup"><span data-stu-id="585eb-668">System.Decimal?</span></span>  
  
-   <span data-ttu-id="585eb-669">System.Single?</span><span class="sxs-lookup"><span data-stu-id="585eb-669">System.Single?</span></span>  
  
-   <span data-ttu-id="585eb-670">System.Double?</span><span class="sxs-lookup"><span data-stu-id="585eb-670">System.Double?</span></span>  
  
-   <span data-ttu-id="585eb-671">System.Guid?</span><span class="sxs-lookup"><span data-stu-id="585eb-671">System.Guid?</span></span>  
  
-   <span data-ttu-id="585eb-672">System.String?</span><span class="sxs-lookup"><span data-stu-id="585eb-672">System.String?</span></span>  
  
-   <span data-ttu-id="585eb-673">System.Char?</span><span class="sxs-lookup"><span data-stu-id="585eb-673">System.Char?</span></span>  
  
-   <span data-ttu-id="585eb-674">System.DateTime?</span><span class="sxs-lookup"><span data-stu-id="585eb-674">System.DateTime?</span></span>  

##  <span data-ttu-id="585eb-675"><a name="Trace"></a> Rastreamento</span><span class="sxs-lookup"><span data-stu-id="585eb-675"><a name="Trace"></a> Trace</span></span>  
 <span data-ttu-id="585eb-676">Olá `trace` política adiciona uma cadeia de caracteres hello [API Inspetor](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) saída.</span><span class="sxs-lookup"><span data-stu-id="585eb-676">hello             `trace` policy adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span> <span data-ttu-id="585eb-677">Olá política será executada somente quando o rastreamento é disparado, ou seja, `Ocp-Apim-Trace` cabeçalho de solicitação está presente e defina o muito`true` e `Ocp-Apim-Subscription-Key` cabeçalho de solicitação está presente e contém uma chave válida associada à conta de administrador de saudação.</span><span class="sxs-lookup"><span data-stu-id="585eb-677">hello policy will execute only when tracing is triggered, i.e. `Ocp-Apim-Trace` request header is present and set too`true` and `Ocp-Apim-Subscription-Key` request header is present and holds a valid key associated with hello admin account.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="585eb-678">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="585eb-678">Policy statement</span></span>  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="585eb-679">Elementos</span><span class="sxs-lookup"><span data-stu-id="585eb-679">Elements</span></span>  
  
|<span data-ttu-id="585eb-680">Elemento</span><span class="sxs-lookup"><span data-stu-id="585eb-680">Element</span></span>|<span data-ttu-id="585eb-681">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-681">Description</span></span>|<span data-ttu-id="585eb-682">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-682">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="585eb-683">trace</span><span class="sxs-lookup"><span data-stu-id="585eb-683">trace</span></span>|<span data-ttu-id="585eb-684">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="585eb-684">Root element.</span></span>|<span data-ttu-id="585eb-685">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-685">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="585eb-686">Atributos</span><span class="sxs-lookup"><span data-stu-id="585eb-686">Attributes</span></span>  
  
|<span data-ttu-id="585eb-687">Atributo</span><span class="sxs-lookup"><span data-stu-id="585eb-687">Attribute</span></span>|<span data-ttu-id="585eb-688">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-688">Description</span></span>|<span data-ttu-id="585eb-689">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-689">Required</span></span>|<span data-ttu-id="585eb-690">Padrão</span><span class="sxs-lookup"><span data-stu-id="585eb-690">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="585eb-691">fonte</span><span class="sxs-lookup"><span data-stu-id="585eb-691">source</span></span>|<span data-ttu-id="585eb-692">Visualizador de rastreamento de toohello significativos literal de cadeia de caracteres e especificando fonte Olá de mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="585eb-692">String literal meaningful toohello trace viewer and specifying hello source of hello message.</span></span>|<span data-ttu-id="585eb-693">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-693">Yes</span></span>|<span data-ttu-id="585eb-694">N/D</span><span class="sxs-lookup"><span data-stu-id="585eb-694">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="585eb-695">Uso</span><span class="sxs-lookup"><span data-stu-id="585eb-695">Usage</span></span>  
 <span data-ttu-id="585eb-696">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="585eb-696">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="585eb-697">**Seções da política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="585eb-697">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="585eb-698">**Escopos da política:** todos os escopos</span><span class="sxs-lookup"><span data-stu-id="585eb-698">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="585eb-699"><a name="Wait"></a> Aguardar</span><span class="sxs-lookup"><span data-stu-id="585eb-699"><a name="Wait"></a> Wait</span></span>  
 <span data-ttu-id="585eb-700">Olá `wait` política executa as políticas de filho imediato em paralelo e aguarda para todos ou um dos seu toocomplete de políticas filho imediato antes de ser concluída.</span><span class="sxs-lookup"><span data-stu-id="585eb-700">hello `wait` policy executes its immediate child policies in parallel, and waits for either all or one of its immediate child policies toocomplete before it completes.</span></span> <span data-ttu-id="585eb-701">Olá espera política pode ter como as políticas de filho imediato [solicitação de envio](api-management-advanced-policies.md#SendRequest), [obter o valor de cache](api-management-caching-policies.md#GetFromCacheByKey), e [fluxo de controle](api-management-advanced-policies.md#choose) políticas.</span><span class="sxs-lookup"><span data-stu-id="585eb-701">hello wait policy can have as its immediate child policies [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), and [Control flow](api-management-advanced-policies.md#choose) policies.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="585eb-702">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="585eb-702">Policy statement</span></span>  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a><span data-ttu-id="585eb-703">Exemplo</span><span class="sxs-lookup"><span data-stu-id="585eb-703">Example</span></span>  
 <span data-ttu-id="585eb-704">Saudação de exemplo a seguir há dois `choose` políticas, como políticas de filho imediato de saudação `wait` política.</span><span class="sxs-lookup"><span data-stu-id="585eb-704">In hello following example there are two `choose` policies as immediate child policies of hello `wait` policy.</span></span> <span data-ttu-id="585eb-705">Cada uma dessas políticas `choose` executadas em paralelo.</span><span class="sxs-lookup"><span data-stu-id="585eb-705">Each of these `choose` policies executes in parallel.</span></span> <span data-ttu-id="585eb-706">Cada `choose` política tentativas tooretrieve um valor armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="585eb-706">Each `choose` policy attempts tooretrieve a cached value.</span></span> <span data-ttu-id="585eb-707">Se houver um erro de cache, um serviço de back-end é chamado de valor de saudação tooprovide.</span><span class="sxs-lookup"><span data-stu-id="585eb-707">If there is a cache miss, a backend service is called tooprovide hello value.</span></span> <span data-ttu-id="585eb-708">Em Olá Este exemplo `wait` política não for concluída até que todas as suas diretivas de filho imediato de concluir, porque Olá `for` atributo está definido muito`all`.</span><span class="sxs-lookup"><span data-stu-id="585eb-708">In this example hello `wait` policy does not complete until all of its immediate child policies complete, because hello `for` attribute is set too`all`.</span></span>   <span data-ttu-id="585eb-709">Em variáveis de contexto de saudação Este exemplo (`execute-branch-one`, `value-one`, `execute-branch-two`, e `value-two`) são declaradas fora do escopo de saudação dessa política de exemplo.</span><span class="sxs-lookup"><span data-stu-id="585eb-709">In this example hello context variables (`execute-branch-one`, `value-one`, `execute-branch-two`, and `value-two`) are declared outside of hello scope of this example policy.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="585eb-710">Elementos</span><span class="sxs-lookup"><span data-stu-id="585eb-710">Elements</span></span>  
  
|<span data-ttu-id="585eb-711">Elemento</span><span class="sxs-lookup"><span data-stu-id="585eb-711">Element</span></span>|<span data-ttu-id="585eb-712">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-712">Description</span></span>|<span data-ttu-id="585eb-713">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-713">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="585eb-714">wait</span><span class="sxs-lookup"><span data-stu-id="585eb-714">wait</span></span>|<span data-ttu-id="585eb-715">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="585eb-715">Root element.</span></span> <span data-ttu-id="585eb-716">Pode conter como elementos filho somente as políticas `send-request`, `cache-lookup-value` e `choose`.</span><span class="sxs-lookup"><span data-stu-id="585eb-716">May contain as child elements only `send-request`, `cache-lookup-value`, and `choose` policies.</span></span>|<span data-ttu-id="585eb-717">Sim</span><span class="sxs-lookup"><span data-stu-id="585eb-717">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="585eb-718">Atributos</span><span class="sxs-lookup"><span data-stu-id="585eb-718">Attributes</span></span>  
  
|<span data-ttu-id="585eb-719">Atributo</span><span class="sxs-lookup"><span data-stu-id="585eb-719">Attribute</span></span>|<span data-ttu-id="585eb-720">Descrição</span><span class="sxs-lookup"><span data-stu-id="585eb-720">Description</span></span>|<span data-ttu-id="585eb-721">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="585eb-721">Required</span></span>|<span data-ttu-id="585eb-722">Padrão</span><span class="sxs-lookup"><span data-stu-id="585eb-722">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="585eb-723">for</span><span class="sxs-lookup"><span data-stu-id="585eb-723">for</span></span>|<span data-ttu-id="585eb-724">Determina se hello `wait` política aguarda até que todos os toobe de políticas de filho imediato concluída ou apenas um.</span><span class="sxs-lookup"><span data-stu-id="585eb-724">Determines whether hello `wait` policy waits for all immediate child policies toobe completed or just one.</span></span> <span data-ttu-id="585eb-725">Valores permitidos são:</span><span class="sxs-lookup"><span data-stu-id="585eb-725">Allowed values are:</span></span><br /><br /> <span data-ttu-id="585eb-726">-   `all`-Aguarde até que todos os toocomplete de políticas de filho imediato</span><span class="sxs-lookup"><span data-stu-id="585eb-726">-   `all` - wait for all immediate child policies toocomplete</span></span><br /><span data-ttu-id="585eb-727">-qualquer - Aguarde toocomplete de política qualquer filho imediato.</span><span class="sxs-lookup"><span data-stu-id="585eb-727">-   any - wait for any immediate child policy toocomplete.</span></span> <span data-ttu-id="585eb-728">Após a conclusão da primeira política de filho imediato saudação, Olá `wait` política é concluída e execução de quaisquer outras políticas filho imediato é encerrada.</span><span class="sxs-lookup"><span data-stu-id="585eb-728">Once hello first immediate child policy has completed, hello `wait` policy completes and execution of any other immediate child policies is terminated.</span></span>|<span data-ttu-id="585eb-729">Não</span><span class="sxs-lookup"><span data-stu-id="585eb-729">No</span></span>|<span data-ttu-id="585eb-730">tudo</span><span class="sxs-lookup"><span data-stu-id="585eb-730">all</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="585eb-731">Uso</span><span class="sxs-lookup"><span data-stu-id="585eb-731">Usage</span></span>  
 <span data-ttu-id="585eb-732">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="585eb-732">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="585eb-733">**Seções de política:** entrada, saída, back-end</span><span class="sxs-lookup"><span data-stu-id="585eb-733">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="585eb-734">**Escopos da política:**todos os escopos</span><span class="sxs-lookup"><span data-stu-id="585eb-734">**Policy scopes:**all scopes</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="585eb-735">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="585eb-735">Next steps</span></span>
<span data-ttu-id="585eb-736">Para obter mais informações sobre como trabalhar com políticas, consulte:</span><span class="sxs-lookup"><span data-stu-id="585eb-736">For more information working with policies, see:</span></span>
-   [<span data-ttu-id="585eb-737">Políticas no Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="585eb-737">Policies in API Management</span></span>](api-management-howto-policies.md) 
-   [<span data-ttu-id="585eb-738">Expressões de política</span><span class="sxs-lookup"><span data-stu-id="585eb-738">Policy expressions</span></span>](api-management-policy-expressions.md)
