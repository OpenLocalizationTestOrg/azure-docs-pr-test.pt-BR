---
title: Adicionar entrada a uma API Web do MVC do .NET usando o ponto de extremidade do Azure AD v2.0 | Microsoft Docs
description: "Agora você tem uma API da Web .NET MVC que aceita tokens de contas da Microsoft pessoais, e contas corporativas ou de estudante."
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
ms.openlocfilehash: b2d7bbfcd9218698f71e9dfdb1ad5d9ff8740f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="secure-an-mvc-web-api"></a><span data-ttu-id="81535-103">Proteger uma API Web do MVC</span><span class="sxs-lookup"><span data-stu-id="81535-103">Secure an MVC web API</span></span>
<span data-ttu-id="81535-104">Com o ponto de extremidade v2.0 do Azure Active Directory, você pode proteger uma API Web usando tokens de acesso [OAuth 2.0](active-directory-v2-protocols.md) , permitindo que usuários com contas pessoais, corporativas ou de estudante da Microsoft acessem sua API Web com segurança.</span><span class="sxs-lookup"><span data-stu-id="81535-104">With Azure Active Directory the v2.0 endpoint, you can protect a Web API using [OAuth 2.0](active-directory-v2-protocols.md) access tokens, enabling users with both personal Microsoft account and work or school accounts to securely access your Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="81535-105">Nem todos os recursos e cenários do Azure Active Directory têm suporte no ponto de extremidade v2.0.</span><span class="sxs-lookup"><span data-stu-id="81535-105">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="81535-106">Para determinar se você deve usar o ponto de extremidade v2.0, leia sobre as [limitações da v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="81535-106">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

<span data-ttu-id="81535-107">Em APIs da Web ASP.NET, você pode conseguir isso usando o middleware OWIN da Microsoft, incluso no .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="81535-107">In ASP.NET web APIs, you can accomplish this using Microsoft’s OWIN middleware included in .NET Framework 4.5.</span></span>  <span data-ttu-id="81535-108">Usaremos aqui o OWIN para compilar uma API Web MVC de "Lista de Tarefas" que permite aos clientes criar e ler tarefas da lista de tarefas pendentes do usuário.</span><span class="sxs-lookup"><span data-stu-id="81535-108">Here we’ll use OWIN to build a "To Do List" MVC Web API that allows clients to create and read tasks from a user's To-Do list.</span></span>  <span data-ttu-id="81535-109">A API Web validará se as solicitações de entrada contém um token de acesso válido e rejeitará as solicitações não aprovadas na validação em uma rota protegida.</span><span class="sxs-lookup"><span data-stu-id="81535-109">The web API will validate that incoming requests contain a valid access token and reject any requests that do not pass validation on a protected route.</span></span>  <span data-ttu-id="81535-110">Este exemplo foi criado usando o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="81535-110">This sample was built using Visual Studio 2015.</span></span>

## <a name="download"></a><span data-ttu-id="81535-111">Baixar</span><span class="sxs-lookup"><span data-stu-id="81535-111">Download</span></span>
<span data-ttu-id="81535-112">O código para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span><span class="sxs-lookup"><span data-stu-id="81535-112">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span></span>  <span data-ttu-id="81535-113">Para acompanhar, você pode [baixar o esqueleto do aplicativo como um .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) ou clonar o esqueleto:</span><span class="sxs-lookup"><span data-stu-id="81535-113">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

<span data-ttu-id="81535-114">O aplicativo de esqueleto inclui todo o código clichê de uma API simples, porém estão faltando todas as partes relacionadas à identidade.</span><span class="sxs-lookup"><span data-stu-id="81535-114">The skeleton app includes all the boilerplate code for a simple API, but is missing all of the identity-related pieces.</span></span> <span data-ttu-id="81535-115">Se você não quiser acompanhar, clone ou [baixe o exemplo completo](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="81535-115">If you don't want to follow along, you can instead clone or [download the completed sample](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span></span>

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="81535-116">Registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="81535-116">Register an app</span></span>
<span data-ttu-id="81535-117">Crie um novo aplicativo em [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ou siga estas [etapas detalhadas](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="81535-117">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="81535-118">Não se esqueça de:</span><span class="sxs-lookup"><span data-stu-id="81535-118">Make sure to:</span></span>

* <span data-ttu-id="81535-119">Copiar a **ID do Aplicativo** designada ao seu aplicativo, você precisará dela logo.</span><span class="sxs-lookup"><span data-stu-id="81535-119">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>

<span data-ttu-id="81535-120">Essa solução do Visual Studio também contém um "TodoListClient”, que é um aplicativo WPF simples.</span><span class="sxs-lookup"><span data-stu-id="81535-120">This visual studio solution also contains a "TodoListClient", which is a simple WPF app.</span></span>  <span data-ttu-id="81535-121">O TodoListClient é usado para demonstrar como um usuário se conecta e como um cliente pode emitir solicitações para sua API Web.</span><span class="sxs-lookup"><span data-stu-id="81535-121">The TodoListClient is used to demonstrate how a user signs-in and how a client can issue requests to your Web API.</span></span>  <span data-ttu-id="81535-122">Nesse caso, tanto o TodoListClient como TodoListService são representados pelo mesmo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="81535-122">In this case, both the TodoListClient and the TodoListService are represented by the same app.</span></span>  <span data-ttu-id="81535-123">Para configurar o TodoListClient, você deverá também:</span><span class="sxs-lookup"><span data-stu-id="81535-123">To configure the TodoListClient, you should also:</span></span>

* <span data-ttu-id="81535-124">Adicione a plataforma **Móvel** de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="81535-124">Add the **Mobile** platform for your app.</span></span>

## <a name="install-owin"></a><span data-ttu-id="81535-125">Instalar a OWIN</span><span class="sxs-lookup"><span data-stu-id="81535-125">Install OWIN</span></span>
<span data-ttu-id="81535-126">Agora que você registrou um aplicativo, é preciso configurar seu aplicativo para se comunicar com o ponto de extremidade v2.0 para validar tokens e solicitações recebidos.</span><span class="sxs-lookup"><span data-stu-id="81535-126">Now that you’ve registered an app, you need to set up your app to communicate with the v2.0 endpoint in order to validate incoming requests & tokens.</span></span>

* <span data-ttu-id="81535-127">Para começar, abra a solução e adicione os pacotes do NuGet de middleware OWIN ao projeto TodoListService usando o Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="81535-127">To begin, open the solution and add the OWIN middleware NuGet packages to the TodoListService project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a><span data-ttu-id="81535-128">Configurar a autenticação OAuth</span><span class="sxs-lookup"><span data-stu-id="81535-128">Configure OAuth authentication</span></span>
* <span data-ttu-id="81535-129">Adicionar uma classe de inicialização OWIN no projeto TodoListService chamado `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="81535-129">Add an OWIN Startup class to the TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="81535-130">Clique com o botão direito do mouse no projeto --> **Adicionar** --> **Novo item** --> pesquise por "OWIN".</span><span class="sxs-lookup"><span data-stu-id="81535-130">Right click on the project --> **Add** --> **New Item** --> Search for “OWIN”.</span></span>  <span data-ttu-id="81535-131">O middleware OWIN invocará o método `Configuration(…)` quando seu aplicativo for iniciado.</span><span class="sxs-lookup"><span data-stu-id="81535-131">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>
* <span data-ttu-id="81535-132">Altere a declaração de classe para `public partial class Startup`; já implementamos parte dessa classe para você em outro arquivo.</span><span class="sxs-lookup"><span data-stu-id="81535-132">Change the class declaration to `public partial class Startup` - we’ve already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="81535-133">No método `Configuration(…)`, faça uma chamada para ConfgureAuth(...) para configurar a autenticação para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="81535-133">In the `Configuration(…)` method, make a call to ConfgureAuth(…) to set up authentication for your web app.</span></span>

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* <span data-ttu-id="81535-134">Abra o arquivo `App_Start\Startup.Auth.cs` e implemente o método `ConfigureAuth(…)`, que vai configurar a API da Web para aceitar tokens do ponto de extremidade v2.0.</span><span class="sxs-lookup"><span data-stu-id="81535-134">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(…)` method, which will set up the Web API to accept tokens from the v2.0 endpoint.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, the TodoListClient and TodoListService
                // are represented using the same Application Id - we use
                // the Application Id to represent the audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that the user's organization (if applicable) has
                // signed up for the app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up the OWIN pipeline to use OAuth 2.0 Bearer authentication.
        // The options provided here tell the middleware about the type of tokens
        // that will be recieved, which are JWTs for the v2.0 endpoint.

        // NOTE: The usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by the v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used to fetch & use the OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* <span data-ttu-id="81535-135">Agora você pode usar `[Authorize]` atributos para proteger os controladores e ações com a autenticação de portador OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="81535-135">Now you can use `[Authorize]` attributes to protect your controllers and actions with OAuth 2.0 bearer authentication.</span></span>  <span data-ttu-id="81535-136">Decore a classe `Controllers\TodoListController.cs` com uma marca de autorização.</span><span class="sxs-lookup"><span data-stu-id="81535-136">Decorate the `Controllers\TodoListController.cs` class with an authorize tag.</span></span>  <span data-ttu-id="81535-137">Isso forçará o usuário a entrar antes de acessar essa página.</span><span class="sxs-lookup"><span data-stu-id="81535-137">This will force the user to sign in before accessing that page.</span></span>

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* <span data-ttu-id="81535-138">Quando um chamador autorizado invoca com êxito uma das `TodoListController` APIs, a ação pode precisar ter acesso às informações sobre o chamador.</span><span class="sxs-lookup"><span data-stu-id="81535-138">When an authorized caller successfully invokes one of the `TodoListController` APIs, the action might need access to information about the caller.</span></span>  <span data-ttu-id="81535-139">O OWIN fornece acesso às declarações dentro do token de portador por meio do objeto `ClaimsPrincpal` .</span><span class="sxs-lookup"><span data-stu-id="81535-139">OWIN provides access to the claims inside the bearer token via the `ClaimsPrincpal` object.</span></span>  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use the ClaimsPrincipal to access information about the
    // user making the call.  In this case, we use the 'sub' or
    // NameIdentifier claim to serve as a key for the tasks in the data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* <span data-ttu-id="81535-140">Por fim, abra o arquivo `web.config` na raiz do projeto TodoListService e insira os valores de configuração na seção `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="81535-140">Finally, open the `web.config` file in the root of the TodoListService project, and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="81535-141">Seu `ida:Audience` é a **ID do Aplicativo** do aplicativo que você inseriu no portal.</span><span class="sxs-lookup"><span data-stu-id="81535-141">Your `ida:Audience` is the **Application Id** of the app that you entered in the portal.</span></span>

## <a name="configure-the-client-app"></a><span data-ttu-id="81535-142">Configurar o aplicativo do cliente</span><span class="sxs-lookup"><span data-stu-id="81535-142">Configure the client app</span></span>
<span data-ttu-id="81535-143">Antes que você possa ver o Serviço de Lista de Tarefas em ação, você precisa configurar o Cliente de Lista de Tarefas para poder obter tokens do ponto de extremidade v2.0 e fazer chamadas para o serviço.</span><span class="sxs-lookup"><span data-stu-id="81535-143">Before you can see the Todo List Service in action, you need to configure the Todo List Client so it can get tokens from the v2.0 endpoint and make calls to the service.</span></span>

* <span data-ttu-id="81535-144">No projeto TodoListClient, abra `App.config` e insira seus valores de configuração na seção `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="81535-144">In the TodoListClient project, open `App.config` and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="81535-145">Sua ID do Aplicativo `ida:ClientId` que você copiou do portal.</span><span class="sxs-lookup"><span data-stu-id="81535-145">Your `ida:ClientId` Application Id you copied from the portal.</span></span>

<span data-ttu-id="81535-146">Por fim, limpe, compile e execute cada projeto!</span><span class="sxs-lookup"><span data-stu-id="81535-146">Finally, clean, build and run each project!</span></span>  <span data-ttu-id="81535-147">Agora você tem uma API da Web .NET MVC que aceita tokens de contas da Microsoft pessoais e contas corporativas ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="81535-147">You now have a .NET MVC Web API that accepts tokens from both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="81535-148">Entre na TodoListClient e chame sua API da Web para adicionar tarefas à Lista de Tarefas do usuário.</span><span class="sxs-lookup"><span data-stu-id="81535-148">Sign into the TodoListClient, and call your web api to add tasks to the user's To-Do list.</span></span>

<span data-ttu-id="81535-149">Para referência, o exemplo concluído (sem os valores de configuração) [é fornecido como um .zip aqui](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), ou você pode cloná-lo do GitHub:</span><span class="sxs-lookup"><span data-stu-id="81535-149">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="81535-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="81535-150">Next steps</span></span>
<span data-ttu-id="81535-151">Agora você pode passar para tópicos adicionais.</span><span class="sxs-lookup"><span data-stu-id="81535-151">You can now move onto additional topics.</span></span>  <span data-ttu-id="81535-152">Você pode desejar experimentar:</span><span class="sxs-lookup"><span data-stu-id="81535-152">You may want to try:</span></span>

[<span data-ttu-id="81535-153">Chamar uma API Web em um aplicativo Web >></span><span class="sxs-lookup"><span data-stu-id="81535-153">Calling a Web API from a Web App >></span></span>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

<span data-ttu-id="81535-154">Para obter recursos adicionais, consulte:</span><span class="sxs-lookup"><span data-stu-id="81535-154">For additional resources, check out:</span></span>

* [<span data-ttu-id="81535-155">Guia do desenvolvedor do v2.0 >></span><span class="sxs-lookup"><span data-stu-id="81535-155">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="81535-156">Marca “azure-active-directory” do StackOverflow >></span><span class="sxs-lookup"><span data-stu-id="81535-156">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="81535-157">Obter atualizações de segurança para nossos produtos</span><span class="sxs-lookup"><span data-stu-id="81535-157">Get security updates for our products</span></span>
<span data-ttu-id="81535-158">Recomendamos que você obtenha notificações sobre a ocorrência de incidentes de segurança visitando [esta página](https://technet.microsoft.com/security/dd252948) e assinando os alertas do Security Advisory.</span><span class="sxs-lookup"><span data-stu-id="81535-158">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>
