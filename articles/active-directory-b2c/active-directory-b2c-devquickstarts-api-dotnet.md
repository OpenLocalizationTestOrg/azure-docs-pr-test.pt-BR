---
title: Azure AD B2C | Microsoft Docs
description: "Como compilar uma API Web do .NET usando o Azure Active Directory B2C, protegido com tokens de acesso OAuth 2.0 para autenticação."
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
ms.openlocfilehash: 48749bfa2ab54a0e766a4aad4f39073cc4e90818
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a><span data-ttu-id="ed34f-103">Azure Active Directory B2C: criar uma API Web do .NET</span><span class="sxs-lookup"><span data-stu-id="ed34f-103">Azure Active Directory B2C: Build a .NET web API</span></span>

<span data-ttu-id="ed34f-104">Com o Active Directory B2C do Azure (AD do Azure), você pode proteger uma API Web usando tokens de acesso do OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="ed34f-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="ed34f-105">Esses tokens permitem que os aplicativos cliente se autentiquem na API.</span><span class="sxs-lookup"><span data-stu-id="ed34f-105">These tokens allow your client apps to authenticate to the API.</span></span> <span data-ttu-id="ed34f-106">Este artigo mostra como criar uma API de "lista de tarefas pendentes" MVC .NET que permite que os usuários do aplicativo cliente executem CRUD para as tarefas.</span><span class="sxs-lookup"><span data-stu-id="ed34f-106">This article shows you how to create a .NET MVC "to-do list" API that allows users of your client application to CRUD tasks.</span></span> <span data-ttu-id="ed34f-107">A API Web é protegida usando o Azure AD B2C e permite que apenas usuários autenticados gerenciem sua lista de tarefas pendentes.</span><span class="sxs-lookup"><span data-stu-id="ed34f-107">The web API is secured using Azure AD B2C and only allows authenticated users to manage their to-do list.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="ed34f-108">Criar um diretório do AD B2C do Azure</span><span class="sxs-lookup"><span data-stu-id="ed34f-108">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="ed34f-109">Antes de usar AD B2C do Azure, você deve criar um diretório ou locatário.</span><span class="sxs-lookup"><span data-stu-id="ed34f-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="ed34f-110">Um diretório é um contêiner para todos os seus usuários, aplicativos, grupos etc.</span><span class="sxs-lookup"><span data-stu-id="ed34f-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="ed34f-111">Se você ainda não tiver um, [crie um diretório B2C](active-directory-b2c-get-started.md) antes de prosseguir neste guia.</span><span class="sxs-lookup"><span data-stu-id="ed34f-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

> [!NOTE]
> <span data-ttu-id="ed34f-112">O aplicativo cliente e a API Web devem usar o mesmo diretório do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ed34f-112">The client application and web API must use the same Azure AD B2C directory.</span></span>
>

## <a name="create-a-web-api"></a><span data-ttu-id="ed34f-113">Criar uma API da Web</span><span class="sxs-lookup"><span data-stu-id="ed34f-113">Create a web API</span></span>

<span data-ttu-id="ed34f-114">Em seguida, você precisa criar um aplicativo de API Web no diretório B2C.</span><span class="sxs-lookup"><span data-stu-id="ed34f-114">Next, you need to create a web API app in your B2C directory.</span></span> <span data-ttu-id="ed34f-115">Isso fornece ao AD do Azure as informações de que ele precisa para se comunicar de forma segura com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ed34f-115">This gives Azure AD information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="ed34f-116">Para criar um aplicativo, [siga estas instruções](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="ed34f-116">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="ed34f-117">É necessário que você:</span><span class="sxs-lookup"><span data-stu-id="ed34f-117">Be sure to:</span></span>

* <span data-ttu-id="ed34f-118">Inclua um **aplicativo Web** ou uma **API Web** no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ed34f-118">Include a **web app** or **web API** in the application.</span></span>
* <span data-ttu-id="ed34f-119">Use o **URI de redirecionamento** `https://localhost:44332/` para o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="ed34f-119">Use the **Redirect URI** `https://localhost:44332/` for the web app.</span></span> <span data-ttu-id="ed34f-120">Esse é o local padrão do aplicativo Web cliente para este exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="ed34f-120">This is the default location of the web app client for this code sample.</span></span>
* <span data-ttu-id="ed34f-121">Copie a **ID de aplicativo** atribuída ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ed34f-121">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="ed34f-122">Você precisará dela mais tarde.</span><span class="sxs-lookup"><span data-stu-id="ed34f-122">You'll need it later.</span></span>
* <span data-ttu-id="ed34f-123">Insira um identificador de aplicativo em **URI da ID do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="ed34f-123">Enter an app identifier into **App ID URI**.</span></span>
* <span data-ttu-id="ed34f-124">Adicione permissões por meio do menu **Escopos publicados**.</span><span class="sxs-lookup"><span data-stu-id="ed34f-124">Add permissions through the **Published scopes** menu.</span></span>

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="ed34f-125">Criar suas políticas</span><span class="sxs-lookup"><span data-stu-id="ed34f-125">Create your policies</span></span>

<span data-ttu-id="ed34f-126">No AD B2C do Azure, cada experiência do usuário é definida por uma [política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="ed34f-126">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="ed34f-127">Você precisará criar uma política para se comunicar com o Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ed34f-127">You will need to create a policy to communicate with Azure AD B2C.</span></span> <span data-ttu-id="ed34f-128">É recomendável usar a política combinada de inscrição/entrada, conforme descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="ed34f-128">We recommend using the combined sign-up/sign-in policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="ed34f-129">Ao criar a política, não se esqueça de:</span><span class="sxs-lookup"><span data-stu-id="ed34f-129">When you create your policy, be sure to:</span></span>

* <span data-ttu-id="ed34f-130">Escolher o **Nome de exibição** e outros atributos de inscrição na política.</span><span class="sxs-lookup"><span data-stu-id="ed34f-130">Choose **Display name** and other sign-up attributes in your policy.</span></span>
* <span data-ttu-id="ed34f-131">Escolher as declarações **Nome de exibição** e **ID de objeto** como declarações de aplicativo para cada política.</span><span class="sxs-lookup"><span data-stu-id="ed34f-131">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="ed34f-132">Você pode escolher outras declarações também.</span><span class="sxs-lookup"><span data-stu-id="ed34f-132">You can choose other claims as well.</span></span>
* <span data-ttu-id="ed34f-133">Copie o **Nome** de cada política depois de criá-la.</span><span class="sxs-lookup"><span data-stu-id="ed34f-133">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="ed34f-134">Posteriormente, você precisará do nome da política.</span><span class="sxs-lookup"><span data-stu-id="ed34f-134">You'll need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="ed34f-135">Após criar a política com êxito, você estará pronto para compilar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ed34f-135">After you have successfully created the policy, you're ready to build your app.</span></span>

## <a name="download-the-code"></a><span data-ttu-id="ed34f-136">Baixar o código</span><span class="sxs-lookup"><span data-stu-id="ed34f-136">Download the code</span></span>

<span data-ttu-id="ed34f-137">O código para este tutorial é mantido no [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="ed34f-137">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="ed34f-138">Você pode clonar a amostra executando:</span><span class="sxs-lookup"><span data-stu-id="ed34f-138">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="ed34f-139">Depois de baixar o código de exemplo, abra o arquivo .sln do Visual Studio para começar.</span><span class="sxs-lookup"><span data-stu-id="ed34f-139">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="ed34f-140">Agora, sua solução contém dois projetos: `TaskWebApp` e `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="ed34f-140">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="ed34f-141">`TaskWebApp` é um aplicativo Web de MVC com o qual o usuário interage.</span><span class="sxs-lookup"><span data-stu-id="ed34f-141">`TaskWebApp` is an MVC web application that the user interacts with.</span></span> <span data-ttu-id="ed34f-142">`TaskService` é API Web back-end do aplicativo que armazena a lista de tarefas de cada usuário.</span><span class="sxs-lookup"><span data-stu-id="ed34f-142">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="ed34f-143">Este artigo discutirá apenas o aplicativo `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="ed34f-143">This article will only discuss the `TaskService` application.</span></span> <span data-ttu-id="ed34f-144">Para saber como criar `TaskWebApp` usando o Azure AD B2C, confira [nosso tutorial do aplicativo Web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="ed34f-144">To learn how to build `TaskWebApp` using Azure AD B2C, see [our .NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>

### <a name="update-the-azure-ad-b2c-configuration"></a><span data-ttu-id="ed34f-145">Atualizar a configuração do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="ed34f-145">Update the Azure AD B2C configuration</span></span>

<span data-ttu-id="ed34f-146">O exemplo é configurado para usar as políticas e a ID do cliente da demonstração.</span><span class="sxs-lookup"><span data-stu-id="ed34f-146">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="ed34f-147">Se quiser usar seu próprio locatário, você precisará fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ed34f-147">If you would like to use your own tenant, you will need to do the following:</span></span>

1. <span data-ttu-id="ed34f-148">Abra `web.config` no projeto `TaskService` e substitua os valores de</span><span class="sxs-lookup"><span data-stu-id="ed34f-148">Open `web.config` in the `TaskService` project and replace the values for</span></span>
    * <span data-ttu-id="ed34f-149">`ida:Tenant` pelo nome do locatário</span><span class="sxs-lookup"><span data-stu-id="ed34f-149">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="ed34f-150">`ida:ClientId` com a ID do aplicativo de API da Web</span><span class="sxs-lookup"><span data-stu-id="ed34f-150">`ida:ClientId` with your web API application ID</span></span>
    * <span data-ttu-id="ed34f-151">`ida:SignUpSignInPolicyId` pelo nome da política "Inscrever-se ou Entrar"</span><span class="sxs-lookup"><span data-stu-id="ed34f-151">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="ed34f-152">Abra `web.config` no projeto `TaskWebApp` e substitua os valores de</span><span class="sxs-lookup"><span data-stu-id="ed34f-152">Open `web.config` in the `TaskWebApp` project and replace the values for</span></span>
    * <span data-ttu-id="ed34f-153">`ida:Tenant` pelo nome do locatário</span><span class="sxs-lookup"><span data-stu-id="ed34f-153">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="ed34f-154">`ida:ClientId` pela ID de aplicativo do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="ed34f-154">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="ed34f-155">`ida:ClientSecret` pela chave de segredo do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="ed34f-155">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="ed34f-156">`ida:SignUpSignInPolicyId` pelo nome da política "Inscrever-se ou Entrar"</span><span class="sxs-lookup"><span data-stu-id="ed34f-156">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="ed34f-157">`ida:EditProfilePolicyId` pelo nome de política "Editar Perfil"</span><span class="sxs-lookup"><span data-stu-id="ed34f-157">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="ed34f-158">`ida:ResetPasswordPolicyId` com o nome de política "Redefinir Senha"</span><span class="sxs-lookup"><span data-stu-id="ed34f-158">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>


## <a name="secure-the-api"></a><span data-ttu-id="ed34f-159">Proteger a API</span><span class="sxs-lookup"><span data-stu-id="ed34f-159">Secure the API</span></span>

<span data-ttu-id="ed34f-160">Quando tem um cliente que chama a API, você pode proteger a API (por exemplo `TaskService`) usando os tokens de portador OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="ed34f-160">When you have a client that calls your API, you can secure your API (e.g `TaskService`) by using OAuth 2.0 bearer tokens.</span></span> <span data-ttu-id="ed34f-161">Isso garante que cada solicitação à API seja válida apenas se a solicitação tiver um token de portador.</span><span class="sxs-lookup"><span data-stu-id="ed34f-161">This ensures that each request to your API will only be valid if the request has a bearer token.</span></span> <span data-ttu-id="ed34f-162">Sua API pode aceitar e validar tokens de portador usando a biblioteca OWIN (Open Web Interface para .NET) da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ed34f-162">Your API can accept and validate bearer tokens by using Microsoft's Open Web Interface for .NET (OWIN) library.</span></span>

### <a name="install-owin"></a><span data-ttu-id="ed34f-163">Instalar a OWIN</span><span class="sxs-lookup"><span data-stu-id="ed34f-163">Install OWIN</span></span>

<span data-ttu-id="ed34f-164">Comece instalando o pipeline de autenticação OWIN OAuth usando o Visual Studio Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="ed34f-164">Begin by installing the OWIN OAuth authentication pipeline by using the Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

<span data-ttu-id="ed34f-165">Isso instalará o middleware OWIN, que aceitará e validará os tokens de portador.</span><span class="sxs-lookup"><span data-stu-id="ed34f-165">This will install the OWIN middleware that will accept and validate bearer tokens.</span></span>

### <a name="add-an-owin-startup-class"></a><span data-ttu-id="ed34f-166">Adicionar uma classe de inicialização da OWIN</span><span class="sxs-lookup"><span data-stu-id="ed34f-166">Add an OWIN startup class</span></span>

<span data-ttu-id="ed34f-167">Adicione uma classe de inicialização OWIN para a API chamada `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="ed34f-167">Add an OWIN startup class to the API called `Startup.cs`.</span></span>  <span data-ttu-id="ed34f-168">Clique com o botão direito do mouse no projeto, selecione **Adicionar** e **Novo Item** e pesquise OWIN.</span><span class="sxs-lookup"><span data-stu-id="ed34f-168">Right-click on the project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="ed34f-169">O middleware OWIN invocará o método `Configuration(…)` quando seu aplicativo for iniciado.</span><span class="sxs-lookup"><span data-stu-id="ed34f-169">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="ed34f-170">Em nossa amostra, alteramos a declaração de classe para `public partial class Startup` e implementamos a outra parte da classe em `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="ed34f-170">In our sample, we changed the class declaration to `public partial class Startup` and implemented the other part of the class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="ed34f-171">No método `Configuration`, adicionamos uma chamada para `ConfigureAuth`, que é definida em `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="ed34f-171">Inside the `Configuration` method, we added a call to `ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="ed34f-172">Após as modificações, `Startup.cs` é semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="ed34f-172">After the modifications, `Startup.cs` looks like the following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // The OWIN middleware will invoke this method when the app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of the class
        ConfigureAuth(app);
    }
}
```

### <a name="configure-oauth-20-authentication"></a><span data-ttu-id="ed34f-173">Configurar a autenticação OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="ed34f-173">Configure OAuth 2.0 authentication</span></span>

<span data-ttu-id="ed34f-174">Abra o arquivo `App_Start\Startup.Auth.cs` e implemente o método `ConfigureAuth(...)`.</span><span class="sxs-lookup"><span data-stu-id="ed34f-174">Open the file `App_Start\Startup.Auth.cs`, and implement the `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="ed34f-175">Por exemplo, ele pode ser semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="ed34f-175">For example, it could look like the following:</span></span>

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
         * Configure the authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where the audience of the token is equal to the client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches the Azure AD B2C metadata & signing keys from the OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-the-task-controller"></a><span data-ttu-id="ed34f-176">Proteger o controlador de tarefa</span><span class="sxs-lookup"><span data-stu-id="ed34f-176">Secure the task controller</span></span>

<span data-ttu-id="ed34f-177">Após a configuração do aplicativo para usar a autenticação OAuth 2.0, você pode proteger a API Web adicionando uma marca `[Authorize]` ao controlador de tarefa.</span><span class="sxs-lookup"><span data-stu-id="ed34f-177">After the app is configured to use OAuth 2.0 authentication, you can secure your web API by adding an `[Authorize]` tag to the task controller.</span></span> <span data-ttu-id="ed34f-178">Este é o controlador onde ocorre toda a manipulação da lista de tarefas, portanto, proteja todo o controlador no nível da classe.</span><span class="sxs-lookup"><span data-stu-id="ed34f-178">This is the controller where all to-do list manipulation takes place, so you should secure the entire controller at the class level.</span></span> <span data-ttu-id="ed34f-179">Você também pode adicionar a marca `[Authorize]` a ações individuais para obter um controle mais refinado.</span><span class="sxs-lookup"><span data-stu-id="ed34f-179">You can also add the `[Authorize]` tag to individual actions for more fine-grained control.</span></span>

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-the-token"></a><span data-ttu-id="ed34f-180">Obter informações de usuário do token</span><span class="sxs-lookup"><span data-stu-id="ed34f-180">Get user information from the token</span></span>

<span data-ttu-id="ed34f-181">`TasksController` armazena tarefas em um banco de dados, no qual cada tarefa tem um usuário associado que é o "proprietário" da tarefa.</span><span class="sxs-lookup"><span data-stu-id="ed34f-181">`TasksController` stores tasks in a database where each task has an associated user who "owns" the task.</span></span> <span data-ttu-id="ed34f-182">O proprietário é identificado pela **ID de objeto**do usuário.</span><span class="sxs-lookup"><span data-stu-id="ed34f-182">The owner is identified by the user's **object ID**.</span></span> <span data-ttu-id="ed34f-183">(É por isso que você precisa adicionar a ID do objeto como uma declaração de aplicativo em todas as suas políticas.)</span><span class="sxs-lookup"><span data-stu-id="ed34f-183">(This is why you needed to add the object ID as an application claim in all of your policies.)</span></span>

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-the-permissions-in-the-token"></a><span data-ttu-id="ed34f-184">Validar as permissões no token</span><span class="sxs-lookup"><span data-stu-id="ed34f-184">Validate the permissions in the token</span></span>

<span data-ttu-id="ed34f-185">Um requisito comum para APIs Web é validar os “escopos” presentes no token.</span><span class="sxs-lookup"><span data-stu-id="ed34f-185">A common requirement for web APIs is to validate the "scopes" present in the token.</span></span> <span data-ttu-id="ed34f-186">Isso garante que o usuário consentiu em conceder as permissões necessárias para acessar o serviço de lista de tarefas pendentes.</span><span class="sxs-lookup"><span data-stu-id="ed34f-186">This ensures that the user has consented to the permissions required to access the to-do list service.</span></span>

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "The Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-the-sample-app"></a><span data-ttu-id="ed34f-187">Executar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="ed34f-187">Run the sample app</span></span>

<span data-ttu-id="ed34f-188">Por fim, compile e execute `TaskWebApp` e `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="ed34f-188">Finally, build and run both `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="ed34f-189">Crie algumas tarefas na lista de tarefas do usuário e observe como elas são persistentes na API, mesmo depois que você para e reinicia o cliente.</span><span class="sxs-lookup"><span data-stu-id="ed34f-189">Create some tasks on the user's to-do list and notice how they are persisted in the API even after you stop and restart the client.</span></span>

## <a name="edit-your-policies"></a><span data-ttu-id="ed34f-190">Editar suas políticas</span><span class="sxs-lookup"><span data-stu-id="ed34f-190">Edit your policies</span></span>

<span data-ttu-id="ed34f-191">Depois de proteger uma API usando o AD B2C do Azure, experimente a política de Inscrição/Entrada e veja o efeito (ou a falta dele) na API.</span><span class="sxs-lookup"><span data-stu-id="ed34f-191">After you have secured an API by using Azure AD B2C, you can experiment with your Sign-in/Sign-up policy and view the effects (or lack thereof) on the API.</span></span> <span data-ttu-id="ed34f-192">Você pode manipular as declarações do aplicativo nas políticas e alterar as informações do usuário que estão disponíveis na API Web.</span><span class="sxs-lookup"><span data-stu-id="ed34f-192">You can manipulate the application claims in the policies and change the user information that is available in the web API.</span></span> <span data-ttu-id="ed34f-193">Quaisquer declarações que você adicionar estarão disponíveis para a API Web de MVC do .NET no objeto `ClaimsPrincipal` , conforme descrito acima.</span><span class="sxs-lookup"><span data-stu-id="ed34f-193">Any claims that you add will be available to your .NET MVC web API in the `ClaimsPrincipal` object, as described earlier in this article.</span></span>
