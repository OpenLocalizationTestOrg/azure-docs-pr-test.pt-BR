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
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a>Azure AD B2C: chamar uma API Web de um aplicativo Web .NET

Usando o Azure AD B2C, você pode adicionar aplicativos web do identidade avançado Gerenciamento recursos tooyour e APIs da web. Este artigo aborda como toorequest tokens de acesso e fazer chamadas de uma "lista de tarefas".NET tooa de aplicativo web .NET web api.

Este artigo não aborda como tooimplement entrar, se inscrever e criar o perfil de gerenciamento com o Azure AD B2C. Ele se concentra em APIs da web chamado depois que o usuário Olá já está autenticado. Se você ainda não fez isto, você deverá:

* Começar com um [aplicativo Web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)
* Começar com uma [API Web .NET](active-directory-b2c-devquickstarts-api-dotnet.md)

## <a name="prerequisite"></a>Pré-requisito

toobuild um aplicativo web que chama uma web api, você precisa:

1. [Criar um locatário do Azure AD B2C](active-directory-b2c-get-started.md).
2. [Registrar uma api Web](active-directory-b2c-app-registration.md#register-a-web-api).
3. [Registrar um aplicativo Web](active-directory-b2c-app-registration.md#register-a-web-app).
4. [Configurar políticas](active-directory-b2c-reference-policies.md).
5. [Grant Olá web app permissões toouse Olá web api](active-directory-b2c-access-tokens.md#publishing-permissions).

> [!IMPORTANT]
> aplicativo de cliente Hello e a API da web devem usar o diretório do B2C Olá mesmo Azure AD.
>

## <a name="download-hello-code"></a>Baixar o código de saudação

código de saudação para este tutorial é mantido em [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). Você pode clonar o exemplo hello executando:

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Depois de baixar o código de exemplo hello, Olá abra o Visual Studio. sln arquivo tooget é iniciado. o arquivo de solução Olá contém dois projetos: `TaskWebApp` e `TaskService`. `TaskWebApp`é um aplicativo da web MVC que Olá usuário interage com. `TaskService`é a API de web de back-end do aplicativo hello que armazena a lista de tarefas de cada usuário. Este artigo não aborda construção Olá `TaskWebApp` aplicativo web ou hello `TaskService` web api. toolearn como toobuild Olá .NET web app usando o Azure AD B2C, consulte nosso [tutorial de aplicativo da web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md). toolearn como toobuild Olá .NET web API protegida usando o Azure AD B2C, consulte nosso [tutorial de API da web .NET](active-directory-b2c-devquickstarts-api-dotnet.md).

### <a name="update-hello-azure-ad-b2c-configuration"></a>Atualizar a configuração de saudação do Azure AD B2C

Nosso exemplo é a ID de cliente e as políticas de Olá de toouse configurado do nosso locatário de demonstração. Se você quiser toouse seu próprio locatário:

1. Abra `web.config` em Olá `TaskService` do projeto e substituir os valores hello para

    * `ida:Tenant` pelo nome do locatário
    * `ida:ClientId` pela ID do aplicativo da API Web
    * `ida:SignUpSignInPolicyId` pelo nome da política "Inscrever-se ou Entrar"

2. Abra `web.config` em Olá `TaskWebApp` do projeto e substituir os valores hello para

    * `ida:Tenant` pelo nome do locatário
    * `ida:ClientId` pela ID de aplicativo do aplicativo Web
    * `ida:ClientSecret` pela chave de segredo do aplicativo Web
    * `ida:SignUpSignInPolicyId` pelo nome da política "Inscrever-se ou Entrar"
    * `ida:EditProfilePolicyId` pelo nome de política "Editar Perfil"
    * `ida:ResetPasswordPolicyId` pelo nome de política "Redefinir Senha"



## <a name="requesting-and-saving-an-access-token"></a>Solicitar e salvar um token de acesso

### <a name="specify-hello-permissions"></a>Especificar permissões de saudação

Na ordem toomake Olá chamada toohello API da web, você precisa de usuário de saudação tooauthenticate (usando a diretiva de entrada-o/entrada) e [receber um token de acesso](active-directory-b2c-access-tokens.md) do Azure AD B2C. Em ordem tooreceive um token de acesso, você deve primeiro especificar permissões de saudação você gostaria que toogrant de token de acesso de saudação. Olá permissões são especificadas em Olá `scope` parâmetro quando você fizer Olá solicitação toohello `/authorize` ponto de extremidade. Por exemplo, tooacquire aplicativo de recurso de toohello de permissão que tem um token de acesso com hello "leitura" hello URI de ID do aplicativo de `https://contoso.onmicrosoft.com/tasks`, escopo Olá seria `https://contoso.onmicrosoft.com/tasks/read`.

escopo de saudação toospecify em nosso arquivo de exemplo, abra Olá `App_Start\Startup.Auth.cs` e definir Olá `Scope` variável OpenIdConnectAuthenticationOptions.

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

### <a name="exchange-hello-authorization-code-for-an-access-token"></a>Código de autorização de saudação do Exchange para um token de acesso

Depois que um usuário conclui a experiência de inscrição ou entrar hello, seu aplicativo receberá um código de autorização do Azure AD B2C. middleware OWIN OpenID Connect do Hello armazenará código hello, mas não a troca para um token de acesso. Você pode usar o hello [biblioteca MSAL](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) toomake intercâmbio de saudação. Em nosso exemplo, configuramos um retorno de chamada de notificação em Olá OpenID Connect middleware sempre que um código de autorização é recebido. No retorno de chamada Olá, podemos usar código de saudação do MSAL tooexchange para um token e salve o token Olá no cache de saudação.

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

## <a name="calling-hello-web-api"></a>Chamar a API da web de saudação

Esta seção discute como o token de saudação do toouse recebido durante a inscrição-o/entrar com o Azure AD B2C em ordem tooaccess Olá API da web.

### <a name="retrieve-hello-saved-token-in-hello-controllers"></a>Recuperar o token Olá salvada em controladores de saudação

Olá `TasksController` é responsável pela comunicação com a API da web hello para enviar tooread de toohello API de solicitações HTTP, criar e excluir tarefas. Como Olá API é protegido pelo Azure AD B2C, é necessário token de saudação recuperar toofirst que Olá acima etapa foi salvo.

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

### <a name="read-tasks-from-hello-web-api"></a>Ler tarefas de API da web hello

Quando você tiver um token, você poderá anexá-lo toohello HTTP `GET` solicitação no hello `Authorization` chamada do cabeçalho toosecurely `TaskService`:

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

### <a name="create-and-delete-tasks-on-hello-web-api"></a>Criar e excluir tarefas na API da web hello

Olá siga mesmo padrão quando você enviar `POST` e `DELETE` solicitações toohello web API, usando o token de acesso de saudação de tooretrieve MSAL do cache de saudação.

## <a name="run-hello-sample-app"></a>Execute o aplicativo de exemplo hello

Por fim, compilar e executar os dois aplicativos de saudação. Inscreva-se e entrar e criar tarefas para o usuário conectado hello. Saia e entre como outro usuário. Crie tarefas para esse usuário. Observe como tarefas de saudação são armazenados por usuário no hello API, porque Olá API extrai Olá a identidade de usuário do token Olá recebe. Além disso, tente brincando com escopos hello. Remover permissão de saudação muito "gravação" e, em seguida, tente adicionar uma tarefa. Verifique se toosign out cada vez que você alterar o escopo de saudação.

