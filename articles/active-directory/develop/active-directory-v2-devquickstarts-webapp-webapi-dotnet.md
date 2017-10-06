---
title: "aaaAzure AD v 2.0 .NET web aplicativo API chamada Introdução | Microsoft Docs"
description: Como toobuild um aplicativo de Web do .NET MVC que chama web services usando o Microsoft pessoal contas e trabalho ou escola contas para entrar.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 56be906e-71de-469d-9a5c-9fc08aae4223
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 1a70791418bc2a7d1fdfbafb9b5126a033a32292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="calling-a-web-api-from-a-net-web-app"></a><span data-ttu-id="49405-103">Chamar uma API Web em um aplicativo Web .NET</span><span class="sxs-lookup"><span data-stu-id="49405-103">Calling a web API from a .NET web app</span></span>
<span data-ttu-id="49405-104">Com o ponto de extremidade Olá v 2.0, você pode adicionar autenticação tooyour web aplicativos e APIs da web com suporte para ambas as contas Microsoft pessoais e contas corporativas ou de estudante rapidamente.</span><span class="sxs-lookup"><span data-stu-id="49405-104">With hello v2.0 endpoint, you can quickly add authentication tooyour web apps and web APIs with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="49405-105">Compilaremos aqui um aplicativo Web MVC que faz logon dos usuários usando o OpenID Connect, com alguma ajuda do middleware OWIN da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="49405-105">Here, we'll build an MVC web app that signs users in using OpenID Connect, with some help from Microsoft's OWIN middleware.</span></span>  <span data-ttu-id="49405-106">Olá web aplicativo obter tokens de acesso OAuth 2.0 para uma web api protegida pelo OAuth 2.0 permite criar, ler e excluir em um determinado usuário "lista de tarefas".</span><span class="sxs-lookup"><span data-stu-id="49405-106">hello web app will get OAuth 2.0 access tokens for a web api secured by OAuth 2.0 that allows create, read, and delete on a given user's "To-Do List".</span></span>

<span data-ttu-id="49405-107">Este tutorial serão responsáveis por usando MSAL tooacquire e usar tokens de acesso em um aplicativo web, descrito por completo [aqui](active-directory-v2-flows.md#web-apps).</span><span class="sxs-lookup"><span data-stu-id="49405-107">This tutorial will focus primarily on using MSAL tooacquire and use access tokens in a web app, described in full [here](active-directory-v2-flows.md#web-apps).</span></span>  <span data-ttu-id="49405-108">Como pré-requisitos, talvez você queira toofirst Saiba como muito[Adicionar aplicativo de web básico entrar tooa](active-directory-v2-devquickstarts-dotnet-web.md) ou como muito[proteger corretamente uma API da web](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="49405-108">As prerequisites, you may want toofirst learn how too[add basic sign-in tooa web app](active-directory-v2-devquickstarts-dotnet-web.md) or how too[properly secure a web API](active-directory-v2-devquickstarts-dotnet-api.md).</span></span>

> [!NOTE]
> <span data-ttu-id="49405-109">Nem todos os recursos e cenários de Active Directory do Azure têm suporte pelo ponto de extremidade do hello v 2.0.</span><span class="sxs-lookup"><span data-stu-id="49405-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="49405-110">toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="49405-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-sample-code"></a><span data-ttu-id="49405-111">Baixar código de exemplo</span><span class="sxs-lookup"><span data-stu-id="49405-111">Download sample code</span></span>
<span data-ttu-id="49405-112">código de saudação para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="49405-112">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="49405-113">toofollow ao longo, você pode [baixar o esqueleto do aplicativo hello como. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) ou esqueleto de saudação do clone:</span><span class="sxs-lookup"><span data-stu-id="49405-113">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

<span data-ttu-id="49405-114">Como alternativa, você pode [baixar o aplicativo hello concluído como. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) ou aplicativo de saudação concluída do clone:</span><span class="sxs-lookup"><span data-stu-id="49405-114">Alternatively, you can [download hello completed app as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) or clone hello completed app:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a><span data-ttu-id="49405-115">Registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="49405-115">Register an app</span></span>
<span data-ttu-id="49405-116">Crie um novo aplicativo em [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ou siga estas [etapas detalhadas](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="49405-116">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="49405-117">Não se esqueça de:</span><span class="sxs-lookup"><span data-stu-id="49405-117">Make sure to:</span></span>

* <span data-ttu-id="49405-118">Cópia para baixo Olá **Id do aplicativo** atribuído tooyour aplicativo, você precisará dele em breve.</span><span class="sxs-lookup"><span data-stu-id="49405-118">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="49405-119">Criar um **segredo do aplicativo** de saudação **senha** tipo e copiar para seu valor para mais tarde</span><span class="sxs-lookup"><span data-stu-id="49405-119">Create an **App Secret** of hello **Password** type, and copy down its value for later</span></span>
* <span data-ttu-id="49405-120">Adicionar Olá **Web** plataforma para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="49405-120">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="49405-121">Digite hello correto **URI de redirecionamento**.</span><span class="sxs-lookup"><span data-stu-id="49405-121">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="49405-122">uri de redirecionamento Hello indica tooAzure AD onde as respostas de autenticação deverá ser direcionadas - Olá padrão para este tutorial é `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="49405-122">hello redirect uri indicates tooAzure AD where authentication responses should be directed - hello default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install-owin"></a><span data-ttu-id="49405-123">Instalar a OWIN</span><span class="sxs-lookup"><span data-stu-id="49405-123">Install OWIN</span></span>
<span data-ttu-id="49405-124">Adicionar Olá OWIN middleware NuGet pacotes toohello `TodoList-WebApp` projeto usando Olá Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="49405-124">Add hello OWIN middleware NuGet packages toohello `TodoList-WebApp` project using hello Package Manager Console.</span></span>  <span data-ttu-id="49405-125">Olá OWIN middleware ser usado tooissue solicitações de entrada e saídas, gerenciar Olá sessão de usuário e obter informações sobre o usuário hello, entre outras coisas.</span><span class="sxs-lookup"><span data-stu-id="49405-125">hello OWIN middleware will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-hello-user-in"></a><span data-ttu-id="49405-126">Usuário de saudação de logon no</span><span class="sxs-lookup"><span data-stu-id="49405-126">Sign hello user in</span></span>
<span data-ttu-id="49405-127">Configurar Olá Olá de toouse de middleware OWIN [protocolo de autenticação OpenID Connect](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="49405-127">Now configure hello OWIN middleware toouse hello [OpenID Connect authentication protocol](active-directory-v2-protocols.md).</span></span>  

* <span data-ttu-id="49405-128">Olá abrir `web.config` arquivo na raiz de saudação da saudação `TodoList-WebApp` do projeto e insira os valores de configuração do aplicativo no hello `<appSettings>` seção.</span><span class="sxs-lookup"><span data-stu-id="49405-128">Open hello `web.config` file in hello root of hello `TodoList-WebApp` project, and enter your app's configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="49405-129">Olá `ida:ClientId` é hello **Id do aplicativo** atribuído tooyour aplicativo no portal de registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="49405-129">hello `ida:ClientId` is hello **Application Id** assigned tooyour app in hello registration portal.</span></span>
  * <span data-ttu-id="49405-130">Olá `ida:ClientSecret` é hello **segredo do aplicativo** criado no portal de registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="49405-130">hello `ida:ClientSecret` is hello **App Secret** you created in hello registration portal.</span></span>
  * <span data-ttu-id="49405-131">Olá `ida:RedirectUri` é hello **Uri de redirecionamento** inserido no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="49405-131">hello `ida:RedirectUri` is hello **Redirect Uri** you entered in hello portal.</span></span>
* <span data-ttu-id="49405-132">Olá abrir `web.config` arquivo na raiz de saudação da saudação `TodoList-Service` do projeto e substituir Olá `ida:Audience` com hello mesmo **Id do aplicativo** como acima.</span><span class="sxs-lookup"><span data-stu-id="49405-132">Open hello `web.config` file in hello root of hello `TodoList-Service` project, and replace hello `ida:Audience` with hello same **Application Id** as above.</span></span>
* <span data-ttu-id="49405-133">Arquivo hello abrir `App_Start\Startup.Auth.cs` e adicione `using` instruções para bibliotecas de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="49405-133">Open hello file `App_Start\Startup.Auth.cs` and add `using` statements for hello libraries from above.</span></span>
* <span data-ttu-id="49405-134">No hello mesmo arquivo, implementar Olá `ConfigureAuth(...)` método.</span><span class="sxs-lookup"><span data-stu-id="49405-134">In hello same file, implement hello `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="49405-135">Olá parâmetros que você fornece em `OpenIDConnectAuthenticationOptions` servirá como coordenadas para toocommunicate seu aplicativo com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49405-135">hello parameters you provide in `OpenIDConnectAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>

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
                    Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0 "),
                    Scope = "openid email profile offline_access",
                    RedirectUri = redirectUri,
                    PostLogoutRedirectUri = redirectUri,
                    TokenValidationParameters = new TokenValidationParameters
                    {
                        ValidateIssuer = false,
                    },

                    // hello `AuthorizationCodeReceived` notification is used toocapture and redeem hello authorization_code that hello v2.0 endpoint returns tooyour app.

                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed,
                        AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    }

        });
}
// ...
```

## <a name="use-msal-tooget-access-tokens"></a><span data-ttu-id="49405-136">Usar tokens de acesso de tooget MSAL</span><span class="sxs-lookup"><span data-stu-id="49405-136">Use MSAL tooget access tokens</span></span>
<span data-ttu-id="49405-137">Em Olá `AuthorizationCodeReceived` notificação, queremos toouse [OAuth 2.0 em tandem com OpenID Connect](active-directory-v2-protocols.md) tooredeem Olá authorization_code para um toohello de token de acesso serviço da lista de tarefas pendentes.</span><span class="sxs-lookup"><span data-stu-id="49405-137">In hello `AuthorizationCodeReceived` notification, we want toouse [OAuth 2.0 in tandem with OpenID Connect](active-directory-v2-protocols.md) tooredeem hello authorization_code for an access token toohello To-Do List Service.</span></span>  <span data-ttu-id="49405-138">A MSAL pode facilitar esse processo para você:</span><span class="sxs-lookup"><span data-stu-id="49405-138">MSAL can make this process easy for you:</span></span>

* <span data-ttu-id="49405-139">Primeiro, instale a versão de visualização de saudação do MSAL:</span><span class="sxs-lookup"><span data-stu-id="49405-139">First, install hello preview version of MSAL:</span></span>

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* <span data-ttu-id="49405-140">E adicione outro `using` instrução toohello `App_Start\Startup.Auth.cs` arquivo para MSAL.</span><span class="sxs-lookup"><span data-stu-id="49405-140">And add another `using` statement toohello `App_Start\Startup.Auth.cs` file for MSAL.</span></span>
* <span data-ttu-id="49405-141">Agora adicione um novo método, hello `OnAuthorizationCodeReceived` manipulador de eventos.</span><span class="sxs-lookup"><span data-stu-id="49405-141">Now add a new method, hello `OnAuthorizationCodeReceived` event handler.</span></span>  <span data-ttu-id="49405-142">Este manipulador usará MSAL tooacquire um toohello de token de acesso API da lista de tarefas e armazenará o token Olá no cache de token do MSAL para mais tarde:</span><span class="sxs-lookup"><span data-stu-id="49405-142">This handler will use MSAL tooacquire an access token toohello To-Do List API, and will store hello token in MSAL's token cache for later:</span></span>

```C#
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
        string userObjectId = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        string tenantID = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
        string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenantID, string.Empty);
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        // Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
        app = new ConfidentialClientApplication(Startup.clientId, redirectUri, cred, new NaiveSessionCache(userObjectId, notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase)) {};
        var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { clientId }, notification.Code);
}
// ...
```

* <span data-ttu-id="49405-143">Em aplicativos da web, MSAL tem um cache de token extensível que pode ser usado toostore tokens.</span><span class="sxs-lookup"><span data-stu-id="49405-143">In web apps, MSAL has an extensible token cache that can be used toostore tokens.</span></span>  <span data-ttu-id="49405-144">Este exemplo implementa Olá `NaiveSessionCache` que usa tokens de toocache de armazenamento de sessão http.</span><span class="sxs-lookup"><span data-stu-id="49405-144">This sample implements hello `NaiveSessionCache` which uses http session storage toocache tokens.</span></span>

<!-- TODO: Token Cache article -->


## <a name="call-hello-web-api"></a><span data-ttu-id="49405-145">Saudação de chamada de API da Web</span><span class="sxs-lookup"><span data-stu-id="49405-145">Call hello Web API</span></span>
<span data-ttu-id="49405-146">Agora é hora tooactually usar access_token Olá que você copiou na etapa 3.</span><span class="sxs-lookup"><span data-stu-id="49405-146">Now it's time tooactually use hello access_token you acquired in step 3.</span></span>  <span data-ttu-id="49405-147">Do aplicativo da web aberto Olá `Controllers\TodoListController.cs` de arquivos, que faz com que todos os Olá CRUD solicitações toohello API da lista de tarefas pendentes.</span><span class="sxs-lookup"><span data-stu-id="49405-147">Open hello web app's `Controllers\TodoListController.cs` file, which makes all hello CRUD requests toohello To-Do List API.</span></span>

* <span data-ttu-id="49405-148">Você pode usar MSAL novamente aqui access_tokens toofetch de Olá cache MSAL.</span><span class="sxs-lookup"><span data-stu-id="49405-148">You can use MSAL again here toofetch access_tokens from hello MSAL cache.</span></span>  <span data-ttu-id="49405-149">Primeiro, adicione um `using` instrução para MSAL toothis arquivo.</span><span class="sxs-lookup"><span data-stu-id="49405-149">First, add a `using` statement for MSAL toothis file.</span></span>
  
    `using Microsoft.Identity.Client;`
* <span data-ttu-id="49405-150">Em Olá `Index` ação, use MSAL `AcquireTokenSilentAsync` método tooget um access_token que podem ser dados tooread usado da saudação serviço de lista de tarefas:</span><span class="sxs-lookup"><span data-stu-id="49405-150">In hello `Index` action, use MSAL's `AcquireTokenSilentAsync` method tooget an access_token that can be used tooread data from hello To-Do List service:</span></span>

```C#
// ...
string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
string tenantID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
string authority = String.Format(CultureInfo.InvariantCulture, Startup.aadInstance, tenantID, string.Empty);
ClientCredential credential = new ClientCredential(Startup.clientId, Startup.clientSecret);

// Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
app = new ConfidentialClientApplication(Startup.clientId, redirectUri, credential, new NaiveSessionCache(userObjectID, this.HttpContext)){};
result = await app.AcquireTokenSilentAsync(new string[] { Startup.clientId });
// ...
```

* <span data-ttu-id="49405-151">Olá exemplo então adiciona solicitação de HTTP GET de token toohello resultante hello como Olá `Authorization` cabeçalho, qual serviço de lista de tarefas pendentes de saudação usa tooauthenticate solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="49405-151">hello sample then adds hello resulting token toohello HTTP GET request as hello `Authorization` header, which hello To-Do List service uses tooauthenticate hello request.</span></span>
* <span data-ttu-id="49405-152">Se Olá serviço de lista de tarefas retornará um `401 Unauthorized` resposta, Olá access_tokens em MSAL se tornam inválidos por alguma razão.</span><span class="sxs-lookup"><span data-stu-id="49405-152">If hello To-Do List service returns a `401 Unauthorized` response, hello access_tokens in MSAL have become invalid for some reason.</span></span>  <span data-ttu-id="49405-153">Nesse caso, você deve remover qualquer access_tokens de saudação cache MSAL e mostrar uma mensagem que talvez seja necessário toosign no novamente, que reiniciará o fluxo de aquisição de token de saudação do usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="49405-153">In this case, you should drop any access_tokens from hello MSAL cache and show hello user a message that they may need toosign in again, which will restart hello token acquisition flow.</span></span>

```C#
// ...
// If hello call failed with access denied, then drop hello current access token from hello cache,
// and show hello user an error indicating they might need toosign-in again.
if (response.StatusCode == System.Net.HttpStatusCode.Unauthorized)
{
        app.AppTokenCache.Clear(Startup.clientId);

        return new RedirectResult("/Error?message=Error: " + response.ReasonPhrase + " You might need toosign in again.");
}
// ...
```

* <span data-ttu-id="49405-154">Da mesma forma, se MSAL for tooreturn não é possível um access_token por qualquer motivo, você deve instruir Olá usuário toosign em novamente.</span><span class="sxs-lookup"><span data-stu-id="49405-154">Similarly, if MSAL is unable tooreturn an access_token for any reason, you should instruct hello user toosign in again.</span></span>  <span data-ttu-id="49405-155">Isso é tão simples quanto capturar qualquer `MSALException`:</span><span class="sxs-lookup"><span data-stu-id="49405-155">This is as simple as catching any `MSALException`:</span></span>

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show hello user an error indicating they might need toosign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading tooDo List: " + ee.Message + " You might need toolog out and log back in.");
}
// ...
```

* <span data-ttu-id="49405-156">Olá exato mesmo `AcquireTokenSilentAsync` chamada é implementd no hello `Create` e `Delete` ações.</span><span class="sxs-lookup"><span data-stu-id="49405-156">hello exact same `AcquireTokenSilentAsync` call is implementd in hello `Create` and `Delete` actions.</span></span>  <span data-ttu-id="49405-157">Em aplicativos da web, você pode usar este access_tokens de tooget MSAL método sempre que você precisar deles em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="49405-157">In web apps, you can use this MSAL method tooget access_tokens whenever you need them in your app.</span></span>  <span data-ttu-id="49405-158">A MSAL se encarregará da aquisição, do caching e da atualização de tokens.</span><span class="sxs-lookup"><span data-stu-id="49405-158">MSAL will take care of acquiring, caching, and refreshing tokens for you.</span></span>

<span data-ttu-id="49405-159">Por fim, compile e execute seu aplicativo!</span><span class="sxs-lookup"><span data-stu-id="49405-159">Finally, build and run your app!</span></span>  <span data-ttu-id="49405-160">Entrar com uma Account da Microsoft ou uma conta do AD do Azure e observe como a identidade do usuário Olá é refletida na barra de navegação superior hello.</span><span class="sxs-lookup"><span data-stu-id="49405-160">Sign in with either a Microsoft Account or an Azure AD Account, and notice how hello user's identity is reflected in hello top navigation bar.</span></span>  <span data-ttu-id="49405-161">Adicionar e excluir alguns itens da lista de tarefas do usuário Olá chama toosee Olá que OAuth 2.0 protegidos API em ação.</span><span class="sxs-lookup"><span data-stu-id="49405-161">Add and delete some items from hello user's To-Do List toosee hello OAuth 2.0 secured API calls in action.</span></span>  <span data-ttu-id="49405-162">Agora você tem um aplicativo Web e uma API Web, ambos protegidos por protocolos padrão do setor, que podem autenticar usuários com as respectivas contas pessoais e corporativas/de estudante.</span><span class="sxs-lookup"><span data-stu-id="49405-162">You now have a web app & web API, both secured using industry standard protocols, that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="49405-163">Para referência, Olá concluída exemplo (sem os valores de configuração) [são fornecidas aqui](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="49405-163">For reference, hello completed sample (without your configuration values) [is provided here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="49405-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="49405-164">Next Steps</span></span>
<span data-ttu-id="49405-165">Para obter recursos adicionais, consulte:</span><span class="sxs-lookup"><span data-stu-id="49405-165">For additional resources, check out:</span></span>

* [<span data-ttu-id="49405-166">Guia do desenvolvedor v 2.0 Olá >></span><span class="sxs-lookup"><span data-stu-id="49405-166">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="49405-167">Marca “azure-active-directory” do StackOverflow >></span><span class="sxs-lookup"><span data-stu-id="49405-167">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="49405-168">Obter atualizações de segurança para nossos produtos</span><span class="sxs-lookup"><span data-stu-id="49405-168">Get security updates for our products</span></span>
<span data-ttu-id="49405-169">Recomendamos que você tooget as notificações quando os incidentes de segurança ocorrem visitando [essa página](https://technet.microsoft.com/security/dd252948) e assinando tooSecurity alertas de aviso.</span><span class="sxs-lookup"><span data-stu-id="49405-169">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

