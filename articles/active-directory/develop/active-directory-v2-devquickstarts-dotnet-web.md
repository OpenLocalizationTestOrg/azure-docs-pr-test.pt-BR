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
# <a name="add-sign-in-tooan-net-mvc-web-app"></a><span data-ttu-id="305f3-103">Adicionar o aplicativo de web .NET MVC tooan entrar</span><span class="sxs-lookup"><span data-stu-id="305f3-103">Add sign-in tooan .NET MVC web app</span></span>
<span data-ttu-id="305f3-104">Com o ponto de extremidade Olá v 2.0, você pode adicionar rapidamente aplicativos de web tooyour autenticação com suporte para ambas as contas Microsoft pessoais e contas corporativa ou escolar.</span><span class="sxs-lookup"><span data-stu-id="305f3-104">With hello v2.0 endpoint, you can quickly add authentication tooyour web apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="305f3-105">Nos aplicativos Web ASP.NET, você pode conseguir isso usando o middleware OWIN da Microsoft, incluso no .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="305f3-105">In ASP.NET web apps, you can accomplish this using Microsoft's OWIN middleware included in .NET Framework 4.5.</span></span>

> [!NOTE]
> <span data-ttu-id="305f3-106">Nem todos os recursos e cenários de Active Directory do Azure têm suporte pelo ponto de extremidade do hello v 2.0.</span><span class="sxs-lookup"><span data-stu-id="305f3-106">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="305f3-107">toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="305f3-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

 <span data-ttu-id="305f3-108">Aqui, criaremos um aplicativo web que usa o usuário de saudação do OWIN toosign na exibição de algumas informações sobre o usuário hello e entrada hello usuário fora do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="305f3-108">Here we'll build an web app that uses OWIN toosign hello user in, display some information about hello user, and sign hello user out of hello app.</span></span>

## <a name="download"></a><span data-ttu-id="305f3-109">Baixar</span><span class="sxs-lookup"><span data-stu-id="305f3-109">Download</span></span>
<span data-ttu-id="305f3-110">código de saudação para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="305f3-110">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="305f3-111">toofollow ao longo, você pode [baixar o esqueleto do aplicativo hello como. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) ou esqueleto de saudação do clone:</span><span class="sxs-lookup"><span data-stu-id="305f3-111">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

<span data-ttu-id="305f3-112">aplicativo Hello concluída é fornecido no final da saudação deste tutorial também.</span><span class="sxs-lookup"><span data-stu-id="305f3-112">hello completed app is provided at hello end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="305f3-113">Registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="305f3-113">Register an app</span></span>
<span data-ttu-id="305f3-114">Crie um novo aplicativo em [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ou siga estas [etapas detalhadas](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="305f3-114">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="305f3-115">Não se esqueça de:</span><span class="sxs-lookup"><span data-stu-id="305f3-115">Make sure to:</span></span>

* <span data-ttu-id="305f3-116">Cópia para baixo Olá **Id do aplicativo** atribuído tooyour aplicativo, você precisará dele em breve.</span><span class="sxs-lookup"><span data-stu-id="305f3-116">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="305f3-117">Adicionar Olá **Web** plataforma para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="305f3-117">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="305f3-118">Digite hello correto **URI de redirecionamento**.</span><span class="sxs-lookup"><span data-stu-id="305f3-118">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="305f3-119">uri de redirecionamento Hello indica tooAzure AD onde as respostas de autenticação deverá ser direcionadas - Olá padrão para este tutorial é `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="305f3-119">hello redirect uri indicates tooAzure AD where authentication responses should be directed - hello default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install--configure-owin-authentication"></a><span data-ttu-id="305f3-120">Instalar e configurar a autenticação OWIN</span><span class="sxs-lookup"><span data-stu-id="305f3-120">Install & configure OWIN authentication</span></span>
<span data-ttu-id="305f3-121">Aqui, configuraremos Olá OWIN middleware toouse Olá OpenID Connect protocolo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="305f3-121">Here, we'll configure hello OWIN middleware toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="305f3-122">OWIN ser usado tooissue solicitações de entrada e saídas, gerenciar a sessão do usuário Olá e obter informações sobre o usuário hello, entre outras coisas.</span><span class="sxs-lookup"><span data-stu-id="305f3-122">OWIN will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

1. <span data-ttu-id="305f3-123">toobegin, abra Olá `web.config` arquivo na raiz de saudação do projeto hello e insira os valores de configuração do aplicativo na Olá `<appSettings>` seção.</span><span class="sxs-lookup"><span data-stu-id="305f3-123">toobegin, open hello `web.config` file in hello root of hello project, and enter your app's configuration values in hello `<appSettings>` section.</span></span>

  * <span data-ttu-id="305f3-124">Olá `ida:ClientId` é hello **Id do aplicativo** atribuído tooyour aplicativo no portal de registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="305f3-124">hello `ida:ClientId` is hello **Application Id** assigned tooyour app in hello registration portal.</span></span>
  * <span data-ttu-id="305f3-125">Olá `ida:RedirectUri` é hello **Uri de redirecionamento** inserido no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="305f3-125">hello `ida:RedirectUri` is hello **Redirect Uri** you entered in hello portal.</span></span>

2. <span data-ttu-id="305f3-126">Em seguida, adicione Olá OWIN middleware NuGet pacotes toohello projeto usando Olá Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="305f3-126">Next, add hello OWIN middleware NuGet packages toohello project using hello Package Manager Console.</span></span>

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. <span data-ttu-id="305f3-127">Adicionar um projeto de toohello "Classe de inicialização OWIN" chamado `Startup.cs` direita, clique no projeto Olá- **adicionar** --> **Novo Item** --> procure "OWIN".</span><span class="sxs-lookup"><span data-stu-id="305f3-127">Add an "OWIN Startup Class" toohello project called `Startup.cs`  Right click on hello project --> **Add** --> **New Item** --> Search for "OWIN".</span></span>  <span data-ttu-id="305f3-128">Olá OWIN middleware invocará Olá `Configuration(...)` método quando seu aplicativo é iniciado.</span><span class="sxs-lookup"><span data-stu-id="305f3-128">hello OWIN middleware will invoke hello `Configuration(...)` method when your app starts.</span></span>
4. <span data-ttu-id="305f3-129">Altere a declaração de classe Olá muito`public partial class Startup` -já implementamos parte dessa classe para você em outro arquivo.</span><span class="sxs-lookup"><span data-stu-id="305f3-129">Change hello class declaration too`public partial class Startup` - we've already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="305f3-130">Em Olá `Configuration(...)` método, faça um tooset tooConfigureAuth(...) de chamada de autenticação para seu aplicativo web</span><span class="sxs-lookup"><span data-stu-id="305f3-130">In hello `Configuration(...)` method, make a call tooConfigureAuth(...) tooset up authentication for your web app</span></span>  

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

5. <span data-ttu-id="305f3-131">Arquivo hello abrir `App_Start\Startup.Auth.cs` e implementar Olá `ConfigureAuth(...)` método.</span><span class="sxs-lookup"><span data-stu-id="305f3-131">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="305f3-132">Olá parâmetros que você fornece em `OpenIdConnectAuthenticationOptions` servirá como coordenadas para toocommunicate seu aplicativo com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="305f3-132">hello parameters you provide in `OpenIdConnectAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>  <span data-ttu-id="305f3-133">Você também precisará tooset a autenticação de Cookie - Olá OpenID Connect middleware usa cookies sob Olá abrange.</span><span class="sxs-lookup"><span data-stu-id="305f3-133">You'll also need tooset up Cookie Authentication - hello OpenID Connect middleware uses cookies underneath hello covers.</span></span>

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

## <a name="send-authentication-requests"></a><span data-ttu-id="305f3-134">Enviar solicitações de autenticação</span><span class="sxs-lookup"><span data-stu-id="305f3-134">Send authentication requests</span></span>
<span data-ttu-id="305f3-135">Seu aplicativo agora está adequadamente configurado toocommunicate com ponto de extremidade v 2.0 hello usando o protocolo de autenticação OpenID Connect Olá.</span><span class="sxs-lookup"><span data-stu-id="305f3-135">Your app is now properly configured toocommunicate with hello v2.0 endpoint using hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="305f3-136">OWIN tiver resolvido todos os detalhes de feio Olá de criação de mensagens de autenticação, validando tokens do AD do Azure e manter a sessão de usuário.</span><span class="sxs-lookup"><span data-stu-id="305f3-136">OWIN has taken care of all of hello ugly details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span>  <span data-ttu-id="305f3-137">Tudo o que permanece é toogive seus usuários uma maneira toosign no e sair.</span><span class="sxs-lookup"><span data-stu-id="305f3-137">All that remains is toogive your users a way toosign in and sign out.</span></span>

- <span data-ttu-id="305f3-138">Você pode usar marcas de autorizar no seu toorequire controladores que o usuário faz logon antes de acessar uma determinada página.</span><span class="sxs-lookup"><span data-stu-id="305f3-138">You can use authorize tags in your controllers toorequire that user signs in before accessing a certain page.</span></span>  <span data-ttu-id="305f3-139">Abra `Controllers\HomeController.cs`e adicione Olá `[Authorize]` marca toohello sobre o controlador.</span><span class="sxs-lookup"><span data-stu-id="305f3-139">Open `Controllers\HomeController.cs`, and add hello `[Authorize]` tag toohello About controller.</span></span>
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- <span data-ttu-id="305f3-140">Você também pode usar as solicitações de autenticação OWIN toodirectly problema de dentro de seu código.</span><span class="sxs-lookup"><span data-stu-id="305f3-140">You can also use OWIN toodirectly issue authentication requests from within your code.</span></span>  <span data-ttu-id="305f3-141">Abra `Controllers\AccountController.cs`.</span><span class="sxs-lookup"><span data-stu-id="305f3-141">Open `Controllers\AccountController.cs`.</span></span>  <span data-ttu-id="305f3-142">Olá SignIn() e ações de SignOut (), emita desafio OpenID Connect e solicitações de saída, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="305f3-142">In hello SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests, respectively.</span></span>

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

- <span data-ttu-id="305f3-143">Agora, abra `Views\Shared\_LoginPartial.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="305f3-143">Now, open `Views\Shared\_LoginPartial.cshtml`.</span></span>  <span data-ttu-id="305f3-144">Isso é onde você mostrar os links de entrada e saída do aplicativo do usuário de saudação e imprima o nome do usuário de saudação em um modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="305f3-144">This is where you'll show hello user your app's sign-in and sign-out links, and print out hello user's name in a view.</span></span>

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

## <a name="display-user-information"></a><span data-ttu-id="305f3-145">Exibir informações do usuário</span><span class="sxs-lookup"><span data-stu-id="305f3-145">Display user information</span></span>
<span data-ttu-id="305f3-146">Ao autenticar usuários com OpenID Connect, o ponto de extremidade do hello v 2.0 retorna um aplicativo de toohello id_token que contém declarações ou asserções sobre usuário hello.</span><span class="sxs-lookup"><span data-stu-id="305f3-146">When authenticating users with OpenID Connect, hello v2.0 endpoint returns an id_token toohello app that contains claims, or assertions about hello user.</span></span>  <span data-ttu-id="305f3-147">Você pode usar essas declarações toopersonalize seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="305f3-147">You can use these claims toopersonalize your app:</span></span>

- <span data-ttu-id="305f3-148">Olá abrir `Controllers\HomeController.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="305f3-148">Open hello `Controllers\HomeController.cs` file.</span></span>  <span data-ttu-id="305f3-149">Você pode acessar declarações saudação do usuário em seus controladores via Olá `ClaimsPrincipal.Current` objeto de segurança.</span><span class="sxs-lookup"><span data-stu-id="305f3-149">You can access hello user's claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

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

## <a name="run"></a><span data-ttu-id="305f3-150">Executar</span><span class="sxs-lookup"><span data-stu-id="305f3-150">Run</span></span>
<span data-ttu-id="305f3-151">Por fim, compile e execute seu aplicativo!</span><span class="sxs-lookup"><span data-stu-id="305f3-151">Finally, build and run your app!</span></span>   <span data-ttu-id="305f3-152">Entrar com um Account pessoal da Microsoft ou uma conta corporativa ou de estudante e observe como a identidade do usuário Olá é refletida na barra de navegação superior hello.</span><span class="sxs-lookup"><span data-stu-id="305f3-152">Sign in with either a personal Microsoft Account or a work or school account, and notice how hello user's identity is reflected in hello top navigation bar.</span></span>  <span data-ttu-id="305f3-153">Agora você tem um aplicativo Web protegido por protocolos padrão do setor, que podem autenticar usuários com as respectivas contas pessoais e corporativas ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="305f3-153">You now have a web app secured using industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="305f3-154">Para referência, Olá concluída exemplo (sem os valores de configuração) [é fornecido como. zip aqui](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), ou você pode cloná-lo do GitHub:</span><span class="sxs-lookup"><span data-stu-id="305f3-154">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="305f3-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="305f3-155">Next steps</span></span>
<span data-ttu-id="305f3-156">Agora você pode ir para tópicos mais avançados.</span><span class="sxs-lookup"><span data-stu-id="305f3-156">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="305f3-157">Você pode desejar tootry:</span><span class="sxs-lookup"><span data-stu-id="305f3-157">You may want tootry:</span></span>

[<span data-ttu-id="305f3-158">Proteger uma API da Web com o ponto de extremidade Olá Olá v 2.0 >></span><span class="sxs-lookup"><span data-stu-id="305f3-158">Secure a Web API with hello hello v2.0 endpoint >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

<span data-ttu-id="305f3-159">Para obter recursos adicionais, consulte:</span><span class="sxs-lookup"><span data-stu-id="305f3-159">For additional resources, check out:</span></span>

* [<span data-ttu-id="305f3-160">Guia do desenvolvedor v 2.0 Olá >></span><span class="sxs-lookup"><span data-stu-id="305f3-160">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="305f3-161">Marca “azure-active-directory” do StackOverflow >></span><span class="sxs-lookup"><span data-stu-id="305f3-161">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="305f3-162">Obter atualizações de segurança para nossos produtos</span><span class="sxs-lookup"><span data-stu-id="305f3-162">Get security updates for our products</span></span>
<span data-ttu-id="305f3-163">Recomendamos que você tooget as notificações quando os incidentes de segurança ocorrem visitando [essa página](https://technet.microsoft.com/security/dd252948) e assinando tooSecurity alertas de aviso.</span><span class="sxs-lookup"><span data-stu-id="305f3-163">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>
