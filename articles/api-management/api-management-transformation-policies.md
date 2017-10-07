---
title: "políticas de transformação do gerenciamento de API aaaAzure | Microsoft Docs"
description: "Saiba mais sobre políticas de transformação de saudação disponíveis para uso no gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7406a8ce-5f9c-4fae-9b0f-e574befb2ee9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2891cc52d0017b717b3c12a98bc4941b5fd7ea78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-transformation-policies"></a>Políticas de transformação de Gerenciamento de API
Este tópico fornece uma referência para Olá políticas de gerenciamento de API a seguir. Para obter mais informações sobre como adicionar e configurar políticas, consulte [Políticas de Gerenciamento de API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="TransformationPolicies"></a> Políticas de transformação  
  
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
  
##  <a name="ConvertJSONtoXML"></a>Converter JSON tooXML  
 Olá `json-to-xml` política converte um corpo de resposta ou solicitação de JSON tooXML.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a>Exemplo  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <json-to-xml apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|  
|----------|-----------------|--------------|  
|json-to-xml|Elemento raiz.|Sim|  
  
### <a name="attributes"></a>Atributos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|aplicar|atributo Olá deve ser definido como tooone de saudação valores a seguir.<br /><br /> –  always – sempre aplicar conversão.<br />–  content-type-json – converter somente se o cabeçalho Content-Type da resposta indica a presença de JSON.|Sim|N/D|  
|consider-accept-header|atributo Olá deve ser definido como tooone de saudação valores a seguir.<br /><br /> –  true – aplica conversão se JSON é solicitado no cabeçalho Accept da solicitação.<br />–  false – sempre aplicar conversão.|Não|verdadeiro|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** de entrada, de saída, em caso de erro  
  
-   **Escopos de política:** global, produto, API, operação  
  
##  <a name="ConvertXMLtoJSON"></a>Converter XML tooJSON  
 Olá `xml-to-json` política converte um corpo de resposta ou solicitação de XML tooJSON. Esta política pode ser usado toomodernize APIs com base em serviços da web de back-end XML apenas.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a>Exemplo  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <xml-to-json kind="direct" apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|  
|----------|-----------------|--------------|  
|xml-to-json|Elemento raiz.|Sim|  
  
### <a name="attributes"></a>Atributos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|kind|atributo Olá deve ser definido como tooone de saudação valores a seguir.<br /><br /> Olá-javascript friendly – converter JSON tem um desenvolvedores tooJavaScript amigável do formulário.<br />-direta - Olá JSON convertido reflete a estrutura do documento do XML de original hello.|Sim|N/D|  
|aplicar|atributo Olá deve ser definido como tooone de saudação valores a seguir.<br /><br /> – always – converter sempre.<br />–  content-type-xml – converter somente se o cabeçalho Content-Type da resposta indica a presença de XML.|Sim|N/D|  
|consider-accept-header|atributo Olá deve ser definido como tooone de saudação valores a seguir.<br /><br /> –  true – aplica conversão se XML é solicitado no cabeçalho Accept da solicitação.<br />–  false – sempre aplicar conversão.|Não|verdadeiro|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** de entrada, de saída, em caso de erro  
  
-   **Escopos de política:** global, produto, API, operação  
  
##  <a name="Findandreplacestringinbody"></a> Localizar e substituir cadeia de caracteres no corpo  
 Olá `find-and-replace` política localiza uma subcadeia de caracteres de solicitação ou resposta e a substitui por uma subcadeia de caracteres diferente.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<find-and-replace from="what tooreplace" to="replacement" />  
```  
  
### <a name="example"></a>Exemplo  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|  
|----------|-----------------|--------------|  
|find-and-replace|Elemento raiz.|Sim|  
  
### <a name="attributes"></a>Atributos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|Da|Olá toosearch de cadeia de caracteres para.|Sim|N/D|  
|para|cadeia de caracteres de substituição de saudação. Especifique uma substituição cadeia de caracteres tooremove Olá pesquisa sequência de tamanho zero.|Sim|N/D|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções da política:** entrada, saída, back-end, em caso de erro  
  
-   **Escopos de política:** global, produto, API, operação  
  
##  <a name="MaskURLSContent"></a> Mascarar URLs no conteúdo  
 Olá `redirect-content-urls` política regrava (mascara) links no corpo de resposta Olá para que eles apontem toohello o link equivalente através do gateway de saudação. Use em toomake links corpo de resposta do hello seção saída toore gravação-los toohello de ponto de gateway. Uso em Olá seção para um efeito oposto de entrada.  
  
> [!NOTE]
>  Essa política não altera nenhum valor de cabeçalho como cabeçalhos `Location`. valores de cabeçalho toochange, use Olá [cabeçalho do conjunto](api-management-transformation-policies.md#SetHTTPheader) política.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a>Exemplo  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|  
|----------|-----------------|--------------|  
|redirect-content-urls|Elemento raiz.|Sim|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** de entrada, de saída  
  
-   **Escopos de política:** global, produto, API, operação  
  
##  <a name="SetBackendService"></a> Definir o serviço de back-end  
 Saudação de uso `set-backend-service` política tooredirect uma entrada de solicitação back-end diferente de tooa de Olá especificado nas configurações de saudação API para essa operação. Essa política altera back-end Olá URL base do serviço de toohello solicitação de entrada hello especificada na política de saudação.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<set-backend-service base-url="base URL of hello backend service" />  
```  
  
### <a name="example"></a>Exemplo  
  
```xml  
<policies>  
    <inbound>  
        <choose>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2013-05")">  
                <set-backend-service base-url="http://contoso.com/api/8.2/" />  
            </when>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2014-03")">  
                <set-backend-service base-url="http://contoso.com/api/9.1/" />  
            </when>  
        </choose>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
Em Olá Este exemplo Definir política de serviço de back-end roteia solicitações com base no valor de versão Olá passado no serviço de back-end diferente de tooa Olá consulta cadeia de caracteres que Olá Olá especificado em uma API.
  
Inicialmente hello URL base do serviço de back-end é derivada de configurações de API de saudação. Olá para a URL de solicitação `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` se torna `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` onde `http://contoso.com/api/10.4/` é a URL do serviço de back-end de saudação especificado nas configurações de API de saudação.  
  
Olá quando [< escolha\> ](api-management-advanced-policies.md#choose) declaração da política é aplicada Olá URL de base do serviço de back-end pode alterar novamente muito`http://contoso.com/api/8.2` ou `http://contoso.com/api/9.1`, dependendo do valor de saudação do parâmetro de consulta de solicitação de versão de saudação. Por exemplo, se hello valor é `"2013-15"` solicitação final de saudação URL será `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.  
  
Se outra transformação de solicitação de saudação será desejado, [políticas de transformação](api-management-transformation-policies.md#TransformationPolicies) pode ser usado. Por exemplo, tooremove Olá versão consulta parâmetro agora que hello solicitação está sendo roteada back-end específico de versão de tooa, hello [definir parâmetro de cadeia de caracteres de consulta](api-management-transformation-policies.md#SetQueryStringParameter) política pode ser o atributo de versão agora redundante Olá tooremove usado.  
  
### <a name="example"></a>Exemplo  
  
```xml  
<policies>  
    <inbound>  
        <set-backend-service backend-id="my-sf-service" sf-partition-key="@(context.Request.Url.Query.GetValueOrDefault("userId","")" sf-replica-type="primary" /> 
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
Neste exemplo hello política rotas Olá solicitação tooa serviço malha back-end, usando a cadeia de caracteres de consulta de userId hello como chave de partição hello e usando Olá réplica primária de partição hello.  

### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|  
|----------|-----------------|--------------|  
|set-backend-service|Elemento raiz.|Sim|  
  
### <a name="attributes"></a>Atributos  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|base-url|Nova URL base do serviço de back-end.|Não|N/D|  
|backend-id|Identificador da saudação tooroute de back-end para.|Não|N/D|  
|sf-partition-key|Só aplicável quando o hello back-end é um serviço de malha do serviço e é especificado usando 'id de back-end'. Usado tooresolve uma partição específica do serviço de resolução de nome de saudação.|Não|N/D|  
|sf-replica-type|Só aplicável quando o hello back-end é um serviço de malha do serviço e é especificado usando 'id de back-end'. Controla se a solicitação de saudação deve ir toohello a réplica primária ou secundária de uma partição. |Não|N/D|    
|sf-resolve-condition|Só é aplicável quando Olá back-end é um serviço de malha do serviço. Identificação de condição se Olá chamar back-end de malha tooService tem toobe repetida com nova resolução.|Não|N/D|    
|sf-service-instance-name|Só é aplicável quando Olá back-end é um serviço de malha do serviço. Permite que toochange instâncias de serviço em tempo de execução. |Não|N/D |    

### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** de entrada, back-end  
  
-   **Escopos de política:** global, produto, API, operação  
  
##  <a name="SetBody"></a> Definir corpo  
 Saudação de uso `set-body` corpo da mensagem de saudação política tooset para solicitações de entrada e saídas. tooaccess Olá corpo de mensagem, você pode usar o hello `context.Request.Body` propriedade ou hello `context.Response.Body`, dependendo se a política de saudação está em Olá seção de entrada ou saída.  
  
> [!IMPORTANT]
>  Observe que, por padrão, quando você acessar Olá corpo de mensagem usando `context.Request.Body` ou `context.Response.Body`, mensagem original de saudação do corpo é perdido e deve ser definido, retornando o corpo de saudação volta na expressão de saudação. corpo da saudação toopreserve conteúdo, defina Olá `preserveContent` parâmetro muito`true` ao acessar a mensagem de saudação. Se `preserveContent` está definido muito`true` e um corpo diferente é retornado pela expressão hello, Olá retornado corpo é usado.  
>   
>  Observação Olá considerações a seguir ao usar o hello `set-body` política.  
>   
>  -   Se você estiver usando Olá `set-body` tooreturn política um corpo de novo ou atualizado não é necessário tooset `preserveContent` muito`true` porque você está fornecendo um novo conteúdo de corpo Olá explicitamente.  
> -   Preservar o conteúdo de saudação de uma resposta no pipeline de entrada hello não faz sentido, porque não há nenhuma resposta ainda.  
> -   Preservar o conteúdo de saudação de uma solicitação no pipeline de saída Olá não faz sentido porque Olá solicitação já foi enviada toohello back-end neste momento.  
> -   Se essa política é usada quando não há nenhum corpo da mensagem, por exemplo em um GET de entrada, uma exceção é lançada.  
  
 Para obter mais informações, consulte Olá `context.Request.Body`, `context.Response.Body`e hello `IMessage` seções Olá [variável de contexto](api-management-policy-expressions.md#ContextVariables) tabela.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a>Exemplos  
  
#### <a name="literal-text-example"></a>Exemplo de texto literal  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-string-note-that-we-are-preserving-hello-original-request-body-so-that-we-can-access-it-later-in-hello-pipeline"></a>Por exemplo, acessando o corpo de saudação como uma cadeia de caracteres. Observe que estamos são preservando corpo da solicitação original Olá para que podemos pode acessá-lo mais tarde no pipeline de saudação.
  
```xml  
<set-body>  
@{   
    string inBody = context.Request.Body.As<string>(preserveContent: true);   
    if (inBody[0] =='c') {   
        inBody[0] = 'm';   
    }   
    return inBody;   
}  
</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-jobject-note-that-since-we-are-not-reserving-hello-original-request-body-accesing-it-later-in-hello-pipeline-will-result-in-an-exception"></a>Por exemplo, acessando o corpo da saudação como um JObject. Observe que, desde que não são reservar o corpo da solicitação original hello, acessar posteriormente no pipeline de saudação resultará em uma exceção.  
  
```xml  
<set-body>   
@{   
    JObject inBody = context.Request.Body.As<JObject>();   
    if (inBody.attribute == <tag>) {   
        inBody[0] = 'm';   
    }   
    return inBody.ToString();   
}   
</set-body>  
  
```  
  
#### <a name="filter-response-based-on-product"></a>Resposta de filtro com base no produto  
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

### <a name="using-liquid-templates-with-set-body"></a>Usando modelos Líquidos com o corpo definido 
Olá `set-body` política pode ser configurado toouse Olá [líquido](https://shopify.github.io/liquid/basics/introduction/) corpo da saudação tootransfom modelagem idioma de uma solicitação ou resposta. Isso pode ser muito eficaz se você precisar de formato de saudação de reformatação toocompletely da mensagem.

> [!IMPORTANT]
> Olá implementação de líquido usado em Olá `set-body` a política é configurada no 'modo de C# '. Isso é particularmente importante ao executar ações como filtragem. Por exemplo, usando um filtro de data requer o uso de saudação do Pascal maiusculas e minúsculas e c#, por exemplo, formatação de data:
>
> {{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}

> [!IMPORTANT]
> Em ordem toocorrectly bind tooan corpo XML usando o modelo líquidos hello, use um `set-header` política tooset Content-Type tooeither aplicativo/xml, texto/xml (ou qualquer tipo que terminam com + xml); para um corpo JSON, ele deve ser aplicativo/json, texto/json (ou final de qualquer tipo com + json).

#### <a name="convert-json-toosoap-using-a-liquid-template"></a>Converter JSON tooSOAP usando um modelo líquido
```xml
<set-body template="liquid">
    <soap:Envelope xmlns="http://tempuri.org/" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Body>
            <GetOpenOrders>
                <cust>{{body.getOpenOrders.cust}}</cust>
            </GetOpenOrders>
        </soap:Body>
    </soap:Envelope>
</set-body>
```

#### <a name="tranform-json-using-a-liquid-template"></a>Transformar JSON usando um modelo Líquido
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|  
|----------|-----------------|--------------|  
|set-body|Elemento raiz. Contém o texto de saudação ou expressões que retornam um corpo.|Sim|  

### <a name="properties"></a>Propriedades  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|template|Modo de modelagem do hello toochange usado Olá definir corpo política executará. Atualmente, o valor de saudação só tem suportada é:<br /><br />Olá - líquido - definir corpo política usará o mecanismo de modelagem líquidos Olá |Não|liquid|  

Para acessar informações sobre Olá solicitação e resposta, modelo líquidos Olá pode vincular o objeto de contexto tooa com hello propriedades a seguir: <br />
<pre>context.
    Request.
        Url
        Method
        OriginalMethod
        OriginalUrl
        IpAddress
        MatchedParameters
        HasBody
        ClientCertificates
        Headers

    Response.
        StatusCode
        Method
        Headers
Url.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString

OriginalUrl.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString
</pre>



### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** entrada, saída, back-end  
  
-   **Escopos de política:** global, produto, API, operação  
  
##  <a name="SetHTTPheader"></a> Definir cabeçalho HTTP  
 Olá `set-header` política atribui um cabeçalho de solicitação e/ou resposta do valor tooan existente ou adiciona um novo cabeçalho de solicitação de e/ou resposta.  
  
 Insere uma lista de cabeçalhos HTTP em uma mensagem HTTP. Quando colocada em um pipeline de entrada, essa política define os cabeçalhos HTTP Olá para solicitação hello está sendo passado toohello serviço de destino. Quando colocada em um pipeline de saída, essa política define os cabeçalhos HTTP Olá para resposta de hello está sendo enviada cliente toohello do gateway.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with hello same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a>Exemplos  
  
#### <a name="example"></a>Exemplo  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a>Encaminhar o serviço de back-end de toohello de informações de contexto  
 Este exemplo mostra como a diretiva tooapply Olá API nível toosupply serviço de back-end de toohello de informações de contexto. Para ver uma demonstração de como configurar e usar essa política, consulte [nuvem abrangem episódio 177: mais recursos de gerenciamento de API com Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e Avançar too10:30. Em 12:10, há uma demonstração de como chamar uma operação no portal do desenvolvedor Olá onde você pode ver a política de saudação no trabalho.  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward some context information, user id and hello region hello gateway is hosted in, toohello backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 Para obter mais informações, veja [Expressões de política](api-management-policy-expressions.md) e [Variável de contexto](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|  
|----------|-----------------|--------------|  
|set-header|Elemento raiz.|Sim|  
|valor|Especifica o valor de saudação do hello cabeçalho toobe conjunto. Para vários cabeçalhos com hello mesmo nome adicionar adicional `value` elementos.|Sim|  
  
### <a name="properties"></a>Propriedades  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|exists-action|Especifica qual ação tootake quando Olá cabeçalho já está especificado. Esse atributo deve ter uma saudação valores a seguir.<br /><br /> -valor de substituição - substitui saudação do cabeçalho existente hello.<br />-Ignorar - não substitui o valor do cabeçalho existente hello.<br />-Acrescentar - acrescenta Olá valor toohello valor do cabeçalho existente.<br />-delete - remove o cabeçalho de saudação da solicitação de saudação.<br /><br /> Quando definido muito`override` alistando várias entradas com hello mesmo nome resultados no cabeçalho Olá sendo conjunto acordo tooall entradas (que serão listadas várias vezes); somente os valores listados serão definidos no resultado de saudação.|Não|override|  
|name|Especifica o nome do conjunto de toobe do cabeçalho de saudação.|Sim|N/D|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções da política:** entrada, saída, back-end, em caso de erro  
  
-   **Escopos de política:** global, produto, API, operação  
  
##  <a name="SetQueryStringParameter"></a> Definir parâmetro de cadeia de consulta  
 Olá `set-query-parameter` política adiciona, substitui o valor, ou parâmetro de cadeia de caracteres de consulta de solicitação de exclusões. Pode ser usado toopass parâmetros de consulta esperados pelo serviço de back-end de saudação que são opcionais ou nunca estão presentes na solicitação de saudação.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with hello same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a>Exemplos  
  
#### <a name="example"></a>Exemplo  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with hello same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a>Encaminhar o serviço de back-end de toohello de informações de contexto  
 Este exemplo mostra como a diretiva tooapply Olá API nível toosupply serviço de back-end de toohello de informações de contexto. Para ver uma demonstração de como configurar e usar essa política, consulte [nuvem abrangem episódio 177: mais recursos de gerenciamento de API com Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e Avançar too10:30. Em 12:10, há uma demonstração de como chamar uma operação no portal do desenvolvedor Olá onde você pode ver a política de saudação no trabalho.  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward a piece of context, product name in this example, toohello backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 Para obter mais informações, veja [Expressões de política](api-management-policy-expressions.md) e [Variável de contexto](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|  
|----------|-----------------|--------------|  
|set-query-parameter|Elemento raiz.|Sim|  
|valor|Especifica o valor de Olá Olá parâmetro toobe do conjunto de consulta. Para vários parâmetros de consulta com hello mesmo nome adicionar adicional `value` elementos.|Sim|  
  
### <a name="properties"></a>Propriedades  
  
|Nome|Descrição|Obrigatório|Padrão|  
|----------|-----------------|--------------|-------------|  
|exists-action|Especifica qual ação tootake quando o parâmetro de consulta Olá já está especificado. Esse atributo deve ter uma saudação valores a seguir.<br /><br /> -Substitua - substitui Olá valor de parâmetro de saudação existente.<br />-Ignorar - não substitui o valor de parâmetro de consulta existente hello.<br />-Acrescentar - acrescenta o valor de parâmetro do hello valor toohello existente consulta.<br />-delete - remove o parâmetro de consulta de saudação da solicitação de saudação.<br /><br /> Quando definido muito`override` alistando várias entradas com hello mesmo nome resultados no parâmetro de consulta Olá sendo conjunto acordo tooall entradas (que serão listadas várias vezes); somente os valores listados serão definidos no resultado de saudação.|Não|override|  
|name|Especifica o nome do conjunto de toobe do parâmetro de consulta de saudação.|Sim|N/D|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** de entrada, back-end  
  
-   **Escopos de política:** global, produto, API, operação  
  
##  <a name="RewriteURL"></a> Reescrever URL  
 Olá `rewrite-uri` política converte uma URL de solicitação de forma pública formulário toohello esperada pelo serviço da web de hello, conforme mostrado no exemplo a seguir de saudação.  
  
-   URL pública – `http://api.example.com/storenumber/ordernumber`  
  
-   URL de Solicitação – `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`  
  
 Essa política pode ser usada quando uma URL humana e/ou navegador amigável deve ser transformada em formato de URL de saudação esperado pelo serviço da web de saudação. Essa política só precisa toobe aplicada ao expor um formato de URL alternativo, como URLs limpas, URLs RESTful, URLs amigáveis ou URLs de SEO amigável que sejam URLs puramente estruturais que não contêm uma cadeia de caracteres de consulta e contêm apenas o caminho de saudação de saudação recurso (após o esquema de saudação e da autoridade de saudação). Frequentemente, isso é feito para fins estéticos, de usabilidade ou de otimização do mecanismo de pesquisa (SEO).  
  
> [!NOTE]
>  Você só pode adicionar parâmetros de cadeia de caracteres de consulta usando a política de saudação. Não é possível adicionar parâmetros de caminho de modelo extra na Olá regravar URL.  

### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a>Exemplo  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/v2/US/hardware/{storenumber}&{ordernumber}?City=city&State=state" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put?c=d -->
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" copy-unmatched-params="false" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put -->
```

### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|  
|----------|-----------------|--------------|  
|rewrite-uri|Elemento raiz.|Sim|  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|Obrigatório|Padrão|  
|---------------|-----------------|--------------|-------------|  
|template|Olá o URL do serviço web real com quaisquer parâmetros de cadeia de caracteres de consulta. Ao usar expressões, o valor de inteiro Olá deve ser uma expressão.|Sim|N/D|  
|copy-unmatched-params|Especifica se os parâmetros de consulta na solicitação de entrada de saudação não está presente no modelo de URL original Olá são adicionados toohello URL definido pelo Olá grave novamente o modelo|Não|verdadeiro|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** de entrada  
  
-   **Escopos de política:** produto, API, operação  
  
##  <a name="XSLTransform"></a> Transformar XML usando um XSLT  
 Olá `Transform XML using an XSLT` política se aplica a um tooXML de transformação XSL no corpo de solicitação ou resposta hello.  
  
### <a name="policy-statement"></a>Declaração de política  
  
```xml  
<xsl-transform>  
    <parameter name="User-Agent">@(context.Request.Headers.GetValueOrDefault("User-Agent","non-specified"))</parameter>  
    <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
        <xsl:output method="xml" indent="yes" />  
        <xsl:param name="User-Agent" />  
        <xsl:template match="* | @* | node()">  
            <xsl:copy>  
                <xsl:if test="self::* and not(parent::*)">  
                    <xsl:attribute name="User-Agent">  
                        <xsl:value-of select="$User-Agent" />  
                    </xsl:attribute>  
                </xsl:if>  
                <xsl:apply-templates select="* | @* | node()" />  
            </xsl:copy>  
        </xsl:template>  
    </xsl:stylesheet>  
  </xsl-transform>  
```  
  
### <a name="example"></a>Exemplo  
  
```xml  
<policies>  
  <inbound>  
      <base />  
  </inbound>  
  <outbound>  
      <base />  
      <xsl-transform>  
        <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
            <xsl:output omit-xml-declaration="yes" method="xml" indent="yes" />  
            <!-- Copy all nodes directly-->  
            <xsl:template match="node()| @*|*">  
                <xsl:copy>  
                    <xsl:apply-templates select="@* | node()|*" />  
                </xsl:copy>  
            </xsl:template>  
        </xsl:stylesheet>  
    </xsl-transform>  
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementos  
  
|Nome|Descrição|Obrigatório|  
|----------|-----------------|--------------|  
|xsl-transform|Elemento raiz.|Sim|  
|parâmetro|Variáveis usadas toodefine usadas na transformação de saudação|Não|  
|xsl:stylesheet|Elemento de folha de estilos de raiz. Todos os elementos e atributos definidos no seguem o padrão de saudação [especificação XSLT](http://www.w3.org/TR/xslt)|Sim|  
  
### <a name="usage"></a>Uso  
 Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Seções de política:** de entrada, de saída  
  
-   **Escopos de política:** global, produto, API, operação  
  
## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre como trabalhar com políticas, veja [Políticas em Gerenciamento de API](api-management-howto-policies.md).  
