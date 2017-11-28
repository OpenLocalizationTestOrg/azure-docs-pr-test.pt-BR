---
title: aaaAzure B2C do Active Directory | Microsoft Docs
description: Como toobuild um aplicativo Web do .NET e chamar uma web api usando tokens de acesso do Azure Active Directory B2C e OAuth 2.0.
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: d3888556-2647-4a42-b068-027f9374aa61
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 9b248e3bf18968e12aae73c07083fa8278befb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a><span data-ttu-id="bd3d8-103">Azure AD B2C: chamar uma API Web de um aplicativo Web .NET</span><span class="sxs-lookup"><span data-stu-id="bd3d8-103">Azure AD B2C: Call a .NET web API from a .NET web app</span></span>

<span data-ttu-id="bd3d8-104">Usando o Azure AD B2C, você pode adicionar aplicativos web do identidade avançado Gerenciamento recursos tooyour e APIs da web.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-104">By using Azure AD B2C, you can add powerful identity management features tooyour web apps and web APIs.</span></span> <span data-ttu-id="bd3d8-105">Este artigo aborda como toorequest tokens de acesso e fazer chamadas de uma "lista de tarefas".NET tooa de aplicativo web .NET web api.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-105">This article discusses how toorequest access tokens and make calls from a .NET "to-do list" web app tooa .NET web api.</span></span>

<span data-ttu-id="bd3d8-106">Este artigo não aborda como tooimplement entrar, se inscrever e criar o perfil de gerenciamento com o Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-106">This article does not cover how tooimplement sign-in, sign-up and profile management with Azure AD B2C.</span></span> <span data-ttu-id="bd3d8-107">Ele se concentra em APIs da web chamado depois que o usuário Olá já está autenticado.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-107">It focuses on calling web APIs after hello user is already authenticated.</span></span> <span data-ttu-id="bd3d8-108">Se você ainda não fez isto, você deverá:</span><span class="sxs-lookup"><span data-stu-id="bd3d8-108">If you haven't already, you should:</span></span>

* <span data-ttu-id="bd3d8-109">Começar com um [aplicativo Web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span><span class="sxs-lookup"><span data-stu-id="bd3d8-109">Get started with a [.NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span></span>
* <span data-ttu-id="bd3d8-110">Começar com uma [API Web .NET](active-directory-b2c-devquickstarts-api-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="bd3d8-110">Get started with a [.NET web api](active-directory-b2c-devquickstarts-api-dotnet.md)</span></span>

## <a name="prerequisite"></a><span data-ttu-id="bd3d8-111">Pré-requisito</span><span class="sxs-lookup"><span data-stu-id="bd3d8-111">Prerequisite</span></span>

<span data-ttu-id="bd3d8-112">toobuild um aplicativo web que chama uma web api, você precisa:</span><span class="sxs-lookup"><span data-stu-id="bd3d8-112">toobuild a web application that calls a web api, you need to:</span></span>

1. <span data-ttu-id="bd3d8-113">[Criar um locatário do Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bd3d8-113">[Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>
2. <span data-ttu-id="bd3d8-114">[Registrar uma api Web](active-directory-b2c-app-registration.md#register-a-web-api).</span><span class="sxs-lookup"><span data-stu-id="bd3d8-114">[Register a web api](active-directory-b2c-app-registration.md#register-a-web-api).</span></span>
3. <span data-ttu-id="bd3d8-115">[Registrar um aplicativo Web](active-directory-b2c-app-registration.md#register-a-web-app).</span><span class="sxs-lookup"><span data-stu-id="bd3d8-115">[Register a web app](active-directory-b2c-app-registration.md#register-a-web-app).</span></span>
4. <span data-ttu-id="bd3d8-116">[Configurar políticas](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="bd3d8-116">[Set up policies](active-directory-b2c-reference-policies.md).</span></span>
5. <span data-ttu-id="bd3d8-117">[Grant Olá web app permissões toouse Olá web api](active-directory-b2c-access-tokens.md#publishing-permissions).</span><span class="sxs-lookup"><span data-stu-id="bd3d8-117">[Grant hello web app permissions toouse hello web api](active-directory-b2c-access-tokens.md#publishing-permissions).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bd3d8-118">aplicativo de cliente Hello e a API da web devem usar o diretório do B2C Olá mesmo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-118">hello client application and web API must use hello same Azure AD B2C directory.</span></span>
>

## <a name="download-hello-code"></a><span data-ttu-id="bd3d8-119">Baixar o código de saudação</span><span class="sxs-lookup"><span data-stu-id="bd3d8-119">Download hello code</span></span>

<span data-ttu-id="bd3d8-120">código de saudação para este tutorial é mantido em [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="bd3d8-120">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="bd3d8-121">Você pode clonar o exemplo hello executando:</span><span class="sxs-lookup"><span data-stu-id="bd3d8-121">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="bd3d8-122">Depois de baixar o código de exemplo hello, Olá abra o Visual Studio. sln arquivo tooget é iniciado.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-122">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="bd3d8-123">o arquivo de solução Olá contém dois projetos: `TaskWebApp` e `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-123">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="bd3d8-124">`TaskWebApp`é um aplicativo da web MVC que Olá usuário interage com.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-124">`TaskWebApp` is a MVC web application that hello user interacts with.</span></span> <span data-ttu-id="bd3d8-125">`TaskService`é a API de web de back-end do aplicativo hello que armazena a lista de tarefas de cada usuário.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-125">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="bd3d8-126">Este artigo não aborda construção Olá `TaskWebApp` aplicativo web ou hello `TaskService` web api.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-126">This article does not cover building hello `TaskWebApp` web app or hello `TaskService` web api.</span></span> <span data-ttu-id="bd3d8-127">toolearn como toobuild Olá .NET web app usando o Azure AD B2C, consulte nosso [tutorial de aplicativo da web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="bd3d8-127">toolearn how toobuild hello .NET web app using Azure AD B2C, see our [.NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span> <span data-ttu-id="bd3d8-128">toolearn como toobuild Olá .NET web API protegida usando o Azure AD B2C, consulte nosso [tutorial de API da web .NET](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="bd3d8-128">toolearn how toobuild hello .NET web API secured using Azure AD B2C, see our [.NET web API tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

### <a name="update-hello-azure-ad-b2c-configuration"></a><span data-ttu-id="bd3d8-129">Atualizar a configuração de saudação do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="bd3d8-129">Update hello Azure AD B2C configuration</span></span>

<span data-ttu-id="bd3d8-130">Nosso exemplo é a ID de cliente e as políticas de Olá de toouse configurado do nosso locatário de demonstração.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-130">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="bd3d8-131">Se você quiser toouse seu próprio locatário:</span><span class="sxs-lookup"><span data-stu-id="bd3d8-131">If you would like toouse your own tenant:</span></span>

1. <span data-ttu-id="bd3d8-132">Abra `web.config` em Olá `TaskService` do projeto e substituir os valores hello para</span><span class="sxs-lookup"><span data-stu-id="bd3d8-132">Open `web.config` in hello `TaskService` project and replace hello values for</span></span>

    * <span data-ttu-id="bd3d8-133">`ida:Tenant` pelo nome do locatário</span><span class="sxs-lookup"><span data-stu-id="bd3d8-133">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="bd3d8-134">`ida:ClientId` pela ID do aplicativo da API Web</span><span class="sxs-lookup"><span data-stu-id="bd3d8-134">`ida:ClientId` with your web api application ID</span></span>
    * <span data-ttu-id="bd3d8-135">`ida:SignUpSignInPolicyId` pelo nome da política "Inscrever-se ou Entrar"</span><span class="sxs-lookup"><span data-stu-id="bd3d8-135">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="bd3d8-136">Abra `web.config` em Olá `TaskWebApp` do projeto e substituir os valores hello para</span><span class="sxs-lookup"><span data-stu-id="bd3d8-136">Open `web.config` in hello `TaskWebApp` project and replace hello values for</span></span>

    * <span data-ttu-id="bd3d8-137">`ida:Tenant` pelo nome do locatário</span><span class="sxs-lookup"><span data-stu-id="bd3d8-137">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="bd3d8-138">`ida:ClientId` pela ID de aplicativo do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="bd3d8-138">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="bd3d8-139">`ida:ClientSecret` pela chave de segredo do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="bd3d8-139">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="bd3d8-140">`ida:SignUpSignInPolicyId` pelo nome da política "Inscrever-se ou Entrar"</span><span class="sxs-lookup"><span data-stu-id="bd3d8-140">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="bd3d8-141">`ida:EditProfilePolicyId` pelo nome de política "Editar Perfil"</span><span class="sxs-lookup"><span data-stu-id="bd3d8-141">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="bd3d8-142">`ida:ResetPasswordPolicyId` pelo nome de política "Redefinir Senha"</span><span class="sxs-lookup"><span data-stu-id="bd3d8-142">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>



## <a name="requesting-and-saving-an-access-token"></a><span data-ttu-id="bd3d8-143">Solicitar e salvar um token de acesso</span><span class="sxs-lookup"><span data-stu-id="bd3d8-143">Requesting and saving an access token</span></span>

### <a name="specify-hello-permissions"></a><span data-ttu-id="bd3d8-144">Especificar permissões de saudação</span><span class="sxs-lookup"><span data-stu-id="bd3d8-144">Specify hello permissions</span></span>

<span data-ttu-id="bd3d8-145">Na ordem toomake Olá chamada toohello API da web, você precisa de usuário de saudação tooauthenticate (usando a diretiva de entrada-o/entrada) e [receber um token de acesso](active-directory-b2c-access-tokens.md) do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-145">In order toomake hello call toohello web API, you need tooauthenticate hello user (using your sign-up/sign-in policy) and [receive an access token](active-directory-b2c-access-tokens.md) from Azure AD B2C.</span></span> <span data-ttu-id="bd3d8-146">Em ordem tooreceive um token de acesso, você deve primeiro especificar permissões de saudação você gostaria que toogrant de token de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-146">In order tooreceive an access token, you first must specify hello permissions you would like hello access token toogrant.</span></span> <span data-ttu-id="bd3d8-147">Olá permissões são especificadas em Olá `scope` parâmetro quando você fizer Olá solicitação toohello `/authorize` ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-147">hello permissions are specified in hello `scope` parameter when you make hello request toohello `/authorize` endpoint.</span></span> <span data-ttu-id="bd3d8-148">Por exemplo, tooacquire aplicativo de recurso de toohello de permissão que tem um token de acesso com hello "leitura" hello URI de ID do aplicativo de `https://contoso.onmicrosoft.com/tasks`, escopo Olá seria `https://contoso.onmicrosoft.com/tasks/read`.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-148">For example, tooacquire an access token with hello “read” permission toohello resource application that has hello App ID URI of `https://contoso.onmicrosoft.com/tasks`, hello scope would be `https://contoso.onmicrosoft.com/tasks/read`.</span></span>

<span data-ttu-id="bd3d8-149">escopo de saudação toospecify em nosso arquivo de exemplo, abra Olá `App_Start\Startup.Auth.cs` e definir Olá `Scope` variável OpenIdConnectAuthenticationOptions.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-149">toospecify hello scope in our sample, open hello file `App_Start\Startup.Auth.cs` and define hello `Scope` variable in OpenIdConnectAuthenticationOptions.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {
            ...

            // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
            Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
        }
    );
}
```

### <a name="exchange-hello-authorization-code-for-an-access-token"></a><span data-ttu-id="bd3d8-150">Código de autorização de saudação do Exchange para um token de acesso</span><span class="sxs-lookup"><span data-stu-id="bd3d8-150">Exchange hello authorization code for an access token</span></span>

<span data-ttu-id="bd3d8-151">Depois que um usuário conclui a experiência de inscrição ou entrar hello, seu aplicativo receberá um código de autorização do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-151">After an user completes hello sign-up or sign-in experience, your app will receive an authorization code from Azure AD B2C.</span></span> <span data-ttu-id="bd3d8-152">middleware OWIN OpenID Connect do Hello armazenará código hello, mas não a troca para um token de acesso.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-152">hello OWIN OpenID Connect middleware will store hello code, but will not exchange it for an access token.</span></span> <span data-ttu-id="bd3d8-153">Você pode usar o hello [biblioteca MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) toomake intercâmbio de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-153">You can use hello [MSAL library](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) toomake hello exchange.</span></span> <span data-ttu-id="bd3d8-154">Em nosso exemplo, configuramos um retorno de chamada de notificação em Olá OpenID Connect middleware sempre que um código de autorização é recebido.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-154">In our sample, we configured a notification callback into hello OpenID Connect middleware whenever an authorization code is received.</span></span> <span data-ttu-id="bd3d8-155">No retorno de chamada Olá, podemos usar código de saudação do MSAL tooexchange para um token e salve o token Olá no cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-155">In hello callback, we use MSAL tooexchange hello code for a token and save hello token into hello cache.</span></span>

```CSharp
/*
* Callback function when an authorization code is received
*/
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
    // Extract hello code from hello response notification
    var code = notification.Code;

    var userObjectId = notification.AuthenticationTicket.Identity.FindFirst(ObjectIdElement).Value;
    var authority = String.Format(AadInstance, Tenant, DefaultPolicy);
    var httpContext = notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase;

    // Exchange hello code for a token. Make sure toospecify hello necessary scopes
    ClientCredential cred = new ClientCredential(ClientSecret);
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                            RedirectUri, cred, new NaiveSessionCache(userObjectId, httpContext));
    var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { ReadTasksScope, WriteTasksScope }, code, DefaultPolicy);
}
```

## <a name="calling-hello-web-api"></a><span data-ttu-id="bd3d8-156">Chamar a API da web de saudação</span><span class="sxs-lookup"><span data-stu-id="bd3d8-156">Calling hello web API</span></span>

<span data-ttu-id="bd3d8-157">Esta seção discute como o token de saudação do toouse recebido durante a inscrição-o/entrar com o Azure AD B2C em ordem tooaccess Olá API da web.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-157">This section discusses how toouse hello token received during sign-up/sign-in with Azure AD B2C in order tooaccess hello web API.</span></span>

### <a name="retrieve-hello-saved-token-in-hello-controllers"></a><span data-ttu-id="bd3d8-158">Recuperar o token Olá salvada em controladores de saudação</span><span class="sxs-lookup"><span data-stu-id="bd3d8-158">Retrieve hello saved token in hello controllers</span></span>

<span data-ttu-id="bd3d8-159">Olá `TasksController` é responsável pela comunicação com a API da web hello para enviar tooread de toohello API de solicitações HTTP, criar e excluir tarefas.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-159">hello `TasksController` is responsible for communicating with hello web API and for sending HTTP requests toohello API tooread, create, and delete tasks.</span></span> <span data-ttu-id="bd3d8-160">Como Olá API é protegido pelo Azure AD B2C, é necessário token de saudação recuperar toofirst que Olá acima etapa foi salvo.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-160">Because hello API is secured by Azure AD B2C, you need toofirst retrieve hello token you saved in hello above step.</span></span>

```CSharp
// Controllers\TasksController.cs

/*
* Uses MSAL tooretrieve hello token from hello cache
*/
private async void acquireToken(String[] scope)
{
    string userObjectID = ClaimsPrincipal.Current.FindFirst(Startup.ObjectIdElement).Value;
    string authority = String.Format(Startup.AadInstance, Startup.Tenant, Startup.DefaultPolicy);

    ClientCredential credential = new ClientCredential(Startup.ClientSecret);

    // Retrieve hello token using hello provided scopes
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                        Startup.RedirectUri, credential,
                                        new NaiveSessionCache(userObjectID, this.HttpContext));
    AuthenticationResult result = await app.AcquireTokenSilentAsync(scope);

    accessToken = result.Token;
}
```

### <a name="read-tasks-from-hello-web-api"></a><span data-ttu-id="bd3d8-161">Ler tarefas de API da web hello</span><span class="sxs-lookup"><span data-stu-id="bd3d8-161">Read tasks from hello web API</span></span>

<span data-ttu-id="bd3d8-162">Quando você tiver um token, você poderá anexá-lo toohello HTTP `GET` solicitação no hello `Authorization` chamada do cabeçalho toosecurely `TaskService`:</span><span class="sxs-lookup"><span data-stu-id="bd3d8-162">When you have a token, you can attach it toohello HTTP `GET` request in hello `Authorization` header toosecurely call `TaskService`:</span></span>

```CSharp
// Controllers\TasksController.cs

public async Task<ActionResult> Index()
{
    try {

        // Retrieve hello token with hello specified scopes
        acquireToken(new string[] { Startup.ReadTasksScope });

        HttpClient client = new HttpClient();
        HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, apiEndpoint);

        // Add token toohello Authorization header and make hello request
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
        HttpResponseMessage response = await client.SendAsync(request);

        // Handle response ...
}

```

### <a name="create-and-delete-tasks-on-hello-web-api"></a><span data-ttu-id="bd3d8-163">Criar e excluir tarefas na API da web hello</span><span class="sxs-lookup"><span data-stu-id="bd3d8-163">Create and delete tasks on hello web API</span></span>

<span data-ttu-id="bd3d8-164">Olá siga mesmo padrão quando você enviar `POST` e `DELETE` solicitações toohello web API, usando o token de acesso de saudação de tooretrieve MSAL do cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-164">Follow hello same pattern when you send `POST` and `DELETE` requests toohello web API, using MSAL tooretrieve hello access token from hello cache.</span></span>

## <a name="run-hello-sample-app"></a><span data-ttu-id="bd3d8-165">Execute o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="bd3d8-165">Run hello sample app</span></span>

<span data-ttu-id="bd3d8-166">Por fim, compilar e executar os dois aplicativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-166">Finally, build and run both hello apps.</span></span> <span data-ttu-id="bd3d8-167">Inscreva-se e entrar e criar tarefas para o usuário conectado hello.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-167">Sign up and sign in, and create tasks for hello signed-in user.</span></span> <span data-ttu-id="bd3d8-168">Saia e entre como outro usuário.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-168">Sign out and sign in as a different user.</span></span> <span data-ttu-id="bd3d8-169">Crie tarefas para esse usuário.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-169">Create tasks for that user.</span></span> <span data-ttu-id="bd3d8-170">Observe como tarefas de saudação são armazenados por usuário no hello API, porque Olá API extrai Olá a identidade de usuário do token Olá recebe.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-170">Notice how hello tasks are stored per-user on hello API, because hello API extracts hello user's identity from hello token it receives.</span></span> <span data-ttu-id="bd3d8-171">Além disso, tente brincando com escopos hello.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-171">Also try playing with hello scopes.</span></span> <span data-ttu-id="bd3d8-172">Remover permissão de saudação muito "gravação" e, em seguida, tente adicionar uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-172">Remove hello permission too"write" and then try adding a task.</span></span> <span data-ttu-id="bd3d8-173">Verifique se toosign out cada vez que você alterar o escopo de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd3d8-173">Just make sure toosign out each time you change hello scope.</span></span>

