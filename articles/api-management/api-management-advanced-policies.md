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
# <a name="api-management-advanced-policies"></a>Políticas avançadas de Gerenciamento de API
Este tópico fornece uma referência para Olá políticas de gerenciamento de API a seguir. Para obter mais informações sobre como adicionar e configurar políticas, consulte [Políticas de Gerenciamento de API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="AdvancedPolicies"></a> Políticas avançadas  
  
-   [Fluxo de controle](api-management-advanced-policies.md#choose) - condicionalmente aplica instruções de política com base nos resultados de saudação da avaliação de saudação de booliano [expressões](api-management-policy-expressions.md).  
  
-   [Enviar solicitação](#ForwardRequest) -encaminha o serviço de back-end do hello solicitação toohello.

-   [Limite a simultaneidade](#LimitConcurrency) -impede entre as políticas de execução por mais de Olá quantidade especificada de solicitações por vez.
  
-   [Log tooEvent Hub](#log-to-eventhub) -envia mensagens de saudação especificado tooan formato Hub de eventos definido por uma entidade de agente de log. 

-   [Resposta de simulação](#mock-response) -anulações de pipeline de execução e retorna uma resposta fictícias diretamente toohello chamador.
  
-   [Repita](#Retry) -tentativas de execução de saudação colocados declarações de política, se e até Olá condição for atendida. A execução será repetida em Olá intervalos de tempo especificado e o toohello especificado contagem de repetição.  
  
-   [Retornar a resposta](#ReturnResponse) -Olá de execução e retorna de anulações de pipeline da resposta especificada diretamente toohello chamador. 
  
-   [Enviar solicitação de uma maneira](#SendOneWayRequest) -envia uma solicitação toohello especificado URL sem aguardar uma resposta.  
  
-   [Enviar solicitação](#SendRequest) -envia uma solicitação toohello especificou a URL.  

-   [Definir o proxy HTTP](#SetHttpProxy) -permite solicitações de tooroute encaminhado por meio de um proxy HTTP.  

-   [Definir o método de solicitação](#SetRequestMethod) -permite que você toochange método de saudação HTTP para uma solicitação.  
  
-   [Definir o código de status](#SetStatus) -valor especificado de toohello de código de status HTTP de saudação alterações.  
  
-   [Definir variável](api-management-advanced-policies.md#set-variable) – persiste um valor em uma variável de [contexto](api-management-policy-expressions.md#ContextVariables) nomeada para acesso posterior.  

-   [Rastreamento](#Trace) -adiciona uma cadeia de caracteres de saudação [API Inspetor](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) saída.  
  
-   [Aguarde](#Wait) -aguarda para colocados [solicitação de envio](api-management-advanced-policies.md#SendRequest), [obter o valor de cache](api-management-caching-policies.md#GetFromCacheByKey), ou [fluxo de controle](api-management-advanced-policies.md#choose) toocomplete políticas antes de continuar.  
  
##  <a name="choose"></a> Controlar fluxo  
 Olá `choose` política se aplica a política anexada construir instruções com base no resultado de saudação da avaliação de expressões Boolianas, semelhante tooan if-then-else ou uma opção em uma linguagem de programação.  
  
###  <a name="ChoosePolicyStatement"></a> Declaração de política  
  
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
  
 Olá política de controle de fluxo deve conter pelo menos um `<when/>` elemento. Olá `<otherwise/>` elemento é opcional. Condições no `<when/>` elementos são avaliados na ordem de sua aparência na política de saudação. Declarações de política em Olá primeiro `<when/>` elemento com atributo de condição é igual a `true` será aplicada. Políticas entre Olá `<otherwise/>` elemento, se houver, será aplicado se todos os de saudação `<when/>` são atributos do elemento condição `false`.  
  
### <a name="examples"></a>Exemplos  
  
####  <a name="ChooseExample"></a> Exemplo  
 Olá exemplo a seguir demonstra um [variável definida](api-management-advanced-policies.md#set-variable) duas políticas de fluxo de controle e de política.  
  
 Olá definir variável política está em Olá seção de entrada e cria um `isMobile` booliano [contexto](api-management-policy-expressions.md#ContextVariables) variável definida tootrue se hello `User-Agent` solicitação cabeçalho contém o texto de saudação `iPad` ou `iPhone`.  
  
 Olá primeira política de fluxo de controle também está em Olá seção de entrada e aplica condicionalmente uma de duas [definir parâmetro de cadeia de caracteres de consulta](api-management-transformation-policies.md#SetQueryStringParameter) políticas dependendo do valor Olá Olá `isMobile` variável de contexto.  
  
 política de fluxo de controle de segundo Hello está na seção de saída de hello e aplica condicionalmente Olá [converter XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) política quando `isMobile` está definido muito`true`.  
  
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
  
#### <a name="example"></a>Exemplo  
 Este exemplo mostra como tooperform a filtragem de conteúdo removendo elementos de dados de resposta de saudação foi recebida do serviço de back-end Olá Olá `Starter` produto. Para ver uma demonstração de como configurar e usar essa política, consulte [nuvem abrangem episódio 177: mais recursos de gerenciamento de API com Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e Avançar too34:30. Iniciar em 31:50 toosee uma visão geral de [Olá escuro API de previsão Sky](https://developer.forecast.io/) usado para esta demonstração.  
  
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
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descrição|Obrigatório|  
|-------------|-----------------|--------------|  
|choose|Elemento raiz.|Sim|  
|when|Olá toouse condição para Olá `if` ou `ifelse` partes da saudação `choose` política. Se hello `choose` política tem vários `when` seções, elas serão avaliadas sequencialmente. Uma vez Olá `condition` de um quando o elemento avalia muito`true`, nenhuma outra `when` condições são avaliadas.|Sim|  
|otherwise|Contém Olá política trecho toobe usado se nenhum Olá `when` condições muito avaliar`true`.|Não|  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|Obrigatório|  
|---------------|-----------------|--------------|  
|condition="Boolean expression &#124; Boolean constant"|expressão booleana Hello ou constante tooevaluated quando Olá contendo `when` declaração da política é avaliada.|Sim|  
  
###  <a name="ChooseUsage"></a> Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções da política:** entrada, saída, back-end, em caso de erro  
  
-   **Escopos da política:** todos os escopos  
  
##  <a name="ForwardRequest"></a> Encaminhar solicitação  
 Olá `forward-request` política encaminha Olá entrada solicitação toohello serviço back-end especificado na solicitação de saudação [contexto](api-management-policy-expressions.md#ContextVariables). Olá URL de serviço de back-end é especificado em Olá API [configurações](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) e pode ser alterado usando Olá [Configurar serviço de back-end](api-management-transformation-policies.md) política.  
  
> [!NOTE]
>  Remover esta política resulta em solicitação Olá não está sendo encaminhada políticas de serviço e hello de back-end de toohello na seção de saída Olá é avaliadas imediatamente após a conclusão bem-sucedida de saudação de políticas do Olá Olá seção de entrada.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a>Exemplos  
  
#### <a name="example"></a>Exemplo  
 Olá seguinte política de nível de API encaminha todas as solicitações de serviço de back-end toohello com um intervalo de tempo limite de 60 segundos.  
  
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
  
#### <a name="example"></a>Exemplo  
 Esta política de nível de operação usa Olá `base` política de back-end do elemento tooinherit saudação do escopo de nível de API do pai de saudação.  
  
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
  
#### <a name="example"></a>Exemplo  
 Essa política de nível de operação explicitamente encaminha todas as solicitações toohello back-end de serviço com um tempo limite de 120 e não herda pai Olá política de nível de back-end de API.  
  
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
  
#### <a name="example"></a>Exemplo  
 Essa política de nível de operação não encaminhar solicitações de serviço de back-end toohello.  
  
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
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descrição|Obrigatório|  
|-------------|-----------------|--------------|  
|forward-request|Elemento raiz.|Sim|  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|Obrigatório|Padrão|  
|---------------|-----------------|--------------|-------------|  
|timeout="integer"|intervalo de tempo limite de saudação em segundos antes que o serviço de back-end do hello chamada toohello falha.|Não|Sem tempo limite|  
|follow-redirects="true &#124; false"|Especifica se os redirecionamentos de serviço de back-end de saudação são seguidos pelo gateway de saudação ou retornados toohello chamador.|Não|false|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** back-end  
  
-   **Escopos da política:** todos os escopos  
  
##  <a name="LimitConcurrency"></a> Simultaneidade de limite  
 Olá `limit-concurrency` política impede entre as políticas de execução por mais de Olá quantidade especificada de solicitações em um determinado momento. Ao exceder o limite de hello, novas solicitações são adicionadas tooa fila, até que o comprimento máximo da fila de saudação é obtido. Quando a fila atinge seu máximo, novas solicitações falham imediatamente.
  
###  <a name="LimitConcurrencyStatement"></a> Declaração de política  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a>Exemplos  
  
####  <a name="ChooseExample"></a> Exemplo  
 Olá exemplo a seguir demonstra como o número de solicitações toolimit encaminhado tooa back-end com base no valor de saudação de uma variável de contexto.
 
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

### <a name="elements"></a>Elementos  
  
|Elemento|Descrição|Obrigatório|  
|-------------|-----------------|--------------|    
|limit-concurrency|Elemento raiz.|Sim|  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|Obrigatório|Padrão|  
|---------------|-----------------|--------------|--------------|  
|chave|Uma cadeia de caracteres. Expressão permitida. Especifica o escopo de simultaneidade hello. Pode ser compartilhado por várias políticas.|Sim|N/D|  
|max-count|Um inteiro. Especifica um número máximo de solicitações permitido tooenter política de saudação.|Sim|N/D|  
|Tempo limite|Um inteiro. Expressão permitida. Especifica o número de saudação de segundos que uma solicitação deve esperar tooenter antes de falhar com um escopo de "403 muito muitas solicitações"|Não|Infinito|  
|max-queue-length|Um inteiro. Expressão permitida. Especifica o comprimento máximo da fila de saudação. Solicitações de entrada tentar tooenter essa política será encerrada com "403 muito muitas solicitações" imediatamente quando a fila de saudação é esgotada.|Não|Infinito|  
  
###  <a name="ChooseUsage"></a> Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções da política:** entrada, saída, back-end, em caso de erro  
  
-   **Escopos da política:** todos os escopos  

##  <a name="log-to-eventhub"></a>Log tooEvent Hub  
 Olá `log-to-eventhub` política envia mensagens de saudação especificado formato tooan Hub de eventos definidos por uma entidade de agente de log. Como o nome sugere, política de saudação é usada para salvar selecionadas informações de contexto de solicitação ou resposta para a análise online ou offline.  
  
> [!NOTE]
>  Para um guia passo a passo sobre como configurar um hub de eventos e log de eventos, consulte [como toolog eventos de gerenciamento de API com Hubs de eventos do Azure](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<log-to-eventhub logger-id="id of hello logger entity" partition-id="index of hello partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string toobe logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a>Exemplo  
 Qualquer cadeia de caracteres pode ser usada como Olá valor toobe registrado em Hubs de eventos. Neste exemplo hello data e hora, o nome do serviço de implantação, o id da solicitação, o endereço ip e o nome da operação para todas as chamadas de entrada são hub de eventos registrados toohello agente registrado com hello `contoso-logger` id.  
  
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
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descrição|Obrigatório|  
|-------------|-----------------|--------------|  
|log-to-eventhub|Elemento raiz. valor Olá desse elemento é o hub de eventos do hello cadeia de caracteres toolog tooyour.|Sim|  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|Obrigatório|  
|---------------|-----------------|--------------|  
|logger-id|id de saudação do hello agente registrado com o serviço de gerenciamento de API.|Sim|  
|partition-id|Especifica o índice de saudação da partição Olá onde as mensagens são enviadas.|Opcional. Esse atributo não poderá ser usado se `partition-key` for usado.|  
|partition-key|Especifica o valor de saudação usado para atribuição de partição quando as mensagens são enviadas.|Opcional. Esse atributo não poderá ser usado se `partition-id` for usado.|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções da política:** entrada, saída, back-end, em caso de erro  
  
-   **Escopos da política:** todos os escopos  

##  <a name="mock-response"></a> Resposta fictícia  
Olá `mock-response`, como nome de saudação implica, é usado toomock APIs e operações. Ele anula a execução do pipeline normal e retorna um chamador de toohello resposta fictícios. política de saudação sempre tenta tooreturn respostas de maior fidelidade. Ela prefere exemplos de conteúdo de resposta, sempre que disponíveis. Ela gera respostas de exemplo com base em esquemas, quando esquemas são fornecidos e exemplos não são fornecidos. Se não forem encontrados exemplos nem esquemas, serão retornadas respostas sem conteúdo.
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a>Exemplos  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, hello content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, hello content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descrição|Obrigatório|  
|-------------|-----------------|--------------|  
|mock-response|Elemento raiz.|Sim|  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|Obrigatório|Padrão|  
|---------------|-----------------|--------------|--------------|  
|status-code|Especifica o código de status de resposta e é exemplo correspondente tooselect usado ou esquema.|Não|200|  
|content-type|Especifica `Content-Type` valor do cabeçalho de resposta e exemplo correspondente tooselect usado ou esquema.|Não|Nenhum|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** de entrada, de saída, em caso de erro  
  
-   **Escopos da política:** todos os escopos

##  <a name="Retry"></a> Repetir  
 Olá `retry` política suas diretivas de filho é executado uma vez e, em seguida, tenta novamente sua execução até repetição Olá `condition` se torna `false` ou repita `count` está esgotada.  
  
### <a name="policy-statement"></a>Declaração de política  
  
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
  
### <a name="example"></a>Exemplo  
 Em Olá forewarding de solicitação de exemplo a seguir é repetida backup tooten usando algoritmo de repetição exponencial. Como `first-fast-retry` é definido como toofalse, todas as tentativas de repetição são algoritmo toohello exponsntial tente novamente.  
  
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
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descrição|Obrigatório|  
|-------------|-----------------|--------------|  
|tentar novamente|Elemento raiz. Pode conter quaisquer outras políticas como seus elementos filho.|Sim|  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|Obrigatório|Padrão|  
|---------------|-----------------|--------------|-------------|  
|condition|Uma [expressão](api-management-policy-expressions.md) ou literal booliano especificando se as novas tentativas devem ser paradas (`false`) ou continuadas (`true`).|Sim|N/D|  
|count|Um número positivo que especifica o número máximo de saudação do tooattempt de novas tentativas.|Sim|N/D|  
|intervalo|Um número positivo, em segundos, especificando o intervalo de espera de saudação entre as tentativas de repetição de saudação.|Sim|N/D|  
|max-interval|Um número positivo, em segundos, especificando o intervalo de espera máximo Olá entre as tentativas de repetição de saudação. É usado tooimplement um algoritmo de repetição exponencial.|Não|N/D|  
|delta|Um número positivo em segundos para especificar o incremento de intervalo de espera de saudação. É usado tooimplement Olá repetição linear e exponencial algoritmos.|Não|N/D|  
|first-fast-retry|Se definir muito `true` , Olá primeira tentativa de repetição é executada imediatamente.|Não|`false`|  
  
> [!NOTE]
>  Quando apenas Olá `interval` for especificado, **fixa** tentativas de intervalo são executadas.  
>  Quando apenas Olá `interval` e `delta` forem especificados, um **linear** é usado pelo algoritmo de nova tentativa de intervalo em que o tempo de espera entre as repetições é Olá calculada de acordo seguinte fórmula - `interval + (count - 1)*delta`.  
>  Olá quando `interval`, `max-interval` e `delta` forem especificados, **exponencial** algoritmo de nova tentativa de intervalo é aplicado, onde o tempo de espera de saudação entre repetições Olá está aumentando exponencialmente do valor de saudação do `interval`valor toohello `max-interval` de acordo com o seguinte toohello forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) . Observe que as restrições de uso de política filho serão herdadas por essa política.  
  
-   **Seções da política:** entrada, saída, back-end, em caso de erro  
  
-   **Escopos da política:** todos os escopos  
  
##  <a name="ReturnResponse"></a> Retornar resposta  
 Olá `return-response` política anula a execução do pipeline e retorna um padrão ou o chamador de toohello de resposta personalizada. A resposta padrão é `200 OK` sem corpo. A resposta personalizada pode ser especificada por meio de declarações de política ou variável de contexto. Quando ambos são fornecidas, resposta Olá contida na variável de contexto de saudação é modificada por declarações de política de saudação antes de serem retornados toohello chamador.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a>Exemplo  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descrição|Obrigatório|  
|-------------|-----------------|--------------|  
|return-response|Elemento raiz.|Sim|  
|set-header|Uma declaração de política [set-header](api-management-transformation-policies.md#SetHTTPheader).|Não|  
|set-body|Uma declaração de política [set-body](api-management-transformation-policies.md#SetBody).|Não|  
|set-status|Uma declaração de política [set-status](api-management-advanced-policies.md#SetStatus).|Não|  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|Obrigatório|  
|---------------|-----------------|--------------|  
|response-variable-name|Hello nome de variável de contexto Olá referenciado, por exemplo, um upstream [solicitação de envio](api-management-advanced-policies.md#SendRequest) política e que contém um `Response` objeto|Opcional.|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções da política:** entrada, saída, back-end, em caso de erro  
  
-   **Escopos da política:** todos os escopos  
  
##  <a name="SendOneWayRequest"></a> Enviar solicitação unidirecional  
 Olá `send-one-way-request` política envia a solicitação de saudação fornecida toohello especificada URL sem aguardar uma resposta.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a>Exemplo  
 Essa política de exemplo mostra um exemplo do uso de saudação `send-one-way-request` política toosend uma mensagem tooa atraso salas de chat se Olá código de resposta HTTP for too500 maior que ou igual. Para obter mais informações sobre esse exemplo, consulte [usando serviços externos de saudação serviço de gerenciamento do Azure API](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
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
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descrição|Obrigatório|  
|-------------|-----------------|--------------|  
|send-one-way-request|Elemento raiz.|Sim|  
|url|Olá URL de solicitação de saudação.|Não se mode=copy, caso contrário, sim.|  
|estático|o método HTTP para solicitação de saudação do Hello.|Não se mode=copy, caso contrário, sim.|  
|cabeçalho|Cabeçalho da solicitação. Use vários elementos de cabeçalho para vários cabeçalhos de solicitação.|Não|  
|body|corpo da solicitação Hello.|Não|  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|Obrigatório|Padrão|  
|---------------|-----------------|--------------|-------------|  
|mode="string"|Determina se esta é uma nova solicitação ou uma cópia da solicitação atual hello. No modo de saída, modo = cópia não inicializar o corpo da solicitação hello.|Não|Novo|  
|name|Especifica o nome de saudação do hello cabeçalho toobe conjunto.|Sim|N/D|  
|exists-action|Especifica qual ação tootake quando Olá cabeçalho já está especificado. Esse atributo deve ter uma saudação valores a seguir.<br /><br /> -valor de substituição - substitui saudação do cabeçalho existente hello.<br />-Ignorar - não substitui o valor do cabeçalho existente hello.<br />-Acrescentar - acrescenta Olá valor toohello valor do cabeçalho existente.<br />-delete - remove o cabeçalho de saudação da solicitação de saudação.<br /><br /> Quando definido muito`override` alistando várias entradas com hello mesmo nome resultados no cabeçalho Olá sendo conjunto acordo tooall entradas (que serão listadas várias vezes); somente os valores listados serão definidos no resultado de saudação.|Não|override|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções da política:** entrada, saída, back-end, em caso de erro  
  
-   **Escopos da política:** todos os escopos  
  
##  <a name="SendRequest"></a> Enviar solicitação  
 Olá `send-request` política envia a solicitação de saudação fornecida toohello especificou a URL, esperando não mais que Olá define valor de tempo limite.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a>Exemplo  
 Este exemplo mostra uma maneira tooverify um token de referência com um servidor de autorização. Para obter mais informações sobre esse exemplo, consulte [usando serviços externos de saudação serviço de gerenciamento do Azure API](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
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
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descrição|Obrigatório|  
|-------------|-----------------|--------------|  
|send-request|Elemento raiz.|Sim|  
|url|Olá URL de solicitação de saudação.|Não se mode=copy, caso contrário, sim.|  
|estático|o método HTTP para solicitação de saudação do Hello.|Não se mode=copy, caso contrário, sim.|  
|cabeçalho|Cabeçalho da solicitação. Use vários elementos de cabeçalho para vários cabeçalhos de solicitação.|Não|  
|body|corpo da solicitação Hello.|Não|  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|Obrigatório|Padrão|  
|---------------|-----------------|--------------|-------------|  
|mode="string"|Determina se esta é uma nova solicitação ou uma cópia da solicitação atual hello. No modo de saída, modo = cópia não inicializar o corpo da solicitação hello.|Não|Novo|  
|response-variable-name="string"|Se não estiver presente, `context.Response` será usado.|Não|N/D|  
|timeout="integer"|intervalo de tempo limite de saudação em segundos, antes da chamada de saudação toohello URL falhará.|Não|60|  
|ignore-error|Se true e hello resulta em um erro de solicitação:<br /><br /> – Se response-variable-name tiver sido especificado, ele conterá um valor nulo.<br />– Se response-variable-name não tiver sido especificado, context.Request não será atualizado.|Não|false|  
|name|Especifica o nome de saudação do hello cabeçalho toobe conjunto.|Sim|N/D|  
|exists-action|Especifica qual ação tootake quando Olá cabeçalho já está especificado. Esse atributo deve ter uma saudação valores a seguir.<br /><br /> -valor de substituição - substitui saudação do cabeçalho existente hello.<br />-Ignorar - não substitui o valor do cabeçalho existente hello.<br />-Acrescentar - acrescenta Olá valor toohello valor do cabeçalho existente.<br />-delete - remove o cabeçalho de saudação da solicitação de saudação.<br /><br /> Quando definido muito`override` alistando várias entradas com hello mesmo nome resultados no cabeçalho Olá sendo conjunto acordo tooall entradas (que serão listadas várias vezes); somente os valores listados serão definidos no resultado de saudação.|Não|override|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções da política:** entrada, saída, back-end, em caso de erro  
  
-   **Escopos da política:** todos os escopos  
  
##  <a name="SetHttpProxy"></a> Definir proxy HTTP  
 Olá `proxy` política permite que você tooroute solicitações encaminhadas toobackends por meio de um proxy HTTP. HTTP (não HTTPS) tem suporte entre o gateway hello e proxy hello. Somente autenticação básica e NTLM.
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a>Exemplo  
Observe o uso de saudação do [propriedades](api-management-howto-properties.md) como valores de saudação username e password tooavoid armazenar informações confidenciais no documento de política de saudação.  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descrição|Obrigatório|  
|-------------|-----------------|--------------|  
|proxy|Elemento raiz|Sim|  

### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|Obrigatório|Padrão|  
|---------------|-----------------|--------------|-------------|  
|url="string"|URL do proxy no formulário de saudação do http://host:port.|Sim|N/D |  
|username="string"|Toobe nome de usuário usado para autenticação com o proxy de saudação.|Não|N/D |  
|password="string"|Toobe senha usado para autenticação com o proxy de saudação.|Não|N/D |  

### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** de entrada  
  
-   **Escopos da política:** todos os escopos  

##  <a name="SetRequestMethod"></a> Definir método de solicitação  
 Olá `set-method` política permite que você toochange método de solicitação Olá HTTP para uma solicitação.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a>Exemplo  
 Essa política de exemplo que usa Olá `set-method` política mostra um exemplo de enviar uma mensagem tooa atraso sala de bate-papo se Olá código de resposta HTTP for maior que ou igual too500. Para obter mais informações sobre esse exemplo, consulte [usando serviços externos de saudação serviço de gerenciamento do Azure API](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
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
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descrição|Obrigatório|  
|-------------|-----------------|--------------|  
|set-method|Elemento raiz. valor de saudação do elemento de saudação especifica o método HTTP de saudação.|Sim|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** entrada, em caso de erro  
  
-   **Escopos da política:** todos os escopos  
  
##  <a name="SetStatus"></a> Definir código de status  
 Olá `set-status` toohello de código de status do política conjuntos Olá HTTP especificou um valor.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a>Exemplo  
 Este exemplo mostra como tooreturn uma resposta 401, se o token de autorização de saudação é inválido. Para obter mais informações, consulte [usando serviços externos de saudação serviço de gerenciamento de API do Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)  
  
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
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descrição|Obrigatório|  
|-------------|-----------------|--------------|  
|set-status|Elemento raiz.|Sim|  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|Obrigatório|Padrão|  
|---------------|-----------------|--------------|-------------|  
|code="integer"|Olá HTTP tooreturn de código de status.|Sim|N/D|  
|reason="string"|Uma descrição do motivo Olá para retornar o código de status de saudação.|Sim|N/D|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** saída, back-end, em caso de erro  
  
-   **Escopos da política:** todos os escopos  

##  <a name="set-variable"></a> Definir variável  
 Olá `set-variable` política declara um [contexto](api-management-policy-expressions.md#ContextVariables) variável e atribui um valor especificado por meio de um [expressão](api-management-policy-expressions.md) ou um literal de cadeia de caracteres. Se a expressão de saudação contém um literal, ele será convertido tooa tipo de cadeia de caracteres e hello do valor de saudação será `System.String`.  
  
###  <a name="set-variablePolicyStatement"></a> Declaração de política  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <a name="set-variableExample"></a> Exemplo  
 Olá, exemplo a seguir demonstra uma política de variável definida no hello seção de entrada. Essa política de variável de conjunto cria uma `isMobile` booliano [contexto](api-management-policy-expressions.md#ContextVariables) variável definida tootrue se hello `User-Agent` solicitação cabeçalho contém o texto de saudação `iPad` ou `iPhone`.  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descrição|Obrigatório|  
|-------------|-----------------|--------------|  
|set-variable|Elemento raiz.|Sim|  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|Obrigatório|  
|---------------|-----------------|--------------|  
|name|nome de saudação da variável de saudação.|Sim|  
|valor|valor de saudação da variável de saudação. Isso pode ser uma expressão ou um valor literal.|Sim|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções da política:** entrada, saída, back-end, em caso de erro  
  
-   **Escopos da política:** todos os escopos  
  
###  <a name="set-variableAllowedTypes"></a> Tipos permitidos  
 As expressões usadas em Olá `set-variable` política deve retornar um dos seguintes tipos básicos de saudação.  
  
-   System.Boolean  
  
-   System.SByte  
  
-   System.Byte  
  
-   System.UInt16  
  
-   System.UInt32  
  
-   System.UInt64  
  
-   System.Int16  
  
-   System.Int32  
  
-   System.Int64  
  
-   System.Decimal  
  
-   System.Single  
  
-   System.Double  
  
-   System.Guid  
  
-   System.String  
  
-   System.Char  
  
-   System.DateTime  
  
-   System.TimeSpan  
  
-   System.Byte?  
  
-   System.UInt16?  
  
-   System.UInt32?  
  
-   System.UInt64?  
  
-   System.Int16?  
  
-   System.Int32?  
  
-   System.Int64?  
  
-   System.Decimal?  
  
-   System.Single?  
  
-   System.Double?  
  
-   System.Guid?  
  
-   System.String?  
  
-   System.Char?  
  
-   System.DateTime?  

##  <a name="Trace"></a> Rastreamento  
 Olá `trace` política adiciona uma cadeia de caracteres hello [API Inspetor](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) saída. Olá política será executada somente quando o rastreamento é disparado, ou seja, `Ocp-Apim-Trace` cabeçalho de solicitação está presente e defina o muito`true` e `Ocp-Apim-Subscription-Key` cabeçalho de solicitação está presente e contém uma chave válida associada à conta de administrador de saudação.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descrição|Obrigatório|  
|-------------|-----------------|--------------|  
|trace|Elemento raiz.|Sim|  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|Obrigatório|Padrão|  
|---------------|-----------------|--------------|-------------|  
|fonte|Visualizador de rastreamento de toohello significativos literal de cadeia de caracteres e especificando fonte Olá de mensagem de saudação.|Sim|N/D|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .  
  
-   **Seções da política:** entrada, saída, back-end, em caso de erro  
  
-   **Escopos da política:** todos os escopos  
  
##  <a name="Wait"></a> Aguardar  
 Olá `wait` política executa as políticas de filho imediato em paralelo e aguarda para todos ou um dos seu toocomplete de políticas filho imediato antes de ser concluída. Olá espera política pode ter como as políticas de filho imediato [solicitação de envio](api-management-advanced-policies.md#SendRequest), [obter o valor de cache](api-management-caching-policies.md#GetFromCacheByKey), e [fluxo de controle](api-management-advanced-policies.md#choose) políticas.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a>Exemplo  
 Saudação de exemplo a seguir há dois `choose` políticas, como políticas de filho imediato de saudação `wait` política. Cada uma dessas políticas `choose` executadas em paralelo. Cada `choose` política tentativas tooretrieve um valor armazenado em cache. Se houver um erro de cache, um serviço de back-end é chamado de valor de saudação tooprovide. Em Olá Este exemplo `wait` política não for concluída até que todas as suas diretivas de filho imediato de concluir, porque Olá `for` atributo está definido muito`all`.   Em variáveis de contexto de saudação Este exemplo (`execute-branch-one`, `value-one`, `execute-branch-two`, e `value-two`) são declaradas fora do escopo de saudação dessa política de exemplo.  
  
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
  
### <a name="elements"></a>Elementos  
  
|Elemento|Descrição|Obrigatório|  
|-------------|-----------------|--------------|  
|wait|Elemento raiz. Pode conter como elementos filho somente as políticas `send-request`, `cache-lookup-value` e `choose`.|Sim|  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|Obrigatório|Padrão|  
|---------------|-----------------|--------------|-------------|  
|for|Determina se hello `wait` política aguarda até que todos os toobe de políticas de filho imediato concluída ou apenas um. Valores permitidos são:<br /><br /> -   `all`-Aguarde até que todos os toocomplete de políticas de filho imediato<br />-qualquer - Aguarde toocomplete de política qualquer filho imediato. Após a conclusão da primeira política de filho imediato saudação, Olá `wait` política é concluída e execução de quaisquer outras políticas filho imediato é encerrada.|Não|tudo|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** entrada, saída, back-end  
  
-   **Escopos da política:**todos os escopos  
  
## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre como trabalhar com políticas, consulte:
-   [Políticas no Gerenciamento de API](api-management-howto-policies.md) 
-   [Expressões de política](api-management-policy-expressions.md)
