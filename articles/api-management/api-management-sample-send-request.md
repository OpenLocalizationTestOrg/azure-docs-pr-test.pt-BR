---
title: "Usando o serviço Gerenciamento de API para gerar solicitações HTTP"
description: "Saiba como usar políticas de solicitação e de resposta no Gerenciamento de API para chamar serviços externos de sua API"
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
ms.openlocfilehash: e778943715d6ca5256ad612d82bdc1f82197df0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="using-external-services-from-the-azure-api-management-service"></a><span data-ttu-id="e3983-103">Uso dos serviços externos do serviço de Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="e3983-103">Using external services from the Azure API Management service</span></span>
<span data-ttu-id="e3983-104">As políticas disponíveis no serviço de Gerenciamento de API do Azure permitem uma ampla variedade de trabalhos úteis com base apenas na solicitação de entrada, na resposta de saída e em informações básicas de configuração.</span><span class="sxs-lookup"><span data-stu-id="e3983-104">The policies available in Azure API Management service can do a wide range of useful work based purely on the incoming request, the outgoing response and basic configuration information.</span></span> <span data-ttu-id="e3983-105">No entanto, a capacidade de interagir com serviços externos das políticas de Gerenciamento de API abre muitas outras oportunidades.</span><span class="sxs-lookup"><span data-stu-id="e3983-105">However, being able to interact with external services from API Management policies opens up many more opportunities.</span></span>

<span data-ttu-id="e3983-106">Vimos anteriormente como podemos interagir com o [serviço Hub de Eventos do Azure para registro em log, monitoramento e análise](api-management-log-to-eventhub-sample.md).</span><span class="sxs-lookup"><span data-stu-id="e3983-106">We have previously seen how we can interact with the [Azure Event Hub service for logging, monitoring and analytics](api-management-log-to-eventhub-sample.md).</span></span> <span data-ttu-id="e3983-107">Neste artigo, demonstraremos as políticas que permitem a interação com qualquer serviço externo baseado em HTTP.</span><span class="sxs-lookup"><span data-stu-id="e3983-107">In this article we will demonstrate policies that allow you to interact with any external HTTP based service.</span></span> <span data-ttu-id="e3983-108">Essas políticas podem ser usadas para disparar eventos remotos ou para recuperar informações que serão usadas para manipular a solicitação e resposta originais de alguma forma.</span><span class="sxs-lookup"><span data-stu-id="e3983-108">These policies can be used for triggering remote events or for retrieving information that will be used to manipulate the original request and response in some way.</span></span>

## <a name="send-one-way-request"></a><span data-ttu-id="e3983-109">Send-One-Way-Request</span><span class="sxs-lookup"><span data-stu-id="e3983-109">Send-One-Way-Request</span></span>
<span data-ttu-id="e3983-110">Possivelmente, a interação externa mais simples é o estilo de solicitação "disparar e esquecer" que permite que um serviço externo seja notificado sobre algum tipo de evento importante.</span><span class="sxs-lookup"><span data-stu-id="e3983-110">Possibly the simplest external interaction is the fire-and-forget style of request that allows an external service to be notified of some kind of important event.</span></span> <span data-ttu-id="e3983-111">Podemos usar a política de fluxo de controle `choose` para detectar qualquer tipo de condição de nosso interesse; se a condição for atendida, poderemos fazer uma solicitação HTTP externa usando a política [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) .</span><span class="sxs-lookup"><span data-stu-id="e3983-111">We can use the control flow policy `choose` to detect any kind of condition that we are interested in and then, if the condition is satisfied, we can make an external HTTP request using the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) policy.</span></span> <span data-ttu-id="e3983-112">Isso inclui uma solicitação para um sistema de mensagens como Hipchat ou Slack, ou uma API de email como SendGrid ou MailChimp, ou para incidentes de suporte críticos, algo como o PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="e3983-112">This could be a request to a messaging system like Hipchat or Slack, or a mail API like SendGrid or MailChimp, or for critical support incidents something like PagerDuty.</span></span> <span data-ttu-id="e3983-113">Todos esses sistemas de mensagens têm APIs HTTP simples que podemos facilmente invocar.</span><span class="sxs-lookup"><span data-stu-id="e3983-113">All of these messaging systems have simple HTTP APIs that we can easily invoke.</span></span>

### <a name="alerting-with-slack"></a><span data-ttu-id="e3983-114">Alertas com Slack</span><span class="sxs-lookup"><span data-stu-id="e3983-114">Alerting with Slack</span></span>
<span data-ttu-id="e3983-115">O exemplo a seguir demonstra como enviar uma mensagem a uma sala de bate-papo do Slack, se o código de status de resposta HTTP for maior ou igual a 500.</span><span class="sxs-lookup"><span data-stu-id="e3983-115">The following example demonstrates how to send a message to a Slack chat room if the HTTP response status code is greater than or equal to 500.</span></span> <span data-ttu-id="e3983-116">Um erro de intervalo 500 indica um problema com nossa API de back-end que o cliente de nossa API não consegue resolver sozinho.</span><span class="sxs-lookup"><span data-stu-id="e3983-116">A 500 range error indicates a problem with our backend API that the client of our API cannot resolve themselves.</span></span> <span data-ttu-id="e3983-117">Isso geralmente exige algum tipo de intervenção de nossa parte.</span><span class="sxs-lookup"><span data-stu-id="e3983-117">It usually requires some kind of intervention on our part.</span></span>  

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

<span data-ttu-id="e3983-118">O Slack tem a noção de ganchos de entrada da Web.</span><span class="sxs-lookup"><span data-stu-id="e3983-118">Slack has the notion of inbound web hooks.</span></span> <span data-ttu-id="e3983-119">Ao configurar um gancho de entrada da Web, o Slack gera uma URL especial que permite a realização de uma solicitação POST simples e a transmissão de uma mensagem para o canal do Slack.</span><span class="sxs-lookup"><span data-stu-id="e3983-119">When configuring an inbound web hook, Slack generates a special URL which allows you to do a simple POST request and to pass a message into the Slack channel.</span></span> <span data-ttu-id="e3983-120">O corpo JSON que criamos se baseia em um formato definido pelo Slack.</span><span class="sxs-lookup"><span data-stu-id="e3983-120">The JSON body that we create is based on a format defined by Slack.</span></span>

![Gancho da Web do Slack](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a><span data-ttu-id="e3983-122">O método "disparar e esquecer" é o suficiente?</span><span class="sxs-lookup"><span data-stu-id="e3983-122">Is fire and forget good enough?</span></span>
<span data-ttu-id="e3983-123">Há certas compensações ao usar um estilo de solicitação "disparar e esquecer".</span><span class="sxs-lookup"><span data-stu-id="e3983-123">There are certain tradeoffs when using a fire-and-forget style of request.</span></span> <span data-ttu-id="e3983-124">Se, por algum motivo, a solicitação falhar, a falha não será registrada.</span><span class="sxs-lookup"><span data-stu-id="e3983-124">If for some reason, the request fails, then the failure will not be reported.</span></span> <span data-ttu-id="e3983-125">Nessa situação específica, a complexidade de ter um sistema de relatório de falhas secundário e o custo adicional de desempenho de ter que espera por uma resposta não oferecem garantias.</span><span class="sxs-lookup"><span data-stu-id="e3983-125">In this particular situation, the complexity of having a secondary failure reporting system and the additional performance cost of waiting for the response is not warranted.</span></span> <span data-ttu-id="e3983-126">Para cenários nos quais é essencial verificar a resposta, a política [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) é uma opção mais adequada.</span><span class="sxs-lookup"><span data-stu-id="e3983-126">For scenarios where it is essential to check the response, then the [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy is a better option.</span></span>

## <a name="send-request"></a><span data-ttu-id="e3983-127">send-request</span><span class="sxs-lookup"><span data-stu-id="e3983-127">Send-Request</span></span>
<span data-ttu-id="e3983-128">A política `send-request` permite o uso de um serviço externo para executar funções complexas de processamento e retornar dados para o serviço de gerenciamento de API, que pode ser usado para um processamento adicional da política.</span><span class="sxs-lookup"><span data-stu-id="e3983-128">The `send-request` policy enables using an external service to perform complex processing functions and return data to the API management service that can be used for further policy processing.</span></span>

### <a name="authorizing-reference-tokens"></a><span data-ttu-id="e3983-129">Autorizando tokens de referência</span><span class="sxs-lookup"><span data-stu-id="e3983-129">Authorizing reference tokens</span></span>
<span data-ttu-id="e3983-130">Uma função importante do Gerenciamento de API é proteger os recursos de back-end.</span><span class="sxs-lookup"><span data-stu-id="e3983-130">A major function of API Management is protecting backend resources.</span></span> <span data-ttu-id="e3983-131">Se o servidor de autorização usado pela sua API criar [tokens JWT](http://jwt.io/) como parte de seu fluxo do OAuth2, assim como faz o [Azure Active Directory](../active-directory/active-directory-aadconnect.md), você poderá usar a política `validate-jwt` para verificar a validade do token.</span><span class="sxs-lookup"><span data-stu-id="e3983-131">If the authorization server used by your API creates [JWT tokens](http://jwt.io/) as part of its OAuth2 flow, as [Azure Active Directory](../active-directory/active-directory-aadconnect.md) does, then you can use the `validate-jwt` policy to verify the validity of the token.</span></span> <span data-ttu-id="e3983-132">No entanto, alguns servidores de autorização criam algo chamado [tokens de referência](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) que não podem ser verificados sem a realização de uma chamada para o servidor de autorização.</span><span class="sxs-lookup"><span data-stu-id="e3983-132">However, some authorization servers create what are called [reference tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) that cannot be verified without making a call back to the authorization server.</span></span>

### <a name="standardized-introspection"></a><span data-ttu-id="e3983-133">Introspecção padronizada</span><span class="sxs-lookup"><span data-stu-id="e3983-133">Standardized introspection</span></span>
<span data-ttu-id="e3983-134">No passado, não havia uma forma padronizada de verificar um token de referência com um servidor de autorização.</span><span class="sxs-lookup"><span data-stu-id="e3983-134">In the past there has been no standardized way of verifying a reference token with an authorization server.</span></span> <span data-ttu-id="e3983-135">No entanto, um padrão proposto recentemente, o [RFC 7662](https://tools.ietf.org/html/rfc7662) , foi publicado pela IETF definindo como um servidor de recursos pode verificar a validade de um token.</span><span class="sxs-lookup"><span data-stu-id="e3983-135">However a recently proposed standard [RFC 7662](https://tools.ietf.org/html/rfc7662) was published by the IETF that defines how a resource server can verify the validity of a token.</span></span>

### <a name="extracting-the-token"></a><span data-ttu-id="e3983-136">Extração do token</span><span class="sxs-lookup"><span data-stu-id="e3983-136">Extracting the token</span></span>
<span data-ttu-id="e3983-137">A primeira etapa é extrair o token do cabeçalho de Autorização.</span><span class="sxs-lookup"><span data-stu-id="e3983-137">The first step is to extract the token from the Authorization header.</span></span> <span data-ttu-id="e3983-138">O valor do cabeçalho deve ser formatado com o esquema de autorização `Bearer` , um espaço único e o token de autorização, conforme a [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span><span class="sxs-lookup"><span data-stu-id="e3983-138">The header value should be formatted with the `Bearer` authorization scheme, a single space and then the authorization token as per [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span></span> <span data-ttu-id="e3983-139">Infelizmente, há casos nos quais o esquema de autorização é omitido.</span><span class="sxs-lookup"><span data-stu-id="e3983-139">Unfortunately there are cases where the authorization scheme is omitted.</span></span> <span data-ttu-id="e3983-140">Para levar isso em conta durante a análise, dividimos o valor do cabeçalho em um espaço e selecionamos a última cadeia de caracteres da matriz de cadeias de caracteres retornada.</span><span class="sxs-lookup"><span data-stu-id="e3983-140">To account for this when parsing, we split the header value on a space and select the last string from the returned array of strings.</span></span> <span data-ttu-id="e3983-141">Isso fornece uma solução alternativa para cabeçalhos de autorização formatados incorretamente.</span><span class="sxs-lookup"><span data-stu-id="e3983-141">This provides a workaround for badly formatted authorization headers.</span></span>

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-the-validation-request"></a><span data-ttu-id="e3983-142">Realização da solicitação de validação</span><span class="sxs-lookup"><span data-stu-id="e3983-142">Making the validation request</span></span>
<span data-ttu-id="e3983-143">Após a obtenção do token de autorização, podemos fazer a solicitação para validar o token.</span><span class="sxs-lookup"><span data-stu-id="e3983-143">Once we have the authorization token, we can make the request to validate the token.</span></span> <span data-ttu-id="e3983-144">A RFC 7662 chama esse processo de introspecção e exige que você aplique `POST` a um formulário HTML para o recurso de introspecção.</span><span class="sxs-lookup"><span data-stu-id="e3983-144">RFC 7662 calls this process introspection and requires that you `POST` a HTML form to the introspection resource.</span></span> <span data-ttu-id="e3983-145">O formulário HTML deve conter pelo menos um par de chave/valor com a chave `token`.</span><span class="sxs-lookup"><span data-stu-id="e3983-145">The HTML form must at least contain a key/value pair with the key `token`.</span></span> <span data-ttu-id="e3983-146">Essa solicitação para o servidor de autorização também deve ser autenticada a fim de garantir que os clientes mal-intencionados não possam vasculhar os tokens válidos.</span><span class="sxs-lookup"><span data-stu-id="e3983-146">This request to the authorization server must also be authenticated to ensure that malicious clients cannot go trawling for valid tokens.</span></span>

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

### <a name="checking-the-response"></a><span data-ttu-id="e3983-147">Verificação da resposta</span><span class="sxs-lookup"><span data-stu-id="e3983-147">Checking the response</span></span>
<span data-ttu-id="e3983-148">O atributo `response-variable-name` é usado para dar acesso à resposta retornada.</span><span class="sxs-lookup"><span data-stu-id="e3983-148">The `response-variable-name` attribute is used to give access the returned response.</span></span> <span data-ttu-id="e3983-149">O nome definido nessa propriedade pode ser usado como uma chave para o dicionário `context.Variables` a fim de acessar o objeto `IResponse`.</span><span class="sxs-lookup"><span data-stu-id="e3983-149">The name defined in this property can be used as a key into the `context.Variables` dictionary to access the `IResponse` object.</span></span>

<span data-ttu-id="e3983-150">Do objeto de resposta, podemos recuperar o corpo e a RFC 7622 nos informa de que a resposta deve ser um objeto JSON e deve conter pelo menos uma propriedade chamada `active` , que é um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="e3983-150">From the response object we can retrieve the body and RFC 7622 tells us that the response must be a JSON object and must contain at least a property called `active` that is a boolean value.</span></span> <span data-ttu-id="e3983-151">Quando `active` é verdadeiro, o token é considerado válido.</span><span class="sxs-lookup"><span data-stu-id="e3983-151">When `active` is true then the token is considered valid.</span></span>

### <a name="reporting-failure"></a><span data-ttu-id="e3983-152">Indicação de falha</span><span class="sxs-lookup"><span data-stu-id="e3983-152">Reporting failure</span></span>
<span data-ttu-id="e3983-153">Usamos uma política `<choose>` para detectar se o token é inválido e, em caso positivo, retornar uma resposta 401.</span><span class="sxs-lookup"><span data-stu-id="e3983-153">We use a `<choose>` policy to detect if the token is invalid and if so, return a 401 response.</span></span>

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

<span data-ttu-id="e3983-154">Conforme a [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3), que descreve como os tokens `bearer` devem ser usados, também retornamos um cabeçalho `WWW-Authenticate` com a resposta 401.</span><span class="sxs-lookup"><span data-stu-id="e3983-154">As per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) which describes how `bearer` tokens should be used, we also return a `WWW-Authenticate` header with the 401 response.</span></span> <span data-ttu-id="e3983-155">O WWW-Authenticate tem como intenção instruir um cliente sobre como construir uma solicitação devidamente autorizada.</span><span class="sxs-lookup"><span data-stu-id="e3983-155">The WWW-Authenticate is intended to instruct a client on how to construct a properly authorized request.</span></span> <span data-ttu-id="e3983-156">Devido à ampla variedade de abordagens possíveis com a estrutura OAuth2, é difícil comunicar todas as informações necessárias.</span><span class="sxs-lookup"><span data-stu-id="e3983-156">Due to the wide variety of approaches possible with the OAuth2 framework, it is difficult to communicate all the needed information.</span></span> <span data-ttu-id="e3983-157">Felizmente, há esforços sendo realizados para ajudar os [clientes a descobrirem como autorizar corretamente as solicitações para um servidor de recursos](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span><span class="sxs-lookup"><span data-stu-id="e3983-157">Fortunately there are efforts underway to help [clients discover how to properly authorize requests to a resource server](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span></span>

### <a name="final-solution"></a><span data-ttu-id="e3983-158">Solução final</span><span class="sxs-lookup"><span data-stu-id="e3983-158">Final solution</span></span>
<span data-ttu-id="e3983-159">Juntando todas as peças, temos a seguinte política:</span><span class="sxs-lookup"><span data-stu-id="e3983-159">Putting all the pieces together, we get the following policy:</span></span>

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

<span data-ttu-id="e3983-160">Este é apenas um dos muitos exemplos de como a política `send-request` pode ser usada para integrar serviços externos úteis ao processo de solicitações e respostas que fluem pelo serviço Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="e3983-160">This is only one of many examples of how the `send-request` policy can be used to integrate useful external services into the process of requests and responses flowing through the API Management service.</span></span>

## <a name="response-composition"></a><span data-ttu-id="e3983-161">Composição da resposta</span><span class="sxs-lookup"><span data-stu-id="e3983-161">Response Composition</span></span>
<span data-ttu-id="e3983-162">A política `send-request` pode ser usada para melhorar a uma solicitação primária para um sistema back-end, como vimos no exemplo anterior, ou pode ser usada como uma substituição completa para a chamada back-end.</span><span class="sxs-lookup"><span data-stu-id="e3983-162">The `send-request` policy can be used for enhancing a primary request to a backend system, as we saw in the previous example, or it can be used as a complete replace for of the backend call.</span></span> <span data-ttu-id="e3983-163">Com essa técnica podemos criar facilmente recursos de composição agregados de vários sistemas diferentes.</span><span class="sxs-lookup"><span data-stu-id="e3983-163">Using this technique we can easily create composite resources that are aggregated from multiple different systems.</span></span>

### <a name="building-a-dashboard"></a><span data-ttu-id="e3983-164">Criando um painel</span><span class="sxs-lookup"><span data-stu-id="e3983-164">Building a dashboard</span></span>
<span data-ttu-id="e3983-165">Às vezes, você quer expor as informações existentes em vários sistemas de back-end, por exemplo, para gerar um painel.</span><span class="sxs-lookup"><span data-stu-id="e3983-165">Sometimes you want to be able to expose information that exists in multiple backend systems, for example, to drive a dashboard.</span></span> <span data-ttu-id="e3983-166">Os KPIs vêm de todos os back-ends diferentes, mas convém não fornecer acesso direto a eles, e seria bom se todas as informações pudessem ser recuperadas em uma única solicitação.</span><span class="sxs-lookup"><span data-stu-id="e3983-166">The KPIs come from all different back-ends, but you would prefer not to provide direct access to them and it would be nice if all the information could be retrieved in a single request.</span></span> <span data-ttu-id="e3983-167">Talvez algumas informações de back-end precisem de um pouco de organização e uma pequena limpeza primeiro!</span><span class="sxs-lookup"><span data-stu-id="e3983-167">Perhaps some of the backend information needs some slicing and dicing and a little sanitizing first!</span></span> <span data-ttu-id="e3983-168">Ser capaz de armazenar em cache o recurso composto é útil para reduzir a carga back-end, pois você sabe que os usuários têm o hábito de pressionar sem parar a tecla F5 para ver se suas métricas com baixo desempenho mudam.</span><span class="sxs-lookup"><span data-stu-id="e3983-168">Being able to cache that composite resource would be a useful to reduce the backend load as you know users have a habit of hammering the F5 key in order to see if their underperforming metrics might change.</span></span>    

### <a name="faking-the-resource"></a><span data-ttu-id="e3983-169">Falsificando o recurso</span><span class="sxs-lookup"><span data-stu-id="e3983-169">Faking the resource</span></span>
<span data-ttu-id="e3983-170">A primeira etapa da construção de nosso recurso de painel é configurar uma nova operação no portal de editor do Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="e3983-170">The first step to building our dashboard resource is to configure a new operation in the API Management publisher portal.</span></span> <span data-ttu-id="e3983-171">Essa será uma operação de espaço reservado usada para configurar nossa política de composição a fim de criar nosso recurso dinâmico.</span><span class="sxs-lookup"><span data-stu-id="e3983-171">This will be a placeholder operation used to configure our composition policy to build our dynamic resource.</span></span>

![Operação de painel](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-the-requests"></a><span data-ttu-id="e3983-173">Fazendo as solicitações</span><span class="sxs-lookup"><span data-stu-id="e3983-173">Making the requests</span></span>
<span data-ttu-id="e3983-174">Após a criação da operação `dashboard` , podemos configurar uma política especificamente para essa operação.</span><span class="sxs-lookup"><span data-stu-id="e3983-174">Once the `dashboard` operation has been created we can configure a policy specifically for that operation.</span></span> 

![Operação de painel](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

<span data-ttu-id="e3983-176">A primeira etapa é extrair parâmetros de consulta da solicitação de entrada, para que possamos encaminhá-los ao nosso back-end.</span><span class="sxs-lookup"><span data-stu-id="e3983-176">The first step  is to extract any query parameters from the incoming request, so that we can forward them to our backend.</span></span> <span data-ttu-id="e3983-177">Neste exemplo, nosso painel está mostrando informações baseadas em um período; portanto, ele apresenta os parâmetros `fromDate` e `toDate`.</span><span class="sxs-lookup"><span data-stu-id="e3983-177">In this example our dashboard is showing information based on a period of time an therefore has a `fromDate` and `toDate` parameter.</span></span> <span data-ttu-id="e3983-178">Podemos usar a política `set-variable` para extrair as informações da URL de solicitação.</span><span class="sxs-lookup"><span data-stu-id="e3983-178">We can use the `set-variable` policy to extract the information from the request URL.</span></span>

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

<span data-ttu-id="e3983-179">Assim que tivermos essas informações poderemos fazer solicitações para todos os sistemas back-end.</span><span class="sxs-lookup"><span data-stu-id="e3983-179">Once we have this information we can make requests to all the backend systems.</span></span> <span data-ttu-id="e3983-180">Cada solicitação constrói uma nova URL com as informações de parâmetro, chama seu respectivo servidor e armazena a resposta em uma variável de contexto.</span><span class="sxs-lookup"><span data-stu-id="e3983-180">Each request constructs a new URL with the parameter information and calls its respective server and stores the response in a context variable.</span></span>

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

<span data-ttu-id="e3983-181">Essas solicitações serão executadas em sequência, o que não é ideal.</span><span class="sxs-lookup"><span data-stu-id="e3983-181">These requests will execute in sequence, which is not ideal.</span></span> <span data-ttu-id="e3983-182">Em uma versão futura apresentaremos uma nova política chamada `wait` , que permitirá a execução em paralelo de todas essas solicitações.</span><span class="sxs-lookup"><span data-stu-id="e3983-182">In an upcoming release we will be introducing a new policy called `wait` that will enable all of these requests to execute in parallel.</span></span>

### <a name="responding"></a><span data-ttu-id="e3983-183">Respondendo</span><span class="sxs-lookup"><span data-stu-id="e3983-183">Responding</span></span>
<span data-ttu-id="e3983-184">Para construir a resposta composta, podemos usar a política [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) .</span><span class="sxs-lookup"><span data-stu-id="e3983-184">To construct the composite response we can use the [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policy.</span></span> <span data-ttu-id="e3983-185">O elemento `set-body` pode usar uma expressão para construir um novo `JObject` com todas as representações de componente incorporadas como propriedades.</span><span class="sxs-lookup"><span data-stu-id="e3983-185">The `set-body` element can use an expression to construct a new `JObject` with all the component representations embedded as properties.</span></span>

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

<span data-ttu-id="e3983-186">A política completa tem a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="e3983-186">The complete policy looks as follows:</span></span>

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

<span data-ttu-id="e3983-187">Na configuração da operação de espaço reservado podemos configurar o recurso de painel para ser armazenado em cache durante pelo menos uma hora, pois entendemos que a natureza dos dados significa que mesmo se estiver uma hora desatualizado, ainda será suficientemente eficaz para transmitir as informações valiosas aos usuários.</span><span class="sxs-lookup"><span data-stu-id="e3983-187">In the configuration of the placeholder operation we can configure the dashboard resource to be cached for at least an hour because we understand the nature of the data means that even if it is an hour out of date, it will still be sufficiently effective to convey valuable information to the users.</span></span>

## <a name="summary"></a><span data-ttu-id="e3983-188">Resumo</span><span class="sxs-lookup"><span data-stu-id="e3983-188">Summary</span></span>
<span data-ttu-id="e3983-189">O serviço de Gerenciamento de API do Azure fornece políticas flexíveis que podem ser aplicadas seletivamente ao tráfego HTTP e permite a composição de serviços back-end.</span><span class="sxs-lookup"><span data-stu-id="e3983-189">Azure API Management service provides flexible policies that can be selectively applied to HTTP traffic and enables composition of backend services.</span></span> <span data-ttu-id="e3983-190">Se você quiser aprimorar seu gateway de API com funções de alerta, verificação e recursos de validação, ou criar novos recursos compostos baseados em vários serviços back-end, a política `send-request` e as políticas relacionadas abrirão um mundo de oportunidades.</span><span class="sxs-lookup"><span data-stu-id="e3983-190">Whether you want to enhance your API gateway with alerting functions, verification, validation capabilities or create new composite resources based on multiple backend services, the `send-request` and related policies open a world of possibilities.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="e3983-191">Assista a uma visão geral dessas políticas em vídeo</span><span class="sxs-lookup"><span data-stu-id="e3983-191">Watch a video overview of these policies</span></span>
<span data-ttu-id="e3983-192">Para obter mais informações sobre as políticas [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) e [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) abordadas neste artigo, assista ao vídeo a seguir.</span><span class="sxs-lookup"><span data-stu-id="e3983-192">For more information on the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), and [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policies covered in this article, please watch the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

