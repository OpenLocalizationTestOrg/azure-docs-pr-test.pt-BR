---
title: "solicitações de toogenerate HTTP de serviço de gerenciamento de API aaaUsing"
description: "Saiba mais políticas de solicitação e resposta toouse em serviços externos de toocall de gerenciamento de API de sua API"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 4539c0fa-21ef-4b1c-a1d4-d89a38c242fa
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 8002ee453057513340328d99f298703c3b3a9531
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-external-services-from-hello-azure-api-management-service"></a><span data-ttu-id="2f051-103">Usando os serviços externos de saudação serviço de gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="2f051-103">Using external services from hello Azure API Management service</span></span>
<span data-ttu-id="2f051-104">políticas de saudação disponíveis no serviço de gerenciamento de API do Azure podem fazer uma ampla gama de trabalho útil com base puramente na solicitação de entrada hello, resposta de saída de hello e informações de configuração básica.</span><span class="sxs-lookup"><span data-stu-id="2f051-104">hello policies available in Azure API Management service can do a wide range of useful work based purely on hello incoming request, hello outgoing response and basic configuration information.</span></span> <span data-ttu-id="2f051-105">No entanto, as políticas sendo capaz de toointeract com serviços externos do gerenciamento de API abre muitos mais oportunidades.</span><span class="sxs-lookup"><span data-stu-id="2f051-105">However, being able toointeract with external services from API Management policies opens up many more opportunities.</span></span>

<span data-ttu-id="2f051-106">Anteriormente, vimos como podemos podem interagir com hello [serviço de Hub de eventos do Azure para registro em log, monitoramento e análise](api-management-log-to-eventhub-sample.md).</span><span class="sxs-lookup"><span data-stu-id="2f051-106">We have previously seen how we can interact with hello [Azure Event Hub service for logging, monitoring and analytics](api-management-log-to-eventhub-sample.md).</span></span> <span data-ttu-id="2f051-107">Neste artigo, tentaremos demonstrar serviço baseado em políticas que permitem que você toointeract com qualquer HTTP externo.</span><span class="sxs-lookup"><span data-stu-id="2f051-107">In this article we will demonstrate policies that allow you toointeract with any external HTTP based service.</span></span> <span data-ttu-id="2f051-108">Essas políticas podem ser usadas para disparar eventos remotos ou para recuperar as informações que serão solicitação original do toomanipulate usado hello e resposta de alguma forma.</span><span class="sxs-lookup"><span data-stu-id="2f051-108">These policies can be used for triggering remote events or for retrieving information that will be used toomanipulate hello original request and response in some way.</span></span>

## <a name="send-one-way-request"></a><span data-ttu-id="2f051-109">Send-One-Way-Request</span><span class="sxs-lookup"><span data-stu-id="2f051-109">Send-One-Way-Request</span></span>
<span data-ttu-id="2f051-110">Possivelmente hello interação externa mais simples é Olá disparar e esquecer de solicitação que permite que um toobe de serviço externo notificado de algum tipo de evento importante.</span><span class="sxs-lookup"><span data-stu-id="2f051-110">Possibly hello simplest external interaction is hello fire-and-forget style of request that allows an external service toobe notified of some kind of important event.</span></span> <span data-ttu-id="2f051-111">Podemos usar política de fluxo de controle Olá `choose` toodetect qualquer tipo de condição que estão interessados e, em seguida, se hello condição for atendida, o que podemos fazer uma solicitação HTTP externa usando Olá [send-uma maneira solicitação](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) política.</span><span class="sxs-lookup"><span data-stu-id="2f051-111">We can use hello control flow policy `choose` toodetect any kind of condition that we are interested in and then, if hello condition is satisfied, we can make an external HTTP request using hello [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) policy.</span></span> <span data-ttu-id="2f051-112">Isso pode ser um tooa de solicitação de mensagens de sistema, como Hipchat ou atraso ou um email de API como SendGrid ou MailChimp, ou para incidentes de suporte crítico algo parecido com PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="2f051-112">This could be a request tooa messaging system like Hipchat or Slack, or a mail API like SendGrid or MailChimp, or for critical support incidents something like PagerDuty.</span></span> <span data-ttu-id="2f051-113">Todos esses sistemas de mensagens têm APIs HTTP simples que podemos facilmente invocar.</span><span class="sxs-lookup"><span data-stu-id="2f051-113">All of these messaging systems have simple HTTP APIs that we can easily invoke.</span></span>

### <a name="alerting-with-slack"></a><span data-ttu-id="2f051-114">Alertas com Slack</span><span class="sxs-lookup"><span data-stu-id="2f051-114">Alerting with Slack</span></span>
<span data-ttu-id="2f051-115">saudação de exemplo a seguir demonstra como toosend tooa uma mensagem atraso salas de chat, se o código de status de resposta HTTP Olá é maior que ou igual a too500.</span><span class="sxs-lookup"><span data-stu-id="2f051-115">hello following example demonstrates how toosend a message tooa Slack chat room if hello HTTP response status code is greater than or equal too500.</span></span> <span data-ttu-id="2f051-116">Um erro de intervalo de 500 indica um problema com nosso API de back-end que Olá cliente da nossa API não pode ser resolvidos sozinhos.</span><span class="sxs-lookup"><span data-stu-id="2f051-116">A 500 range error indicates a problem with our backend API that hello client of our API cannot resolve themselves.</span></span> <span data-ttu-id="2f051-117">Isso geralmente exige algum tipo de intervenção de nossa parte.</span><span class="sxs-lookup"><span data-stu-id="2f051-117">It usually requires some kind of intervention on our part.</span></span>  

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

<span data-ttu-id="2f051-118">Margem de atraso tem noção de saudação de conexões de entrada da web.</span><span class="sxs-lookup"><span data-stu-id="2f051-118">Slack has hello notion of inbound web hooks.</span></span> <span data-ttu-id="2f051-119">Ao configurar um gancho da web de entrada, o atraso gera uma URL especial que permite que você toodo uma solicitação POST simple e toopass uma mensagem em canal de margem de atraso de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f051-119">When configuring an inbound web hook, Slack generates a special URL which allows you toodo a simple POST request and toopass a message into hello Slack channel.</span></span> <span data-ttu-id="2f051-120">Olá corpo JSON que criamos baseia-se em um formato definido pela margem de atraso.</span><span class="sxs-lookup"><span data-stu-id="2f051-120">hello JSON body that we create is based on a format defined by Slack.</span></span>

![Gancho da Web do Slack](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a><span data-ttu-id="2f051-122">O método "disparar e esquecer" é o suficiente?</span><span class="sxs-lookup"><span data-stu-id="2f051-122">Is fire and forget good enough?</span></span>
<span data-ttu-id="2f051-123">Há certas compensações ao usar um estilo de solicitação "disparar e esquecer".</span><span class="sxs-lookup"><span data-stu-id="2f051-123">There are certain tradeoffs when using a fire-and-forget style of request.</span></span> <span data-ttu-id="2f051-124">Se por algum motivo, Olá solicitação falhará e falha de saudação não será reportada.</span><span class="sxs-lookup"><span data-stu-id="2f051-124">If for some reason, hello request fails, then hello failure will not be reported.</span></span> <span data-ttu-id="2f051-125">Nessa situação específica, complexidade de saudação de ter um sistema de relatórios de falhas secundário e o custo de desempenho adicionais de saudação de aguardando resposta Olá não está garantida.</span><span class="sxs-lookup"><span data-stu-id="2f051-125">In this particular situation, hello complexity of having a secondary failure reporting system and hello additional performance cost of waiting for hello response is not warranted.</span></span> <span data-ttu-id="2f051-126">Para cenários em que é essencial toocheck resposta de hello, em seguida, Olá [solicitação de envio](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) política é uma opção melhor.</span><span class="sxs-lookup"><span data-stu-id="2f051-126">For scenarios where it is essential toocheck hello response, then hello [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy is a better option.</span></span>

## <a name="send-request"></a><span data-ttu-id="2f051-127">send-request</span><span class="sxs-lookup"><span data-stu-id="2f051-127">Send-Request</span></span>
<span data-ttu-id="2f051-128">Olá `send-request` política permite usar um tooperform de serviço externo complexo de funções e serviço de gerenciamento de toohello API retorna dados que pode ser usado para processamento adicional de diretiva de processamento.</span><span class="sxs-lookup"><span data-stu-id="2f051-128">hello `send-request` policy enables using an external service tooperform complex processing functions and return data toohello API management service that can be used for further policy processing.</span></span>

### <a name="authorizing-reference-tokens"></a><span data-ttu-id="2f051-129">Autorizando tokens de referência</span><span class="sxs-lookup"><span data-stu-id="2f051-129">Authorizing reference tokens</span></span>
<span data-ttu-id="2f051-130">Uma função importante do Gerenciamento de API é proteger os recursos de back-end.</span><span class="sxs-lookup"><span data-stu-id="2f051-130">A major function of API Management is protecting backend resources.</span></span> <span data-ttu-id="2f051-131">Se o servidor de autorização Olá usado pela sua API cria [tokens JWT](http://jwt.io/) como parte de seu fluxo de OAuth2, como [Active Directory do Azure](../active-directory/active-directory-aadconnect.md) faz, em seguida, você pode usar o hello `validate-jwt` validade de saudação tooverify política do token de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f051-131">If hello authorization server used by your API creates [JWT tokens](http://jwt.io/) as part of its OAuth2 flow, as [Azure Active Directory](../active-directory/active-directory-aadconnect.md) does, then you can use hello `validate-jwt` policy tooverify hello validity of hello token.</span></span> <span data-ttu-id="2f051-132">No entanto, alguns servidores de autorização criam o que chamamos de [referência tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) que não pode ser verificada sem fazer um servidor de autorização de toohello de retorno de chamada.</span><span class="sxs-lookup"><span data-stu-id="2f051-132">However, some authorization servers create what are called [reference tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) that cannot be verified without making a call back toohello authorization server.</span></span>

### <a name="standardized-introspection"></a><span data-ttu-id="2f051-133">Introspecção padronizada</span><span class="sxs-lookup"><span data-stu-id="2f051-133">Standardized introspection</span></span>
<span data-ttu-id="2f051-134">Olá passado não tem havido nenhuma maneira padronizada de verificar um token de referência com um servidor de autorização.</span><span class="sxs-lookup"><span data-stu-id="2f051-134">In hello past there has been no standardized way of verifying a reference token with an authorization server.</span></span> <span data-ttu-id="2f051-135">No entanto um padrão proposto recentemente [7662 RFC](https://tools.ietf.org/html/rfc7662) foi publicada por Olá IETF que define como um servidor de recurso pode verificar a validade de saudação de um token.</span><span class="sxs-lookup"><span data-stu-id="2f051-135">However a recently proposed standard [RFC 7662](https://tools.ietf.org/html/rfc7662) was published by hello IETF that defines how a resource server can verify hello validity of a token.</span></span>

### <a name="extracting-hello-token"></a><span data-ttu-id="2f051-136">Extraindo o token Olá</span><span class="sxs-lookup"><span data-stu-id="2f051-136">Extracting hello token</span></span>
<span data-ttu-id="2f051-137">Olá primeira etapa é tooextract token de saudação do cabeçalho de autorização de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f051-137">hello first step is tooextract hello token from hello Authorization header.</span></span> <span data-ttu-id="2f051-138">valor de cabeçalho Olá deve ser formatado com hello `Bearer` esquema de autorização, um único espaço e, em seguida, autorização de saudação do token de acordo [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span><span class="sxs-lookup"><span data-stu-id="2f051-138">hello header value should be formatted with hello `Bearer` authorization scheme, a single space and then hello authorization token as per [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span></span> <span data-ttu-id="2f051-139">Infelizmente, há casos em que o esquema de autorização de saudação for omitida.</span><span class="sxs-lookup"><span data-stu-id="2f051-139">Unfortunately there are cases where hello authorization scheme is omitted.</span></span> <span data-ttu-id="2f051-140">tooaccount para isso durante a análise, podemos dividir o valor do cabeçalho Olá em um espaço e a última cadeia de caracteres de saudação selecione de hello retornada a matriz de cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="2f051-140">tooaccount for this when parsing, we split hello header value on a space and select hello last string from hello returned array of strings.</span></span> <span data-ttu-id="2f051-141">Isso fornece uma solução alternativa para cabeçalhos de autorização formatados incorretamente.</span><span class="sxs-lookup"><span data-stu-id="2f051-141">This provides a workaround for badly formatted authorization headers.</span></span>

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-hello-validation-request"></a><span data-ttu-id="2f051-142">Fazer a solicitação de validação de saudação</span><span class="sxs-lookup"><span data-stu-id="2f051-142">Making hello validation request</span></span>
<span data-ttu-id="2f051-143">Assim que tivermos o token de autorização hello, podemos Olá solicitação toovalidate Olá token.</span><span class="sxs-lookup"><span data-stu-id="2f051-143">Once we have hello authorization token, we can make hello request toovalidate hello token.</span></span> <span data-ttu-id="2f051-144">RFC 7662 chama introspecção esse processo e requer que você `POST` um recurso de introspecção de toohello de formulário HTML.</span><span class="sxs-lookup"><span data-stu-id="2f051-144">RFC 7662 calls this process introspection and requires that you `POST` a HTML form toohello introspection resource.</span></span> <span data-ttu-id="2f051-145">saudação do formulário HTML deve conter pelo menos um par chave/valor com chave Olá `token`.</span><span class="sxs-lookup"><span data-stu-id="2f051-145">hello HTML form must at least contain a key/value pair with hello key `token`.</span></span> <span data-ttu-id="2f051-146">Esse servidor de autorização toohello solicitação também deve ser autenticado tooensure que não é possível ir trawling clientes mal-intencionado para tokens válidos.</span><span class="sxs-lookup"><span data-stu-id="2f051-146">This request toohello authorization server must also be authenticated tooensure that malicious clients cannot go trawling for valid tokens.</span></span>

```xml
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
```

### <a name="checking-hello-response"></a><span data-ttu-id="2f051-147">Verificação de resposta de saudação</span><span class="sxs-lookup"><span data-stu-id="2f051-147">Checking hello response</span></span>
<span data-ttu-id="2f051-148">Olá `response-variable-name` atributo é usado toogive Olá de acesso retornada uma resposta.</span><span class="sxs-lookup"><span data-stu-id="2f051-148">hello `response-variable-name` attribute is used toogive access hello returned response.</span></span> <span data-ttu-id="2f051-149">Olá nome definido na propriedade pode ser usado como uma chave no hello `context.Variables` saudação do dicionário tooaccess `IResponse` objeto.</span><span class="sxs-lookup"><span data-stu-id="2f051-149">hello name defined in this property can be used as a key into hello `context.Variables` dictionary tooaccess hello `IResponse` object.</span></span>

<span data-ttu-id="2f051-150">Do objeto de resposta Olá podemos recuperar corpo hello e RFC 7622 informa que a resposta de saudação deve ser um objeto JSON e deve conter pelo menos uma propriedade chamada `active` que é um valor booleano.</span><span class="sxs-lookup"><span data-stu-id="2f051-150">From hello response object we can retrieve hello body and RFC 7622 tells us that hello response must be a JSON object and must contain at least a property called `active` that is a boolean value.</span></span> <span data-ttu-id="2f051-151">Quando `active` for true, o token de saudação é considerado válido.</span><span class="sxs-lookup"><span data-stu-id="2f051-151">When `active` is true then hello token is considered valid.</span></span>

### <a name="reporting-failure"></a><span data-ttu-id="2f051-152">Indicação de falha</span><span class="sxs-lookup"><span data-stu-id="2f051-152">Reporting failure</span></span>
<span data-ttu-id="2f051-153">Usamos uma `<choose>` toodetect de política se Olá token é inválido e nesse caso, retornar uma resposta 401.</span><span class="sxs-lookup"><span data-stu-id="2f051-153">We use a `<choose>` policy toodetect if hello token is invalid and if so, return a 401 response.</span></span>

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

<span data-ttu-id="2f051-154">Como por [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) que descreve como `bearer` tokens devem ser usados, podemos também retornar um `WWW-Authenticate` cabeçalho de resposta Olá 401.</span><span class="sxs-lookup"><span data-stu-id="2f051-154">As per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) which describes how `bearer` tokens should be used, we also return a `WWW-Authenticate` header with hello 401 response.</span></span> <span data-ttu-id="2f051-155">Olá WWW-Authenticate é pretendido tooinstruct um cliente sobre como tooconstruct uma solicitação autorizada corretamente.</span><span class="sxs-lookup"><span data-stu-id="2f051-155">hello WWW-Authenticate is intended tooinstruct a client on how tooconstruct a properly authorized request.</span></span> <span data-ttu-id="2f051-156">Devido a ampla variedade de abordagens possíveis com o framework Olá OAuth2 toohello, é difícil toocommunicate todos Olá necessárias informações.</span><span class="sxs-lookup"><span data-stu-id="2f051-156">Due toohello wide variety of approaches possible with hello OAuth2 framework, it is difficult toocommunicate all hello needed information.</span></span> <span data-ttu-id="2f051-157">Felizmente, há esforços em andamento toohelp [clientes descobrir como tooproperly autorizar o servidor de recurso solicitações tooa](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span><span class="sxs-lookup"><span data-stu-id="2f051-157">Fortunately there are efforts underway toohelp [clients discover how tooproperly authorize requests tooa resource server](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span></span>

### <a name="final-solution"></a><span data-ttu-id="2f051-158">Solução final</span><span class="sxs-lookup"><span data-stu-id="2f051-158">Final solution</span></span>
<span data-ttu-id="2f051-159">Reunir todas as partes da saudação, obtemos Olá diretiva a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f051-159">Putting all hello pieces together, we get hello following policy:</span></span>

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

<span data-ttu-id="2f051-160">Isso é apenas um dos vários exemplos de como Olá `send-request` política pode ser serviços externos útil de toointegrate usado no processo de saudação de solicitações e respostas que passam por Olá serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="2f051-160">This is only one of many examples of how hello `send-request` policy can be used toointegrate useful external services into hello process of requests and responses flowing through hello API Management service.</span></span>

## <a name="response-composition"></a><span data-ttu-id="2f051-161">Composição da resposta</span><span class="sxs-lookup"><span data-stu-id="2f051-161">Response Composition</span></span>
<span data-ttu-id="2f051-162">Olá `send-request` política pode ser usada para melhorar a um sistema de back-end de tooa solicitação primária, conforme vimos no exemplo anterior hello, ou ele pode ser usado como uma substituição completa para chamada de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f051-162">hello `send-request` policy can be used for enhancing a primary request tooa backend system, as we saw in hello previous example, or it can be used as a complete replace for of hello backend call.</span></span> <span data-ttu-id="2f051-163">Com essa técnica podemos criar facilmente recursos de composição agregados de vários sistemas diferentes.</span><span class="sxs-lookup"><span data-stu-id="2f051-163">Using this technique we can easily create composite resources that are aggregated from multiple different systems.</span></span>

### <a name="building-a-dashboard"></a><span data-ttu-id="2f051-164">Criando um painel</span><span class="sxs-lookup"><span data-stu-id="2f051-164">Building a dashboard</span></span>
<span data-ttu-id="2f051-165">Às vezes, você deseja toobe tooexpose capaz de informações que existe em vários sistemas de back-end, por exemplo, toodrive um painel.</span><span class="sxs-lookup"><span data-stu-id="2f051-165">Sometimes you want toobe able tooexpose information that exists in multiple backend systems, for example, toodrive a dashboard.</span></span> <span data-ttu-id="2f051-166">Olá KPIs vêm de todos os diferentes back-ends, mas você prefere que não as toothem tooprovide acesso direto e seria interessante se todas as informações de saudação podem ser recuperadas em uma única solicitação.</span><span class="sxs-lookup"><span data-stu-id="2f051-166">hello KPIs come from all different back-ends, but you would prefer not tooprovide direct access toothem and it would be nice if all hello information could be retrieved in a single request.</span></span> <span data-ttu-id="2f051-167">Talvez algumas das informações de back-end Olá precisa de alguns divisão e repartir um pouco de limpeza e primeiro!</span><span class="sxs-lookup"><span data-stu-id="2f051-167">Perhaps some of hello backend information needs some slicing and dicing and a little sanitizing first!</span></span> <span data-ttu-id="2f051-168">Olá back-end seja capaz de toocache que o recurso de composição seria um tooreduce útil carregar como você sabe que os usuários têm o hábito de anti-hammering a tecla F5 de saudação em ordem toosee se suas métricas com baixo desempenho podem ser alterado.</span><span class="sxs-lookup"><span data-stu-id="2f051-168">Being able toocache that composite resource would be a useful tooreduce hello backend load as you know users have a habit of hammering hello F5 key in order toosee if their underperforming metrics might change.</span></span>    

### <a name="faking-hello-resource"></a><span data-ttu-id="2f051-169">Recurso de Olá falsificação</span><span class="sxs-lookup"><span data-stu-id="2f051-169">Faking hello resource</span></span>
<span data-ttu-id="2f051-170">Olá primeiro toobuilding de etapa nosso recurso de painel é tooconfigure uma nova operação no portal do publicador de gerenciamento de API de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f051-170">hello first step toobuilding our dashboard resource is tooconfigure a new operation in hello API Management publisher portal.</span></span> <span data-ttu-id="2f051-171">Isso será um tooconfigure da operação usada de espaço reservado nosso toobuild de política de composição nosso recurso dinâmico.</span><span class="sxs-lookup"><span data-stu-id="2f051-171">This will be a placeholder operation used tooconfigure our composition policy toobuild our dynamic resource.</span></span>

![Operação de painel](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-hello-requests"></a><span data-ttu-id="2f051-173">Fazendo solicitações Olá</span><span class="sxs-lookup"><span data-stu-id="2f051-173">Making hello requests</span></span>
<span data-ttu-id="2f051-174">Uma vez Olá `dashboard` operação tiver sido criada, pode configurar uma política especificamente para essa operação.</span><span class="sxs-lookup"><span data-stu-id="2f051-174">Once hello `dashboard` operation has been created we can configure a policy specifically for that operation.</span></span> 

![Operação de painel](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

<span data-ttu-id="2f051-176">primeira etapa de saudação é tooextract os parâmetros de consulta de solicitação de entrada hello, de forma que podemos pode encaminhar tooour back-end.</span><span class="sxs-lookup"><span data-stu-id="2f051-176">hello first step  is tooextract any query parameters from hello incoming request, so that we can forward them tooour backend.</span></span> <span data-ttu-id="2f051-177">Neste exemplo, nosso painel está mostrando informações baseadas em um período; portanto, ele apresenta os parâmetros `fromDate` e `toDate`.</span><span class="sxs-lookup"><span data-stu-id="2f051-177">In this example our dashboard is showing information based on a period of time an therefore has a `fromDate` and `toDate` parameter.</span></span> <span data-ttu-id="2f051-178">Podemos usar o hello `set-variable` informações de URL de solicitação Olá Olá de tooextract de diretiva.</span><span class="sxs-lookup"><span data-stu-id="2f051-178">We can use hello `set-variable` policy tooextract hello information from hello request URL.</span></span>

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

<span data-ttu-id="2f051-179">Essas informações se houver podemos solicitações tooall sistemas de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f051-179">Once we have this information we can make requests tooall hello backend systems.</span></span> <span data-ttu-id="2f051-180">Cada solicitação constrói uma nova URL com informações de parâmetro hello e chama seu respectivo servidor e armazena a resposta de saudação em uma variável de contexto.</span><span class="sxs-lookup"><span data-stu-id="2f051-180">Each request constructs a new URL with hello parameter information and calls its respective server and stores hello response in a context variable.</span></span>

```xml
<send-request mode="new" response-variable-name="revenuedata" timeout="20" ignore-error="true">
  <set-url>@($"https://accounting.acme.com/salesdata?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="materialdata" timeout="20" ignore-error="true">
  <set-url>@($"https://inventory.acme.com/materiallevels?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="throughputdata" timeout="20" ignore-error="true">
<set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="accidentdata" timeout="20" ignore-error="true">
<set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="2f051-181">Essas solicitações serão executadas em sequência, o que não é ideal.</span><span class="sxs-lookup"><span data-stu-id="2f051-181">These requests will execute in sequence, which is not ideal.</span></span> <span data-ttu-id="2f051-182">Em uma versão futura apresentaremos uma nova política chamada `wait` permitir que todos esses tooexecute solicitações em paralelo.</span><span class="sxs-lookup"><span data-stu-id="2f051-182">In an upcoming release we will be introducing a new policy called `wait` that will enable all of these requests tooexecute in parallel.</span></span>

### <a name="responding"></a><span data-ttu-id="2f051-183">Respondendo</span><span class="sxs-lookup"><span data-stu-id="2f051-183">Responding</span></span>
<span data-ttu-id="2f051-184">resposta composto de saudação tooconstruct usamos Olá [resposta de retorno](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) política.</span><span class="sxs-lookup"><span data-stu-id="2f051-184">tooconstruct hello composite response we can use hello [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policy.</span></span> <span data-ttu-id="2f051-185">Olá `set-body` elemento pode usar uma expressão tooconstruct um novo `JObject` com todas as representações de componente Olá inseridas como propriedades.</span><span class="sxs-lookup"><span data-stu-id="2f051-185">hello `set-body` element can use an expression tooconstruct a new `JObject` with all hello component representations embedded as properties.</span></span>

```xml
<return-response response-variable-name="existing response variable">
  <set-status code="200" reason="OK" />
  <set-header name="Content-Type" exists-action="override">
    <value>application/json</value>
  </set-header>
  <set-body>
    @(new JObject(new JProperty("revenuedata",((IResponse)context.Variables["revenuedata"]).Body.As<JObject>()),
                  new JProperty("materialdata",((IResponse)context.Variables["materialdata"]).Body.As<JObject>()),
                  new JProperty("throughputdata",((IResponse)context.Variables["throughputdata"]).Body.As<JObject>()),
                  new JProperty("accidentdata",((IResponse)context.Variables["accidentdata"]).Body.As<JObject>())
                  ).ToString())
  </set-body>
</return-response>
```

<span data-ttu-id="2f051-186">diretiva completa Olá será semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="2f051-186">hello complete policy looks as follows:</span></span>

```xml
<policies>
    <inbound>

  <set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
  <set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">

    <send-request mode="new" response-variable-name="revenuedata" timeout="20" ignore-error="true">
      <set-url>@($"https://accounting.acme.com/salesdata?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="materialdata" timeout="20" ignore-error="true">
      <set-url>@($"https://inventory.acme.com/materiallevels?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="throughputdata" timeout="20" ignore-error="true">
    <set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="accidentdata" timeout="20" ignore-error="true">
    <set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <return-response response-variable-name="existing response variable">
      <set-status code="200" reason="OK" />
      <set-header name="Content-Type" exists-action="override">
        <value>application/json</value>
      </set-header>
      <set-body>
        @(new JObject(new JProperty("revenuedata",((IResponse)context.Variables["revenuedata"]).Body.As<JObject>()),
                      new JProperty("materialdata",((IResponse)context.Variables["materialdata"]).Body.As<JObject>()),
                      new JProperty("throughputdata",((IResponse)context.Variables["throughputdata"]).Body.As<JObject>()),
                      new JProperty("accidentdata",((IResponse)context.Variables["accidentdata"]).Body.As<JObject>())
                      ).ToString())
      </set-body>
    </return-response>
    </inbound>
    <backend>
        <base />
    </backend>
    <outbound>
        <base />
    </outbound>
</policies>
```

<span data-ttu-id="2f051-187">Na configuração de saudação da operação de espaço reservado de saudação que podemos configurar Olá painel recursos toobe armazenado em cache pelo menos uma hora como compreendemos natureza Olá dados saudação significa que, mesmo se houver uma hora desatualizada, que ele ainda estará suficientemente eficaz usuários que toohello tooconvey informações valiosas.</span><span class="sxs-lookup"><span data-stu-id="2f051-187">In hello configuration of hello placeholder operation we can configure hello dashboard resource toobe cached for at least an hour because we understand hello nature of hello data means that even if it is an hour out of date, it will still be sufficiently effective tooconvey valuable information toohello users.</span></span>

## <a name="summary"></a><span data-ttu-id="2f051-188">Resumo</span><span class="sxs-lookup"><span data-stu-id="2f051-188">Summary</span></span>
<span data-ttu-id="2f051-189">Serviço de gerenciamento de API do Azure fornece políticas flexíveis que podem ser seletivamente aplicadas tooHTTP tráfego e permite a composição de serviços back-end.</span><span class="sxs-lookup"><span data-stu-id="2f051-189">Azure API Management service provides flexible policies that can be selectively applied tooHTTP traffic and enables composition of backend services.</span></span> <span data-ttu-id="2f051-190">Se você deseja tooenhance seu gateway de API com funções, recursos de validação e verificação de alerta ou cria novos recursos de composição, com base em vários serviços de back-end, Olá `send-request` e políticas relacionadas abrem um mundo de possibilidades.</span><span class="sxs-lookup"><span data-stu-id="2f051-190">Whether you want tooenhance your API gateway with alerting functions, verification, validation capabilities or create new composite resources based on multiple backend services, hello `send-request` and related policies open a world of possibilities.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="2f051-191">Assista a uma visão geral dessas políticas em vídeo</span><span class="sxs-lookup"><span data-stu-id="2f051-191">Watch a video overview of these policies</span></span>
<span data-ttu-id="2f051-192">Para obter mais informações sobre Olá [send-uma maneira solicitação](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [solicitação de envio](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), e [resposta de retorno](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) políticas abordadas neste artigo, assista Olá vídeo a seguir.</span><span class="sxs-lookup"><span data-stu-id="2f051-192">For more information on hello [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), and [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policies covered in this article, please watch hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

