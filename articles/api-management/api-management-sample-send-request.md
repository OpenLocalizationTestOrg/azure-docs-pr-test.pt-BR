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
# <a name="using-external-services-from-hello-azure-api-management-service"></a>Usando os serviços externos de saudação serviço de gerenciamento de API do Azure
políticas de saudação disponíveis no serviço de gerenciamento de API do Azure podem fazer uma ampla gama de trabalho útil com base puramente na solicitação de entrada hello, resposta de saída de hello e informações de configuração básica. No entanto, as políticas sendo capaz de toointeract com serviços externos do gerenciamento de API abre muitos mais oportunidades.

Anteriormente, vimos como podemos podem interagir com hello [serviço de Hub de eventos do Azure para registro em log, monitoramento e análise](api-management-log-to-eventhub-sample.md). Neste artigo, tentaremos demonstrar serviço baseado em políticas que permitem que você toointeract com qualquer HTTP externo. Essas políticas podem ser usadas para disparar eventos remotos ou para recuperar as informações que serão solicitação original do toomanipulate usado hello e resposta de alguma forma.

## <a name="send-one-way-request"></a>Send-One-Way-Request
Possivelmente hello interação externa mais simples é Olá disparar e esquecer de solicitação que permite que um toobe de serviço externo notificado de algum tipo de evento importante. Podemos usar política de fluxo de controle Olá `choose` toodetect qualquer tipo de condição que estão interessados e, em seguida, se hello condição for atendida, o que podemos fazer uma solicitação HTTP externa usando Olá [send-uma maneira solicitação](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) política. Isso pode ser um tooa de solicitação de mensagens de sistema, como Hipchat ou atraso ou um email de API como SendGrid ou MailChimp, ou para incidentes de suporte crítico algo parecido com PagerDuty. Todos esses sistemas de mensagens têm APIs HTTP simples que podemos facilmente invocar.

### <a name="alerting-with-slack"></a>Alertas com Slack
saudação de exemplo a seguir demonstra como toosend tooa uma mensagem atraso salas de chat, se o código de status de resposta HTTP Olá é maior que ou igual a too500. Um erro de intervalo de 500 indica um problema com nosso API de back-end que Olá cliente da nossa API não pode ser resolvidos sozinhos. Isso geralmente exige algum tipo de intervenção de nossa parte.  

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

Margem de atraso tem noção de saudação de conexões de entrada da web. Ao configurar um gancho da web de entrada, o atraso gera uma URL especial que permite que você toodo uma solicitação POST simple e toopass uma mensagem em canal de margem de atraso de saudação. Olá corpo JSON que criamos baseia-se em um formato definido pela margem de atraso.

![Gancho da Web do Slack](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a>O método "disparar e esquecer" é o suficiente?
Há certas compensações ao usar um estilo de solicitação "disparar e esquecer". Se por algum motivo, Olá solicitação falhará e falha de saudação não será reportada. Nessa situação específica, complexidade de saudação de ter um sistema de relatórios de falhas secundário e o custo de desempenho adicionais de saudação de aguardando resposta Olá não está garantida. Para cenários em que é essencial toocheck resposta de hello, em seguida, Olá [solicitação de envio](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) política é uma opção melhor.

## <a name="send-request"></a>send-request
Olá `send-request` política permite usar um tooperform de serviço externo complexo de funções e serviço de gerenciamento de toohello API retorna dados que pode ser usado para processamento adicional de diretiva de processamento.

### <a name="authorizing-reference-tokens"></a>Autorizando tokens de referência
Uma função importante do Gerenciamento de API é proteger os recursos de back-end. Se o servidor de autorização Olá usado pela sua API cria [tokens JWT](http://jwt.io/) como parte de seu fluxo de OAuth2, como [Active Directory do Azure](../active-directory/active-directory-aadconnect.md) faz, em seguida, você pode usar o hello `validate-jwt` validade de saudação tooverify política do token de saudação. No entanto, alguns servidores de autorização criam o que chamamos de [referência tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) que não pode ser verificada sem fazer um servidor de autorização de toohello de retorno de chamada.

### <a name="standardized-introspection"></a>Introspecção padronizada
Olá passado não tem havido nenhuma maneira padronizada de verificar um token de referência com um servidor de autorização. No entanto um padrão proposto recentemente [7662 RFC](https://tools.ietf.org/html/rfc7662) foi publicada por Olá IETF que define como um servidor de recurso pode verificar a validade de saudação de um token.

### <a name="extracting-hello-token"></a>Extraindo o token Olá
Olá primeira etapa é tooextract token de saudação do cabeçalho de autorização de saudação. valor de cabeçalho Olá deve ser formatado com hello `Bearer` esquema de autorização, um único espaço e, em seguida, autorização de saudação do token de acordo [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1). Infelizmente, há casos em que o esquema de autorização de saudação for omitida. tooaccount para isso durante a análise, podemos dividir o valor do cabeçalho Olá em um espaço e a última cadeia de caracteres de saudação selecione de hello retornada a matriz de cadeias de caracteres. Isso fornece uma solução alternativa para cabeçalhos de autorização formatados incorretamente.

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-hello-validation-request"></a>Fazer a solicitação de validação de saudação
Assim que tivermos o token de autorização hello, podemos Olá solicitação toovalidate Olá token. RFC 7662 chama introspecção esse processo e requer que você `POST` um recurso de introspecção de toohello de formulário HTML. saudação do formulário HTML deve conter pelo menos um par chave/valor com chave Olá `token`. Esse servidor de autorização toohello solicitação também deve ser autenticado tooensure que não é possível ir trawling clientes mal-intencionado para tokens válidos.

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

### <a name="checking-hello-response"></a>Verificação de resposta de saudação
Olá `response-variable-name` atributo é usado toogive Olá de acesso retornada uma resposta. Olá nome definido na propriedade pode ser usado como uma chave no hello `context.Variables` saudação do dicionário tooaccess `IResponse` objeto.

Do objeto de resposta Olá podemos recuperar corpo hello e RFC 7622 informa que a resposta de saudação deve ser um objeto JSON e deve conter pelo menos uma propriedade chamada `active` que é um valor booleano. Quando `active` for true, o token de saudação é considerado válido.

### <a name="reporting-failure"></a>Indicação de falha
Usamos uma `<choose>` toodetect de política se Olá token é inválido e nesse caso, retornar uma resposta 401.

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

Como por [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) que descreve como `bearer` tokens devem ser usados, podemos também retornar um `WWW-Authenticate` cabeçalho de resposta Olá 401. Olá WWW-Authenticate é pretendido tooinstruct um cliente sobre como tooconstruct uma solicitação autorizada corretamente. Devido a ampla variedade de abordagens possíveis com o framework Olá OAuth2 toohello, é difícil toocommunicate todos Olá necessárias informações. Felizmente, há esforços em andamento toohelp [clientes descobrir como tooproperly autorizar o servidor de recurso solicitações tooa](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).

### <a name="final-solution"></a>Solução final
Reunir todas as partes da saudação, obtemos Olá diretiva a seguir:

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

Isso é apenas um dos vários exemplos de como Olá `send-request` política pode ser serviços externos útil de toointegrate usado no processo de saudação de solicitações e respostas que passam por Olá serviço de gerenciamento de API.

## <a name="response-composition"></a>Composição da resposta
Olá `send-request` política pode ser usada para melhorar a um sistema de back-end de tooa solicitação primária, conforme vimos no exemplo anterior hello, ou ele pode ser usado como uma substituição completa para chamada de back-end de saudação. Com essa técnica podemos criar facilmente recursos de composição agregados de vários sistemas diferentes.

### <a name="building-a-dashboard"></a>Criando um painel
Às vezes, você deseja toobe tooexpose capaz de informações que existe em vários sistemas de back-end, por exemplo, toodrive um painel. Olá KPIs vêm de todos os diferentes back-ends, mas você prefere que não as toothem tooprovide acesso direto e seria interessante se todas as informações de saudação podem ser recuperadas em uma única solicitação. Talvez algumas das informações de back-end Olá precisa de alguns divisão e repartir um pouco de limpeza e primeiro! Olá back-end seja capaz de toocache que o recurso de composição seria um tooreduce útil carregar como você sabe que os usuários têm o hábito de anti-hammering a tecla F5 de saudação em ordem toosee se suas métricas com baixo desempenho podem ser alterado.    

### <a name="faking-hello-resource"></a>Recurso de Olá falsificação
Olá primeiro toobuilding de etapa nosso recurso de painel é tooconfigure uma nova operação no portal do publicador de gerenciamento de API de saudação. Isso será um tooconfigure da operação usada de espaço reservado nosso toobuild de política de composição nosso recurso dinâmico.

![Operação de painel](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-hello-requests"></a>Fazendo solicitações Olá
Uma vez Olá `dashboard` operação tiver sido criada, pode configurar uma política especificamente para essa operação. 

![Operação de painel](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

primeira etapa de saudação é tooextract os parâmetros de consulta de solicitação de entrada hello, de forma que podemos pode encaminhar tooour back-end. Neste exemplo, nosso painel está mostrando informações baseadas em um período; portanto, ele apresenta os parâmetros `fromDate` e `toDate`. Podemos usar o hello `set-variable` informações de URL de solicitação Olá Olá de tooextract de diretiva.

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

Essas informações se houver podemos solicitações tooall sistemas de back-end de saudação. Cada solicitação constrói uma nova URL com informações de parâmetro hello e chama seu respectivo servidor e armazena a resposta de saudação em uma variável de contexto.

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

Essas solicitações serão executadas em sequência, o que não é ideal. Em uma versão futura apresentaremos uma nova política chamada `wait` permitir que todos esses tooexecute solicitações em paralelo.

### <a name="responding"></a>Respondendo
resposta composto de saudação tooconstruct usamos Olá [resposta de retorno](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) política. Olá `set-body` elemento pode usar uma expressão tooconstruct um novo `JObject` com todas as representações de componente Olá inseridas como propriedades.

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

diretiva completa Olá será semelhante ao seguinte:

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

Na configuração de saudação da operação de espaço reservado de saudação que podemos configurar Olá painel recursos toobe armazenado em cache pelo menos uma hora como compreendemos natureza Olá dados saudação significa que, mesmo se houver uma hora desatualizada, que ele ainda estará suficientemente eficaz usuários que toohello tooconvey informações valiosas.

## <a name="summary"></a>Resumo
Serviço de gerenciamento de API do Azure fornece políticas flexíveis que podem ser seletivamente aplicadas tooHTTP tráfego e permite a composição de serviços back-end. Se você deseja tooenhance seu gateway de API com funções, recursos de validação e verificação de alerta ou cria novos recursos de composição, com base em vários serviços de back-end, Olá `send-request` e políticas relacionadas abrem um mundo de possibilidades.

## <a name="watch-a-video-overview-of-these-policies"></a>Assista a uma visão geral dessas políticas em vídeo
Para obter mais informações sobre Olá [send-uma maneira solicitação](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [solicitação de envio](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), e [resposta de retorno](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) políticas abordadas neste artigo, assista Olá vídeo a seguir.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

