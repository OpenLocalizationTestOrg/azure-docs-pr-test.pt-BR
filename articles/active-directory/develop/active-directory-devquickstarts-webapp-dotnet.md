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
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a>Entrada e saída do aplicativo Web ASP.NET com o Azure AD
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Fornecendo uma única entrada e saída com apenas algumas linhas de código, o Azure Active Directory (AD do Azure) facilita você toooutsource aplicativo web para gerenciamento de identidade. Você pode assinar os usuários e aplicativos web do ASP.NET usando a implementação da Interface Web aberta Microsoft Olá para o middleware .NET (OWIN). O middleware OWIN voltado para a comunidade está incluído no .NET Framework 4.5. Este artigo mostra como toouse OWIN para:

* Conectar usuários tooweb aplicativos usando o AD do Azure como provedor de identidade hello.
* Exibir informações do usuário.
* Conectar usuários fora da saudação aplicativos.

## <a name="before-you-get-started"></a>Antes de começar
* Baixar Olá [esqueleto de aplicativo](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) ou baixar Olá [exemplo concluído](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).
* Também é necessário um locatário Azure AD no qual aplicativo de saudação tooregister. Se você ainda não tiver um locatário Azure AD, [Saiba como tooget uma](active-directory-howto-tenant.md).

Quando você estiver pronto, siga Olá procedimentos Olá quatro seções.

## <a name="step-1-register-hello-new-app-with-azure-ad"></a>Etapa 1: Registrar Olá novo aplicativo com o Azure AD
tooset usuários de tooauthenticate do aplicativo hello, primeiro registrá-lo em seu locatário fazendo Olá seguinte:

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Na barra superior do hello, clique em seu nome de conta. Em Olá **diretório** lista, o locatário do Active Directory hello selecione onde você deseja que o aplicativo de saudação tooregister.
3. Clique em **mais serviços** Olá painel esquerdo e, em seguida, selecione **Active Directory do Azure**.
4. Clique em **Registros do aplicativo** e, em seguida, selecione **Adicionar**.
5. Siga Olá solicita toocreate um novo **aplicativo Web e/ou WebAPI**.
  * **Nome** descreve Olá toousers de aplicativo.
  * **URL de logon** é Olá a URL base do aplicativo hello. URL de padrão do esqueleto Olá é https://localhost:44320 /.
6. Depois de concluir o registro de saudação, o Azure AD atribui aplicativo hello uma ID exclusiva do aplicativo. Copie o valor de saudação da saudação aplicativo página toouse nas seções próximas hello.
7. De saudação **configurações** -> **propriedades** página para seu aplicativo, Olá URI da ID do aplicativo de atualização. Olá **URI da ID do aplicativo** é um identificador exclusivo para o aplicativo hello. Olá convenção de nomenclatura é `https://<tenant-domain>/<app-name>` (por exemplo, `https://contoso.onmicrosoft.com/my-first-aad-app`).

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a>Etapa 2: Configurar o pipeline de autenticação Olá aplicativo toouse Olá OWIN
Nesta etapa, você configurará Olá OWIN middleware toouse Olá OpenID Connect protocolo de autenticação. Usar OWIN tooissue solicitações de entrada e saídas, gerenciar sessões de usuário, obter informações de usuário e assim por diante.

1. toobegin, adicionar o projeto de toohello Olá OWIN middleware NuGet pacotes usando Olá Package Manager Console.

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. tooadd chamado de um projeto de toohello de classe de inicialização OWIN `Startup.cs`, clique com botão direito hello, selecione **adicionar**, selecione **Novo Item**e, em seguida, procure **OWIN**. Olá OWIN middleware chama Olá **Configuration(...)**  método quando o aplicativo hello for iniciado.
3. Altere a declaração de classe Olá muito`public partial class Startup`. Já implementamos parte dessa classe para você em outro arquivo. Em Olá **Configuration(...)**  método, fazer uma chamada muito**ConfgureAuth(...)**  tooset a autenticação para o aplicativo hello.  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. Abrir o arquivo de App_Start\Startup.Auth.cs hello e implementar Olá **ConfigureAuth(...)**  método. Olá parâmetros que você fornece em *OpenIDConnectAuthenticationOptions* servem como coordenadas de saudação toocommunicate de aplicativo com o Azure AD. Você também precisa tooset a autenticação de cookie, pois Olá OpenID Connect middleware usa cookies no plano de fundo de saudação.

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

5. Abra o arquivo de Web. config de Olá na raiz de saudação do projeto hello e digite os valores de configuração de saudação em Olá `<appSettings>` seção.
  * `ida:ClientId`: Olá GUID que você copiou da saudação portal do Azure em "etapa 1: registrar Olá novo aplicativo com o Azure AD."
  * `ida:Tenant`: nome de saudação do seu locatário do AD do Azure (por exemplo, contoso.onmicrosoft.com).
  * `ida:PostLogoutRedirectUri`: indicador Olá que informa ao AD do Azure em que um usuário deve ser redirecionado após uma solicitação de logout é concluída com êxito.

## <a name="step-3-use-owin-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Etapa 3: Usar OWIN tooissue entrada e saída solicitações tooAzure AD
aplicativo Hello agora está toocommunicate corretamente configurado com o Azure AD usando o protocolo de autenticação OpenID Connect hello. OWIN tratou todos os detalhes de saudação da criação de mensagens de autenticação, validando tokens do AD do Azure e manter as sessões do usuário. Tudo o que permanece é toogive seus usuários uma maneira toosign no e sair.

1. Você pode usar autorizar marcas no seu toosign de usuários toorequire controladores em antes de acessarem certas páginas. toodo assim, abra Controllers\HomeController.cs e adicione Olá `[Authorize]` marca toohello sobre o controlador.

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. Você também pode usar as solicitações de autenticação OWIN toodirectly problema de dentro de seu código. toodo isso, abra Controllers\AccountController.cs. Em seguida, em ações Olá SignIn() e SignOut (), emita desafio OpenID Connect e solicitações de saída.

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

3. Abra exibições \ compartilhadas\_LoginPartial.cshtml tooshow Olá usuário Olá aplicativo entrada e saídos e links tooprint nome do usuário da saudação em uma exibição.

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

## <a name="step-4-display-user-information"></a>Etapa 4: exibir informações do usuário
Quando ele autentica os usuários com OpenID Connect, o AD do Azure retorna um aplicativo de toohello id_token que contém "declarações", ou declarações sobre o usuário hello. Você pode usar o aplicativo de saudação de toopersonalize essas declarações fazendo Olá seguinte:

1. Abra o arquivo de Controllers\HomeController.cs de saudação. Você pode acessar declarações saudação do usuário em seus controladores via Olá `ClaimsPrincipal.Current` objeto de segurança.

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

2. Compilar e executar o aplicativo hello. Se você ainda não criou um novo usuário em seu locatário com um domínio c o m, agora é Olá tempo toodo assim. Faça assim:

  a. Entrar com esse usuário e observe como identidade do usuário Olá é refletida na barra superior hello.

  b. Saia e entre novamente como outro usuário em seu locatário.

  c. Se você estiver se sentindo particularmente ambicioso, registre e execute outra instância deste aplicativo (com sua própria clientId) e veja o logon único em ação.

## <a name="next-steps"></a>Próximas etapas
Para referência, consulte [exemplo hello concluída](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (sem os valores de configuração).

Agora você pode mover toomore tópicos avançados. Por exemplo, experimento [Proteger uma API Web com o Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
