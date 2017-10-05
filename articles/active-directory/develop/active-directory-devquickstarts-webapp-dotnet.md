---
title: "Introdução ao aplicativo Web .NET do Azure AD | Microsoft Docs"
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
ms.openlocfilehash: 7ac5d3e5cc28ead993e159d003244e6451acb0cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="f088d-103">Entrada e saída do aplicativo Web ASP.NET com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="f088d-103">ASP.NET web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="f088d-104">O Azure AD (Azure Active Directory) torna simples e direto terceirizar o gerenciamento de identidades de seu aplicativo Web, fornecendo uma única entrada e uma única saída com apenas algumas linhas de código.</span><span class="sxs-lookup"><span data-stu-id="f088d-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you to outsource web-app identity management.</span></span> <span data-ttu-id="f088d-105">Você pode fazer com que os usuários entrem e saiam de aplicativos Web do ASP.NET usando a implementação da Microsoft do middleware OWIN (Open Web Interface para .NET).</span><span class="sxs-lookup"><span data-stu-id="f088d-105">You can sign users in and out of ASP.NET web apps by using the Microsoft implementation of Open Web Interface for .NET (OWIN) middleware.</span></span> <span data-ttu-id="f088d-106">O middleware OWIN voltado para a comunidade está incluído no .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="f088d-106">Community-driven OWIN middleware is included in .NET Framework 4.5.</span></span> <span data-ttu-id="f088d-107">Este artigo mostra como usar o OWIN para:</span><span class="sxs-lookup"><span data-stu-id="f088d-107">This article shows how to use OWIN to:</span></span>

* <span data-ttu-id="f088d-108">Fazer com que usuários entrem em aplicativos Web usando o Azure AD como o provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="f088d-108">Sign users in to web apps by using Azure AD as the identity provider.</span></span>
* <span data-ttu-id="f088d-109">Exibir informações do usuário.</span><span class="sxs-lookup"><span data-stu-id="f088d-109">Display some user information.</span></span>
* <span data-ttu-id="f088d-110">Desconectar os usuários dos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f088d-110">Sign users out of the apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="f088d-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="f088d-111">Before you get started</span></span>
* <span data-ttu-id="f088d-112">Baixe o [esqueleto do aplicativo](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) ou baixe a [amostra concluída](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="f088d-112">Download the [app skeleton](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or download the [completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span></span>
* <span data-ttu-id="f088d-113">Você também precisará de um locatário do Azure AD no qual registrar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f088d-113">You also need an Azure AD tenant in which to register the app.</span></span> <span data-ttu-id="f088d-114">Se você ainda não tiver um locatário do Azure AD, [saiba como obter um](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="f088d-114">If you don't already have an Azure AD tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="f088d-115">Quando estiver pronto, siga os procedimentos nas próximas quatro seções.</span><span class="sxs-lookup"><span data-stu-id="f088d-115">When you are ready, follow the procedures in the next four sections.</span></span>

## <a name="step-1-register-the-new-app-with-azure-ad"></a><span data-ttu-id="f088d-116">Etapa 1: registrar o novo aplicativo com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="f088d-116">Step 1: Register the new app with Azure AD</span></span>
<span data-ttu-id="f088d-117">Para configurar o aplicativo para autenticar usuários, primeiro registre-o em seu locatário, fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f088d-117">To set up the app to authenticate users, first register it in your tenant by doing the following:</span></span>

1. <span data-ttu-id="f088d-118">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f088d-118">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f088d-119">Na barra superior, clique no nome da conta.</span><span class="sxs-lookup"><span data-stu-id="f088d-119">On the top bar, click your account name.</span></span> <span data-ttu-id="f088d-120">Na lista **Diretório** , selecione o locatário do Active Directory em que você deseja registrar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f088d-120">Under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="f088d-121">Clique em **Mais serviços** no painel esquerdo e selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f088d-121">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="f088d-122">Clique em **Registros do aplicativo** e, em seguida, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f088d-122">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="f088d-123">Siga os prompts para criar um **Aplicativo Web e/ou uma API Web**.</span><span class="sxs-lookup"><span data-stu-id="f088d-123">Follow the prompts to create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="f088d-124">**Nome** descreve o aplicativo aos usuários.</span><span class="sxs-lookup"><span data-stu-id="f088d-124">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="f088d-125">A **URL de logon** é a URL base do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f088d-125">**Sign-On URL** is the base URL of the app.</span></span> <span data-ttu-id="f088d-126">URL de padrão do esqueleto é https://localhost:44320/.</span><span class="sxs-lookup"><span data-stu-id="f088d-126">The skeleton's default URL is https://localhost:44320/.</span></span>
6. <span data-ttu-id="f088d-127">Depois de você concluir o registro, o Azure AD atribui uma ID do aplicativo exclusiva ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f088d-127">After you've completed the registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="f088d-128">Copie o valor da página do aplicativo para usar nas próximas seções.</span><span class="sxs-lookup"><span data-stu-id="f088d-128">Copy the value from the app page to use in the next sections.</span></span>
7. <span data-ttu-id="f088d-129">Na página **Configurações** -> **Propriedades** do aplicativo, atualize o URI da ID do Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f088d-129">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="f088d-130">O **URI da ID do Aplicativo** é um identificador exclusivo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f088d-130">The **App ID URI** is a unique identifier for the app.</span></span> <span data-ttu-id="f088d-131">A convenção de nomenclatura é `https://<tenant-domain>/<app-name>` (por exemplo, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span><span class="sxs-lookup"><span data-stu-id="f088d-131">The naming convention is `https://<tenant-domain>/<app-name>` (for example, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span></span>

## <a name="step-2-set-up-the-app-to-use-the-owin-authentication-pipeline"></a><span data-ttu-id="f088d-132">Etapa 2: configurar o aplicativo para usar o pipeline de autenticação OWIN</span><span class="sxs-lookup"><span data-stu-id="f088d-132">Step 2: Set up the app to use the OWIN authentication pipeline</span></span>
<span data-ttu-id="f088d-133">Nesta etapa, você configurará o middleware OWIN para usar o protocolo de autenticação OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f088d-133">In this step, you configure the OWIN middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="f088d-134">Você usa o OWIN para emitir solicitações de entrada e saída, gerenciar sessões de usuário, obter informações do usuário e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="f088d-134">You use OWIN to issue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

1. <span data-ttu-id="f088d-135">Para começar, adicione os pacotes do NuGet de middleware OWIN ao projeto usando o Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="f088d-135">To begin, add the OWIN middleware NuGet packages to the project by using the Package Manager Console.</span></span>

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. <span data-ttu-id="f088d-136">Para adicionar uma classe de inicialização do OWIN ao projeto chamado `Startup.cs`, clique com o botão direito do mouse no projeto, selecione **Adicionar**, **Novo Item** e então pesquise por **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="f088d-136">To add an OWIN Startup class to the project called `Startup.cs`, right-click the project, select **Add**, select **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="f088d-137">O middleware OWIN invoca o método **Configuration(...)** quando o aplicativo é iniciado.</span><span class="sxs-lookup"><span data-stu-id="f088d-137">The OWIN middleware invokes the **Configuration(...)** method when the app starts.</span></span>
3. <span data-ttu-id="f088d-138">Altere a declaração de classe para `public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="f088d-138">Change the class declaration to `public partial class Startup`.</span></span> <span data-ttu-id="f088d-139">Já implementamos parte dessa classe para você em outro arquivo.</span><span class="sxs-lookup"><span data-stu-id="f088d-139">We've already implemented part of this class for you in another file.</span></span> <span data-ttu-id="f088d-140">No método **Configuration(...)**, faça uma chamada para método **ConfgureAuth(...)** para configurar a autenticação para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f088d-140">In the **Configuration(...)** method, make a call to **ConfgureAuth(...)** to set up authentication for the app.</span></span>  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. <span data-ttu-id="f088d-141">Abra o arquivo App_Start\Startup.Auth.cs e implemente o método **ConfigureAuth(...)** .</span><span class="sxs-lookup"><span data-stu-id="f088d-141">Open the App_Start\Startup.Auth.cs file, and then implement the **ConfigureAuth(...)** method.</span></span> <span data-ttu-id="f088d-142">Os parâmetros que você fornece em *OpenIDConnectAuthenticationOptions* servirão como coordenadas para seu aplicativo se comunicar com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f088d-142">The parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for the app to communicate with Azure AD.</span></span> <span data-ttu-id="f088d-143">Você também precisa configurar a autenticação de Cookies – o middleware OpenID Connect usa cookies em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="f088d-143">You also need to set up cookie authentication, because the OpenID Connect middleware uses cookies in the background.</span></span>

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

5. <span data-ttu-id="f088d-144">Abra o arquivo web.config na raiz do projeto e insira os valores de configuração na seção `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="f088d-144">Open the web.config file in the root of the project, and then enter the configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="f088d-145">`ida:ClientId`: O GUID que você copiou do Portal do Azure em "Etapa 1: Registrar o novo aplicativo com o Azure AD".</span><span class="sxs-lookup"><span data-stu-id="f088d-145">`ida:ClientId`: The GUID you copied from the Azure portal in "Step 1: Register the new app with Azure AD."</span></span>
  * <span data-ttu-id="f088d-146">`ida:Tenant`: o nome do seu locatário do Azure AD (por exemplo, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="f088d-146">`ida:Tenant`: The name of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="f088d-147">`ida:PostLogoutRedirectUri`: indica ao Azure AD para o qual um usuário deverá ser redirecionado após uma solicitação de saída ser concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="f088d-147">`ida:PostLogoutRedirectUri`: The indicator that tells Azure AD where a user should be redirected after a sign-out request is successfully completed.</span></span>

## <a name="step-3-use-owin-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="f088d-148">Etapa 3: usar o OWIN para emitir solicitações de entrada e saída ao Azure AD</span><span class="sxs-lookup"><span data-stu-id="f088d-148">Step 3: Use OWIN to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="f088d-149">O aplicativo agora está configurado corretamente para se comunicar com o Azure AD usando o protocolo de autenticação OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f088d-149">The app is now properly configured to communicate with Azure AD by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="f088d-150">O OWIN cuidou de todos os detalhes da criação de mensagens de autenticação, validação de tokens do Azure AD e manutenção da sessão do usuário.</span><span class="sxs-lookup"><span data-stu-id="f088d-150">OWIN has handled all of the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="f088d-151">Tudo o que falta é oferecer aos usuários uma maneira de entrar e sair.</span><span class="sxs-lookup"><span data-stu-id="f088d-151">All that remains is to give your users a way to sign in and sign out.</span></span>

1. <span data-ttu-id="f088d-152">Você pode usar autorizar marcas em seus controladores para exigir que os usuários entrem antes de acessarem uma determinada página.</span><span class="sxs-lookup"><span data-stu-id="f088d-152">You can use authorize tags in your controllers to require users to sign in before they access certain pages.</span></span> <span data-ttu-id="f088d-153">Para fazer isso, abra Controllers\HomeController.cs e, em seguida, adicione a marcação `[Authorize]` ao controlador About.</span><span class="sxs-lookup"><span data-stu-id="f088d-153">To do so, open Controllers\HomeController.cs, and then add the `[Authorize]` tag to the About controller.</span></span>

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. <span data-ttu-id="f088d-154">Você também pode usar o OWIN para emitir diretamente solicitações de autenticação de dentro de seu código.</span><span class="sxs-lookup"><span data-stu-id="f088d-154">You can also use OWIN to directly issue authentication requests from within your code.</span></span> <span data-ttu-id="f088d-155">Para fazer isso, abra Controllers\AccountController.cs.</span><span class="sxs-lookup"><span data-stu-id="f088d-155">To do so, open Controllers\AccountController.cs.</span></span> <span data-ttu-id="f088d-156">Em seguida, nas ações SignIn() e SignOut(), emita as solicitações de desafio e de saída do OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f088d-156">Then, in the SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests.</span></span>

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

3. <span data-ttu-id="f088d-157">Abra Views\Shared\_LoginPartial.cshtml para mostrar os links de entrada e saída do aplicativo ao usuário e para imprimir o nome do usuário em uma exibição.</span><span class="sxs-lookup"><span data-stu-id="f088d-157">Open Views\Shared\_LoginPartial.cshtml to show the user the app sign-in and sign-out links, and to print out the user's name in a view.</span></span>

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

## <a name="step-4-display-user-information"></a><span data-ttu-id="f088d-158">Etapa 4: exibir informações do usuário</span><span class="sxs-lookup"><span data-stu-id="f088d-158">Step 4: Display user information</span></span>
<span data-ttu-id="f088d-159">Ao autenticar usuários com o OpenID Connect, o Azure AD retorna um id_token para o aplicativo que contém "declarações" ou afirmações sobre o usuário.</span><span class="sxs-lookup"><span data-stu-id="f088d-159">When it authenticates users with OpenID Connect, Azure AD returns an id_token to the app that contains "claims," or assertions about the user.</span></span> <span data-ttu-id="f088d-160">Você pode usar essas declarações para personalizar o aplicativo fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f088d-160">You can use these claims to personalize the app by doing the following:</span></span>

1. <span data-ttu-id="f088d-161">Abra o arquivo Controllers\HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="f088d-161">Open the Controllers\HomeController.cs file.</span></span> <span data-ttu-id="f088d-162">Você pode acessar as declarações do usuário em seus controladores por meio do objeto principal de segurança `ClaimsPrincipal.Current` .</span><span class="sxs-lookup"><span data-stu-id="f088d-162">You can access the user's claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

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

2. <span data-ttu-id="f088d-163">Compile e execute o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f088d-163">Build and run the app.</span></span> <span data-ttu-id="f088d-164">Se você ainda não fez isso, agora é o momento de criar um novo usuário em seu locatário com um domínio onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="f088d-164">If you haven't already created a new user in your tenant with an onmicrosoft.com domain, now is the time to do so.</span></span> <span data-ttu-id="f088d-165">Faça assim:</span><span class="sxs-lookup"><span data-stu-id="f088d-165">Here's how:</span></span>

  <span data-ttu-id="f088d-166">a.</span><span class="sxs-lookup"><span data-stu-id="f088d-166">a.</span></span> <span data-ttu-id="f088d-167">Entre com esse usuário e observe como a identidade do usuário é refletida na barra superior.</span><span class="sxs-lookup"><span data-stu-id="f088d-167">Sign in with that user, and note how the user's identity is reflected on the top bar.</span></span>

  <span data-ttu-id="f088d-168">b.</span><span class="sxs-lookup"><span data-stu-id="f088d-168">b.</span></span> <span data-ttu-id="f088d-169">Saia e entre novamente como outro usuário em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="f088d-169">Sign out, and then sign back in as another user in your tenant.</span></span>

  <span data-ttu-id="f088d-170">c.</span><span class="sxs-lookup"><span data-stu-id="f088d-170">c.</span></span> <span data-ttu-id="f088d-171">Se você estiver se sentindo particularmente ambicioso, registre e execute outra instância deste aplicativo (com sua própria clientId) e veja o logon único em ação.</span><span class="sxs-lookup"><span data-stu-id="f088d-171">If you're feeling particularly ambitious, register and run another instance of this app (with its own clientId), and watch single sign-in in action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f088d-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f088d-172">Next steps</span></span>
<span data-ttu-id="f088d-173">Para referência, veja [a amostra concluída](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (sem seus valores de configuração).</span><span class="sxs-lookup"><span data-stu-id="f088d-173">For reference, see [the completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="f088d-174">Agora você pode passar para tópicos mais avançados.</span><span class="sxs-lookup"><span data-stu-id="f088d-174">You can now move on to more advanced topics.</span></span> <span data-ttu-id="f088d-175">Por exemplo, experimento [Proteger uma API Web com o Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="f088d-175">For example, try [Secure a Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
