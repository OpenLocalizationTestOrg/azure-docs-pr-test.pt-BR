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
# <a name="secure-an-mvc-web-api"></a><span data-ttu-id="0d971-103">Proteger uma API Web do MVC</span><span class="sxs-lookup"><span data-stu-id="0d971-103">Secure an MVC web API</span></span>
<span data-ttu-id="0d971-104">Com o ponto de extremidade de Active Directory do Azure Olá v 2.0, você pode proteger uma API da Web usando [OAuth 2.0](active-directory-v2-protocols.md) tokens de acesso, permitindo que os usuários com ambas as conta pessoal da Microsoft e contas corporativas ou de estudante toosecurely acessar a API da Web.</span><span class="sxs-lookup"><span data-stu-id="0d971-104">With Azure Active Directory hello v2.0 endpoint, you can protect a Web API using [OAuth 2.0](active-directory-v2-protocols.md) access tokens, enabling users with both personal Microsoft account and work or school accounts toosecurely access your Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="0d971-105">Nem todos os recursos e cenários de Active Directory do Azure têm suporte pelo ponto de extremidade do hello v 2.0.</span><span class="sxs-lookup"><span data-stu-id="0d971-105">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="0d971-106">toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="0d971-106">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

<span data-ttu-id="0d971-107">Em APIs da Web ASP.NET, você pode conseguir isso usando o middleware OWIN da Microsoft, incluso no .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="0d971-107">In ASP.NET web APIs, you can accomplish this using Microsoft’s OWIN middleware included in .NET Framework 4.5.</span></span>  <span data-ttu-id="0d971-108">Aqui vamos usar OWIN toobuild uma API da Web MVC de "tooDo lista" que permite que os clientes toocreate e ler tarefas da lista de tarefas do usuário.</span><span class="sxs-lookup"><span data-stu-id="0d971-108">Here we’ll use OWIN toobuild a "tooDo List" MVC Web API that allows clients toocreate and read tasks from a user's To-Do list.</span></span>  <span data-ttu-id="0d971-109">API da web Hello validará que as solicitações de entrada contém um token de acesso válido e rejeitar todas as solicitações que não passou na validação em uma rota protegida.</span><span class="sxs-lookup"><span data-stu-id="0d971-109">hello web API will validate that incoming requests contain a valid access token and reject any requests that do not pass validation on a protected route.</span></span>  <span data-ttu-id="0d971-110">Este exemplo foi criado usando o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="0d971-110">This sample was built using Visual Studio 2015.</span></span>

## <a name="download"></a><span data-ttu-id="0d971-111">Baixar</span><span class="sxs-lookup"><span data-stu-id="0d971-111">Download</span></span>
<span data-ttu-id="0d971-112">código de saudação para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span><span class="sxs-lookup"><span data-stu-id="0d971-112">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span></span>  <span data-ttu-id="0d971-113">toofollow ao longo, você pode [baixar o esqueleto do aplicativo hello como. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) ou esqueleto de saudação do clone:</span><span class="sxs-lookup"><span data-stu-id="0d971-113">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

<span data-ttu-id="0d971-114">aplicativo de esqueleto Olá inclui todo o código clichê Olá para uma API simples, mas não tem todas as partes relacionadas à identidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="0d971-114">hello skeleton app includes all hello boilerplate code for a simple API, but is missing all of hello identity-related pieces.</span></span> <span data-ttu-id="0d971-115">Se você não quiser toofollow ao longo, em vez disso, você pode clonar ou [baixar exemplo hello concluída](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="0d971-115">If you don't want toofollow along, you can instead clone or [download hello completed sample](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span></span>

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="0d971-116">Registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="0d971-116">Register an app</span></span>
<span data-ttu-id="0d971-117">Crie um novo aplicativo em [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ou siga estas [etapas detalhadas](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="0d971-117">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="0d971-118">Não se esqueça de:</span><span class="sxs-lookup"><span data-stu-id="0d971-118">Make sure to:</span></span>

* <span data-ttu-id="0d971-119">Cópia para baixo Olá **Id do aplicativo** atribuído tooyour aplicativo, você precisará dele em breve.</span><span class="sxs-lookup"><span data-stu-id="0d971-119">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>

<span data-ttu-id="0d971-120">Essa solução do Visual Studio também contém um "TodoListClient”, que é um aplicativo WPF simples.</span><span class="sxs-lookup"><span data-stu-id="0d971-120">This visual studio solution also contains a "TodoListClient", which is a simple WPF app.</span></span>  <span data-ttu-id="0d971-121">Olá TodoListClient é toodemonstrate usado como um usuário entrar e como um cliente pode emitir solicitações tooyour API da Web.</span><span class="sxs-lookup"><span data-stu-id="0d971-121">hello TodoListClient is used toodemonstrate how a user signs-in and how a client can issue requests tooyour Web API.</span></span>  <span data-ttu-id="0d971-122">Nesse caso, a saudação TodoListClient e Olá TodoListService são representados por Olá mesmo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0d971-122">In this case, both hello TodoListClient and hello TodoListService are represented by hello same app.</span></span>  <span data-ttu-id="0d971-123">tooconfigure Olá TodoListClient, você também deve:</span><span class="sxs-lookup"><span data-stu-id="0d971-123">tooconfigure hello TodoListClient, you should also:</span></span>

* <span data-ttu-id="0d971-124">Adicionar Olá **Mobile** plataforma para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0d971-124">Add hello **Mobile** platform for your app.</span></span>

## <a name="install-owin"></a><span data-ttu-id="0d971-125">Instalar a OWIN</span><span class="sxs-lookup"><span data-stu-id="0d971-125">Install OWIN</span></span>
<span data-ttu-id="0d971-126">Agora que você já registrou um aplicativo, você precisa tooset backup toocommunicate seu aplicativo com ponto de extremidade do hello v 2.0 em ordem toovalidate solicitações de entrada e tokens.</span><span class="sxs-lookup"><span data-stu-id="0d971-126">Now that you’ve registered an app, you need tooset up your app toocommunicate with hello v2.0 endpoint in order toovalidate incoming requests & tokens.</span></span>

* <span data-ttu-id="0d971-127">toobegin, abra a solução hello e adicione Olá OWIN middleware NuGet pacotes toohello projeto TodoListService usando Olá Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="0d971-127">toobegin, open hello solution and add hello OWIN middleware NuGet packages toohello TodoListService project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a><span data-ttu-id="0d971-128">Configurar a autenticação OAuth</span><span class="sxs-lookup"><span data-stu-id="0d971-128">Configure OAuth authentication</span></span>
* <span data-ttu-id="0d971-129">Adicionar um projeto TodoListService do toohello da classe de inicialização OWIN chamado `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="0d971-129">Add an OWIN Startup class toohello TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="0d971-130">--> Do botão direito do mouse no projeto de saudação **adicionar** --> **Novo Item** --> procure "OWIN".</span><span class="sxs-lookup"><span data-stu-id="0d971-130">Right click on hello project --> **Add** --> **New Item** --> Search for “OWIN”.</span></span>  <span data-ttu-id="0d971-131">Olá OWIN middleware invocará Olá `Configuration(…)` método quando seu aplicativo é iniciado.</span><span class="sxs-lookup"><span data-stu-id="0d971-131">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>
* <span data-ttu-id="0d971-132">Altere a declaração de classe Olá muito`public partial class Startup` -já implementamos parte dessa classe para você em outro arquivo.</span><span class="sxs-lookup"><span data-stu-id="0d971-132">Change hello class declaration too`public partial class Startup` - we’ve already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="0d971-133">Em Olá `Configuration(…)` método, faça um tooset tooConfgureAuth(...) de chamada de autenticação para seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="0d971-133">In hello `Configuration(…)` method, make a call tooConfgureAuth(…) tooset up authentication for your web app.</span></span>

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* <span data-ttu-id="0d971-134">Arquivo hello abrir `App_Start\Startup.Auth.cs` e implementar Olá `ConfigureAuth(…)` método, que irá configurar tokens de tooaccept de API da Web de saudação do ponto de extremidade do hello v 2.0.</span><span class="sxs-lookup"><span data-stu-id="0d971-134">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(…)` method, which will set up hello Web API tooaccept tokens from hello v2.0 endpoint.</span></span>

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

* <span data-ttu-id="0d971-135">Agora você pode usar `[Authorize]` atributos tooprotect seus controladores e ações com autenticação do portador do OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="0d971-135">Now you can use `[Authorize]` attributes tooprotect your controllers and actions with OAuth 2.0 bearer authentication.</span></span>  <span data-ttu-id="0d971-136">Decore Olá `Controllers\TodoListController.cs` classe com uma marca de autorização.</span><span class="sxs-lookup"><span data-stu-id="0d971-136">Decorate hello `Controllers\TodoListController.cs` class with an authorize tag.</span></span>  <span data-ttu-id="0d971-137">Isso forçará Olá usuário toosign em antes de acessar essa página.</span><span class="sxs-lookup"><span data-stu-id="0d971-137">This will force hello user toosign in before accessing that page.</span></span>

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* <span data-ttu-id="0d971-138">Quando um chamador autorizado com êxito invoca uma saudação `TodoListController` APIs, ação Olá pode precisar acessar tooinformation sobre chamador hello.</span><span class="sxs-lookup"><span data-stu-id="0d971-138">When an authorized caller successfully invokes one of hello `TodoListController` APIs, hello action might need access tooinformation about hello caller.</span></span>  <span data-ttu-id="0d971-139">OWIN fornece acesso toohello declarações no token de portador Olá via Olá `ClaimsPrincpal` objeto.</span><span class="sxs-lookup"><span data-stu-id="0d971-139">OWIN provides access toohello claims inside hello bearer token via hello `ClaimsPrincpal` object.</span></span>  

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

* <span data-ttu-id="0d971-140">Por fim, abra Olá `web.config` na raiz de saudação do projeto TodoListService de saudação do arquivo e insira os valores de configuração no hello `<appSettings>` seção.</span><span class="sxs-lookup"><span data-stu-id="0d971-140">Finally, open hello `web.config` file in hello root of hello TodoListService project, and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="0d971-141">O `ida:Audience` é hello **Id do aplicativo** do aplicativo hello que você inseriu no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="0d971-141">Your `ida:Audience` is hello **Application Id** of hello app that you entered in hello portal.</span></span>

## <a name="configure-hello-client-app"></a><span data-ttu-id="0d971-142">Configurar o aplicativo de cliente Olá</span><span class="sxs-lookup"><span data-stu-id="0d971-142">Configure hello client app</span></span>
<span data-ttu-id="0d971-143">Antes de poder ver Olá serviço de lista de tarefas em ação, você precisa tooconfigure Olá cliente da lista de tarefas para que possa obter tokens do ponto de extremidade do hello v 2.0 e fazer chamadas toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="0d971-143">Before you can see hello Todo List Service in action, you need tooconfigure hello Todo List Client so it can get tokens from hello v2.0 endpoint and make calls toohello service.</span></span>

* <span data-ttu-id="0d971-144">No projeto de TodoListClient hello, abra `App.config` e insira os valores de configuração no hello `<appSettings>` seção.</span><span class="sxs-lookup"><span data-stu-id="0d971-144">In hello TodoListClient project, open `App.config` and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="0d971-145">O `ida:ClientId` é copiada do portal de saudação de Id do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0d971-145">Your `ida:ClientId` Application Id you copied from hello portal.</span></span>

<span data-ttu-id="0d971-146">Por fim, limpe, compile e execute cada projeto!</span><span class="sxs-lookup"><span data-stu-id="0d971-146">Finally, clean, build and run each project!</span></span>  <span data-ttu-id="0d971-147">Agora você tem uma API da Web .NET MVC que aceita tokens de contas da Microsoft pessoais e contas corporativas ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="0d971-147">You now have a .NET MVC Web API that accepts tokens from both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="0d971-148">Entrar Olá TodoListClient e chamar a lista de tarefas de web api tooadd tarefas toohello do usuário.</span><span class="sxs-lookup"><span data-stu-id="0d971-148">Sign into hello TodoListClient, and call your web api tooadd tasks toohello user's To-Do list.</span></span>

<span data-ttu-id="0d971-149">Para referência, Olá concluída exemplo (sem os valores de configuração) [é fornecido como. zip aqui](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), ou você pode cloná-lo do GitHub:</span><span class="sxs-lookup"><span data-stu-id="0d971-149">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="0d971-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0d971-150">Next steps</span></span>
<span data-ttu-id="0d971-151">Agora você pode passar para tópicos adicionais.</span><span class="sxs-lookup"><span data-stu-id="0d971-151">You can now move onto additional topics.</span></span>  <span data-ttu-id="0d971-152">Você pode desejar tootry:</span><span class="sxs-lookup"><span data-stu-id="0d971-152">You may want tootry:</span></span>

[<span data-ttu-id="0d971-153">Chamar uma API Web em um aplicativo Web >></span><span class="sxs-lookup"><span data-stu-id="0d971-153">Calling a Web API from a Web App >></span></span>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

<span data-ttu-id="0d971-154">Para obter recursos adicionais, consulte:</span><span class="sxs-lookup"><span data-stu-id="0d971-154">For additional resources, check out:</span></span>

* [<span data-ttu-id="0d971-155">Guia do desenvolvedor v 2.0 Olá >></span><span class="sxs-lookup"><span data-stu-id="0d971-155">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="0d971-156">Marca “azure-active-directory” do StackOverflow >></span><span class="sxs-lookup"><span data-stu-id="0d971-156">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="0d971-157">Obter atualizações de segurança para nossos produtos</span><span class="sxs-lookup"><span data-stu-id="0d971-157">Get security updates for our products</span></span>
<span data-ttu-id="0d971-158">Recomendamos que você tooget as notificações quando os incidentes de segurança ocorrem visitando [essa página](https://technet.microsoft.com/security/dd252948) e assinando tooSecurity alertas de aviso.</span><span class="sxs-lookup"><span data-stu-id="0d971-158">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>
