---
title: aaaAzure AD B2C | Microsoft Docs
description: "Como toobuild uma API da Web do .NET usando o Azure Active Directory B2C, protegida usando tokens de acesso OAuth 2.0 para autenticação."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: 7146ed7f-2eb5-49e9-8d8b-ea1a895e1966
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: d45364216deda38ef44b60dd11e86d9a089ad509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a>Azure Active Directory B2C: criar uma API Web do .NET

Com o Active Directory B2C do Azure (AD do Azure), você pode proteger uma API Web usando tokens de acesso do OAuth 2.0. Esses tokens permitem que seu cliente aplicativos tooauthenticate toohello API. Este artigo mostra como toocreate uma API de "lista de tarefas".NET MVC que permite que os usuários do cliente de tarefas de tooCRUD do aplicativo. Olá web API é protegida usando o Azure AD B2C e só permite que os usuários autenticados toomanage sua lista de tarefas pendentes.

## <a name="create-an-azure-ad-b2c-directory"></a>Criar um diretório do AD B2C do Azure

Antes de usar AD B2C do Azure, você deve criar um diretório ou locatário. Um diretório é um contêiner para todos os seus usuários, aplicativos, grupos etc. Se você ainda não tiver um, [crie um diretório B2C](active-directory-b2c-get-started.md) antes de prosseguir neste guia.

> [!NOTE]
> aplicativo de cliente Hello e a API da web devem usar o diretório do B2C Olá mesmo Azure AD.
>

## <a name="create-a-web-api"></a>Criar uma API da Web

Em seguida, você precisa toocreate um aplicativo de API da web no seu diretório do B2C. Isso fornece informações do AD do Azure que ele precisa toosecurely se comunicar com seu aplicativo. toocreate um aplicativo, siga [estas instruções](active-directory-b2c-app-registration.md). É necessário que você:

* Incluir um **aplicativo web** ou **web API** no aplicativo hello.
* Saudação de uso **URI de redirecionamento** `https://localhost:44332/` para o aplicativo web de saudação. Este é o local padrão de saudação do cliente de aplicativo web Olá para este exemplo de código.
* Saudação de cópia **ID do aplicativo** que é atribuído tooyour aplicativo. Você precisará dela mais tarde.
* Insira um identificador de aplicativo em **URI da ID do aplicativo**.
* Adicionar permissões através de saudação **publicado escopos** menu.

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Criar suas políticas

No AD B2C do Azure, cada experiência do usuário é definida por uma [política](active-directory-b2c-reference-policies.md). Você precisará toocreate toocommunicate uma política com o Azure AD B2C. É recomendável usar Olá combinados inscrição-o/política, conforme descrito em Olá [artigo de referência de política](active-directory-b2c-reference-policies.md). Ao criar a política, não se esqueça de:

* Escolher o **Nome de exibição** e outros atributos de inscrição na política.
* Escolher as declarações **Nome de exibição** e **ID de objeto** como declarações de aplicativo para cada política. Você pode escolher outras declarações também.
* Saudação de cópia **nome** de cada política depois de criá-lo. Você precisará nome da política hello mais tarde.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Depois que você criou com êxito a diretiva hello, você está pronto toobuild seu aplicativo.

## <a name="download-hello-code"></a>Baixar o código de saudação

código de saudação para este tutorial é mantido em [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). Você pode clonar o exemplo hello executando:

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Depois de baixar o código de exemplo hello, Olá abra o Visual Studio. sln arquivo tooget é iniciado. o arquivo de solução Olá contém dois projetos: `TaskWebApp` e `TaskService`. `TaskWebApp`é um aplicativo MVC que Olá usuário interage com. `TaskService`é a API de web de back-end do aplicativo hello que armazena a lista de tarefas de cada usuário. Este artigo discutirá somente Olá `TaskService` aplicativo. toolearn como toobuild `TaskWebApp` usando o Azure AD B2C, consulte [nosso tutorial de aplicativo web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).

### <a name="update-hello-azure-ad-b2c-configuration"></a>Atualizar a configuração de saudação do Azure AD B2C

Nosso exemplo é a ID de cliente e as políticas de Olá de toouse configurado do nosso locatário de demonstração. Se você quiser toouse seu próprio locatário, você precisará Olá toodo a seguir:

1. Abra `web.config` em Olá `TaskService` do projeto e substituir os valores hello para
    * `ida:Tenant` pelo nome do locatário
    * `ida:ClientId` com a ID do aplicativo de API da Web
    * `ida:SignUpSignInPolicyId` pelo nome da política "Inscrever-se ou Entrar"

2. Abra `web.config` em Olá `TaskWebApp` do projeto e substituir os valores hello para
    * `ida:Tenant` pelo nome do locatário
    * `ida:ClientId` pela ID de aplicativo do aplicativo Web
    * `ida:ClientSecret` pela chave de segredo do aplicativo Web
    * `ida:SignUpSignInPolicyId` pelo nome da política "Inscrever-se ou Entrar"
    * `ida:EditProfilePolicyId` pelo nome de política "Editar Perfil"
    * `ida:ResetPasswordPolicyId` pelo nome de política "Redefinir Senha"


## <a name="secure-hello-api"></a>Proteger a saudação API

Quando tem um cliente que chama a API, você pode proteger a API (por exemplo `TaskService`) usando os tokens de portador OAuth 2.0. Isso garante que cada API de tooyour solicitação só será válido se a solicitação de saudação tem um token de portador. Sua API pode aceitar e validar tokens de portador usando a biblioteca OWIN (Open Web Interface para .NET) da Microsoft.

### <a name="install-owin"></a>Instalar a OWIN

Comece instalando o pipeline de autenticação OWIN OAuth hello usando Olá Visual Studio Package Manager Console.

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

Isso irá instalar Olá owin que aceitará e validará os tokens de portador.

### <a name="add-an-owin-startup-class"></a>Adicionar uma classe de inicialização da OWIN

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

### <a name="configure-oauth-20-authentication"></a>Configurar a autenticação OAuth 2.0

Arquivo hello abrir `App_Start\Startup.Auth.cs`e implementar Olá `ConfigureAuth(...)` método. Por exemplo, ele pode ser semelhante a saudação a seguir:

```CSharp
// App_Start\Startup.Auth.cs

 public partial class Startup
    {
        // These values are pulled from web.config
        public static string AadInstance = ConfigurationManager.AppSettings["ida:AadInstance"];
        public static string Tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        public static string ClientId = ConfigurationManager.AppSettings["ida:ClientId"];
        public static string SignUpSignInPolicy = ConfigurationManager.AppSettings["ida:SignUpSignInPolicyId"];
        public static string DefaultPolicy = SignUpSignInPolicy;

        /*
         * Configure hello authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where hello audience of hello token is equal toohello client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches hello Azure AD B2C metadata & signing keys from hello OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-hello-task-controller"></a>Olá tarefa controlador seguro

Após o aplicativo hello autenticação toouse configurado OAuth 2.0, você pode proteger sua API da web adicionando um `[Authorize]` controlador de tarefas marca toohello. Este é o controlador de saudação onde todos os manipulação de lista de tarefas pendentes ocorre, portanto você deve proteger o controlador de saudação inteira no nível de classe hello. Você também pode adicionar Olá `[Authorize]` tooindividual ações para um controle mais refinado de marca.

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-hello-token"></a>Obter informações de usuário do hello token

`TasksController`armazena as tarefas em um banco de dados onde cada tarefa tem um usuário associado à tarefa hello "proprietário". proprietário de saudação é identificado pelo usuário Olá **ID de objeto**. (Isso é porque necessário tooadd Olá ID de objeto como um aplicativo declaração em todas as suas políticas.)

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-hello-permissions-in-hello-token"></a>Validar Olá permissões no token Olá

Um requisito comum para APIs da web é toovalidate hello "escopos" presentes no token de saudação. Isso garante que o usuário Olá consentiu permissões toohello Olá tooaccess necessário serviço da lista de tarefas pendentes.

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "hello Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-hello-sample-app"></a>Execute o aplicativo de exemplo hello

Por fim, compile e execute `TaskWebApp` e `TaskService`. Criar algumas tarefas na lista de tarefas do usuário hello e observe como eles são persistentes no hello API mesmo depois que você parar e reiniciar o cliente hello.

## <a name="edit-your-policies"></a>Editar suas políticas

Depois que você protegeu uma API usando o Azure AD B2C, você pode testar sua política de entrada-em/entrada o e efeitos de saudação do modo de exibição (ou não) em Olá API. Você pode manipular as declarações de aplicativo hello nas políticas hello e alterar Olá informações do usuário que estão disponíveis na API da web hello. Quaisquer declarações que você adicionar serão tooyour disponível .NET MVC web API no hello `ClaimsPrincipal` do objeto, conforme descrito anteriormente neste artigo.
