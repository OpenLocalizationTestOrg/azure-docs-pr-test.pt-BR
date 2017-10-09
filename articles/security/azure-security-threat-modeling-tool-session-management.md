---
title: "aaaSession de gerenciamento - ferramenta de modelagem de ameaça Microsoft - Azure | Microsoft Docs"
description: "reduções de ameaças expostas em Olá, ferramenta de modelagem de ameaça"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 915ffae3f775ca6902fcfb93e7e1952ce85612f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-session-management--articles"></a>Quadro de segurança: Gerenciamento de sessão | Artigos 
| Produto/Serviço | Artigo |
| --------------- | ------- |
| **Azure AD**    | <ul><li>[Implementar o logoff apropriado usando métodos ADAL ao usar o Azure AD](#logout-adal)</li></ul> |
| Dispositivo IoT | <ul><li>[Usar tempos de vida finitos para tokens SaS gerados](#finite-tokens)</li></ul> |
| **Azure DocumentDB** | <ul><li>[Usar tempos de vida mínimos de tokens para tokens de Recurso gerados](#resource-tokens)</li></ul> |
| **ADFS** | <ul><li>[Implementar o logoff apropriado usando métodos WsFederation ao usar o ADFS](#wsfederation-logout)</li></ul> |
| **Identity Server** | <ul><li>[Implementar o logoff adequado ao usar o Servidor de identidade](#proper-logout)</li></ul> |
| **Aplicativo Web** | <ul><li>[Os aplicativos disponíveis via HTTPS devem usar cookies seguros](#https-secure-cookies)</li><li>[Todo aplicativo baseado em http deve especificar http somente para definição de cookie](#cookie-definition)</li><li>[Atenuar ataques CSRF (solicitação intersite forjada) em páginas Web ASP.NET](#csrf-asp)</li><li>[Configurar sessão para tempo de vida de inatividade](#inactivity-lifetime)</li><li>[Implementar o logout adequado do aplicativo hello](#proper-app-logout)</li></ul> |
| **API da Web** | <ul><li>[Atenuar ataques CSRF (solicitação intersite forjada) em APIs da Web ASP.NET](#csrf-api)</li></ul> |

## <a id="logout-adal"></a>Implementar o logoff apropriado usando métodos ADAL ao usar o Azure AD

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | AD do Azure | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Se o aplicativo hello depende de token de acesso emitido pelo AD do Azure, o manipulador de eventos de logoff de saudação deve chamar |

### <a name="example"></a>Exemplo
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a>Exemplo
Também deve destruir a sessão do usuário chamando o método Session.Abandon(). O método a seguir mostra a implementação segura do logoff do usuário:
```C#
    [HttpPost]
        [ValidateAntiForgeryToken]
        public void LogOff()
        {
            string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            AuthenticationContext authContext = new AuthenticationContext(Authority + TenantId, new NaiveSessionCache(userObjectID));
            authContext.TokenCache.Clear();
            Session.Clear();
            Session.Abandon();
            Response.SetCookie(new HttpCookie("ASP.NET_SessionId", string.Empty));
            HttpContext.GetOwinContext().Authentication.SignOut(
                OpenIdConnectAuthenticationDefaults.AuthenticationType,
                CookieAuthenticationDefaults.AuthenticationType);
        } 
```

## <a id="finite-tokens"></a>Usar tempos de vida finitos para tokens SaS gerados

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Dispositivo IoT | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Tokens SaS gerados para autenticar tooAzure IoT Hub devem ter um período de expiração Finitas. Manter Olá SaS tempos de vida de token tooa toolimit mínimo Olá quantidade de tempo que podem ser reproduzidos no caso de tokens de saudação sejam comprometidos.|

## <a id="resource-tokens"></a>Usar tempos de vida mínimos de tokens para tokens de Recurso gerados

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Azure Document DB | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Reduza o timespan de saudação do valor mínimo de tooa token de recurso necessário. Tokens de recurso têm um intervalo de tempo válido padrão de uma hora.|

## <a id="wsfederation-logout"></a>Implementar o logoff apropriado usando métodos WsFederation ao usar o ADFS

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | ADFS | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Se o aplicativo hello depende de token do STS emitido pelo ADFS, manipulador de eventos de logout Olá deve chamar WSFederationAuthenticationModule.FederatedSignOut() método toolog usuário hello. Também hello atual sessão deve ser destruída, e o valor do token de sessão Olá deve ser redefinido e inúteis.|

### <a name="example"></a>Exemplo
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes hello user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at hello specified security token service (STS) by using hello WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of hello current session and raises hello appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at hello specified security token service (STS) by using hello WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <a id="proper-logout"></a>Implementar o logoff adequado ao usar o Servidor de identidade

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Servidor de Identidade | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Saída do IdentityServer3-Federated](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| **Etapas** | IdentityServer oferece suporte a saudação capacidade toofederate com provedores de identidade externa. Quando um usuário sai de um provedor de identidade upstream, dependendo do protocolo de saudação usado, talvez seja possível tooreceive uma notificação quando Olá usuário sai. Ele permite toonotify IdentityServer seus clientes para que eles também podem entrar Olá usuário out. Verifique a documentação na seção de referências de saudação para obter detalhes de implementação Olá Olá.|

## <a id="https-secure-cookies"></a>Os aplicativos disponíveis via HTTPS devem usar cookies seguros

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | EnvironmentType - OnPrem |
| **Referências**              | [httpCookies Element (Esquema de configurações ASP.NET)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [Propriedade HttpCookie.Secure](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx) |
| **Etapas** | Os cookies são normalmente apenas domínio toohello acessível para o qual eles foram escopo. Infelizmente, definição de saudação do "domínio" não inclui protocolo Olá para que cookies que são criados por HTTPS são acessíveis por meio de HTTP. atributo "segura" Hello indica que o navegador toohello Olá cookie deve apenas ser disponibilizada via HTTPS. Verifique se todos os cookies definido por HTTPS usam Olá **segura** atributo. requisito de saudação pode ser imposto no arquivo Web. config de saudação definindo Olá requireSSL atributo tootrue. É Olá preferencial abordagem porque ele aplicará Olá **segura** atributo para todos os cookies atuais e futuros sem Olá necessidade toomake as alterações de código adicional.|

### <a name="example"></a>Exemplo
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
configuração de saudação é imposta mesmo que o HTTP é usado tooaccess Olá aplicativo. Se o HTTP é usado tooaccess Olá aplicativo, quebras de configuração aplicativo hello porque cookies Olá são definidos com navegador seguro de atributo e Olá Olá não enviará-los hello volta toohello aplicativo.

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Web Forms, MVC5 |
| **Atributos**              | EnvironmentType - OnPrem |
| **Referências**              | N/D  |
| **Etapas** | Quando Olá web aplicativo hello terceira parte confiável, e Olá IdP servidor ADFS, atributo de segurança do token de FedAuth Olá pode ser configurado por definindo o requireSSL tooTrue em `system.identityModel.services` seção de Web. config:|

### <a name="example"></a>Exemplo
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <a id="cookie-definition"></a>Todo aplicativo baseado em http deve especificar http somente para definição de cookie

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Atributo Secure Cookie](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| **Etapas** | toomitigate o risco de saudação de divulgação de informações com um ataque de script entre sites (XSS), um novo atributo - httpOnly - foi introduzido toocookies e é suportado por todos os principais navegadores. atributo de saudação especifica que um cookie não é acessível por meio de script. Usando cookies HttpOnly, um aplicativo web reduz a possibilidade de saudação que informações confidenciais contidas no cookie de saudação seja roubadas por meio de script e enviadas site tooan invasor. |

### <a name="example"></a>Exemplo
Todos os aplicativos com base em HTTP que usam cookies devem especificar HttpOnly na definição de cookie hello, Implementando a seguinte configuração no Web. config:
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Formulários da Web |
| **Atributos**              | N/D  |
| **Referências**              | [Propriedade FormsAuthentication.RequireSSL](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| **Etapas** | Olá RequireSSL valor da propriedade é definida no arquivo de configuração de saudação para um aplicativo ASP.NET usando o atributo requireSSL de saudação do elemento de configuração de saudação. Você pode especificar no arquivo Web. config de saudação para seu aplicativo ASP.NET se SSL (Secure Sockets Layer) é servidor de toohello de cookie tooreturn necessário Olá autenticação de formulários ao definir atributo de requireSSL hello.|

### <a name="example"></a>Exemplo 
Olá exemplo de código a seguir define Olá requireSSL atributo no arquivo Web. config de saudação.
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | MVC5 |
| **Atributos**              | EnvironmentType - OnPrem |
| **Referências**              | [Configuração do Windows Identity Foundation (WIF) – Part II](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) |
| **Etapas** | atributo de httpOnly tooset cookies FedAuth, o valor do atributo hideFromCsript deve ser definido tooTrue. |

### <a name="example"></a>Exemplo
Configuração a seguir mostra a configuração correta de saudação:
```XML
<federatedAuthentication>
<cookieHandler mode="Custom"
                       hideFromScript="true"
                       name="FedAuth"
                       path="/"
                       requireSsl="true"
                       persistentSessionLifetime="25">
</cookieHandler>
</federatedAuthentication>
```

## <a id="csrf-asp"></a>Atenuar ataques CSRF (solicitação intersite forjada) em páginas Web ASP.NET

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Falsificação de solicitação entre sites (CSRF ou XSRF) é um tipo de ataque em que um invasor pode realizar ações no contexto de segurança de saudação da sessão de um usuário diferente estabelecida em um site da web. meta de saudação é toomodify ou excluir o conteúdo, se o site de destino-Olá se basear exclusivamente em cookies de sessão tooauthenticate solicitação recebida. Um invasor pode explorar essa vulnerabilidade obtendo tooload do navegador de um usuário diferente uma URL com um comando de um site vulnerável no qual usuário Olá já estiver conectado. Há várias maneiras para um toodo invasor que, como hospedar um site diferente que carrega um recurso de servidor vulnerável hello, ou tooclick de usuário Olá obtendo um link. ataque de saudação pode ser evitado se o servidor de saudação envia um cliente toohello token adicionais, requer Olá cliente tooinclude esse token em todas as solicitações futuras e verifica se todas as solicitações futuras incluem um token que pertence toohello sessão atual, como por usando Olá AntiForgeryToken ASP.NET ou ViewState. |

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | MVC5, MVC6 |
| **Atributos**              | N/D  |
| **Referências**              | [Prevenção de XSRF/CSRF no ASP.NET MVC e páginas Web](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) |
| **Etapas** | Formulários de anti-CSRF e ASP.NET MVC - Olá Use `AntiForgeryToken` método auxiliar em exibições; coloque um `Html.AntiForgeryToken()` em formulário hello, por exemplo,|

### <a name="example"></a>Exemplo
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a>Exemplo
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a>Exemplo
A saudação mesmo momento, visitante de saudação do Html.AntiForgeryToken() oferece um cookie chamado __RequestVerificationToken, com o mesmo valor como valor oculto aleatório Olá mostrado acima de saudação. Em seguida, toovalidate uma postagem de formulário de entrada, adicione o método de ação do hello [ValidateAntiForgeryToken] filtro toohello destino. Por exemplo:
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
Filtro de autorização que verifica se:
* solicitação de entrada Hello tem um cookie chamado __RequestVerificationToken
* Olá solicitação de entrada tem um `Request.Form` entrada chamada __RequestVerificationToken
* Esses cookies e `Request.Form` correspondência de valores, supondo que todas as é bem, Olá solicitação passa por como normal. Mas, se não estiver, uma falha de autorização com a mensagem "Um token antifalsificação necessário não foi fornecido ou era inválido". 

### <a name="example"></a>Exemplo
Anti-CSRF e AJAX: token de formulário de saudação pode ser um problema para solicitações do AJAX, porque uma solicitação AJAX pode enviar dados JSON, não os dados de formulário HTML. Uma solução é tokens de saudação do toosend em um cabeçalho HTTP personalizado. Hello código a seguir usa os tokens de saudação do Razor sintaxe toogenerate e, em seguida, adiciona Olá tokens tooan AJAX solicitação. 
```C#
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }

    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a>Exemplo
Ao processar solicitação Olá, extrai tokens de saudação do cabeçalho de solicitação de saudação. Chame Olá AntiForgery.Validate método toovalidate tokens de saudação. Olá método Validate lança uma exceção se os tokens de saudação não são válidos.
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Formulários da Web |
| **Atributos**              | N/D  |
| **Referências**              | [Tirar proveito dos recursos internos do ASP.NET tooFend Off ataques de Web](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| **Etapas** | Ataques CSRF em aplicativos de formulário da Web com base podem ser atenuadas definindo ViewStateUserKey tooa cadeia de caracteres aleatória que varia para cada usuário - ID de usuário ou, melhor ainda, ID de sessão. Por diversos motivos técnicos e sociais, ID de sessão é uma opção bem melhor, pois é imprevisível, atinge um tempo limite e varia de acordo com o usuário.|

### <a name="example"></a>Exemplo
Aqui está o código de saudação necessário toohave em todas as páginas:
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <a id="inactivity-lifetime"></a>Configurar sessão para tempo de vida de inatividade

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | [Propriedade HttpSessionState.Timeout](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx) |
| **Etapas** | Tempo limite da sessão representa Olá eventos que ocorrem quando um usuário não executará qualquer ação em um site da web durante um intervalo (definido pelo servidor web). Olá evento no lado do servidor, altere o status de saudação do hello too'invalid de sessão de usuário ' (por exemplo "não usado mais") e instruir Olá web server toodestroy-lo (excluindo todos os dados contidos nele). Hello exemplo de código a seguir define Olá tempo limite sessão atributo too15 minutos no arquivo Web. config de saudação.|

### <a name="example"></a>Exemplo
```código XML <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Formulários da Web |
| **Atributos**              | N/D  |
| **Referências**              | [Elemento forms para autenticação (Esquema de configuração ASP.NET)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx) |
| **Etapas** | Definir minutos Olá too15 de tempo limite de cookie do tíquete de autenticação de formulários|

### <a name="example"></a>Exemplo
```código XML <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When hello web application is Relying Party and ADFS is hello STS, hello lifetime of hello authentication cookies - FedAuth tokens - can be set by hello following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use hello code below tooenable encryption-decryption of claims received from ADFS. Thumbprint value varies based on hello certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a>Exemplo
Também Olá ADFS emitido o tempo de vida do token de SAML declaração deve ser definido como too15 minutos, executando Olá comando do powershell no servidor ADFS Olá a seguir:
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <a id="proper-app-logout"></a>Implementar o logout adequado do aplicativo hello

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | Aplicativo Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Execute sair adequado do aplicativo hello, quando o usuário pressionar botão de logoff. Após o logoff, o aplicativo deve destruir a sessão do usuário e também redefinir e anular o valor do cookie de sessão, juntamente com a redefinição e anulação do valor do cookie de autenticação. Além disso, quando várias sessões estão empatados tooa identidade de usuário único, eles devem ser coletivamente terminados no lado do servidor de saudação no tempo limite ou logoff. Por fim, certifique-se de que a funcionalidade de Logoff esteja disponível em cada página. |

## <a id="csrf-api"></a>Atenuar ataques CSRF (solicitação intersite forjada) em APIs da Web ASP.NET

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | Genérico |
| **Atributos**              | N/D  |
| **Referências**              | N/D  |
| **Etapas** | Falsificação de solicitação entre sites (CSRF ou XSRF) é um tipo de ataque em que um invasor pode realizar ações no contexto de segurança de saudação da sessão de um usuário diferente estabelecida em um site da web. meta de saudação é toomodify ou excluir o conteúdo, se o site de destino-Olá se basear exclusivamente em cookies de sessão tooauthenticate solicitação recebida. Um invasor pode explorar essa vulnerabilidade obtendo tooload do navegador de um usuário diferente uma URL com um comando de um site vulnerável no qual usuário Olá já estiver conectado. Há várias maneiras para um toodo invasor que, como hospedar um site diferente que carrega um recurso de servidor vulnerável hello, ou tooclick de usuário Olá obtendo um link. ataque de saudação pode ser evitado se o servidor de saudação envia um cliente toohello token adicionais, requer Olá cliente tooinclude esse token em todas as solicitações futuras e verifica se todas as solicitações futuras incluem um token que pertence toohello sessão atual, como por usando Olá AntiForgeryToken ASP.NET ou ViewState. |

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | MVC5, MVC6 |
| **Atributos**              | N/D  |
| **Referências**              | [Impedir ataques CSRF (solicitação intersite forjada) em APIs da Web ASP.NET](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) |
| **Etapas** | Anti-CSRF e AJAX: token de formulário de saudação pode ser um problema para solicitações do AJAX, porque uma solicitação AJAX pode enviar dados JSON, não os dados de formulário HTML. Uma solução é tokens de saudação do toosend em um cabeçalho HTTP personalizado. Hello código a seguir usa os tokens de saudação do Razor sintaxe toogenerate e, em seguida, adiciona Olá tokens tooan AJAX solicitação. |

### <a name="example"></a>Exemplo
```Javascript
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }
    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a>Exemplo
Ao processar solicitação Olá, extrai tokens de saudação do cabeçalho de solicitação de saudação. Chame Olá AntiForgery.Validate método toovalidate tokens de saudação. Olá método Validate lança uma exceção se os tokens de saudação não são válidos.
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

### <a name="example"></a>Exemplo
Anti-CSRF e formulários do ASP.NET MVC - Olá Use método de auxiliar AntiForgeryToken em modos de exibição; colocar um Html.AntiForgeryToken() no formulário hello, por exemplo,
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a>Exemplo
exemplo Hello acima produzirá algo semelhante Olá seguinte:
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a>Exemplo
A saudação mesmo momento, visitante de saudação do Html.AntiForgeryToken() oferece um cookie chamado __RequestVerificationToken, com o mesmo valor como valor oculto aleatório Olá mostrado acima de saudação. Em seguida, toovalidate uma postagem de formulário de entrada, adicione o método de ação do hello [ValidateAntiForgeryToken] filtro toohello destino. Por exemplo:
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
Filtro de autorização que verifica se:
* solicitação de entrada Hello tem um cookie chamado __RequestVerificationToken
* Olá solicitação de entrada tem um `Request.Form` entrada chamada __RequestVerificationToken
* Esses cookies e `Request.Form` correspondência de valores, supondo que todas as é bem, Olá solicitação passa por como normal. Mas, se não estiver, uma falha de autorização com a mensagem "Um token antifalsificação necessário não foi fornecido ou era inválido".

| Title                   | Detalhes      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase do SDL**               | Compilação |  
| **Tecnologias aplicáveis** | MVC5, MVC6 |
| **Atributos**              | Provedor de Identidade - ADFS, Provedor de Identidade - Azure AD |
| **Referências**              | [Proteger uma API Web com contas individuais e logon local na API Web ASP.NET 2.2](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) |
| **Etapas** | Se Olá API da Web é protegido usando OAuth 2.0, em seguida, ele espera um token de portador na solicitação cabeçalho e concede acesso toohello solicitação de autorização somente se o token Olá é válido. Ao contrário de autenticação baseada em cookie, navegadores não anexe Olá toorequests de tokens de portador. Olá solicitando o cliente precisa tooexplicitly anexar o token de portador Olá no cabeçalho de solicitação de saudação. Portanto, para APIs Web ASP.NET protegidas usando o OAuth 2.0, os tokens de portador são considerados uma defesa contra ataques de CSRF. Observe que se parte do MVC de saudação do aplicativo hello usa autenticação de formulários (ou seja, usa cookies), tokens antifalsificação toobe usado pelo aplicativo de web MVC hello. |

### <a name="example"></a>Exemplo
Olá API da Web tem toobe informado toorely apenas em tokens de portador e não em cookies. Isso pode ser feito por Olá seguinte configuração em `WebApiConfig.Register` método: ' ' configuração de código C-Sharp. SuppressDefaultHostAuthentication(); config. Filters.Add (nova HostAuthenticationFilter(OAuthDefaults.AuthenticationType));
```
hello SuppressDefaultHostAuthentication method tells Web API tooignore any authentication that happens before hello request reaches hello Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API tooauthenticate only using bearer tokens.
