---
title: "Introdução à API de chamada do aplicativo Web .NET v2.0 do Azure AD | Microsoft Docs"
description: "Como criar um aplicativo Web do MVC .NET que chama serviços Web usando contas pessoais da Microsoft e contas corporativas ou de estudante para conexão."
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
ms.openlocfilehash: dc3162ae8e6ce622139125c2e78fa45d2e90d534
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="calling-a-web-api-from-a-net-web-app"></a><span data-ttu-id="19767-103">Chamar uma API Web em um aplicativo Web .NET</span><span class="sxs-lookup"><span data-stu-id="19767-103">Calling a web API from a .NET web app</span></span>
<span data-ttu-id="19767-104">Com o ponto de extremidade v2.0, você pode adicionar autenticação rapidamente a seus aplicativos Web e APIs Web com suporte a contas pessoais da Microsoft e contas corporativas ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="19767-104">With the v2.0 endpoint, you can quickly add authentication to your web apps and web APIs with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="19767-105">Compilaremos aqui um aplicativo Web MVC que faz logon dos usuários usando o OpenID Connect, com alguma ajuda do middleware OWIN da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19767-105">Here, we'll build an MVC web app that signs users in using OpenID Connect, with some help from Microsoft's OWIN middleware.</span></span>  <span data-ttu-id="19767-106">O aplicativo Web obterá tokens de acesso OAuth 2.0 para uma API Web protegida pelo OAuth 2.0 que permite criar, ler e excluir itens de uma determinado “Lista de Tarefas Pendentes” do usuário.</span><span class="sxs-lookup"><span data-stu-id="19767-106">The web app will get OAuth 2.0 access tokens for a web api secured by OAuth 2.0 that allows create, read, and delete on a given user's "To-Do List".</span></span>

<span data-ttu-id="19767-107">Este tutorial se concentrará principalmente em usar ADAL para adquirir e usar tokens de acesso em um aplicativo Web, descrito por completo [aqui](active-directory-v2-flows.md#web-apps).</span><span class="sxs-lookup"><span data-stu-id="19767-107">This tutorial will focus primarily on using MSAL to acquire and use access tokens in a web app, described in full [here](active-directory-v2-flows.md#web-apps).</span></span>  <span data-ttu-id="19767-108">Como pré-requisitos, talvez você queira aprender primeiro a [adicionar conexão básica a um aplicativo Web](active-directory-v2-devquickstarts-dotnet-web.md) ou a [proteger corretamente uma API Web](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="19767-108">As prerequisites, you may want to first learn how to [add basic sign-in to a web app](active-directory-v2-devquickstarts-dotnet-web.md) or how to [properly secure a web API](active-directory-v2-devquickstarts-dotnet-api.md).</span></span>

> [!NOTE]
> <span data-ttu-id="19767-109">Nem todos os recursos e cenários do Azure Active Directory têm suporte no ponto de extremidade v2.0.</span><span class="sxs-lookup"><span data-stu-id="19767-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="19767-110">Para determinar se você deve usar o ponto de extremidade v2.0, leia sobre as [limitações da v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="19767-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-sample-code"></a><span data-ttu-id="19767-111">Baixar código de exemplo</span><span class="sxs-lookup"><span data-stu-id="19767-111">Download sample code</span></span>
<span data-ttu-id="19767-112">O código para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="19767-112">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="19767-113">Para acompanhar, você pode [baixar o esqueleto do aplicativo como um .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) ou clonar o esqueleto:</span><span class="sxs-lookup"><span data-stu-id="19767-113">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

<span data-ttu-id="19767-114">Como alternativa, você pode [baixar o aplicativo concluído como. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) ou clonar o aplicativo concluído:</span><span class="sxs-lookup"><span data-stu-id="19767-114">Alternatively, you can [download the completed app as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) or clone the completed app:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a><span data-ttu-id="19767-115">Registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="19767-115">Register an app</span></span>
<span data-ttu-id="19767-116">Crie um novo aplicativo em [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ou siga estas [etapas detalhadas](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="19767-116">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="19767-117">Não se esqueça de:</span><span class="sxs-lookup"><span data-stu-id="19767-117">Make sure to:</span></span>

* <span data-ttu-id="19767-118">Copiar a **ID do Aplicativo** designada ao seu aplicativo, você precisará dela logo.</span><span class="sxs-lookup"><span data-stu-id="19767-118">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="19767-119">Crie um **Segredo de Aplicativo** do tipo **Senha** e anote seu valor para uso posterior</span><span class="sxs-lookup"><span data-stu-id="19767-119">Create an **App Secret** of the **Password** type, and copy down its value for later</span></span>
* <span data-ttu-id="19767-120">Adicionar a plataforma **Web** para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="19767-120">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="19767-121">Inserir o **URI de Redirecionamento**correto.</span><span class="sxs-lookup"><span data-stu-id="19767-121">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="19767-122">O URI de redirecionamento indica ao Azure AD para onde as respostas de autenticação devem ser direcionadas — o padrão para este tutorial é `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="19767-122">The redirect uri indicates to Azure AD where authentication responses should be directed - the default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install-owin"></a><span data-ttu-id="19767-123">Instalar a OWIN</span><span class="sxs-lookup"><span data-stu-id="19767-123">Install OWIN</span></span>
<span data-ttu-id="19767-124">Agora adicione os pacotes NuGet do middleware OWIN ao projeto `TodoList-WebApp` usando o Console de Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="19767-124">Add the OWIN middleware NuGet packages to the `TodoList-WebApp` project using the Package Manager Console.</span></span>  <span data-ttu-id="19767-125">O OWIN será usado para emitir solicitações de entrada e saída, gerenciar a sessão do usuário e obter informações sobre o usuário, entre outras coisas.</span><span class="sxs-lookup"><span data-stu-id="19767-125">The OWIN middleware will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-the-user-in"></a><span data-ttu-id="19767-126">Conectar o usuário</span><span class="sxs-lookup"><span data-stu-id="19767-126">Sign the user in</span></span>
<span data-ttu-id="19767-127">Configuraremos aqui o middleware OWIN para usar o [protocolo de autenticação do OpenID Connect](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="19767-127">Now configure the OWIN middleware to use the [OpenID Connect authentication protocol](active-directory-v2-protocols.md).</span></span>  

* <span data-ttu-id="19767-128">Abra o arquivo `web.config` na raiz do projeto `TodoList-WebApp` e insira os valores de configuração do aplicativo na seção `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="19767-128">Open the `web.config` file in the root of the `TodoList-WebApp` project, and enter your app's configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="19767-129">`ida:ClientId` é a **ID do Aplicativo** atribuída ao seu aplicativo no portal de registro.</span><span class="sxs-lookup"><span data-stu-id="19767-129">The `ida:ClientId` is the **Application Id** assigned to your app in the registration portal.</span></span>
  * <span data-ttu-id="19767-130">O `ida:ClientSecret` é o **Segredo de Aplicativo** criado no portal de registro.</span><span class="sxs-lookup"><span data-stu-id="19767-130">The `ida:ClientSecret` is the **App Secret** you created in the registration portal.</span></span>
  * <span data-ttu-id="19767-131">`ida:RedirectUri` é o **URI de Redirecionamento** inserido no portal.</span><span class="sxs-lookup"><span data-stu-id="19767-131">The `ida:RedirectUri` is the **Redirect Uri** you entered in the portal.</span></span>
* <span data-ttu-id="19767-132">Abra o arquivo `web.config` na raiz do projeto `TodoList-Service` e substitua `ida:Audience` pela mesma **Id de Aplicativo**, como acima.</span><span class="sxs-lookup"><span data-stu-id="19767-132">Open the `web.config` file in the root of the `TodoList-Service` project, and replace the `ida:Audience` with the same **Application Id** as above.</span></span>
* <span data-ttu-id="19767-133">Abra o arquivo `App_Start\Startup.Auth.cs` e adicione instruções `using` para as bibliotecas acima.</span><span class="sxs-lookup"><span data-stu-id="19767-133">Open the file `App_Start\Startup.Auth.cs` and add `using` statements for the libraries from above.</span></span>
* <span data-ttu-id="19767-134">No mesmo arquivo, implemente o método `ConfigureAuth(...)` .</span><span class="sxs-lookup"><span data-stu-id="19767-134">In the same file, implement the `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="19767-135">Os parâmetros que você fornece em `OpenIDConnectAuthenticationOptions` servirão como coordenadas para seu aplicativo para se comunicar com o AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="19767-135">The parameters you provide in `OpenIDConnectAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>

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
                    Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0 "),
                    Scope = "openid email profile offline_access",
                    RedirectUri = redirectUri,
                    PostLogoutRedirectUri = redirectUri,
                    TokenValidationParameters = new TokenValidationParameters
                    {
                        ValidateIssuer = false,
                    },

                    // The `AuthorizationCodeReceived` notification is used to capture and redeem the authorization_code that the v2.0 endpoint returns to your app.

                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed,
                        AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    }

        });
}
// ...
```

## <a name="use-msal-to-get-access-tokens"></a><span data-ttu-id="19767-136">Usar a MSAL para obter acesso a tokens</span><span class="sxs-lookup"><span data-stu-id="19767-136">Use MSAL to get access tokens</span></span>
<span data-ttu-id="19767-137">Na notificação `AuthorizationCodeReceived`, queremos usar [OAuth 2.0 em conjunto com o OpenID Connect](active-directory-v2-protocols.md) para resgatar o authorization_code de um token de acesso para o Serviço Lista de Tarefas Pendentes.</span><span class="sxs-lookup"><span data-stu-id="19767-137">In the `AuthorizationCodeReceived` notification, we want to use [OAuth 2.0 in tandem with OpenID Connect](active-directory-v2-protocols.md) to redeem the authorization_code for an access token to the To-Do List Service.</span></span>  <span data-ttu-id="19767-138">A MSAL pode facilitar esse processo para você:</span><span class="sxs-lookup"><span data-stu-id="19767-138">MSAL can make this process easy for you:</span></span>

* <span data-ttu-id="19767-139">Primeiramente, instale a versão de visualização da MSAL:</span><span class="sxs-lookup"><span data-stu-id="19767-139">First, install the preview version of MSAL:</span></span>

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* <span data-ttu-id="19767-140">E adicione outra instrução `using` ao arquivo `App_Start\Startup.Auth.cs`da MSAL.</span><span class="sxs-lookup"><span data-stu-id="19767-140">And add another `using` statement to the `App_Start\Startup.Auth.cs` file for MSAL.</span></span>
* <span data-ttu-id="19767-141">Agora, adicione um novo método, o manipulador de eventos `OnAuthorizationCodeReceived`.</span><span class="sxs-lookup"><span data-stu-id="19767-141">Now add a new method, the `OnAuthorizationCodeReceived` event handler.</span></span>  <span data-ttu-id="19767-142">Esse manipulador usará a MSAL para adquirir um token de acesso para a API Lista de Tarefas Pendentes e armazenará o token no cache do token da MSAL para depois:</span><span class="sxs-lookup"><span data-stu-id="19767-142">This handler will use MSAL to acquire an access token to the To-Do List API, and will store the token in MSAL's token cache for later:</span></span>

```C#
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
        string userObjectId = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        string tenantID = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
        string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenantID, string.Empty);
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        // Here you ask for a token using the web app's clientId as the scope, since the web app and service share the same clientId.
        app = new ConfidentialClientApplication(Startup.clientId, redirectUri, cred, new NaiveSessionCache(userObjectId, notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase)) {};
        var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { clientId }, notification.Code);
}
// ...
```

* <span data-ttu-id="19767-143">Em aplicativos Web, a MSAL tem um cache de token extensível que pode ser usado para armazenar tokens.</span><span class="sxs-lookup"><span data-stu-id="19767-143">In web apps, MSAL has an extensible token cache that can be used to store tokens.</span></span>  <span data-ttu-id="19767-144">Este exemplo implementa o `NaiveSessionCache` , que usa o armazenamento de sessão http para tokens de cache.</span><span class="sxs-lookup"><span data-stu-id="19767-144">This sample implements the `NaiveSessionCache` which uses http session storage to cache tokens.</span></span>

<!-- TODO: Token Cache article -->


## <a name="call-the-web-api"></a><span data-ttu-id="19767-145">Chamar a API Web</span><span class="sxs-lookup"><span data-stu-id="19767-145">Call the Web API</span></span>
<span data-ttu-id="19767-146">Agora é hora de usar de fato o access_token que você acabou de adquirir na etapa 3.</span><span class="sxs-lookup"><span data-stu-id="19767-146">Now it's time to actually use the access_token you acquired in step 3.</span></span>  <span data-ttu-id="19767-147">Abra o arquivo `Controllers\TodoListController.cs` do aplicativo Web, que faz todas as solicitações CRUD à API da Lista de Tarefas Pendentes.</span><span class="sxs-lookup"><span data-stu-id="19767-147">Open the web app's `Controllers\TodoListController.cs` file, which makes all the CRUD requests to the To-Do List API.</span></span>

* <span data-ttu-id="19767-148">Aqui, você pode usar a MSAL novamente para buscar access_tokens no cache da MSAL.</span><span class="sxs-lookup"><span data-stu-id="19767-148">You can use MSAL again here to fetch access_tokens from the MSAL cache.</span></span>  <span data-ttu-id="19767-149">Primeiramente, adicione uma instrução `using` para MSAL a este arquivo.</span><span class="sxs-lookup"><span data-stu-id="19767-149">First, add a `using` statement for MSAL to this file.</span></span>
  
    `using Microsoft.Identity.Client;`
* <span data-ttu-id="19767-150">Na ação `Index`, use o método `AcquireTokenSilentAsync` da MSAL para obter um access_token que possa ser usado para ler dados no serviço Lista de Tarefas Pendentes:</span><span class="sxs-lookup"><span data-stu-id="19767-150">In the `Index` action, use MSAL's `AcquireTokenSilentAsync` method to get an access_token that can be used to read data from the To-Do List service:</span></span>

```C#
// ...
string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
string tenantID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
string authority = String.Format(CultureInfo.InvariantCulture, Startup.aadInstance, tenantID, string.Empty);
ClientCredential credential = new ClientCredential(Startup.clientId, Startup.clientSecret);

// Here you ask for a token using the web app's clientId as the scope, since the web app and service share the same clientId.
app = new ConfidentialClientApplication(Startup.clientId, redirectUri, credential, new NaiveSessionCache(userObjectID, this.HttpContext)){};
result = await app.AcquireTokenSilentAsync(new string[] { Startup.clientId });
// ...
```

* <span data-ttu-id="19767-151">O exemplo adiciona o token resultante à solicitação HTTP GET, como o cabeçalho `Authorization`, que o serviço Lista de Tarefas Pendentes usa para autenticar a solicitação.</span><span class="sxs-lookup"><span data-stu-id="19767-151">The sample then adds the resulting token to the HTTP GET request as the `Authorization` header, which the To-Do List service uses to authenticate the request.</span></span>
* <span data-ttu-id="19767-152">Se o serviço Lista de Tarefas Pendentes retornar uma resposta `401 Unauthorized`, access_tokens na MSAL se tornarão inválidos por algum motivo.</span><span class="sxs-lookup"><span data-stu-id="19767-152">If the To-Do List service returns a `401 Unauthorized` response, the access_tokens in MSAL have become invalid for some reason.</span></span>  <span data-ttu-id="19767-153">Nesse caso, você deve descartar todos os access_token do cache da MSAL e mostrar ao usuário uma mensagem que ele pode precisar para entrar novamente, que reiniciará o fluxo de aquisição de token.</span><span class="sxs-lookup"><span data-stu-id="19767-153">In this case, you should drop any access_tokens from the MSAL cache and show the user a message that they may need to sign in again, which will restart the token acquisition flow.</span></span>

```C#
// ...
// If the call failed with access denied, then drop the current access token from the cache,
// and show the user an error indicating they might need to sign-in again.
if (response.StatusCode == System.Net.HttpStatusCode.Unauthorized)
{
        app.AppTokenCache.Clear(Startup.clientId);

        return new RedirectResult("/Error?message=Error: " + response.ReasonPhrase + " You might need to sign in again.");
}
// ...
```

* <span data-ttu-id="19767-154">Da mesma forma, se a MSAL não puder retornar um access_token por algum motivo, você deverá orientar o usuário a entrar novamente.</span><span class="sxs-lookup"><span data-stu-id="19767-154">Similarly, if MSAL is unable to return an access_token for any reason, you should instruct the user to sign in again.</span></span>  <span data-ttu-id="19767-155">Isso é tão simples quanto capturar qualquer `MSALException`:</span><span class="sxs-lookup"><span data-stu-id="19767-155">This is as simple as catching any `MSALException`:</span></span>

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show the user an error indicating they might need to sign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading To Do List: " + ee.Message + " You might need to log out and log back in.");
}
// ...
```

* <span data-ttu-id="19767-156">A mesma chamada `AcquireTokenSilentAsync` é implementada nas ações `Create` e `Delete`.</span><span class="sxs-lookup"><span data-stu-id="19767-156">The exact same `AcquireTokenSilentAsync` call is implementd in the `Create` and `Delete` actions.</span></span>  <span data-ttu-id="19767-157">Em aplicativos Web, você pode usar esse método MSAL para obter access_tokens sempre que precisar deles em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="19767-157">In web apps, you can use this MSAL method to get access_tokens whenever you need them in your app.</span></span>  <span data-ttu-id="19767-158">A MSAL se encarregará da aquisição, do caching e da atualização de tokens.</span><span class="sxs-lookup"><span data-stu-id="19767-158">MSAL will take care of acquiring, caching, and refreshing tokens for you.</span></span>

<span data-ttu-id="19767-159">Por fim, compile e execute seu aplicativo!</span><span class="sxs-lookup"><span data-stu-id="19767-159">Finally, build and run your app!</span></span>  <span data-ttu-id="19767-160">Entre com uma conta da Microsoft ou uma Conta do AD do Azure e observe como a identidade do usuário é refletida na barra de navegação superior.</span><span class="sxs-lookup"><span data-stu-id="19767-160">Sign in with either a Microsoft Account or an Azure AD Account, and notice how the user's identity is reflected in the top navigation bar.</span></span>  <span data-ttu-id="19767-161">Adicione e exclua alguns itens na Lista de Tarefas do usuário para ver as chamadas à API protegidas pelo OAuth 2.0 em ação.</span><span class="sxs-lookup"><span data-stu-id="19767-161">Add and delete some items from the user's To-Do List to see the OAuth 2.0 secured API calls in action.</span></span>  <span data-ttu-id="19767-162">Agora você tem um aplicativo Web e uma API Web, ambos protegidos por protocolos padrão do setor, que podem autenticar usuários com as respectivas contas pessoais e corporativas/de estudante.</span><span class="sxs-lookup"><span data-stu-id="19767-162">You now have a web app & web API, both secured using industry standard protocols, that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="19767-163">Para referência, o exemplo concluído (sem seus valores de configuração) [é fornecido aqui](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="19767-163">For reference, the completed sample (without your configuration values) [is provided here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="19767-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="19767-164">Next Steps</span></span>
<span data-ttu-id="19767-165">Para obter recursos adicionais, consulte:</span><span class="sxs-lookup"><span data-stu-id="19767-165">For additional resources, check out:</span></span>

* [<span data-ttu-id="19767-166">Guia do desenvolvedor do v2.0 >></span><span class="sxs-lookup"><span data-stu-id="19767-166">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="19767-167">Marca “azure-active-directory” do StackOverflow >></span><span class="sxs-lookup"><span data-stu-id="19767-167">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="19767-168">Obter atualizações de segurança para nossos produtos</span><span class="sxs-lookup"><span data-stu-id="19767-168">Get security updates for our products</span></span>
<span data-ttu-id="19767-169">Recomendamos que você obtenha notificações sobre a ocorrência de incidentes de segurança visitando [esta página](https://technet.microsoft.com/security/dd252948) e assinando os alertas do Security Advisory.</span><span class="sxs-lookup"><span data-stu-id="19767-169">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

