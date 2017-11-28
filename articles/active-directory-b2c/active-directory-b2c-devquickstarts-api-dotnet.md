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
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a><span data-ttu-id="3c437-103">Azure Active Directory B2C: criar uma API Web do .NET</span><span class="sxs-lookup"><span data-stu-id="3c437-103">Azure Active Directory B2C: Build a .NET web API</span></span>

<span data-ttu-id="3c437-104">Com o Active Directory B2C do Azure (AD do Azure), você pode proteger uma API Web usando tokens de acesso do OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="3c437-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="3c437-105">Esses tokens permitem que seu cliente aplicativos tooauthenticate toohello API.</span><span class="sxs-lookup"><span data-stu-id="3c437-105">These tokens allow your client apps tooauthenticate toohello API.</span></span> <span data-ttu-id="3c437-106">Este artigo mostra como toocreate uma API de "lista de tarefas".NET MVC que permite que os usuários do cliente de tarefas de tooCRUD do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3c437-106">This article shows you how toocreate a .NET MVC "to-do list" API that allows users of your client application tooCRUD tasks.</span></span> <span data-ttu-id="3c437-107">Olá web API é protegida usando o Azure AD B2C e só permite que os usuários autenticados toomanage sua lista de tarefas pendentes.</span><span class="sxs-lookup"><span data-stu-id="3c437-107">hello web API is secured using Azure AD B2C and only allows authenticated users toomanage their to-do list.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="3c437-108">Criar um diretório do AD B2C do Azure</span><span class="sxs-lookup"><span data-stu-id="3c437-108">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="3c437-109">Antes de usar AD B2C do Azure, você deve criar um diretório ou locatário.</span><span class="sxs-lookup"><span data-stu-id="3c437-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="3c437-110">Um diretório é um contêiner para todos os seus usuários, aplicativos, grupos etc.</span><span class="sxs-lookup"><span data-stu-id="3c437-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="3c437-111">Se você ainda não tiver um, [crie um diretório B2C](active-directory-b2c-get-started.md) antes de prosseguir neste guia.</span><span class="sxs-lookup"><span data-stu-id="3c437-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

> [!NOTE]
> <span data-ttu-id="3c437-112">aplicativo de cliente Hello e a API da web devem usar o diretório do B2C Olá mesmo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3c437-112">hello client application and web API must use hello same Azure AD B2C directory.</span></span>
>

## <a name="create-a-web-api"></a><span data-ttu-id="3c437-113">Criar uma API da Web</span><span class="sxs-lookup"><span data-stu-id="3c437-113">Create a web API</span></span>

<span data-ttu-id="3c437-114">Em seguida, você precisa toocreate um aplicativo de API da web no seu diretório do B2C.</span><span class="sxs-lookup"><span data-stu-id="3c437-114">Next, you need toocreate a web API app in your B2C directory.</span></span> <span data-ttu-id="3c437-115">Isso fornece informações do AD do Azure que ele precisa toosecurely se comunicar com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3c437-115">This gives Azure AD information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="3c437-116">toocreate um aplicativo, siga [estas instruções](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="3c437-116">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="3c437-117">É necessário que você:</span><span class="sxs-lookup"><span data-stu-id="3c437-117">Be sure to:</span></span>

* <span data-ttu-id="3c437-118">Incluir um **aplicativo web** ou **web API** no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="3c437-118">Include a **web app** or **web API** in hello application.</span></span>
* <span data-ttu-id="3c437-119">Saudação de uso **URI de redirecionamento** `https://localhost:44332/` para o aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c437-119">Use hello **Redirect URI** `https://localhost:44332/` for hello web app.</span></span> <span data-ttu-id="3c437-120">Este é o local padrão de saudação do cliente de aplicativo web Olá para este exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="3c437-120">This is hello default location of hello web app client for this code sample.</span></span>
* <span data-ttu-id="3c437-121">Saudação de cópia **ID do aplicativo** que é atribuído tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3c437-121">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="3c437-122">Você precisará dela mais tarde.</span><span class="sxs-lookup"><span data-stu-id="3c437-122">You'll need it later.</span></span>
* <span data-ttu-id="3c437-123">Insira um identificador de aplicativo em **URI da ID do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="3c437-123">Enter an app identifier into **App ID URI**.</span></span>
* <span data-ttu-id="3c437-124">Adicionar permissões através de saudação **publicado escopos** menu.</span><span class="sxs-lookup"><span data-stu-id="3c437-124">Add permissions through hello **Published scopes** menu.</span></span>

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="3c437-125">Criar suas políticas</span><span class="sxs-lookup"><span data-stu-id="3c437-125">Create your policies</span></span>

<span data-ttu-id="3c437-126">No AD B2C do Azure, cada experiência do usuário é definida por uma [política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="3c437-126">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="3c437-127">Você precisará toocreate toocommunicate uma política com o Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="3c437-127">You will need toocreate a policy toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="3c437-128">É recomendável usar Olá combinados inscrição-o/política, conforme descrito em Olá [artigo de referência de política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="3c437-128">We recommend using hello combined sign-up/sign-in policy, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="3c437-129">Ao criar a política, não se esqueça de:</span><span class="sxs-lookup"><span data-stu-id="3c437-129">When you create your policy, be sure to:</span></span>

* <span data-ttu-id="3c437-130">Escolher o **Nome de exibição** e outros atributos de inscrição na política.</span><span class="sxs-lookup"><span data-stu-id="3c437-130">Choose **Display name** and other sign-up attributes in your policy.</span></span>
* <span data-ttu-id="3c437-131">Escolher as declarações **Nome de exibição** e **ID de objeto** como declarações de aplicativo para cada política.</span><span class="sxs-lookup"><span data-stu-id="3c437-131">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="3c437-132">Você pode escolher outras declarações também.</span><span class="sxs-lookup"><span data-stu-id="3c437-132">You can choose other claims as well.</span></span>
* <span data-ttu-id="3c437-133">Saudação de cópia **nome** de cada política depois de criá-lo.</span><span class="sxs-lookup"><span data-stu-id="3c437-133">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="3c437-134">Você precisará nome da política hello mais tarde.</span><span class="sxs-lookup"><span data-stu-id="3c437-134">You'll need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="3c437-135">Depois que você criou com êxito a diretiva hello, você está pronto toobuild seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3c437-135">After you have successfully created hello policy, you're ready toobuild your app.</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="3c437-136">Baixar o código de saudação</span><span class="sxs-lookup"><span data-stu-id="3c437-136">Download hello code</span></span>

<span data-ttu-id="3c437-137">código de saudação para este tutorial é mantido em [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="3c437-137">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="3c437-138">Você pode clonar o exemplo hello executando:</span><span class="sxs-lookup"><span data-stu-id="3c437-138">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="3c437-139">Depois de baixar o código de exemplo hello, Olá abra o Visual Studio. sln arquivo tooget é iniciado.</span><span class="sxs-lookup"><span data-stu-id="3c437-139">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="3c437-140">o arquivo de solução Olá contém dois projetos: `TaskWebApp` e `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="3c437-140">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="3c437-141">`TaskWebApp`é um aplicativo MVC que Olá usuário interage com.</span><span class="sxs-lookup"><span data-stu-id="3c437-141">`TaskWebApp` is an MVC web application that hello user interacts with.</span></span> <span data-ttu-id="3c437-142">`TaskService`é a API de web de back-end do aplicativo hello que armazena a lista de tarefas de cada usuário.</span><span class="sxs-lookup"><span data-stu-id="3c437-142">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="3c437-143">Este artigo discutirá somente Olá `TaskService` aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3c437-143">This article will only discuss hello `TaskService` application.</span></span> <span data-ttu-id="3c437-144">toolearn como toobuild `TaskWebApp` usando o Azure AD B2C, consulte [nosso tutorial de aplicativo web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="3c437-144">toolearn how toobuild `TaskWebApp` using Azure AD B2C, see [our .NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>

### <a name="update-hello-azure-ad-b2c-configuration"></a><span data-ttu-id="3c437-145">Atualizar a configuração de saudação do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="3c437-145">Update hello Azure AD B2C configuration</span></span>

<span data-ttu-id="3c437-146">Nosso exemplo é a ID de cliente e as políticas de Olá de toouse configurado do nosso locatário de demonstração.</span><span class="sxs-lookup"><span data-stu-id="3c437-146">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="3c437-147">Se você quiser toouse seu próprio locatário, você precisará Olá toodo a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c437-147">If you would like toouse your own tenant, you will need toodo hello following:</span></span>

1. <span data-ttu-id="3c437-148">Abra `web.config` em Olá `TaskService` do projeto e substituir os valores hello para</span><span class="sxs-lookup"><span data-stu-id="3c437-148">Open `web.config` in hello `TaskService` project and replace hello values for</span></span>
    * <span data-ttu-id="3c437-149">`ida:Tenant` pelo nome do locatário</span><span class="sxs-lookup"><span data-stu-id="3c437-149">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="3c437-150">`ida:ClientId` com a ID do aplicativo de API da Web</span><span class="sxs-lookup"><span data-stu-id="3c437-150">`ida:ClientId` with your web API application ID</span></span>
    * <span data-ttu-id="3c437-151">`ida:SignUpSignInPolicyId` pelo nome da política "Inscrever-se ou Entrar"</span><span class="sxs-lookup"><span data-stu-id="3c437-151">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="3c437-152">Abra `web.config` em Olá `TaskWebApp` do projeto e substituir os valores hello para</span><span class="sxs-lookup"><span data-stu-id="3c437-152">Open `web.config` in hello `TaskWebApp` project and replace hello values for</span></span>
    * <span data-ttu-id="3c437-153">`ida:Tenant` pelo nome do locatário</span><span class="sxs-lookup"><span data-stu-id="3c437-153">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="3c437-154">`ida:ClientId` pela ID de aplicativo do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="3c437-154">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="3c437-155">`ida:ClientSecret` pela chave de segredo do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="3c437-155">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="3c437-156">`ida:SignUpSignInPolicyId` pelo nome da política "Inscrever-se ou Entrar"</span><span class="sxs-lookup"><span data-stu-id="3c437-156">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="3c437-157">`ida:EditProfilePolicyId` pelo nome de política "Editar Perfil"</span><span class="sxs-lookup"><span data-stu-id="3c437-157">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="3c437-158">`ida:ResetPasswordPolicyId` pelo nome de política "Redefinir Senha"</span><span class="sxs-lookup"><span data-stu-id="3c437-158">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>


## <a name="secure-hello-api"></a><span data-ttu-id="3c437-159">Proteger a saudação API</span><span class="sxs-lookup"><span data-stu-id="3c437-159">Secure hello API</span></span>

<span data-ttu-id="3c437-160">Quando tem um cliente que chama a API, você pode proteger a API (por exemplo `TaskService`) usando os tokens de portador OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="3c437-160">When you have a client that calls your API, you can secure your API (e.g `TaskService`) by using OAuth 2.0 bearer tokens.</span></span> <span data-ttu-id="3c437-161">Isso garante que cada API de tooyour solicitação só será válido se a solicitação de saudação tem um token de portador.</span><span class="sxs-lookup"><span data-stu-id="3c437-161">This ensures that each request tooyour API will only be valid if hello request has a bearer token.</span></span> <span data-ttu-id="3c437-162">Sua API pode aceitar e validar tokens de portador usando a biblioteca OWIN (Open Web Interface para .NET) da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3c437-162">Your API can accept and validate bearer tokens by using Microsoft's Open Web Interface for .NET (OWIN) library.</span></span>

### <a name="install-owin"></a><span data-ttu-id="3c437-163">Instalar a OWIN</span><span class="sxs-lookup"><span data-stu-id="3c437-163">Install OWIN</span></span>

<span data-ttu-id="3c437-164">Comece instalando o pipeline de autenticação OWIN OAuth hello usando Olá Visual Studio Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="3c437-164">Begin by installing hello OWIN OAuth authentication pipeline by using hello Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

<span data-ttu-id="3c437-165">Isso irá instalar Olá owin que aceitará e validará os tokens de portador.</span><span class="sxs-lookup"><span data-stu-id="3c437-165">This will install hello OWIN middleware that will accept and validate bearer tokens.</span></span>

### <a name="add-an-owin-startup-class"></a><span data-ttu-id="3c437-166">Adicionar uma classe de inicialização da OWIN</span><span class="sxs-lookup"><span data-stu-id="3c437-166">Add an OWIN startup class</span></span>

<span data-ttu-id="3c437-167">Adicionar uma toohello de classe de inicialização OWIN API chamado `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="3c437-167">Add an OWIN startup class toohello API called `Startup.cs`.</span></span>  <span data-ttu-id="3c437-168">Clique com botão direito no projeto hello, selecione **adicionar** e **Novo Item**e, em seguida, procure a OWIN.</span><span class="sxs-lookup"><span data-stu-id="3c437-168">Right-click on hello project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="3c437-169">Olá OWIN middleware invocará Olá `Configuration(…)` método quando seu aplicativo é iniciado.</span><span class="sxs-lookup"><span data-stu-id="3c437-169">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="3c437-170">Em nosso exemplo, alteramos declaração de classe Olá muito`public partial class Startup` e implementado Olá outra parte da classe Olá no `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="3c437-170">In our sample, we changed hello class declaration too`public partial class Startup` and implemented hello other part of hello class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="3c437-171">Olá interna `Configuration` método, adicionamos uma chamada muito`ConfigureAuth`, que é definido em `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="3c437-171">Inside hello `Configuration` method, we added a call too`ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="3c437-172">Depois de modificações de saudação `Startup.cs` parece com hello seguinte:</span><span class="sxs-lookup"><span data-stu-id="3c437-172">After hello modifications, `Startup.cs` looks like hello following:</span></span>

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

### <a name="configure-oauth-20-authentication"></a><span data-ttu-id="3c437-173">Configurar a autenticação OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="3c437-173">Configure OAuth 2.0 authentication</span></span>

<span data-ttu-id="3c437-174">Arquivo hello abrir `App_Start\Startup.Auth.cs`e implementar Olá `ConfigureAuth(...)` método.</span><span class="sxs-lookup"><span data-stu-id="3c437-174">Open hello file `App_Start\Startup.Auth.cs`, and implement hello `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="3c437-175">Por exemplo, ele pode ser semelhante a saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c437-175">For example, it could look like hello following:</span></span>

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

### <a name="secure-hello-task-controller"></a><span data-ttu-id="3c437-176">Olá tarefa controlador seguro</span><span class="sxs-lookup"><span data-stu-id="3c437-176">Secure hello task controller</span></span>

<span data-ttu-id="3c437-177">Após o aplicativo hello autenticação toouse configurado OAuth 2.0, você pode proteger sua API da web adicionando um `[Authorize]` controlador de tarefas marca toohello.</span><span class="sxs-lookup"><span data-stu-id="3c437-177">After hello app is configured toouse OAuth 2.0 authentication, you can secure your web API by adding an `[Authorize]` tag toohello task controller.</span></span> <span data-ttu-id="3c437-178">Este é o controlador de saudação onde todos os manipulação de lista de tarefas pendentes ocorre, portanto você deve proteger o controlador de saudação inteira no nível de classe hello.</span><span class="sxs-lookup"><span data-stu-id="3c437-178">This is hello controller where all to-do list manipulation takes place, so you should secure hello entire controller at hello class level.</span></span> <span data-ttu-id="3c437-179">Você também pode adicionar Olá `[Authorize]` tooindividual ações para um controle mais refinado de marca.</span><span class="sxs-lookup"><span data-stu-id="3c437-179">You can also add hello `[Authorize]` tag tooindividual actions for more fine-grained control.</span></span>

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-hello-token"></a><span data-ttu-id="3c437-180">Obter informações de usuário do hello token</span><span class="sxs-lookup"><span data-stu-id="3c437-180">Get user information from hello token</span></span>

<span data-ttu-id="3c437-181">`TasksController`armazena as tarefas em um banco de dados onde cada tarefa tem um usuário associado à tarefa hello "proprietário".</span><span class="sxs-lookup"><span data-stu-id="3c437-181">`TasksController` stores tasks in a database where each task has an associated user who "owns" hello task.</span></span> <span data-ttu-id="3c437-182">proprietário de saudação é identificado pelo usuário Olá **ID de objeto**.</span><span class="sxs-lookup"><span data-stu-id="3c437-182">hello owner is identified by hello user's **object ID**.</span></span> <span data-ttu-id="3c437-183">(Isso é porque necessário tooadd Olá ID de objeto como um aplicativo declaração em todas as suas políticas.)</span><span class="sxs-lookup"><span data-stu-id="3c437-183">(This is why you needed tooadd hello object ID as an application claim in all of your policies.)</span></span>

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-hello-permissions-in-hello-token"></a><span data-ttu-id="3c437-184">Validar Olá permissões no token Olá</span><span class="sxs-lookup"><span data-stu-id="3c437-184">Validate hello permissions in hello token</span></span>

<span data-ttu-id="3c437-185">Um requisito comum para APIs da web é toovalidate hello "escopos" presentes no token de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c437-185">A common requirement for web APIs is toovalidate hello "scopes" present in hello token.</span></span> <span data-ttu-id="3c437-186">Isso garante que o usuário Olá consentiu permissões toohello Olá tooaccess necessário serviço da lista de tarefas pendentes.</span><span class="sxs-lookup"><span data-stu-id="3c437-186">This ensures that hello user has consented toohello permissions required tooaccess hello to-do list service.</span></span>

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

## <a name="run-hello-sample-app"></a><span data-ttu-id="3c437-187">Execute o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="3c437-187">Run hello sample app</span></span>

<span data-ttu-id="3c437-188">Por fim, compile e execute `TaskWebApp` e `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="3c437-188">Finally, build and run both `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="3c437-189">Criar algumas tarefas na lista de tarefas do usuário hello e observe como eles são persistentes no hello API mesmo depois que você parar e reiniciar o cliente hello.</span><span class="sxs-lookup"><span data-stu-id="3c437-189">Create some tasks on hello user's to-do list and notice how they are persisted in hello API even after you stop and restart hello client.</span></span>

## <a name="edit-your-policies"></a><span data-ttu-id="3c437-190">Editar suas políticas</span><span class="sxs-lookup"><span data-stu-id="3c437-190">Edit your policies</span></span>

<span data-ttu-id="3c437-191">Depois que você protegeu uma API usando o Azure AD B2C, você pode testar sua política de entrada-em/entrada o e efeitos de saudação do modo de exibição (ou não) em Olá API.</span><span class="sxs-lookup"><span data-stu-id="3c437-191">After you have secured an API by using Azure AD B2C, you can experiment with your Sign-in/Sign-up policy and view hello effects (or lack thereof) on hello API.</span></span> <span data-ttu-id="3c437-192">Você pode manipular as declarações de aplicativo hello nas políticas hello e alterar Olá informações do usuário que estão disponíveis na API da web hello.</span><span class="sxs-lookup"><span data-stu-id="3c437-192">You can manipulate hello application claims in hello policies and change hello user information that is available in hello web API.</span></span> <span data-ttu-id="3c437-193">Quaisquer declarações que você adicionar serão tooyour disponível .NET MVC web API no hello `ClaimsPrincipal` do objeto, conforme descrito anteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="3c437-193">Any claims that you add will be available tooyour .NET MVC web API in hello `ClaimsPrincipal` object, as described earlier in this article.</span></span>
