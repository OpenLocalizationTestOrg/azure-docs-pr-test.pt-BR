---
title: Azure Active Directory B2C | Microsoft Docs
description: Como compilar um aplicativo Web .NET e chamar uma API Web usando os tokens de acesso do OAuth 2.0 e Azure Active Directory B2C.
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
ms.openlocfilehash: 48452eb68f826d1c7aa61d5e5531f941ac1422b0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a><span data-ttu-id="91f71-103">Azure AD B2C: chamar uma API Web de um aplicativo Web .NET</span><span class="sxs-lookup"><span data-stu-id="91f71-103">Azure AD B2C: Call a .NET web API from a .NET web app</span></span>

<span data-ttu-id="91f71-104">Usando o Azure AD B2C, você pode adicionar recursos poderosos de gerenciamento de identidades a seus aplicativos Web e APIs Web.</span><span class="sxs-lookup"><span data-stu-id="91f71-104">By using Azure AD B2C, you can add powerful identity management features to your web apps and web APIs.</span></span> <span data-ttu-id="91f71-105">Este artigo descreve como solicitar tokens de acesso e fazer chamadas de um aplicativo Web de “lista de tarefas pendentes” do .NET para uma API Web .NET.</span><span class="sxs-lookup"><span data-stu-id="91f71-105">This article discusses how to request access tokens and make calls from a .NET "to-do list" web app to a .NET web api.</span></span>

<span data-ttu-id="91f71-106">Este artigo não aborda como implementar conexão, registro e gerenciamento de perfil com o Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="91f71-106">This article does not cover how to implement sign-in, sign-up and profile management with Azure AD B2C.</span></span> <span data-ttu-id="91f71-107">Ele se concentra na chamada a APIs Web depois que o usuário já está autenticado.</span><span class="sxs-lookup"><span data-stu-id="91f71-107">It focuses on calling web APIs after the user is already authenticated.</span></span> <span data-ttu-id="91f71-108">Se você ainda não fez isto, você deverá:</span><span class="sxs-lookup"><span data-stu-id="91f71-108">If you haven't already, you should:</span></span>

* <span data-ttu-id="91f71-109">Começar com um [aplicativo Web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span><span class="sxs-lookup"><span data-stu-id="91f71-109">Get started with a [.NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span></span>
* <span data-ttu-id="91f71-110">Começar com uma [API Web .NET](active-directory-b2c-devquickstarts-api-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="91f71-110">Get started with a [.NET web api](active-directory-b2c-devquickstarts-api-dotnet.md)</span></span>

## <a name="prerequisite"></a><span data-ttu-id="91f71-111">Pré-requisito</span><span class="sxs-lookup"><span data-stu-id="91f71-111">Prerequisite</span></span>

<span data-ttu-id="91f71-112">Para criar um aplicativo Web que chame uma API Web, você deve:</span><span class="sxs-lookup"><span data-stu-id="91f71-112">To build a web application that calls a web api, you need to:</span></span>

1. <span data-ttu-id="91f71-113">[Criar um locatário do Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="91f71-113">[Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>
2. <span data-ttu-id="91f71-114">[Registrar uma api Web](active-directory-b2c-app-registration.md#register-a-web-api).</span><span class="sxs-lookup"><span data-stu-id="91f71-114">[Register a web api](active-directory-b2c-app-registration.md#register-a-web-api).</span></span>
3. <span data-ttu-id="91f71-115">[Registrar um aplicativo Web](active-directory-b2c-app-registration.md#register-a-web-app).</span><span class="sxs-lookup"><span data-stu-id="91f71-115">[Register a web app](active-directory-b2c-app-registration.md#register-a-web-app).</span></span>
4. <span data-ttu-id="91f71-116">[Configurar políticas](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="91f71-116">[Set up policies](active-directory-b2c-reference-policies.md).</span></span>
5. <span data-ttu-id="91f71-117">[Conceder permissões para usar a API Web ao aplicativo Web](active-directory-b2c-access-tokens.md#publishing-permissions).</span><span class="sxs-lookup"><span data-stu-id="91f71-117">[Grant the web app permissions to use the web api](active-directory-b2c-access-tokens.md#publishing-permissions).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91f71-118">O aplicativo cliente e a API Web devem usar o mesmo diretório do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="91f71-118">The client application and web API must use the same Azure AD B2C directory.</span></span>
>

## <a name="download-the-code"></a><span data-ttu-id="91f71-119">Baixar o código</span><span class="sxs-lookup"><span data-stu-id="91f71-119">Download the code</span></span>

<span data-ttu-id="91f71-120">O código para este tutorial é mantido no [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="91f71-120">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="91f71-121">Você pode clonar a amostra executando:</span><span class="sxs-lookup"><span data-stu-id="91f71-121">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="91f71-122">Depois de baixar o código de exemplo, abra o arquivo .sln do Visual Studio para começar.</span><span class="sxs-lookup"><span data-stu-id="91f71-122">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="91f71-123">Agora, sua solução contém dois projetos: `TaskWebApp` e `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="91f71-123">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="91f71-124">`TaskWebApp` é um aplicativo Web MVC com o qual o usuário interage.</span><span class="sxs-lookup"><span data-stu-id="91f71-124">`TaskWebApp` is a MVC web application that the user interacts with.</span></span> <span data-ttu-id="91f71-125">`TaskService` é API Web back-end do aplicativo que armazena a lista de tarefas de cada usuário.</span><span class="sxs-lookup"><span data-stu-id="91f71-125">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="91f71-126">Este artigo não abrange a criação do aplicativo Web `TaskWebApp` nem da API Web `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="91f71-126">This article does not cover building the `TaskWebApp` web app or the `TaskService` web api.</span></span> <span data-ttu-id="91f71-127">Para saber como criar um aplicativo Web .NET usando o Azure AD B2C, confira [nosso tutorial do aplicativo Web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="91f71-127">To learn how to build the .NET web app using Azure AD B2C, see our [.NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span> <span data-ttu-id="91f71-128">Para saber como criar uma API Web .NET protegida usando o Azure AD B2C, confira [nosso tutorial da API Web .NET](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="91f71-128">To learn how to build the .NET web API secured using Azure AD B2C, see our [.NET web API tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

### <a name="update-the-azure-ad-b2c-configuration"></a><span data-ttu-id="91f71-129">Atualizar a configuração do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="91f71-129">Update the Azure AD B2C configuration</span></span>

<span data-ttu-id="91f71-130">Nossa amostra é configurada para usar as políticas e a ID do cliente de nosso locatário de demonstração.</span><span class="sxs-lookup"><span data-stu-id="91f71-130">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="91f71-131">Se você quiser usar seu próprio locatário:</span><span class="sxs-lookup"><span data-stu-id="91f71-131">If you would like to use your own tenant:</span></span>

1. <span data-ttu-id="91f71-132">Abra `web.config` no projeto `TaskService` e substitua os valores de</span><span class="sxs-lookup"><span data-stu-id="91f71-132">Open `web.config` in the `TaskService` project and replace the values for</span></span>

    * <span data-ttu-id="91f71-133">`ida:Tenant` pelo nome do locatário</span><span class="sxs-lookup"><span data-stu-id="91f71-133">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="91f71-134">`ida:ClientId` pela ID do aplicativo da API Web</span><span class="sxs-lookup"><span data-stu-id="91f71-134">`ida:ClientId` with your web api application ID</span></span>
    * <span data-ttu-id="91f71-135">`ida:SignUpSignInPolicyId` pelo nome da política "Inscrever-se ou Entrar"</span><span class="sxs-lookup"><span data-stu-id="91f71-135">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="91f71-136">Abra `web.config` no projeto `TaskWebApp` e substitua os valores de</span><span class="sxs-lookup"><span data-stu-id="91f71-136">Open `web.config` in the `TaskWebApp` project and replace the values for</span></span>

    * <span data-ttu-id="91f71-137">`ida:Tenant` pelo nome do locatário</span><span class="sxs-lookup"><span data-stu-id="91f71-137">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="91f71-138">`ida:ClientId` pela ID de aplicativo do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="91f71-138">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="91f71-139">`ida:ClientSecret` pela chave de segredo do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="91f71-139">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="91f71-140">`ida:SignUpSignInPolicyId` pelo nome da política "Inscrever-se ou Entrar"</span><span class="sxs-lookup"><span data-stu-id="91f71-140">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="91f71-141">`ida:EditProfilePolicyId` pelo nome de política "Editar Perfil"</span><span class="sxs-lookup"><span data-stu-id="91f71-141">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="91f71-142">`ida:ResetPasswordPolicyId` pelo nome de política "Redefinir Senha"</span><span class="sxs-lookup"><span data-stu-id="91f71-142">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>



## <a name="requesting-and-saving-an-access-token"></a><span data-ttu-id="91f71-143">Solicitar e salvar um token de acesso</span><span class="sxs-lookup"><span data-stu-id="91f71-143">Requesting and saving an access token</span></span>

### <a name="specify-the-permissions"></a><span data-ttu-id="91f71-144">Especificar as permissões</span><span class="sxs-lookup"><span data-stu-id="91f71-144">Specify the permissions</span></span>

<span data-ttu-id="91f71-145">Para fazer a chamada para a API Web, você precisa autenticar o usuário (usando a política de inscrever-se ou entrar) e [receber um token de acesso](active-directory-b2c-access-tokens.md) do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="91f71-145">In order to make the call to the web API, you need to authenticate the user (using your sign-up/sign-in policy) and [receive an access token](active-directory-b2c-access-tokens.md) from Azure AD B2C.</span></span> <span data-ttu-id="91f71-146">Para receber um token de acesso, você deve primeiro especificar as permissões que você deseja que sejam concedidas pelo token de acesso.</span><span class="sxs-lookup"><span data-stu-id="91f71-146">In order to receive an access token, you first must specify the permissions you would like the access token to grant.</span></span> <span data-ttu-id="91f71-147">As permissões são especificadas no parâmetro `scope` quando você faz a solicitação para o ponto de extremidade `/authorize`.</span><span class="sxs-lookup"><span data-stu-id="91f71-147">The permissions are specified in the `scope` parameter when you make the request to the `/authorize` endpoint.</span></span> <span data-ttu-id="91f71-148">Por exemplo, para obter um token de acesso com a permissão de "leitura" para o aplicativo de recurso que tem o URI de ID do aplicativo de `https://contoso.onmicrosoft.com/tasks`, o escopo seria `https://contoso.onmicrosoft.com/tasks/read`.</span><span class="sxs-lookup"><span data-stu-id="91f71-148">For example, to acquire an access token with the “read” permission to the resource application that has the App ID URI of `https://contoso.onmicrosoft.com/tasks`, the scope would be `https://contoso.onmicrosoft.com/tasks/read`.</span></span>

<span data-ttu-id="91f71-149">Para especificar o escopo em nosso exemplo, abra o arquivo `App_Start\Startup.Auth.cs` e defina a variável `Scope` em OpenIdConnectAuthenticationOptions.</span><span class="sxs-lookup"><span data-stu-id="91f71-149">To specify the scope in our sample, open the file `App_Start\Startup.Auth.cs` and define the `Scope` variable in OpenIdConnectAuthenticationOptions.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {
            ...

            // Specify the scope by appending all of the scopes requested into one string (seperated by a blank space)
            Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
        }
    );
}
```

### <a name="exchange-the-authorization-code-for-an-access-token"></a><span data-ttu-id="91f71-150">Permutar o código de autorização de um token de acesso</span><span class="sxs-lookup"><span data-stu-id="91f71-150">Exchange the authorization code for an access token</span></span>

<span data-ttu-id="91f71-151">Após um usuário concluir a experiência de inscrição ou entrada, seu aplicativo receberá um código de autorização do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="91f71-151">After an user completes the sign-up or sign-in experience, your app will receive an authorization code from Azure AD B2C.</span></span> <span data-ttu-id="91f71-152">O middleware OWIN OpenID Connect armazenará o código, mas não o permutará por um token de acesso.</span><span class="sxs-lookup"><span data-stu-id="91f71-152">The OWIN OpenID Connect middleware will store the code, but will not exchange it for an access token.</span></span> <span data-ttu-id="91f71-153">Você pode usar a [biblioteca MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) para realizar a permuta.</span><span class="sxs-lookup"><span data-stu-id="91f71-153">You can use the [MSAL library](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) to make the exchange.</span></span> <span data-ttu-id="91f71-154">Em nosso exemplo, configuramos um retorno de chamada de notificação para o middleware OpenID Connect sempre que um código de autorização é recebido.</span><span class="sxs-lookup"><span data-stu-id="91f71-154">In our sample, we configured a notification callback into the OpenID Connect middleware whenever an authorization code is received.</span></span> <span data-ttu-id="91f71-155">No retorno de chamada, usamos o MSAL para permutar o código por um token e salvar o token no cache.</span><span class="sxs-lookup"><span data-stu-id="91f71-155">In the callback, we use MSAL to exchange the code for a token and save the token into the cache.</span></span>

```CSharp
/*
* Callback function when an authorization code is received
*/
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
    // Extract the code from the response notification
    var code = notification.Code;

    var userObjectId = notification.AuthenticationTicket.Identity.FindFirst(ObjectIdElement).Value;
    var authority = String.Format(AadInstance, Tenant, DefaultPolicy);
    var httpContext = notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase;

    // Exchange the code for a token. Make sure to specify the necessary scopes
    ClientCredential cred = new ClientCredential(ClientSecret);
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                            RedirectUri, cred, new NaiveSessionCache(userObjectId, httpContext));
    var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { ReadTasksScope, WriteTasksScope }, code, DefaultPolicy);
}
```

## <a name="calling-the-web-api"></a><span data-ttu-id="91f71-156">Chamar a API da web</span><span class="sxs-lookup"><span data-stu-id="91f71-156">Calling the web API</span></span>

<span data-ttu-id="91f71-157">Esta seção discute como usar o token recebido durante a inscrição/entrada com o Azure AD B2C para acessar a API Web.</span><span class="sxs-lookup"><span data-stu-id="91f71-157">This section discusses how to use the token received during sign-up/sign-in with Azure AD B2C in order to access the web API.</span></span>

### <a name="retrieve-the-saved-token-in-the-controllers"></a><span data-ttu-id="91f71-158">Recuperar o token salvo nos controladores</span><span class="sxs-lookup"><span data-stu-id="91f71-158">Retrieve the saved token in the controllers</span></span>

<span data-ttu-id="91f71-159">O `TasksController` é responsável pela comunicação com a API Web e por enviar solicitações HTTP à API para ler, criar e excluir tarefas.</span><span class="sxs-lookup"><span data-stu-id="91f71-159">The `TasksController` is responsible for communicating with the web API and for sending HTTP requests to the API to read, create, and delete tasks.</span></span> <span data-ttu-id="91f71-160">Já que a API é protegida pelo Azure AD B2C, primeiro você precisa recuperar o token que salvou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="91f71-160">Because the API is secured by Azure AD B2C, you need to first retrieve the token you saved in the above step.</span></span>

```CSharp
// Controllers\TasksController.cs

/*
* Uses MSAL to retrieve the token from the cache
*/
private async void acquireToken(String[] scope)
{
    string userObjectID = ClaimsPrincipal.Current.FindFirst(Startup.ObjectIdElement).Value;
    string authority = String.Format(Startup.AadInstance, Startup.Tenant, Startup.DefaultPolicy);

    ClientCredential credential = new ClientCredential(Startup.ClientSecret);

    // Retrieve the token using the provided scopes
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                        Startup.RedirectUri, credential,
                                        new NaiveSessionCache(userObjectID, this.HttpContext));
    AuthenticationResult result = await app.AcquireTokenSilentAsync(scope);

    accessToken = result.Token;
}
```

### <a name="read-tasks-from-the-web-api"></a><span data-ttu-id="91f71-161">Ler tarefas da API Web</span><span class="sxs-lookup"><span data-stu-id="91f71-161">Read tasks from the web API</span></span>

<span data-ttu-id="91f71-162">Quando você tiver um token, poderá anexá-lo à solicitação `GET` HTTP no cabeçalho `Authorization` para chamar com segurança o `TaskService`:</span><span class="sxs-lookup"><span data-stu-id="91f71-162">When you have a token, you can attach it to the HTTP `GET` request in the `Authorization` header to securely call `TaskService`:</span></span>

```CSharp
// Controllers\TasksController.cs

public async Task<ActionResult> Index()
{
    try {

        // Retrieve the token with the specified scopes
        acquireToken(new string[] { Startup.ReadTasksScope });

        HttpClient client = new HttpClient();
        HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, apiEndpoint);

        // Add token to the Authorization header and make the request
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
        HttpResponseMessage response = await client.SendAsync(request);

        // Handle response ...
}

```

### <a name="create-and-delete-tasks-on-the-web-api"></a><span data-ttu-id="91f71-163">Criar e excluir tarefas na API Web</span><span class="sxs-lookup"><span data-stu-id="91f71-163">Create and delete tasks on the web API</span></span>

<span data-ttu-id="91f71-164">Siga o mesmo padrão ao enviar solicitações de `POST` e `DELETE` à API Web, usando o MSAL para recuperar o token de acesso do cache.</span><span class="sxs-lookup"><span data-stu-id="91f71-164">Follow the same pattern when you send `POST` and `DELETE` requests to the web API, using MSAL to retrieve the access token from the cache.</span></span>

## <a name="run-the-sample-app"></a><span data-ttu-id="91f71-165">Executar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="91f71-165">Run the sample app</span></span>

<span data-ttu-id="91f71-166">Finalmente, compile e execute ambos os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="91f71-166">Finally, build and run both the apps.</span></span> <span data-ttu-id="91f71-167">Inscreva-se e entre e crie tarefas para o usuário conectado.</span><span class="sxs-lookup"><span data-stu-id="91f71-167">Sign up and sign in, and create tasks for the signed-in user.</span></span> <span data-ttu-id="91f71-168">Saia e entre como outro usuário.</span><span class="sxs-lookup"><span data-stu-id="91f71-168">Sign out and sign in as a different user.</span></span> <span data-ttu-id="91f71-169">Crie tarefas para esse usuário.</span><span class="sxs-lookup"><span data-stu-id="91f71-169">Create tasks for that user.</span></span> <span data-ttu-id="91f71-170">Observe como as tarefas são armazenados por usuário na API, pois a API extrai a identidade do usuário do token que recebe.</span><span class="sxs-lookup"><span data-stu-id="91f71-170">Notice how the tasks are stored per-user on the API, because the API extracts the user's identity from the token it receives.</span></span> <span data-ttu-id="91f71-171">Além disso, experimente mudar os escopos.</span><span class="sxs-lookup"><span data-stu-id="91f71-171">Also try playing with the scopes.</span></span> <span data-ttu-id="91f71-172">Remova a permissão de "gravação" e, em seguida, tente adicionar uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="91f71-172">Remove the permission to "write" and then try adding a task.</span></span> <span data-ttu-id="91f71-173">Apenas certifique-se de sair sempre que você alterar o escopo.</span><span class="sxs-lookup"><span data-stu-id="91f71-173">Just make sure to sign out each time you change the scope.</span></span>

