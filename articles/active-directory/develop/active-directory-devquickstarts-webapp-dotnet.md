---
title: "aplicativo web do .NET aaaAzure AD Introdução | Microsoft Docs"
description: Criar um aplicativo Web MVC do .NET que se integra ao Azure AD para entrar.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e15a41a4-dc5d-4c90-b3fe-5dc33b9a1e96
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 6d3098c9e3d7e1916ccb110c703f501ae52e788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="987a7-103">Entrada e saída do aplicativo Web ASP.NET com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="987a7-103">ASP.NET web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="987a7-104">Fornecendo uma única entrada e saída com apenas algumas linhas de código, o Azure Active Directory (AD do Azure) facilita você toooutsource aplicativo web para gerenciamento de identidade.</span><span class="sxs-lookup"><span data-stu-id="987a7-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you toooutsource web-app identity management.</span></span> <span data-ttu-id="987a7-105">Você pode assinar os usuários e aplicativos web do ASP.NET usando a implementação da Interface Web aberta Microsoft Olá para o middleware .NET (OWIN).</span><span class="sxs-lookup"><span data-stu-id="987a7-105">You can sign users in and out of ASP.NET web apps by using hello Microsoft implementation of Open Web Interface for .NET (OWIN) middleware.</span></span> <span data-ttu-id="987a7-106">O middleware OWIN voltado para a comunidade está incluído no .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="987a7-106">Community-driven OWIN middleware is included in .NET Framework 4.5.</span></span> <span data-ttu-id="987a7-107">Este artigo mostra como toouse OWIN para:</span><span class="sxs-lookup"><span data-stu-id="987a7-107">This article shows how toouse OWIN to:</span></span>

* <span data-ttu-id="987a7-108">Conectar usuários tooweb aplicativos usando o AD do Azure como provedor de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="987a7-108">Sign users in tooweb apps by using Azure AD as hello identity provider.</span></span>
* <span data-ttu-id="987a7-109">Exibir informações do usuário.</span><span class="sxs-lookup"><span data-stu-id="987a7-109">Display some user information.</span></span>
* <span data-ttu-id="987a7-110">Conectar usuários fora da saudação aplicativos.</span><span class="sxs-lookup"><span data-stu-id="987a7-110">Sign users out of hello apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="987a7-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="987a7-111">Before you get started</span></span>
* <span data-ttu-id="987a7-112">Baixar Olá [esqueleto de aplicativo](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) ou baixar Olá [exemplo concluído](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="987a7-112">Download hello [app skeleton](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or download hello [completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span></span>
* <span data-ttu-id="987a7-113">Também é necessário um locatário Azure AD no qual aplicativo de saudação tooregister.</span><span class="sxs-lookup"><span data-stu-id="987a7-113">You also need an Azure AD tenant in which tooregister hello app.</span></span> <span data-ttu-id="987a7-114">Se você ainda não tiver um locatário Azure AD, [Saiba como tooget uma](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="987a7-114">If you don't already have an Azure AD tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="987a7-115">Quando você estiver pronto, siga Olá procedimentos Olá quatro seções.</span><span class="sxs-lookup"><span data-stu-id="987a7-115">When you are ready, follow hello procedures in hello next four sections.</span></span>

## <a name="step-1-register-hello-new-app-with-azure-ad"></a><span data-ttu-id="987a7-116">Etapa 1: Registrar Olá novo aplicativo com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="987a7-116">Step 1: Register hello new app with Azure AD</span></span>
<span data-ttu-id="987a7-117">tooset usuários de tooauthenticate do aplicativo hello, primeiro registrá-lo em seu locatário fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="987a7-117">tooset up hello app tooauthenticate users, first register it in your tenant by doing hello following:</span></span>

1. <span data-ttu-id="987a7-118">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="987a7-118">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="987a7-119">Na barra superior do hello, clique em seu nome de conta.</span><span class="sxs-lookup"><span data-stu-id="987a7-119">On hello top bar, click your account name.</span></span> <span data-ttu-id="987a7-120">Em Olá **diretório** lista, o locatário do Active Directory hello selecione onde você deseja que o aplicativo de saudação tooregister.</span><span class="sxs-lookup"><span data-stu-id="987a7-120">Under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="987a7-121">Clique em **mais serviços** Olá painel esquerdo e, em seguida, selecione **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="987a7-121">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="987a7-122">Clique em **Registros do aplicativo** e, em seguida, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="987a7-122">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="987a7-123">Siga Olá solicita toocreate um novo **aplicativo Web e/ou WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="987a7-123">Follow hello prompts toocreate a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="987a7-124">**Nome** descreve Olá toousers de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="987a7-124">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="987a7-125">**URL de logon** é Olá a URL base do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="987a7-125">**Sign-On URL** is hello base URL of hello app.</span></span> <span data-ttu-id="987a7-126">URL de padrão do esqueleto Olá é https://localhost:44320 /.</span><span class="sxs-lookup"><span data-stu-id="987a7-126">hello skeleton's default URL is https://localhost:44320/.</span></span>
6. <span data-ttu-id="987a7-127">Depois de concluir o registro de saudação, o Azure AD atribui aplicativo hello uma ID exclusiva do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="987a7-127">After you've completed hello registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="987a7-128">Copie o valor de saudação da saudação aplicativo página toouse nas seções próximas hello.</span><span class="sxs-lookup"><span data-stu-id="987a7-128">Copy hello value from hello app page toouse in hello next sections.</span></span>
7. <span data-ttu-id="987a7-129">De saudação **configurações** -> **propriedades** página para seu aplicativo, Olá URI da ID do aplicativo de atualização.</span><span class="sxs-lookup"><span data-stu-id="987a7-129">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="987a7-130">Olá **URI da ID do aplicativo** é um identificador exclusivo para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="987a7-130">hello **App ID URI** is a unique identifier for hello app.</span></span> <span data-ttu-id="987a7-131">Olá convenção de nomenclatura é `https://<tenant-domain>/<app-name>` (por exemplo, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span><span class="sxs-lookup"><span data-stu-id="987a7-131">hello naming convention is `https://<tenant-domain>/<app-name>` (for example, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span></span>

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a><span data-ttu-id="987a7-132">Etapa 2: Configurar o pipeline de autenticação Olá aplicativo toouse Olá OWIN</span><span class="sxs-lookup"><span data-stu-id="987a7-132">Step 2: Set up hello app toouse hello OWIN authentication pipeline</span></span>
<span data-ttu-id="987a7-133">Nesta etapa, você configurará Olá OWIN middleware toouse Olá OpenID Connect protocolo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="987a7-133">In this step, you configure hello OWIN middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="987a7-134">Usar OWIN tooissue solicitações de entrada e saídas, gerenciar sessões de usuário, obter informações de usuário e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="987a7-134">You use OWIN tooissue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

1. <span data-ttu-id="987a7-135">toobegin, adicionar o projeto de toohello Olá OWIN middleware NuGet pacotes usando Olá Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="987a7-135">toobegin, add hello OWIN middleware NuGet packages toohello project by using hello Package Manager Console.</span></span>

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. <span data-ttu-id="987a7-136">tooadd chamado de um projeto de toohello de classe de inicialização OWIN `Startup.cs`, clique com botão direito hello, selecione **adicionar**, selecione **Novo Item**e, em seguida, procure **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="987a7-136">tooadd an OWIN Startup class toohello project called `Startup.cs`, right-click hello project, select **Add**, select **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="987a7-137">Olá OWIN middleware chama Olá **Configuration(...)**  método quando o aplicativo hello for iniciado.</span><span class="sxs-lookup"><span data-stu-id="987a7-137">hello OWIN middleware invokes hello **Configuration(...)** method when hello app starts.</span></span>
3. <span data-ttu-id="987a7-138">Altere a declaração de classe Olá muito`public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="987a7-138">Change hello class declaration too`public partial class Startup`.</span></span> <span data-ttu-id="987a7-139">Já implementamos parte dessa classe para você em outro arquivo.</span><span class="sxs-lookup"><span data-stu-id="987a7-139">We've already implemented part of this class for you in another file.</span></span> <span data-ttu-id="987a7-140">Em Olá **Configuration(...)**  método, fazer uma chamada muito**ConfgureAuth(...)**  tooset a autenticação para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="987a7-140">In hello **Configuration(...)** method, make a call too**ConfgureAuth(...)** tooset up authentication for hello app.</span></span>  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. <span data-ttu-id="987a7-141">Abrir o arquivo de App_Start\Startup.Auth.cs hello e implementar Olá **ConfigureAuth(...)**  método.</span><span class="sxs-lookup"><span data-stu-id="987a7-141">Open hello App_Start\Startup.Auth.cs file, and then implement hello **ConfigureAuth(...)** method.</span></span> <span data-ttu-id="987a7-142">Olá parâmetros que você fornece em *OpenIDConnectAuthenticationOptions* servem como coordenadas de saudação toocommunicate de aplicativo com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="987a7-142">hello parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for hello app toocommunicate with Azure AD.</span></span> <span data-ttu-id="987a7-143">Você também precisa tooset a autenticação de cookie, pois Olá OpenID Connect middleware usa cookies no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="987a7-143">You also need tooset up cookie authentication, because hello OpenID Connect middleware uses cookies in hello background.</span></span>

     ```C#
     public void ConfigureAuth(IAppBuilder app)
     {
         app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

         app.UseCookieAuthentication(new CookieAuthenticationOptions());

         app.UseOpenIdConnectAuthentication(
             new OpenIdConnectAuthenticationOptions
             {
                 ClientId = clientId,
                 Authority = authority,
                 PostLogoutRedirectUri = postLogoutRedirectUri,
                 Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = context =>
                        {
                            context.HandleResponse();
                            context.Response.Redirect("/Error?message=" + context.Exception.Message);
                            return Task.FromResult(0);
                        }
                    }
             });
     }
     ```

5. <span data-ttu-id="987a7-144">Abra o arquivo de Web. config de Olá na raiz de saudação do projeto hello e digite os valores de configuração de saudação em Olá `<appSettings>` seção.</span><span class="sxs-lookup"><span data-stu-id="987a7-144">Open hello web.config file in hello root of hello project, and then enter hello configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="987a7-145">`ida:ClientId`: Olá GUID que você copiou da saudação portal do Azure em "etapa 1: registrar Olá novo aplicativo com o Azure AD."</span><span class="sxs-lookup"><span data-stu-id="987a7-145">`ida:ClientId`: hello GUID you copied from hello Azure portal in "Step 1: Register hello new app with Azure AD."</span></span>
  * <span data-ttu-id="987a7-146">`ida:Tenant`: nome de saudação do seu locatário do AD do Azure (por exemplo, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="987a7-146">`ida:Tenant`: hello name of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="987a7-147">`ida:PostLogoutRedirectUri`: indicador Olá que informa ao AD do Azure em que um usuário deve ser redirecionado após uma solicitação de logout é concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="987a7-147">`ida:PostLogoutRedirectUri`: hello indicator that tells Azure AD where a user should be redirected after a sign-out request is successfully completed.</span></span>

## <a name="step-3-use-owin-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="987a7-148">Etapa 3: Usar OWIN tooissue entrada e saída solicitações tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="987a7-148">Step 3: Use OWIN tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="987a7-149">aplicativo Hello agora está toocommunicate corretamente configurado com o Azure AD usando o protocolo de autenticação OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="987a7-149">hello app is now properly configured toocommunicate with Azure AD by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="987a7-150">OWIN tratou todos os detalhes de saudação da criação de mensagens de autenticação, validando tokens do AD do Azure e manter as sessões do usuário.</span><span class="sxs-lookup"><span data-stu-id="987a7-150">OWIN has handled all of hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="987a7-151">Tudo o que permanece é toogive seus usuários uma maneira toosign no e sair.</span><span class="sxs-lookup"><span data-stu-id="987a7-151">All that remains is toogive your users a way toosign in and sign out.</span></span>

1. <span data-ttu-id="987a7-152">Você pode usar autorizar marcas no seu toosign de usuários toorequire controladores em antes de acessarem certas páginas.</span><span class="sxs-lookup"><span data-stu-id="987a7-152">You can use authorize tags in your controllers toorequire users toosign in before they access certain pages.</span></span> <span data-ttu-id="987a7-153">toodo assim, abra Controllers\HomeController.cs e adicione Olá `[Authorize]` marca toohello sobre o controlador.</span><span class="sxs-lookup"><span data-stu-id="987a7-153">toodo so, open Controllers\HomeController.cs, and then add hello `[Authorize]` tag toohello About controller.</span></span>

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. <span data-ttu-id="987a7-154">Você também pode usar as solicitações de autenticação OWIN toodirectly problema de dentro de seu código.</span><span class="sxs-lookup"><span data-stu-id="987a7-154">You can also use OWIN toodirectly issue authentication requests from within your code.</span></span> <span data-ttu-id="987a7-155">toodo isso, abra Controllers\AccountController.cs.</span><span class="sxs-lookup"><span data-stu-id="987a7-155">toodo so, open Controllers\AccountController.cs.</span></span> <span data-ttu-id="987a7-156">Em seguida, em ações Olá SignIn() e SignOut (), emita desafio OpenID Connect e solicitações de saída.</span><span class="sxs-lookup"><span data-stu-id="987a7-156">Then, in hello SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests.</span></span>

     ```C#
     public void SignIn()
     {
         // Send an OpenID Connect sign-in request.
         if (!Request.IsAuthenticated)
         {
             HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
         }
     }
     public void SignOut()
     {
         // Send an OpenID Connect sign-out request.
         HttpContext.GetOwinContext().Authentication.SignOut(
              OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType);
     }
     ```

3. <span data-ttu-id="987a7-157">Abra exibições \ compartilhadas\_LoginPartial.cshtml tooshow Olá usuário Olá aplicativo entrada e saídos e links tooprint nome do usuário da saudação em uma exibição.</span><span class="sxs-lookup"><span data-stu-id="987a7-157">Open Views\Shared\_LoginPartial.cshtml tooshow hello user hello app sign-in and sign-out links, and tooprint out hello user's name in a view.</span></span>

    ```HTML
    @if (Request.IsAuthenticated)
    {
     <text>
         <ul class="nav navbar-nav navbar-right">
             <li class="navbar-text">
                 Hello, @User.Identity.Name!
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

## <a name="step-4-display-user-information"></a><span data-ttu-id="987a7-158">Etapa 4: exibir informações do usuário</span><span class="sxs-lookup"><span data-stu-id="987a7-158">Step 4: Display user information</span></span>
<span data-ttu-id="987a7-159">Quando ele autentica os usuários com OpenID Connect, o AD do Azure retorna um aplicativo de toohello id_token que contém "declarações", ou declarações sobre o usuário hello.</span><span class="sxs-lookup"><span data-stu-id="987a7-159">When it authenticates users with OpenID Connect, Azure AD returns an id_token toohello app that contains "claims," or assertions about hello user.</span></span> <span data-ttu-id="987a7-160">Você pode usar o aplicativo de saudação de toopersonalize essas declarações fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="987a7-160">You can use these claims toopersonalize hello app by doing hello following:</span></span>

1. <span data-ttu-id="987a7-161">Abra o arquivo de Controllers\HomeController.cs de saudação.</span><span class="sxs-lookup"><span data-stu-id="987a7-161">Open hello Controllers\HomeController.cs file.</span></span> <span data-ttu-id="987a7-162">Você pode acessar declarações saudação do usuário em seus controladores via Olá `ClaimsPrincipal.Current` objeto de segurança.</span><span class="sxs-lookup"><span data-stu-id="987a7-162">You can access hello user's claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

 ```C#
 public ActionResult About()
 {
     ViewBag.Name = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value;
     ViewBag.ObjectId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
     ViewBag.GivenName = ClaimsPrincipal.Current.FindFirst(ClaimTypes.GivenName).Value;
     ViewBag.Surname = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Surname).Value;
     ViewBag.UPN = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn).Value;

     return View();
 }
 ```

2. <span data-ttu-id="987a7-163">Compilar e executar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="987a7-163">Build and run hello app.</span></span> <span data-ttu-id="987a7-164">Se você ainda não criou um novo usuário em seu locatário com um domínio c o m, agora é Olá tempo toodo assim.</span><span class="sxs-lookup"><span data-stu-id="987a7-164">If you haven't already created a new user in your tenant with an onmicrosoft.com domain, now is hello time toodo so.</span></span> <span data-ttu-id="987a7-165">Faça assim:</span><span class="sxs-lookup"><span data-stu-id="987a7-165">Here's how:</span></span>

  <span data-ttu-id="987a7-166">a.</span><span class="sxs-lookup"><span data-stu-id="987a7-166">a.</span></span> <span data-ttu-id="987a7-167">Entrar com esse usuário e observe como identidade do usuário Olá é refletida na barra superior hello.</span><span class="sxs-lookup"><span data-stu-id="987a7-167">Sign in with that user, and note how hello user's identity is reflected on hello top bar.</span></span>

  <span data-ttu-id="987a7-168">b.</span><span class="sxs-lookup"><span data-stu-id="987a7-168">b.</span></span> <span data-ttu-id="987a7-169">Saia e entre novamente como outro usuário em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="987a7-169">Sign out, and then sign back in as another user in your tenant.</span></span>

  <span data-ttu-id="987a7-170">c.</span><span class="sxs-lookup"><span data-stu-id="987a7-170">c.</span></span> <span data-ttu-id="987a7-171">Se você estiver se sentindo particularmente ambicioso, registre e execute outra instância deste aplicativo (com sua própria clientId) e veja o logon único em ação.</span><span class="sxs-lookup"><span data-stu-id="987a7-171">If you're feeling particularly ambitious, register and run another instance of this app (with its own clientId), and watch single sign-in in action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="987a7-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="987a7-172">Next steps</span></span>
<span data-ttu-id="987a7-173">Para referência, consulte [exemplo hello concluída](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (sem os valores de configuração).</span><span class="sxs-lookup"><span data-stu-id="987a7-173">For reference, see [hello completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="987a7-174">Agora você pode mover toomore tópicos avançados.</span><span class="sxs-lookup"><span data-stu-id="987a7-174">You can now move on toomore advanced topics.</span></span> <span data-ttu-id="987a7-175">Por exemplo, experimento [Proteger uma API Web com o Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="987a7-175">For example, try [Secure a Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
