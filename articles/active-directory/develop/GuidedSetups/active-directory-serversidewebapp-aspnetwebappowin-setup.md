---
title: "aaaAzure AD v2 ASP.NET Web Server Introdução - instalação | Microsoft Docs"
description: "Implementando a opção Entrar com uma Conta da Microsoft em uma solução ASP.NET com um aplicativo tradicional baseado em navegador da Web usando o padrão OpenID Connect"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: eadc59666557e9cd294e6e99391001120579144c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a>Configurar o seu projeto

Esta seção mostra Olá etapas tooinstall e configurar o pipeline de autenticação Olá por meio do middleware OWIN em um projeto ASP.NET que usa o OpenID Connect. 

> Preferir toodownload este projeto do Visual Studio em vez disso? [Baixar um projeto](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) e ignorar toohello [etapa de configuração](#create-an-application-express) exemplo de código tooconfigure hello antes de executar.

<!--start-collapse-->
> ### <a name="create-your-aspnet-project"></a>Criar seu projeto do ASP.NET

> 1. No Visual Studio: `File` > `New` > `Project`<br/>
> 2. Em *Visual C#\Web*, selecione `ASP.NET Web Application (.NET Framework)`.
> 3. Nomeie o aplicativo e clique em *OK*
> 4. Selecione `Empty` e Olá selecione caixa de seleção tooadd `MVC` referências
<!--end-collapse-->

## <a name="add-authentication-components"></a>Adicionar componentes de autenticação

1. No Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`
2. Adicionar *pacotes do NuGet middleware OWIN* digitando o seguinte de saudação na janela do Console do Gerenciador de pacotes de saudação:

```powershell
Install-Package Microsoft.Owin.Security.OpenIdConnect
Install-Package Microsoft.Owin.Security.Cookies
Install-Package Microsoft.Owin.Host.SystemWeb
```

<!--start-collapse-->
> ### <a name="about-these-libraries"></a>Sobre estas bibliotecas

>bibliotecas de saudação acima permitem logon único (SSO) usando o OpenID Connect através da autenticação baseada em cookie. Após a autenticação é concluída e token Olá representando Olá usuário é enviado tooyour aplicativo, o middleware OWIN cria um cookie de sessão. Olá navegador, em seguida, usa esse cookie em solicitações subsequentes para que usuário Olá não seja necessário tooretype sua senha, e nenhuma verificação adicional é necessária.
<!--end-collapse-->

## <a name="configure-hello-authentication-pipeline"></a>Configurar o pipeline de autenticação Olá
Olá etapas a seguir são usada toocreate uma autenticação OpenID Connect OWIN middleware classe inicialização tooconfigure. Essa classe será executada automaticamente quando o processo do IIS for iniciado.

> Se seu projeto não tem um `Startup.cs` arquivo na pasta raiz de saudação:<br/>
> 1. Clique com o botão direito na pasta raiz do projeto Olá: >`Add` > `New Item...` > `OWIN Startup class`<br/>
> 2. Nomeie-o `Startup.cs`

> Certifique-se de classe Olá selecionada é uma classe de inicialização OWIN e não uma padrão classe c#. Confirmar isso verificando se você vir `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` acima Olá namespace.


1. Adicionar *OWIN* e *Microsoft. IdentityModel* referencia muito`Startup.cs`:

```csharp
using Microsoft.Owin;
using Owin;
using Microsoft.IdentityModel.Protocols;
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
using Microsoft.Owin.Security.Notifications;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Substitua a classe de inicialização com o código de saudação abaixo:
</li>
</ol>

```csharp
public class Startup
{        
    // hello Client ID is used by hello application toouniquely identify itself tooAzure AD.
    string clientId = System.Configuration.ConfigurationManager.AppSettings["ClientId"];

    // RedirectUri is hello URL where hello user will be redirected tooafter they sign in.
    string redirectUri = System.Configuration.ConfigurationManager.AppSettings["RedirectUri"];

    // Tenant is hello tenant ID (e.g. contoso.onmicrosoft.com, or 'common' for multi-tenant)
    static string tenant = System.Configuration.ConfigurationManager.AppSettings["Tenant"];

    // Authority is hello URL for authority, composed by Azure Active Directory v2 endpoint and hello tenant name (e.g. https://login.microsoftonline.com/contoso.onmicrosoft.com/v2.0)
    string authority = String.Format(System.Globalization.CultureInfo.InvariantCulture, System.Configuration.ConfigurationManager.AppSettings["Authority"], tenant);

    /// <summary>
    /// Configure OWIN toouse OpenIdConnect 
    /// </summary>
    /// <param name="app"></param>
    public void Configuration(IAppBuilder app)
    {
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseCookieAuthentication(new CookieAuthenticationOptions());
            app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Sets hello ClientId, authority, RedirectUri as obtained from web.config
                ClientId = clientId,
                Authority = authority,
                RedirectUri = redirectUri,
                // PostLogoutRedirectUri is hello page that users will be redirected tooafter sign-out. In this case, it is using hello home page
                PostLogoutRedirectUri = redirectUri,
                Scope = OpenIdConnectScopes.OpenIdProfile,
                // ResponseType is set toorequest hello id_token - which contains basic information about hello signed-in user
                ResponseType = OpenIdConnectResponseTypes.IdToken,
                // ValidateIssuer set toofalse tooallow personal and work accounts from any organization toosign in tooyour application
                // tooonly allow users from a single organizations, set ValidateIssuer tootrue and 'tenant' setting in web.config toohello tenant name
                // tooallow users from only a list of specific organizations, set ValidateIssuer tootrue and use ValidIssuers parameter 
                TokenValidationParameters = new System.IdentityModel.Tokens.TokenValidationParameters() { ValidateIssuer = false },
                // OpenIdConnectAuthenticationNotifications configures OWIN toosend notification of failed authentications tooOnAuthenticationFailed method
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    AuthenticationFailed = OnAuthenticationFailed
                }
            }
        );
    }

    /// <summary>
    /// Handle failed authentication requests by redirecting hello user toohello home page with an error in hello query string
    /// </summary>
    /// <param name="context"></param>
    /// <returns></returns>
    private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> context)
    {
        context.HandleResponse();
        context.Response.Redirect("/?errormessage=" + context.Exception.Message);
        return Task.FromResult(0);
    }
}

```
<!--start-collapse-->
> ### <a name="more-information"></a>Mais informações

> Olá parâmetros que você fornece em *OpenIDConnectAuthenticationOptions* servem como coordenadas de saudação toocommunicate de aplicativo com o Azure AD. Como Olá OpenID Connect middleware usa cookies no plano de fundo hello, você também precisa tooset a autenticação de cookie como código Olá acima mostra. Olá *ValidateIssuer* valor informa OpenIdConnect toonot restringir acesso tooone determinada organização.
<!--end-collapse-->

