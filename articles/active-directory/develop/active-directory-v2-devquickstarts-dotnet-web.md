---
title: "aaaAzure AD v 2.0 .NET da web app no guia de Introdução | Microsoft Docs"
description: "Como toobuild um aplicativo de Web .NET MVC que entrar usuários com ambos os Account pessoal da Microsoft e contas corporativa ou escolar."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: c8b97ac6-0a06-4367-81b6-7d1d98152b14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 241e9c90bd752fbecc3696ce4f1bed3f9772189d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-net-mvc-web-app"></a>Adicionar o aplicativo de web .NET MVC tooan entrar
Com o ponto de extremidade Olá v 2.0, você pode adicionar rapidamente aplicativos de web tooyour autenticação com suporte para ambas as contas Microsoft pessoais e contas corporativa ou escolar.  Nos aplicativos Web ASP.NET, você pode conseguir isso usando o middleware OWIN da Microsoft, incluso no .NET Framework 4.5.

> [!NOTE]
> Nem todos os recursos e cenários de Active Directory do Azure têm suporte pelo ponto de extremidade do hello v 2.0.  toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).
>
>

 Aqui, criaremos um aplicativo web que usa o usuário de saudação do OWIN toosign na exibição de algumas informações sobre o usuário hello e entrada hello usuário fora do aplicativo hello.

## <a name="download"></a>Baixar
código de saudação para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).  toofollow ao longo, você pode [baixar o esqueleto do aplicativo hello como. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) ou esqueleto de saudação do clone:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

aplicativo Hello concluída é fornecido no final da saudação deste tutorial também.

## <a name="register-an-app"></a>Registrar um aplicativo
Crie um novo aplicativo em [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ou siga estas [etapas detalhadas](active-directory-v2-app-registration.md).  Não se esqueça de:

* Cópia para baixo Olá **Id do aplicativo** atribuído tooyour aplicativo, você precisará dele em breve.
* Adicionar Olá **Web** plataforma para seu aplicativo.
* Digite hello correto **URI de redirecionamento**. uri de redirecionamento Hello indica tooAzure AD onde as respostas de autenticação deverá ser direcionadas - Olá padrão para este tutorial é `https://localhost:44326/`.

## <a name="install--configure-owin-authentication"></a>Instalar e configurar a autenticação OWIN
Aqui, configuraremos Olá OWIN middleware toouse Olá OpenID Connect protocolo de autenticação.  OWIN ser usado tooissue solicitações de entrada e saídas, gerenciar a sessão do usuário Olá e obter informações sobre o usuário hello, entre outras coisas.

1. toobegin, abra Olá `web.config` arquivo na raiz de saudação do projeto hello e insira os valores de configuração do aplicativo na Olá `<appSettings>` seção.

  * Olá `ida:ClientId` é hello **Id do aplicativo** atribuído tooyour aplicativo no portal de registro de saudação.
  * Olá `ida:RedirectUri` é hello **Uri de redirecionamento** inserido no portal de saudação.

2. Em seguida, adicione Olá OWIN middleware NuGet pacotes toohello projeto usando Olá Package Manager Console.

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. Adicionar um projeto de toohello "Classe de inicialização OWIN" chamado `Startup.cs` direita, clique no projeto Olá- **adicionar** --> **Novo Item** --> procure "OWIN".  Olá OWIN middleware invocará Olá `Configuration(...)` método quando seu aplicativo é iniciado.
4. Altere a declaração de classe Olá muito`public partial class Startup` -já implementamos parte dessa classe para você em outro arquivo.  Em Olá `Configuration(...)` método, faça um tooset tooConfigureAuth(...) de chamada de autenticação para seu aplicativo web  

        ```C#
        [assembly: OwinStartup(typeof(Startup))]
        
        namespace TodoList_WebApp
        {
            public partial class Startup
            {
                public void Configuration(IAppBuilder app)
                {
                    ConfigureAuth(app);
                }
            }
        }
        ```

5. Arquivo hello abrir `App_Start\Startup.Auth.cs` e implementar Olá `ConfigureAuth(...)` método.  Olá parâmetros que você fornece em `OpenIdConnectAuthenticationOptions` servirá como coordenadas para toocommunicate seu aplicativo com o Azure AD.  Você também precisará tooset a autenticação de Cookie - Olá OpenID Connect middleware usa cookies sob Olá abrange.

        ```C#
        public void ConfigureAuth(IAppBuilder app)
                     {
                             app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);
        
                             app.UseCookieAuthentication(new CookieAuthenticationOptions());
        
                             app.UseOpenIdConnectAuthentication(
                                     new OpenIdConnectAuthenticationOptions
                                     {
                                             // hello `Authority` represents hello v2.0 endpoint - https://login.microsoftonline.com/common/v2.0
                                             // hello `Scope` describes hello permissions that your app will need.  See https://azure.microsoft.com/documentation/articles/active-directory-v2-scopes/
                                             // In a real application you could use issuer validation for additional checks, like making sure hello user's organization has signed up for your app, for instance.
        
                                             ClientId = clientId,
                                             Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0"),
                                             RedirectUri = redirectUri,
                                             Scope = "openid email profile",
                                             ResponseType = "id_token",
                                             PostLogoutRedirectUri = redirectUri,
                                             TokenValidationParameters = new TokenValidationParameters
                                             {
                                                     ValidateIssuer = false,
                                             },
                                             Notifications = new OpenIdConnectAuthenticationNotifications
                                             {
                                                     AuthenticationFailed = OnAuthenticationFailed,
                                             }
                                     });
                     }
        ```

## <a name="send-authentication-requests"></a>Enviar solicitações de autenticação
Seu aplicativo agora está adequadamente configurado toocommunicate com ponto de extremidade v 2.0 hello usando o protocolo de autenticação OpenID Connect Olá.  OWIN tiver resolvido todos os detalhes de feio Olá de criação de mensagens de autenticação, validando tokens do AD do Azure e manter a sessão de usuário.  Tudo o que permanece é toogive seus usuários uma maneira toosign no e sair.

- Você pode usar marcas de autorizar no seu toorequire controladores que o usuário faz logon antes de acessar uma determinada página.  Abra `Controllers\HomeController.cs`e adicione Olá `[Authorize]` marca toohello sobre o controlador.
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- Você também pode usar as solicitações de autenticação OWIN toodirectly problema de dentro de seu código.  Abra `Controllers\AccountController.cs`.  Olá SignIn() e ações de SignOut (), emita desafio OpenID Connect e solicitações de saída, respectivamente.

        ```C#
        public void SignIn()
        {
            // Send an OpenID Connect sign-in request.
            if (!Request.IsAuthenticated)
            {
                HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
            }
        }
        
        // BUGBUG: Ending a session with hello v2.0 endpoint is not yet supported.  Here, we just end hello session with hello web app.  
        public void SignOut()
        {
            // Send an OpenID Connect sign-out request.
            HttpContext.GetOwinContext().Authentication.SignOut(CookieAuthenticationDefaults.AuthenticationType);
            Response.Redirect("/");
        }
        ```

- Agora, abra `Views\Shared\_LoginPartial.cshtml`.  Isso é onde você mostrar os links de entrada e saída do aplicativo do usuário de saudação e imprima o nome do usuário de saudação em um modo de exibição.

        ```HTML
        @if (Request.IsAuthenticated)
        {
            <text>
                <ul class="nav navbar-nav navbar-right">
                    <li class="navbar-text">
        
                        @*hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves.*@
        
                        Hello, @(System.Security.Claims.ClaimsPrincipal.Current.FindFirst("preferred_username").Value)!
                    </li>
                    <li>
                        @Html.ActionLink("Sign out", "SignOut", "Account")
                    </li>
                </ul>
            </text>
        }
        else
        {
            <ul class="nav navbar-nav navbar-right">
                <li>@Html.ActionLink("Sign in", "SignIn", "Account", routeValues: null, htmlAttributes: new { id = "loginLink" })</li>
            </ul>
        }
        ```

## <a name="display-user-information"></a>Exibir informações do usuário
Ao autenticar usuários com OpenID Connect, o ponto de extremidade do hello v 2.0 retorna um aplicativo de toohello id_token que contém declarações ou asserções sobre usuário hello.  Você pode usar essas declarações toopersonalize seu aplicativo:

- Olá abrir `Controllers\HomeController.cs` arquivo.  Você pode acessar declarações saudação do usuário em seus controladores via Olá `ClaimsPrincipal.Current` objeto de segurança.

        ```C#
        [Authorize]
        public ActionResult About()
        {
            ViewBag.Name = ClaimsPrincipal.Current.FindFirst("name").Value;
        
            // hello object ID claim will only be emitted for work or school accounts at this time.
            Claim oid = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier");
            ViewBag.ObjectId = oid == null ? string.Empty : oid.Value;
        
            // hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves
            ViewBag.Username = ClaimsPrincipal.Current.FindFirst("preferred_username").Value;
        
            // hello subject or nameidentifier claim can be used toouniquely identify hello user
            ViewBag.Subject = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        
            return View();
        }
        ```

## <a name="run"></a>Executar
Por fim, compile e execute seu aplicativo!   Entrar com um Account pessoal da Microsoft ou uma conta corporativa ou de estudante e observe como a identidade do usuário Olá é refletida na barra de navegação superior hello.  Agora você tem um aplicativo Web protegido por protocolos padrão do setor, que podem autenticar usuários com as respectivas contas pessoais e corporativas ou de estudante.

Para referência, Olá concluída exemplo (sem os valores de configuração) [é fornecido como. zip aqui](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), ou você pode cloná-lo do GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a>Próximas etapas
Agora você pode ir para tópicos mais avançados.  Você pode desejar tootry:

[Proteger uma API da Web com o ponto de extremidade Olá Olá v 2.0 >>](active-directory-devquickstarts-webapi-dotnet.md)

Para obter recursos adicionais, consulte:

* [Guia do desenvolvedor v 2.0 Olá >>](active-directory-appmodel-v2-overview.md)
* [Marca “azure-active-directory” do StackOverflow >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Obter atualizações de segurança para nossos produtos
Recomendamos que você tooget as notificações quando os incidentes de segurança ocorrem visitando [essa página](https://technet.microsoft.com/security/dd252948) e assinando tooSecurity alertas de aviso.
