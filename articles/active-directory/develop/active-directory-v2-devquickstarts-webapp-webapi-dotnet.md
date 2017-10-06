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
# <a name="calling-a-web-api-from-a-net-web-app"></a>Chamar uma API Web em um aplicativo Web .NET
Com o ponto de extremidade Olá v 2.0, você pode adicionar autenticação tooyour web aplicativos e APIs da web com suporte para ambas as contas Microsoft pessoais e contas corporativas ou de estudante rapidamente.  Compilaremos aqui um aplicativo Web MVC que faz logon dos usuários usando o OpenID Connect, com alguma ajuda do middleware OWIN da Microsoft.  Olá web aplicativo obter tokens de acesso OAuth 2.0 para uma web api protegida pelo OAuth 2.0 permite criar, ler e excluir em um determinado usuário "lista de tarefas".

Este tutorial serão responsáveis por usando MSAL tooacquire e usar tokens de acesso em um aplicativo web, descrito por completo [aqui](active-directory-v2-flows.md#web-apps).  Como pré-requisitos, talvez você queira toofirst Saiba como muito[Adicionar aplicativo de web básico entrar tooa](active-directory-v2-devquickstarts-dotnet-web.md) ou como muito[proteger corretamente uma API da web](active-directory-v2-devquickstarts-dotnet-api.md).

> [!NOTE]
> Nem todos os recursos e cenários de Active Directory do Azure têm suporte pelo ponto de extremidade do hello v 2.0.  toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="download-sample-code"></a>Baixar código de exemplo
código de saudação para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).  toofollow ao longo, você pode [baixar o esqueleto do aplicativo hello como. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) ou esqueleto de saudação do clone:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

Como alternativa, você pode [baixar o aplicativo hello concluído como. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) ou aplicativo de saudação concluída do clone:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a>Registrar um aplicativo
Crie um novo aplicativo em [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ou siga estas [etapas detalhadas](active-directory-v2-app-registration.md).  Não se esqueça de:

* Cópia para baixo Olá **Id do aplicativo** atribuído tooyour aplicativo, você precisará dele em breve.
* Criar um **segredo do aplicativo** de saudação **senha** tipo e copiar para seu valor para mais tarde
* Adicionar Olá **Web** plataforma para seu aplicativo.
* Digite hello correto **URI de redirecionamento**. uri de redirecionamento Hello indica tooAzure AD onde as respostas de autenticação deverá ser direcionadas - Olá padrão para este tutorial é `https://localhost:44326/`.

## <a name="install-owin"></a>Instalar a OWIN
Adicionar Olá OWIN middleware NuGet pacotes toohello `TodoList-WebApp` projeto usando Olá Package Manager Console.  Olá OWIN middleware ser usado tooissue solicitações de entrada e saídas, gerenciar Olá sessão de usuário e obter informações sobre o usuário hello, entre outras coisas.

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-hello-user-in"></a>Usuário de saudação de logon no
Configurar Olá Olá de toouse de middleware OWIN [protocolo de autenticação OpenID Connect](active-directory-v2-protocols.md).  

* Olá abrir `web.config` arquivo na raiz de saudação da saudação `TodoList-WebApp` do projeto e insira os valores de configuração do aplicativo no hello `<appSettings>` seção.
  * Olá `ida:ClientId` é hello **Id do aplicativo** atribuído tooyour aplicativo no portal de registro de saudação.
  * Olá `ida:ClientSecret` é hello **segredo do aplicativo** criado no portal de registro de saudação.
  * Olá `ida:RedirectUri` é hello **Uri de redirecionamento** inserido no portal de saudação.
* Olá abrir `web.config` arquivo na raiz de saudação da saudação `TodoList-Service` do projeto e substituir Olá `ida:Audience` com hello mesmo **Id do aplicativo** como acima.
* Arquivo hello abrir `App_Start\Startup.Auth.cs` e adicione `using` instruções para bibliotecas de saudação acima.
* No hello mesmo arquivo, implementar Olá `ConfigureAuth(...)` método.  Olá parâmetros que você fornece em `OpenIDConnectAuthenticationOptions` servirá como coordenadas para toocommunicate seu aplicativo com o Azure AD.

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

## <a name="use-msal-tooget-access-tokens"></a>Usar tokens de acesso de tooget MSAL
Em Olá `AuthorizationCodeReceived` notificação, queremos toouse [OAuth 2.0 em tandem com OpenID Connect](active-directory-v2-protocols.md) tooredeem Olá authorization_code para um toohello de token de acesso serviço da lista de tarefas pendentes.  A MSAL pode facilitar esse processo para você:

* Primeiro, instale a versão de visualização de saudação do MSAL:

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* E adicione outro `using` instrução toohello `App_Start\Startup.Auth.cs` arquivo para MSAL.
* Agora adicione um novo método, hello `OnAuthorizationCodeReceived` manipulador de eventos.  Este manipulador usará MSAL tooacquire um toohello de token de acesso API da lista de tarefas e armazenará o token Olá no cache de token do MSAL para mais tarde:

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

* Em aplicativos da web, MSAL tem um cache de token extensível que pode ser usado toostore tokens.  Este exemplo implementa Olá `NaiveSessionCache` que usa tokens de toocache de armazenamento de sessão http.

<!-- TODO: Token Cache article -->


## <a name="call-hello-web-api"></a>Saudação de chamada de API da Web
Agora é hora tooactually usar access_token Olá que você copiou na etapa 3.  Do aplicativo da web aberto Olá `Controllers\TodoListController.cs` de arquivos, que faz com que todos os Olá CRUD solicitações toohello API da lista de tarefas pendentes.

* Você pode usar MSAL novamente aqui access_tokens toofetch de Olá cache MSAL.  Primeiro, adicione um `using` instrução para MSAL toothis arquivo.
  
    `using Microsoft.Identity.Client;`
* Em Olá `Index` ação, use MSAL `AcquireTokenSilentAsync` método tooget um access_token que podem ser dados tooread usado da saudação serviço de lista de tarefas:

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

* Olá exemplo então adiciona solicitação de HTTP GET de token toohello resultante hello como Olá `Authorization` cabeçalho, qual serviço de lista de tarefas pendentes de saudação usa tooauthenticate solicitação de saudação.
* Se Olá serviço de lista de tarefas retornará um `401 Unauthorized` resposta, Olá access_tokens em MSAL se tornam inválidos por alguma razão.  Nesse caso, você deve remover qualquer access_tokens de saudação cache MSAL e mostrar uma mensagem que talvez seja necessário toosign no novamente, que reiniciará o fluxo de aquisição de token de saudação do usuário de saudação.

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

* Da mesma forma, se MSAL for tooreturn não é possível um access_token por qualquer motivo, você deve instruir Olá usuário toosign em novamente.  Isso é tão simples quanto capturar qualquer `MSALException`:

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show hello user an error indicating they might need toosign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading tooDo List: " + ee.Message + " You might need toolog out and log back in.");
}
// ...
```

* Olá exato mesmo `AcquireTokenSilentAsync` chamada é implementd no hello `Create` e `Delete` ações.  Em aplicativos da web, você pode usar este access_tokens de tooget MSAL método sempre que você precisar deles em seu aplicativo.  A MSAL se encarregará da aquisição, do caching e da atualização de tokens.

Por fim, compile e execute seu aplicativo!  Entrar com uma Account da Microsoft ou uma conta do AD do Azure e observe como a identidade do usuário Olá é refletida na barra de navegação superior hello.  Adicionar e excluir alguns itens da lista de tarefas do usuário Olá chama toosee Olá que OAuth 2.0 protegidos API em ação.  Agora você tem um aplicativo Web e uma API Web, ambos protegidos por protocolos padrão do setor, que podem autenticar usuários com as respectivas contas pessoais e corporativas/de estudante.

Para referência, Olá concluída exemplo (sem os valores de configuração) [são fornecidas aqui](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).  

## <a name="next-steps"></a>Próximas etapas
Para obter recursos adicionais, consulte:

* [Guia do desenvolvedor v 2.0 Olá >>](active-directory-appmodel-v2-overview.md)
* [Marca “azure-active-directory” do StackOverflow >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Obter atualizações de segurança para nossos produtos
Recomendamos que você tooget as notificações quando os incidentes de segurança ocorrem visitando [essa página](https://technet.microsoft.com/security/dd252948) e assinando tooSecurity alertas de aviso.

