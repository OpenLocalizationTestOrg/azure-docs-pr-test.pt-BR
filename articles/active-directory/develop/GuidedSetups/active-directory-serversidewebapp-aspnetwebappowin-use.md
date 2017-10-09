---
title: "aaaAzure AD v2 ASP.NET Web Server Introdução - uso | Microsoft Docs"
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
ms.openlocfilehash: 03afce6fa6598215e8c4af841c00762c143a0cd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="add-a-controller-toohandle-sign-in-and-sign-out-requests"></a>Adicione um solicitações de entrada e saída de toohandle do controlador

Esta etapa mostra como toocreate um novo tooexpose de controlador entrar e métodos de saída.

1.  Clique com botão direito Olá `Controllers` pasta e selecione`Add` > `Controller`
2.  Selecione `MVC (.NET version) Controller – Empty`.
3.  Clique em *Adicionar*
4.  Nomeie-o `HomeController` e clique em *Adicionar*
5.  Adicionar *OWIN* referencia a classe toohello:

```csharp
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
```
<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
Adicione dois métodos Olá abaixo toohandle entrada e saída tooyour controlador iniciando um desafio de autenticação por meio de código:
</li>
</ol>

```csharp
/// <summary>
/// Send an OpenID Connect sign-in request.
/// Alternatively, you can just decorate hello SignIn method with hello [Authorize] attribute
/// </summary>
public void SignIn()
{
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge(
            new AuthenticationProperties{ RedirectUri = "/" },
            OpenIdConnectAuthenticationDefaults.AuthenticationType);
    }
}

/// <summary>
/// Send an OpenID Connect sign-out request.
/// </summary>
public void SignOut()
{
    HttpContext.GetOwinContext().Authentication.SignOut(
            OpenIdConnectAuthenticationDefaults.AuthenticationType,
            CookieAuthenticationDefaults.AuthenticationType);
}
```

## <a name="create-hello-apps-home-page-toosign-in-users-via-a-sign-in-button"></a>Criar toosign de página inicial do aplicativo hello em usuários por meio de um botão de login

No Visual Studio, crie um novo modo de exibição tooadd Olá botão entrar e exibir informações do usuário após a autenticação:

1.  Clique com botão direito Olá `Views\Home` pasta e selecione`Add View`
2.  Nomeie-o `Index`.
3.  Adicione Olá HTML, que inclui a saudação botão de login, toohello arquivo a seguir:

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Guide</title>
</head>
<body>
@if (!Request.IsAuthenticated)
{
    <!-- If hello user is not authenticated, display hello sign-in button -->
    <a href="@Url.Action("SignIn", "Home")" style="text-decoration: none;">
        <svg xmlns="http://www.w3.org/2000/svg" xml:space="preserve" width="300px" height="50px" viewBox="0 0 3278 522" class="SignInButton">
        <style type="text/css">.fil0:hover {fill: #4B4B4B;} .fnt0 {font-size: 260px;font-family: 'Segoe UI Semibold', 'Segoe UI'; text-decoration: none;}</style>
        <rect class="fil0" x="2" y="2" width="3174" height="517" fill="black" />
        <rect x="150" y="129" width="122" height="122" fill="#F35325" />
        <rect x="284" y="129" width="122" height="122" fill="#81BC06" />
        <rect x="150" y="263" width="122" height="122" fill="#05A6F0" />
        <rect x="284" y="263" width="122" height="122" fill="#FFBA08" />
        <text x="470" y="357" fill="white" class="fnt0">Sign in with Microsoft</text>
        </svg>
    </a>
}
else
{
    <span><br/>Hello @System.Security.Claims.ClaimsPrincipal.Current.FindFirst("name").Value;</span>
    <br /><br />
    @Html.ActionLink("See Your Claims", "Index", "Claims")
    <br /><br />
    @Html.ActionLink("Sign out", "SignOut", "Home")
}
@if (!string.IsNullOrWhiteSpace(Request.QueryString["errormessage"]))
{
    <div style="background-color:red;color:white;font-weight: bold;">Error: @Request.QueryString["errormessage"]</div>
}
</body>
</html>
```
<!--start-collapse-->
### <a name="more-information"></a>Mais informações
> Esta página adiciona um botão de conexão no formato SVG com uma tela de fundo preta:<br/>![Entrar com uma Conta da Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)<br/> Para obter mais botões de login, visite toohello [essa página](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "diretrizes da marca").
<!--end-collapse-->

## <a name="add-a-controller-toodisplay-users-claims"></a>Adicionar declarações do usuário toodisplay controlador
Esse controlador demonstra Olá usos de saudação `[Authorize]` tooprotect um controlador de atributo. Esse atributo restringe o controlador de toohello de acesso, permitindo que apenas usuários autenticados. Olá código a seguir usa Olá atributo toodisplay declarações de usuário que foram recuperadas como parte da saudação entrar.

1.  Clique com botão direito Olá `Controllers` pasta:`Add` > `Controller`
2.  Selecione `MVC {version} Controller – Empty`.
3.  Clique em *Adicionar*
4.  Nomeie-o `ClaimsController`
5.  Substitua o código de saudação da classe do controlador com o código de saudação abaixo - adiciona Olá `[Authorize]` toohello classe de atributo:

```csharp
[Authorize]
public class ClaimsController : Controller
{
    /// <summary>
    /// Add user's claims tooviewbag
    /// </summary>
    /// <returns></returns>
    public ActionResult Index()
    {
        var claimsPrincipalCurrent = System.Security.Claims.ClaimsPrincipal.Current;
        //You get hello user’s first and last name below:
        ViewBag.Name = claimsPrincipalCurrent.FindFirst("name").Value;

        // hello 'preferred_username' claim can be used for showing hello username
        ViewBag.Username = claimsPrincipalCurrent.FindFirst("preferred_username").Value;

        // hello subject claim can be used toouniquely identify hello user across hello web
        ViewBag.Subject = claimsPrincipalCurrent.FindFirst(System.Security.Claims.ClaimTypes.NameIdentifier).Value;

        // TenantId is hello unique Tenant Id - which represents an organization in Azure AD
        ViewBag.TenantId = claimsPrincipalCurrent.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;

        return View();
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a>Mais informações
> Por causa do uso Olá Olá `[Authorize]` atributo, todos os métodos deste controlador só pode ser executado se Olá usuário é autenticado. Se usuário Olá não for autenticado e tenta tooaccess controlador de hello, OWIN iniciam um desafio de autenticação e forçar Olá tooauthenticate de usuário. coleção de saudação de declarações de código Olá acima examina Olá `ClaimsPrincipal.Current` instância para atributos específicos do usuário incluído no token de saudação do usuário. Esses atributos incluem o nome completo do usuário hello e nome de usuário, bem como o assunto de identificador de usuário global hello. Ele também contém Olá *ID de locatário*, que representa a ID de saudação de organização saudação do usuário. 
<!--end-collapse-->

## <a name="create-a-view-toodisplay-hello-users-claims"></a>Criar uma exibição de declarações do usuário do toodisplay Olá

No Visual Studio, crie uma nova exibição de declarações do usuário de saudação toodisplay em uma página da web:

1.  Clique com botão direito Olá `Views\Claims` pasta e:`Add View`
2.  Nomeie-o `Index`.
3.  Adicione Olá arquivo toohello HTML a seguir:

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Sample</title>
    <link href="@Url.Content("~/Content/bootstrap.min.css")" rel="stylesheet" type="text/css" />
</head>
<body style="padding:50px">
    <h3>Main Claims:</h3>
    <table class="table table-striped table-bordered table-hover">
        <tr><td>Name</td><td>@ViewBag.Name</td></tr>
        <tr><td>Username</td><td>@ViewBag.Username</td></tr>
        <tr><td>Subject</td><td>@ViewBag.Subject</td></tr>
        <tr><td>TenantId</td><td>@ViewBag.TenantId</td></tr>
    </table>
    <br />
    <h3>All Claims:</h3>
    <table class="table table-striped table-bordered table-hover table-condensed">
    @foreach (var claim in System.Security.Claims.ClaimsPrincipal.Current.Claims)
    {
        <tr><td>@claim.Type</td><td>@claim.Value</td></tr>
    }
</table>
    <br />
    <br />
    @Html.ActionLink("Sign out", "SignOut", "Home", null, new { @class = "btn btn-primary" })
</body>
</html>
```
