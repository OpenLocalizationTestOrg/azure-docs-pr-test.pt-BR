---
title: aaaAzure B2C do Active Directory | Microsoft Docs
description: "Como o perfil toobuild um aplicativo web que tem inscrição-o/entrar, editar e redefinição de senha usando o Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: barbaraselden
ms.assetid: 30261336-d7a5-4a6d-8c1a-7943ad76ed25
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 187f99a8dd50d212de4f0517f552cdbbe5a8edf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a>Criar um aplicativo Web ASP.NET com inscrição/entrada, edição de perfil e redefinição de senha do Azure Active Directory B2C

Este tutorial mostra como:

> [!div class="checklist"]
> * Adicionar o aplicativo web do Azure AD B2C identidade recursos tooyour
> * Registrar seu aplicativo Web em seu diretório do Azure AD B2C
> * Criar inscrição/entrada, edição de perfil e política de redefinição de senha de usuário para o seu aplicativo Web

## <a name="prerequisites"></a>Pré-requisitos

- Você deve conectar o tooan B2C locatário conta do Azure. Você pode criar uma conta gratuita do Azure [aqui](https://azure.microsoft.com/en-us/).
- Você precisa [Microsoft Visual Studio](https://www.visualstudio.com/) ou semelhantes tooview de programa e modificar o código de exemplo hello.

## <a name="create-an-azure-ad-b2c-directory"></a>Criar um diretório do AD B2C do Azure

Antes de usar AD B2C do Azure, você deve criar um diretório ou locatário. Um diretório é um contêiner para todos os seus usuários, aplicativos, grupos e muito mais. Se você ainda não tiver um, crie um diretório B2C antes de prosseguir neste guia.

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> É necessário tooconnect Olá B2C locatário tooyour assinatura do Azure. Depois de selecionar **criar**, selecione Olá **toomy Link um existente B2C de AD do Azure locatário assinatura do Azure** opção e, em seguida, em Olá **locatário Azure AD B2C** lista suspensa, selecione locatário Olá tooassociate desejado.

## <a name="create-and-register-an-application"></a>Criar e registrar um aplicativo

Em seguida, você precisa toocreate e registrar o aplicativo hello em seu diretório do B2C. Isso fornece informações que o Azure AD B2C precisa toosecurely se comunicar com seu aplicativo. 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

Quando você terminar, você terá uma API e um aplicativo nativo nas suas configurações de aplicativo.

## <a name="create-policies-on-your-b2c-tenant"></a>Criar políticas em seu locatário B2C

No AD B2C do Azure, cada experiência do usuário é definida por uma [política](active-directory-b2c-reference-policies.md). Este exemplo de código contém três experiências de identidade: **inscrição e entrada**, **edição de perfil** e **redefinição de senha**.  Você precisa de uma política de toocreate de cada tipo, conforme descrito em Olá [artigo de referência de política](active-directory-b2c-reference-policies.md). Para cada política, ser-se de atributo de nome de exibição tooselect hello ou declaração e toocopy nome hello da política para uso posterior.

### <a name="add-your-identity-providers"></a>Adicionar seus provedores de identidade

Nas configurações, selecione **Provedores de Identidade** e escolha Inscrição do nome de usuário ou Inscrição de email.

### <a name="create-a-sign-up-and-sign-in-policy"></a>Criar uma política de inscrição e entrada

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a>Criar uma política de edição de perfil

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a>Criar uma política de redefinição de senha

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

Depois de criar as políticas, você está pronto toobuild seu aplicativo.

## <a name="download-hello-sample-code"></a>Baixar o código de exemplo hello

código de saudação para este tutorial é mantido em [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). Você pode clonar o exemplo hello executando:

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Depois de baixar o código de exemplo hello, Olá abra o Visual Studio. sln arquivo tooget é iniciado. o arquivo de solução Olá contém dois projetos: `TaskWebApp` e `TaskService`. `TaskWebApp`é Olá aplicativo web MVC que Olá usuário interage com. `TaskService`é a API de web de back-end do aplicativo hello que armazena a lista de tarefas de cada usuário. Este artigo discutirá somente Olá `TaskWebApp` aplicativo. toolearn como toobuild `TaskService` usando o Azure AD B2C, consulte [nosso tutorial de api da web .NET](active-directory-b2c-devquickstarts-api-dotnet.md).

## <a name="update-code-toouse-your-tenant-and-policies"></a>Atualizar código toouse as políticas e seu locatário

Nosso exemplo é a ID de cliente e as políticas de Olá de toouse configurado do nosso locatário de demonstração. tooconnect-locatário da própria tooyour, você precisa tooopen `web.config` em Olá `TaskWebApp` do projeto e substituir Olá valores a seguir:

* `ida:Tenant` pelo nome do locatário
* `ida:ClientId` pela ID de aplicativo do aplicativo Web
* `ida:ClientSecret` pela chave de segredo do aplicativo Web
* `ida:SignUpSignInPolicyId` pelo nome da política "Inscrever-se ou Entrar"
* `ida:EditProfilePolicyId` pelo nome de política "Editar Perfil"
* `ida:ResetPasswordPolicyId` pelo nome de política "Redefinir Senha"

## <a name="launch-hello-app"></a>Inicie o aplicativo hello
De dentro do Visual Studio, inicie o aplicativo hello. Navegue toohello guia de lista de tarefas e Olá Observação URl é: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*& client_id = *YourclientID*...

Inscreva-se para o aplicativo hello usando seu nome de usuário ou endereço de email. Sair, e entrar novamente e editar o perfil de saudação ou redefinir a senha de saudação. Saia e entre como outro usuário. 

## <a name="add-social-idps"></a>Adicionar IDPs sociais

Atualmente, o aplicativo hello suporta apenas o usuário se inscrever e entrar usando **contas locais**; contas armazenadas no seu diretório do B2C que usam um nome de usuário e senha. Com o Azure AD B2C, você pode adicionar suporte a outros **provedores de identidade** (IDPs), sem alterar qualquer código.

tooadd social IDPs tooyour aplicativo, comece seguindo Olá detalhadas as instruções neste artigo. Para cada IDP toosupport desejado, você precisa tooregister um aplicativo no sistema e obter uma ID de cliente.

* [Configurar o Facebook como um IDP](active-directory-b2c-setup-fb-app.md)
* [Configurar o Google como um IDP](active-directory-b2c-setup-goog-app.md)
* [Configurar o Amazon como um IDP](active-directory-b2c-setup-amzn-app.md)
* [Configurar o LinkedIn como um IDP](active-directory-b2c-setup-li-app.md)

Depois de adicionar tooyour de provedores de identidade Olá directory B2C, edite seu tooinclude três políticas Olá IDPs novo, conforme descrito em Olá [artigo de referência de política](active-directory-b2c-reference-policies.md). Depois de salvar suas políticas, execute novamente o aplicativo hello.  Você deve ver Olá que idps novo são adicionados como opções de entrada e inscreva-se em cada uma das suas experiências de identidade.

Você pode fazer experiências com suas políticas e observar o efeito de saudação em seu aplicativo de exemplo. Adicione ou remova IDPs, manipule declarações de aplicativo ou altere os atributos de inscrição. Experimente até começar a entender como as políticas, solicitações de autenticação e OWIN funcionam juntos.

## <a name="sample-code-walkthrough"></a>Passo a passo do código de exemplo
Olá seções a seguir mostra como o código do aplicativo de exemplo hello está configurado. Você pode usar isso como um guia no desenvolvimento do seu futuro aplicativo.

### <a name="add-authentication-support"></a>Adicionar suporte a autenticação

Agora você pode configurar seu toouse de aplicativo do Azure AD B2C. Seu aplicativo se comunica com o Azure AD B2C ao enviar solicitações de autenticação OpenID Connect. solicitações Hello ditam experiência do usuário Olá seu aplicativo deseja tooexecute especificando a diretiva de saudação. Você pode usar toosend de biblioteca do Microsoft OWIN essas solicitações, executar políticas, gerenciar sessões de usuário e muito mais.

#### <a name="install-owin"></a>Instalar a OWIN

toobegin, Adicionar projeto de toohello Olá OWIN middleware NuGet pacotes usando Olá Visual Studio Package Manager Console.

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a>Adicionar uma classe de inicialização da OWIN

Adicionar uma toohello de classe de inicialização OWIN API chamado `Startup.cs`.  Clique com botão direito no projeto hello, selecione **adicionar** e **Novo Item**e, em seguida, procure a OWIN. Olá OWIN middleware invocará Olá `Configuration(…)` método quando seu aplicativo é iniciado.

Em nosso exemplo, alteramos declaração de classe Olá muito`public partial class Startup` e implementado Olá outra parte da classe Olá no `App_Start\Startup.Auth.cs`. Olá interna `Configuration` método, adicionamos uma chamada muito`ConfigureAuth`, que é definido em `Startup.Auth.cs`. Depois de modificações de saudação `Startup.cs` parece com hello seguinte:

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-hello-authentication-middleware"></a>Configurar o middleware de autenticação Olá

Arquivo hello abrir `App_Start\Startup.Auth.cs` e implementar Olá `ConfigureAuth(...)` método. Olá parâmetros que você fornece em `OpenIdConnectAuthenticationOptions` servem como coordenadas para toocommunicate seu aplicativo com o Azure AD B2C. Se você não especificar certos parâmetros, ele usará o valor padrão de saudação. Por exemplo, não especificamos Olá `ResponseType` no exemplo hello, Olá assim o valor padrão `code id_token` serão usados em cada tooAzure de solicitação de saída AD B2C.

Você também precisa tooset a autenticação de cookie. Olá OpenID Connect middleware usa sessões do usuário toomaintain cookies, entre outras coisas.

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure hello OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate hello metadata address using hello tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify hello callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify hello claims toovalidate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement hello "Notification" methods...
}
```

Em `OpenIdConnectAuthenticationOptions` acima, definimos um conjunto de funções de retorno de chamada para notificações específicas que são recebidas pelo middleware de OpenID Connect hello. Esses comportamentos são definidos usando um `OpenIdConnectAuthenticationNotifications` de objeto e armazenados em Olá `Notifications` variável. Em nosso exemplo, podemos definir três retornos de chamada diferentes dependendo do evento hello.

### <a name="using-different-policies"></a>Usando políticas diferentes

Olá `RedirectToIdentityProvider` notificação é acionada sempre que uma solicitação é feita tooAzure AD B2C. Na função de retorno de chamada hello `OnRedirectToIdentityProvider`, verificamos em Olá chamada de saída se quisermos toouse uma regra diferente. Em ordem toodo uma senha redefinida ou editar um perfil, você precisa política correspondente do toouse hello como política em vez da saudação "Inscrever ou entrar" diretiva de redefinição de senha de saudação.

Em nosso exemplo, quando um usuário deseja senha de saudação tooreset ou editar o perfil de hello, adicionamos política Olá que preferir toouse no contexto do OWIN hello. Isso pode ser feito fazendo Olá seguinte:

```CSharp
    // Let hello middleware know you are trying toouse hello edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

E você pode implementar uma função de retorno de chamada hello `OnRedirectToIdentityProvider` fazendo Olá seguinte:

```CSharp
/*
*  On each call tooAzure AD B2C, check if a policy (e.g. hello profile edit or password reset policy) has been specified in hello OWIN context.
*  If so, use that policy when making hello call. Also, don't request a code (since it won't be needed).
*/
private Task OnRedirectToIdentityProvider(RedirectToIdentityProviderNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    var policy = notification.OwinContext.Get<string>("Policy");

    if (!string.IsNullOrEmpty(policy) && !policy.Equals(DefaultPolicy))
    {
        notification.ProtocolMessage.Scope = OpenIdConnectScopes.OpenId;
        notification.ProtocolMessage.ResponseType = OpenIdConnectResponseTypes.IdToken;
        notification.ProtocolMessage.IssuerAddress = notification.ProtocolMessage.IssuerAddress.Replace(DefaultPolicy, policy);
    }

    return Task.FromResult(0);
}
```

### <a name="handling-authorization-codes"></a>Manipulando códigos de autorização

Olá `AuthorizationCodeReceived` notificação é acionada quando um código de autorização é recebido. Olá OpenID Connect middleware não dá suporte a códigos de troca para tokens de acesso. Você pode trocar manualmente código Olá para o token de saudação em uma função de retorno de chamada. Para obter mais informações, examine a saudação [documentação](active-directory-b2c-devquickstarts-web-api-dotnet.md) que explica como.

### <a name="handling-errors"></a>Tratamento de erros

Olá `AuthenticationFailed` notificação é disparada quando a autenticação falhará. Em seu método de retorno de chamada, você pode manipular erros hello como desejar. No entanto, você deve adicionar uma verificação de código de erro Olá `AADB2C90118`. Durante a execução Olá Olá política "Inscrever ou entrar", o usuário de saudação tem Olá oportunidade tooselect um **esqueceu sua senha?** link. Nesse caso, o Azure AD B2C envia seu aplicativo esse código de erro indicando que o aplicativo deve fazer uma solicitação usando a política de redefinição de senha Olá em vez disso.

```CSharp
/*
* Catch any failures received by hello authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle hello error code that Azure AD B2C throws when trying tooreset a password from hello login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If hello user clicked hello reset password link, redirect toohello reset password route
        notification.Response.Redirect("/Account/ResetPassword");
    }
    else if (notification.Exception.Message == "access_denied")
    {
        notification.Response.Redirect("/");
    }
    else
    {
        notification.Response.Redirect("/Home/Error?message=" + notification.Exception.Message);
    }

    return Task.FromResult(0);
}
```

### <a name="send-authentication-requests-tooazure-ad"></a>Enviar solicitações de autenticação tooAzure AD

Seu aplicativo agora está toocommunicate corretamente configurado com o Azure AD B2C usando o protocolo de autenticação OpenID Connect hello. OWIN gerencia os detalhes de saudação de criação de mensagens de autenticação, validando tokens do Azure AD B2C e manter a sessão de usuário. Tudo o que permanece é tooinitiate fluxo de cada usuário.

Quando um usuário seleciona **Sign up/entrar**, **Editar perfil**, ou **Redefinir senha** no Olá web app, ação Olá associado é invocada em `Controllers\AccountController.cs`:

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign up or sign in
*/
public void SignUpSignIn()
{
    // Use hello default policy tooprocess hello sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting tooedit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let hello middleware know you are trying toouse hello edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set hello page tooredirect tooafter editing hello profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting tooreset a password
*/
public void ResetPassword()
{
    // Let hello middleware know you are trying toouse hello reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set hello page tooredirect tooafter changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

Você também pode usar toosign OWIN usuário saudação do aplicativo hello. Em `Controllers\AccountController.cs`, temos:

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign out
*/
public void SignOut()
{
    // toosign out hello user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

Em adição tooexplicitly de invocar uma política, você pode usar um `[Authorize]` marca em seus controladores que executa uma política, se o usuário Olá não está conectado. Abra `Controllers\HomeController.cs` e adicione Olá `[Authorize]` marca toohello declarações controlador.  OWIN seleciona a última política de saudação configurada quando hello `[Authorize]` marca for atingida.

```CSharp
// Controllers\HomeController.cs

// You can use hello Authorize decorator tooexecute a certain policy if hello user is not already signed into hello app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a>Exibir informações do usuário

Quando você autenticar usuários usando o OpenID Connect, o Azure AD B2C retorna um aplicativo de toohello token de ID que contém **declarações**. Esses são afirmações sobre usuário hello. Você pode usar declarações toopersonalize seu aplicativo.

Olá abrir `Controllers\HomeController.cs` arquivo. Você pode acessar as declarações de usuário em seus controladores via Olá `ClaimsPrincipal.Current` objeto de segurança.

```CSharp
// Controllers\HomeController.cs

[Authorize]
public ActionResult Claims()
{
    Claim displayName = ClaimsPrincipal.Current.FindFirst(ClaimsPrincipal.Current.Identities.First().NameClaimType);
    ViewBag.DisplayName = displayName != null ? displayName.Value : string.Empty;
    return View();
}
```

Você pode acessar qualquer declaração que seu aplicativo recebe em Olá mesmo modo.  Uma lista de todas as declarações de Olá Olá aplicativo recebe está disponível para você no hello **declarações** página.
