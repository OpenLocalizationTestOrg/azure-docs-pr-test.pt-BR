---
title: "aaaAdd tooa entrar API da web .NET MVC usando Olá o ponto de extremidade do AD do Azure v 2.0 | Microsoft Docs"
description: Como toobuild uma Api da Web MVC do .NET que aceita tokens de ambos os Account pessoal da Microsoft e contas corporativa ou escolar.
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e77bc4e0-d0c9-4075-a3f6-769e2c810206
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4e517145422bb6e9368e82a7eef4a5c57cce530a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-mvc-web-api"></a>Proteger uma API Web do MVC
Com o ponto de extremidade de Active Directory do Azure Olá v 2.0, você pode proteger uma API da Web usando [OAuth 2.0](active-directory-v2-protocols.md) tokens de acesso, permitindo que os usuários com ambas as conta pessoal da Microsoft e contas corporativas ou de estudante toosecurely acessar a API da Web.

> [!NOTE]
> Nem todos os recursos e cenários de Active Directory do Azure têm suporte pelo ponto de extremidade do hello v 2.0.  toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).
>
>

Em APIs da Web ASP.NET, você pode conseguir isso usando o middleware OWIN da Microsoft, incluso no .NET Framework 4.5.  Aqui vamos usar OWIN toobuild uma API da Web MVC de "tooDo lista" que permite que os clientes toocreate e ler tarefas da lista de tarefas do usuário.  API da web Hello validará que as solicitações de entrada contém um token de acesso válido e rejeitar todas as solicitações que não passou na validação em uma rota protegida.  Este exemplo foi criado usando o Visual Studio 2015.

## <a name="download"></a>Baixar
código de saudação para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).  toofollow ao longo, você pode [baixar o esqueleto do aplicativo hello como. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) ou esqueleto de saudação do clone:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

aplicativo de esqueleto Olá inclui todo o código clichê Olá para uma API simples, mas não tem todas as partes relacionadas à identidade de saudação. Se você não quiser toofollow ao longo, em vez disso, você pode clonar ou [baixar exemplo hello concluída](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a>Registrar um aplicativo
Crie um novo aplicativo em [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ou siga estas [etapas detalhadas](active-directory-v2-app-registration.md).  Não se esqueça de:

* Cópia para baixo Olá **Id do aplicativo** atribuído tooyour aplicativo, você precisará dele em breve.

Essa solução do Visual Studio também contém um "TodoListClient”, que é um aplicativo WPF simples.  Olá TodoListClient é toodemonstrate usado como um usuário entrar e como um cliente pode emitir solicitações tooyour API da Web.  Nesse caso, a saudação TodoListClient e Olá TodoListService são representados por Olá mesmo aplicativo.  tooconfigure Olá TodoListClient, você também deve:

* Adicionar Olá **Mobile** plataforma para seu aplicativo.

## <a name="install-owin"></a>Instalar a OWIN
Agora que você já registrou um aplicativo, você precisa tooset backup toocommunicate seu aplicativo com ponto de extremidade do hello v 2.0 em ordem toovalidate solicitações de entrada e tokens.

* toobegin, abra a solução hello e adicione Olá OWIN middleware NuGet pacotes toohello projeto TodoListService usando Olá Package Manager Console.

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a>Configurar a autenticação OAuth
* Adicionar um projeto TodoListService do toohello da classe de inicialização OWIN chamado `Startup.cs`.  --> Do botão direito do mouse no projeto de saudação **adicionar** --> **Novo Item** --> procure "OWIN".  Olá OWIN middleware invocará Olá `Configuration(…)` método quando seu aplicativo é iniciado.
* Altere a declaração de classe Olá muito`public partial class Startup` -já implementamos parte dessa classe para você em outro arquivo.  Em Olá `Configuration(…)` método, faça um tooset tooConfgureAuth(...) de chamada de autenticação para seu aplicativo web.

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* Arquivo hello abrir `App_Start\Startup.Auth.cs` e implementar Olá `ConfigureAuth(…)` método, que irá configurar tokens de tooaccept de API da Web de saudação do ponto de extremidade do hello v 2.0.

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, hello TodoListClient and TodoListService
                // are represented using hello same Application Id - we use
                // hello Application Id toorepresent hello audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that hello user's organization (if applicable) has
                // signed up for hello app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up hello OWIN pipeline toouse OAuth 2.0 Bearer authentication.
        // hello options provided here tell hello middleware about hello type of tokens
        // that will be recieved, which are JWTs for hello v2.0 endpoint.

        // NOTE: hello usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by hello v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used toofetch & use hello OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* Agora você pode usar `[Authorize]` atributos tooprotect seus controladores e ações com autenticação do portador do OAuth 2.0.  Decore Olá `Controllers\TodoListController.cs` classe com uma marca de autorização.  Isso forçará Olá usuário toosign em antes de acessar essa página.

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* Quando um chamador autorizado com êxito invoca uma saudação `TodoListController` APIs, ação Olá pode precisar acessar tooinformation sobre chamador hello.  OWIN fornece acesso toohello declarações no token de portador Olá via Olá `ClaimsPrincpal` objeto.  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use hello ClaimsPrincipal tooaccess information about the
    // user making hello call.  In this case, we use hello 'sub' or
    // NameIdentifier claim tooserve as a key for hello tasks in hello data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* Por fim, abra Olá `web.config` na raiz de saudação do projeto TodoListService de saudação do arquivo e insira os valores de configuração no hello `<appSettings>` seção.
  * O `ida:Audience` é hello **Id do aplicativo** do aplicativo hello que você inseriu no portal de saudação.

## <a name="configure-hello-client-app"></a>Configurar o aplicativo de cliente Olá
Antes de poder ver Olá serviço de lista de tarefas em ação, você precisa tooconfigure Olá cliente da lista de tarefas para que possa obter tokens do ponto de extremidade do hello v 2.0 e fazer chamadas toohello serviço.

* No projeto de TodoListClient hello, abra `App.config` e insira os valores de configuração no hello `<appSettings>` seção.
  * O `ida:ClientId` é copiada do portal de saudação de Id do aplicativo.

Por fim, limpe, compile e execute cada projeto!  Agora você tem uma API da Web .NET MVC que aceita tokens de contas da Microsoft pessoais e contas corporativas ou de estudante.  Entrar Olá TodoListClient e chamar a lista de tarefas de web api tooadd tarefas toohello do usuário.

Para referência, Olá concluída exemplo (sem os valores de configuração) [é fornecido como. zip aqui](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), ou você pode cloná-lo do GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a>Próximas etapas
Agora você pode passar para tópicos adicionais.  Você pode desejar tootry:

[Chamar uma API Web em um aplicativo Web >>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

Para obter recursos adicionais, consulte:

* [Guia do desenvolvedor v 2.0 Olá >>](active-directory-appmodel-v2-overview.md)
* [Marca “azure-active-directory” do StackOverflow >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Obter atualizações de segurança para nossos produtos
Recomendamos que você tooget as notificações quando os incidentes de segurança ocorrem visitando [essa página](https://technet.microsoft.com/security/dd252948) e assinando tooSecurity alertas de aviso.
