---
title: "Introdução à conexão do aplicativo Web .NET v2.0 do Azure AD | Microsoft Docs"
description: "Como criar um aplicativo Web do .NET MVC que conecte usuários com a conta pessoal da Microsoft e as contas corporativas ou de estudante."
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
ms.openlocfilehash: ba5bdf7daba6086b70aec54ebe25d4445fa708c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-net-mvc-web-app"></a><span data-ttu-id="65654-103">Adicionar as credenciais para um aplicativo Web .NET MVC</span><span class="sxs-lookup"><span data-stu-id="65654-103">Add sign-in to an .NET MVC web app</span></span>
<span data-ttu-id="65654-104">Com o ponto de extremidade v2.0, você pode adicionar autenticação rapidamente a seus aplicativos Web com suporte a contas pessoais da Microsoft e contas corporativas ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="65654-104">With the v2.0 endpoint, you can quickly add authentication to your web apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="65654-105">Nos aplicativos Web ASP.NET, você pode conseguir isso usando o middleware OWIN da Microsoft, incluso no .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="65654-105">In ASP.NET web apps, you can accomplish this using Microsoft's OWIN middleware included in .NET Framework 4.5.</span></span>

> [!NOTE]
> <span data-ttu-id="65654-106">Nem todos os recursos e cenários do Azure Active Directory têm suporte no ponto de extremidade v2.0.</span><span class="sxs-lookup"><span data-stu-id="65654-106">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="65654-107">Para determinar se você deve usar o ponto de extremidade v2.0, leia sobre as [limitações da v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="65654-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

 <span data-ttu-id="65654-108">Compilaremos aqui um aplicativo Web que usa o OWIN para fazer logon do usuário, exibir algumas informações sobre o usuário e fazer logout do usuário do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="65654-108">Here we'll build an web app that uses OWIN to sign the user in, display some information about the user, and sign the user out of the app.</span></span>

## <a name="download"></a><span data-ttu-id="65654-109">Baixar</span><span class="sxs-lookup"><span data-stu-id="65654-109">Download</span></span>
<span data-ttu-id="65654-110">O código para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="65654-110">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="65654-111">Para acompanhar, você pode [baixar o esqueleto do aplicativo como um .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) ou clonar o esqueleto:</span><span class="sxs-lookup"><span data-stu-id="65654-111">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

<span data-ttu-id="65654-112">O aplicativo concluído é fornecido também no final desse tutorial.</span><span class="sxs-lookup"><span data-stu-id="65654-112">The completed app is provided at the end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="65654-113">Registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="65654-113">Register an app</span></span>
<span data-ttu-id="65654-114">Crie um novo aplicativo em [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ou siga estas [etapas detalhadas](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="65654-114">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="65654-115">Não se esqueça de:</span><span class="sxs-lookup"><span data-stu-id="65654-115">Make sure to:</span></span>

* <span data-ttu-id="65654-116">Copiar a **ID do Aplicativo** designada ao seu aplicativo, você precisará dela logo.</span><span class="sxs-lookup"><span data-stu-id="65654-116">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="65654-117">Adicionar a plataforma **Web** para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="65654-117">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="65654-118">Inserir o **URI de Redirecionamento**correto.</span><span class="sxs-lookup"><span data-stu-id="65654-118">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="65654-119">O URI de redirecionamento indica ao Azure AD para onde as respostas de autenticação devem ser direcionadas — o padrão para este tutorial é `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="65654-119">The redirect uri indicates to Azure AD where authentication responses should be directed - the default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install--configure-owin-authentication"></a><span data-ttu-id="65654-120">Instalar e configurar a autenticação OWIN</span><span class="sxs-lookup"><span data-stu-id="65654-120">Install & configure OWIN authentication</span></span>
<span data-ttu-id="65654-121">Aqui, configuraremos middleware OWIN para usar o protocolo de autenticação OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="65654-121">Here, we'll configure the OWIN middleware to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="65654-122">OWIN será usado para emitir solicitações de entrada e saída, gerenciar a sessão do usuário e obter informações sobre o usuário, entre outras coisas.</span><span class="sxs-lookup"><span data-stu-id="65654-122">OWIN will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

1. <span data-ttu-id="65654-123">Para começar, abra o arquivo `web.config` na raiz do projeto e insira os valores de configuração do aplicativo na seção `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="65654-123">To begin, open the `web.config` file in the root of the project, and enter your app's configuration values in the `<appSettings>` section.</span></span>

  * <span data-ttu-id="65654-124">`ida:ClientId` é a **ID do Aplicativo** atribuída ao seu aplicativo no portal de registro.</span><span class="sxs-lookup"><span data-stu-id="65654-124">The `ida:ClientId` is the **Application Id** assigned to your app in the registration portal.</span></span>
  * <span data-ttu-id="65654-125">`ida:RedirectUri` é o **URI de Redirecionamento** inserido no portal.</span><span class="sxs-lookup"><span data-stu-id="65654-125">The `ida:RedirectUri` is the **Redirect Uri** you entered in the portal.</span></span>

2. <span data-ttu-id="65654-126">Em seguida, adicione o ADAL aos pacotes NuGet de middleware ao projeto usando o Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="65654-126">Next, add the OWIN middleware NuGet packages to the project using the Package Manager Console.</span></span>

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. <span data-ttu-id="65654-127">Adicione uma classe de inicialização do OWIN ao projeto chamado `Startup.cs` Clique com o botão direito do mouse no projeto --> **Adicionar** --> **Novo item** --> pesquise por "OWIN".</span><span class="sxs-lookup"><span data-stu-id="65654-127">Add an "OWIN Startup Class" to the project called `Startup.cs`  Right click on the project --> **Add** --> **New Item** --> Search for "OWIN".</span></span>  <span data-ttu-id="65654-128">O middleware OWIN invocará o método `Configuration(...)` quando seu aplicativo for iniciado.</span><span class="sxs-lookup"><span data-stu-id="65654-128">The OWIN middleware will invoke the `Configuration(...)` method when your app starts.</span></span>
4. <span data-ttu-id="65654-129">Altere a declaração de classe para `public partial class Startup` -já implementamos parte dessa classe para você em outro arquivo.</span><span class="sxs-lookup"><span data-stu-id="65654-129">Change the class declaration to `public partial class Startup` - we've already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="65654-130">No método `Configuration(...)` , faça uma chamada para ConfigureAuth(...) para configurar a autenticação para seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="65654-130">In the `Configuration(...)` method, make a call to ConfigureAuth(...) to set up authentication for your web app</span></span>  

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

5. <span data-ttu-id="65654-131">Abra o arquivo `App_Start\Startup.Auth.cs` e implemente o método `ConfigureAuth(...)`.</span><span class="sxs-lookup"><span data-stu-id="65654-131">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="65654-132">Os parâmetros que você fornece em `OpenIdConnectAuthenticationOptions` servirão como coordenadas para seu aplicativo para se comunicar com o AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="65654-132">The parameters you provide in `OpenIdConnectAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>  <span data-ttu-id="65654-133">Você também precisa configurar a autenticação de Cookies - o middleware OpenID Connect usa cookies nos bastidores.</span><span class="sxs-lookup"><span data-stu-id="65654-133">You'll also need to set up Cookie Authentication - the OpenID Connect middleware uses cookies underneath the covers.</span></span>

        ```C#
        public void ConfigureAuth(IAppBuilder app)
                     {
                             app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);
        
                             app.UseCookieAuthentication(new CookieAuthenticationOptions());
        
                             app.UseOpenIdConnectAuthentication(
                                     new OpenIdConnectAuthenticationOptions
                                     {
                                             // The `Authority` represents the v2.0 endpoint - https://login.microsoftonline.com/common/v2.0
                                             // The `Scope` describes the permissions that your app will need.  See https://azure.microsoft.com/documentation/articles/active-directory-v2-scopes/
                                             // In a real application you could use issuer validation for additional checks, like making sure the user's organization has signed up for your app, for instance.
        
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

## <a name="send-authentication-requests"></a><span data-ttu-id="65654-134">Enviar solicitações de autenticação</span><span class="sxs-lookup"><span data-stu-id="65654-134">Send authentication requests</span></span>
<span data-ttu-id="65654-135">Seu aplicativo agora está configurado corretamente para se comunicar com o ponto de extremidade v2.0 usando o protocolo de autenticação OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="65654-135">Your app is now properly configured to communicate with the v2.0 endpoint using the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="65654-136">O OWIN cuidou de todos os detalhes difíceis da criação de mensagens de autenticação, validação de tokens do AD do Azure e manutenção da sessão do usuário.</span><span class="sxs-lookup"><span data-stu-id="65654-136">OWIN has taken care of all of the ugly details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span>  <span data-ttu-id="65654-137">Tudo o que falta é oferecer aos usuários uma maneira de entrar e sair.</span><span class="sxs-lookup"><span data-stu-id="65654-137">All that remains is to give your users a way to sign in and sign out.</span></span>

- <span data-ttu-id="65654-138">Você pode usar autorizar marcas em seus controladores para exigir que o usuário entre antes de acessar uma determinada página.</span><span class="sxs-lookup"><span data-stu-id="65654-138">You can use authorize tags in your controllers to require that user signs in before accessing a certain page.</span></span>  <span data-ttu-id="65654-139">Abra `Controllers\HomeController.cs` e adicione a marca `[Authorize]` ao controlador Sobre.</span><span class="sxs-lookup"><span data-stu-id="65654-139">Open `Controllers\HomeController.cs`, and add the `[Authorize]` tag to the About controller.</span></span>
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- <span data-ttu-id="65654-140">Você também pode usar o OWIN para emitir diretamente solicitações de autenticação de dentro de seu código.</span><span class="sxs-lookup"><span data-stu-id="65654-140">You can also use OWIN to directly issue authentication requests from within your code.</span></span>  <span data-ttu-id="65654-141">Abra `Controllers\AccountController.cs`.</span><span class="sxs-lookup"><span data-stu-id="65654-141">Open `Controllers\AccountController.cs`.</span></span>  <span data-ttu-id="65654-142">Nas ações SignIn() e SignOut(), emita as solicitações de desafio do OpenID Connect e de saída, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="65654-142">In the SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests, respectively.</span></span>

        ```C#
        public void SignIn()
        {
            // Send an OpenID Connect sign-in request.
            if (!Request.IsAuthenticated)
            {
                HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
            }
        }
        
        // BUGBUG: Ending a session with the v2.0 endpoint is not yet supported.  Here, we just end the session with the web app.  
        public void SignOut()
        {
            // Send an OpenID Connect sign-out request.
            HttpContext.GetOwinContext().Authentication.SignOut(CookieAuthenticationDefaults.AuthenticationType);
            Response.Redirect("/");
        }
        ```

- <span data-ttu-id="65654-143">Agora, abra `Views\Shared\_LoginPartial.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="65654-143">Now, open `Views\Shared\_LoginPartial.cshtml`.</span></span>  <span data-ttu-id="65654-144">É aqui que você vai mostrar ao usuário links de entrada e saída do seu aplicativo e imprimir o nome do usuário em uma exibição.</span><span class="sxs-lookup"><span data-stu-id="65654-144">This is where you'll show the user your app's sign-in and sign-out links, and print out the user's name in a view.</span></span>

        ```HTML
        @if (Request.IsAuthenticated)
        {
            <text>
                <ul class="nav navbar-nav navbar-right">
                    <li class="navbar-text">
        
                        @*The 'preferred_username' claim can be used for showing the user's primary way of identifying themselves.*@
        
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

## <a name="display-user-information"></a><span data-ttu-id="65654-145">Exibir informações do usuário</span><span class="sxs-lookup"><span data-stu-id="65654-145">Display user information</span></span>
<span data-ttu-id="65654-146">Ao autenticar os usuários com o OpenID Connect, o ponto de extremidade v2.0 retorna um id_token para o aplicativo que contém declarações ou afirmações sobre o usuário.</span><span class="sxs-lookup"><span data-stu-id="65654-146">When authenticating users with OpenID Connect, the v2.0 endpoint returns an id_token to the app that contains claims, or assertions about the user.</span></span>  <span data-ttu-id="65654-147">Você pode usar essas declarações para personalizar seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="65654-147">You can use these claims to personalize your app:</span></span>

- <span data-ttu-id="65654-148">Abra o arquivo `Controllers\HomeController.cs` .</span><span class="sxs-lookup"><span data-stu-id="65654-148">Open the `Controllers\HomeController.cs` file.</span></span>  <span data-ttu-id="65654-149">Você pode acessar as declarações do usuário em seus controladores por meio do objeto principal de segurança `ClaimsPrincipal.Current` .</span><span class="sxs-lookup"><span data-stu-id="65654-149">You can access the user's claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

        ```C#
        [Authorize]
        public ActionResult About()
        {
            ViewBag.Name = ClaimsPrincipal.Current.FindFirst("name").Value;
        
            // The object ID claim will only be emitted for work or school accounts at this time.
            Claim oid = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier");
            ViewBag.ObjectId = oid == null ? string.Empty : oid.Value;
        
            // The 'preferred_username' claim can be used for showing the user's primary way of identifying themselves
            ViewBag.Username = ClaimsPrincipal.Current.FindFirst("preferred_username").Value;
        
            // The subject or nameidentifier claim can be used to uniquely identify the user
            ViewBag.Subject = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        
            return View();
        }
        ```

## <a name="run"></a><span data-ttu-id="65654-150">Executar</span><span class="sxs-lookup"><span data-stu-id="65654-150">Run</span></span>
<span data-ttu-id="65654-151">Por fim, compile e execute seu aplicativo!</span><span class="sxs-lookup"><span data-stu-id="65654-151">Finally, build and run your app!</span></span>   <span data-ttu-id="65654-152">Entre com uma conta pessoal da Microsoft ou uma conta corporativa ou de estudante e observe como a identidade do usuário é exibida na barra de navegação superior.</span><span class="sxs-lookup"><span data-stu-id="65654-152">Sign in with either a personal Microsoft Account or a work or school account, and notice how the user's identity is reflected in the top navigation bar.</span></span>  <span data-ttu-id="65654-153">Agora você tem um aplicativo Web protegido por protocolos padrão do setor, que podem autenticar usuários com as respectivas contas pessoais e corporativas ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="65654-153">You now have a web app secured using industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="65654-154">Para referência, o exemplo concluído (sem seus valores de configuração) [é fornecido como um .zip aqui](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), ou você pode cloná-lo do GitHub:</span><span class="sxs-lookup"><span data-stu-id="65654-154">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="65654-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="65654-155">Next steps</span></span>
<span data-ttu-id="65654-156">Agora você pode ir para tópicos mais avançados.</span><span class="sxs-lookup"><span data-stu-id="65654-156">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="65654-157">Você pode desejar experimentar:</span><span class="sxs-lookup"><span data-stu-id="65654-157">You may want to try:</span></span>

[<span data-ttu-id="65654-158">Proteger uma API Web com o ponto de extremidade v2.0 >></span><span class="sxs-lookup"><span data-stu-id="65654-158">Secure a Web API with the the v2.0 endpoint >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

<span data-ttu-id="65654-159">Para obter recursos adicionais, consulte:</span><span class="sxs-lookup"><span data-stu-id="65654-159">For additional resources, check out:</span></span>

* [<span data-ttu-id="65654-160">Guia do desenvolvedor do v2.0 >></span><span class="sxs-lookup"><span data-stu-id="65654-160">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="65654-161">Marca “azure-active-directory” do StackOverflow >></span><span class="sxs-lookup"><span data-stu-id="65654-161">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="65654-162">Obter atualizações de segurança para nossos produtos</span><span class="sxs-lookup"><span data-stu-id="65654-162">Get security updates for our products</span></span>
<span data-ttu-id="65654-163">Recomendamos que você obtenha notificações sobre a ocorrência de incidentes de segurança visitando [esta página](https://technet.microsoft.com/security/dd252948) e assinando os alertas do Security Advisory.</span><span class="sxs-lookup"><span data-stu-id="65654-163">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>
