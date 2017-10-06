---
title: "aaaAzure AD .NET web API Introdução | Microsoft Docs"
description: "Como toobuild uma API da web .NET MVC que se integra com o Azure AD para autenticação e autorização."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 67e74774-1748-43ea-8130-55275a18320f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 91c93e1fe18855f5648076e59e2ccf081eec34bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a><span data-ttu-id="d7b13-103">Proteger uma API Web usando os tokens de portador do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7b13-103">Help protect a web API by using bearer tokens from Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="d7b13-104">Se você estiver criando um aplicativo que fornece acesso a recursos tooprotected, será necessário tooknow como tooprevent injustificada acessar os recursos de toothose.</span><span class="sxs-lookup"><span data-stu-id="d7b13-104">If you’re building an application that provides access tooprotected resources, you need tooknow how tooprevent unwarranted access toothose resources.</span></span>
<span data-ttu-id="d7b13-105">Azure Active Directory (AD do Azure) torna simples e direto toohelp proteger uma API da web usando os tokens de acesso de portador OAuth 2.0 com apenas algumas linhas de código.</span><span class="sxs-lookup"><span data-stu-id="d7b13-105">Azure Active Directory (Azure AD) makes it simple and straightforward toohelp protect a web API by using OAuth 2.0 bearer access tokens with only a few lines of code.</span></span>

<span data-ttu-id="d7b13-106">Em aplicativos da web ASP.NET, você pode realizar essa proteção usando a implementação da Microsoft de saudação do hello dirigida pela comunidade middleware OWIN incluído no .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="d7b13-106">In ASP.NET web apps, you can accomplish this protection by using hello Microsoft implementation of hello community-driven OWIN middleware included in .NET Framework 4.5.</span></span> <span data-ttu-id="d7b13-107">Aqui, usaremos OWIN toobuild uma API da web "tooDo lista" que:</span><span class="sxs-lookup"><span data-stu-id="d7b13-107">Here we’ll use OWIN toobuild a "tooDo List" web API that:</span></span>

* <span data-ttu-id="d7b13-108">Designa quais APIs estão protegidas.</span><span class="sxs-lookup"><span data-stu-id="d7b13-108">Designates which APIs are protected.</span></span>
* <span data-ttu-id="d7b13-109">Valida que Olá chamadas de API da web contém um token de acesso válido.</span><span class="sxs-lookup"><span data-stu-id="d7b13-109">Validates that hello web API calls contain a valid access token.</span></span>

<span data-ttu-id="d7b13-110">saudação de toobuild tooDo API da lista, primeiro você precisa:</span><span class="sxs-lookup"><span data-stu-id="d7b13-110">toobuild hello tooDo List API, you first need to:</span></span>

1. <span data-ttu-id="d7b13-111">Registrar um aplicativo com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7b13-111">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="d7b13-112">Configure o pipeline de autenticação Olá aplicativo toouse Olá OWIN.</span><span class="sxs-lookup"><span data-stu-id="d7b13-112">Set up hello app toouse hello OWIN authentication pipeline.</span></span>
3. <span data-ttu-id="d7b13-113">Configure um cliente aplicativo toocall Olá API da web.</span><span class="sxs-lookup"><span data-stu-id="d7b13-113">Configure a client application toocall hello web API.</span></span>

<span data-ttu-id="d7b13-114">tooget iniciado, [baixar o esqueleto do aplicativo hello](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) ou [baixar exemplo hello concluída](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="d7b13-114">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="d7b13-115">Cada um é uma solução do Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="d7b13-115">Each is a Visual Studio 2013 solution.</span></span> <span data-ttu-id="d7b13-116">Também é necessário um locatário Azure AD no qual tooregister seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d7b13-116">You also need an Azure AD tenant in which tooregister your application.</span></span> <span data-ttu-id="d7b13-117">Se você não tiver uma, [Saiba como tooget uma](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="d7b13-117">If you don't have one already, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="d7b13-118">Etapa 1: registrar um aplicativo com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="d7b13-118">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="d7b13-119">toohelp proteger seu aplicativo, você primeiro precisa toocreate um aplicativo no seu locatário e fornece algumas informações importantes de AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d7b13-119">toohelp secure your application, you first need toocreate an application in your tenant and provide Azure AD with a few key pieces of information.</span></span>

1. <span data-ttu-id="d7b13-120">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d7b13-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="d7b13-121">Na barra superior do hello, clique em sua conta.</span><span class="sxs-lookup"><span data-stu-id="d7b13-121">On hello top bar, click your account.</span></span> <span data-ttu-id="d7b13-122">Em Olá **diretório** , escolha o locatário de saudação do AD do Azure onde deseja tooregister seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d7b13-122">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="d7b13-123">Clique em **mais serviços** Olá painel esquerdo e, em seguida, selecione **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="d7b13-123">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="d7b13-124">Clique em **Registros do aplicativo** e, em seguida, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d7b13-124">Click **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="d7b13-125">Siga os prompts de saudação e criar um novo **aplicativo Web e/ou API da Web**.</span><span class="sxs-lookup"><span data-stu-id="d7b13-125">Follow hello prompts and create a new **Web Application and/or Web API**.</span></span>
  * <span data-ttu-id="d7b13-126">**Nome** descreve toousers seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d7b13-126">**Name** describes your application toousers.</span></span> <span data-ttu-id="d7b13-127">Digite **tooDo lista serviço**.</span><span class="sxs-lookup"><span data-stu-id="d7b13-127">Enter **tooDo List Service**.</span></span>
  * <span data-ttu-id="d7b13-128">**Uri de redirecionamento** é uma combinação de esquema e a cadeia de caracteres que usa o AD do Azure tooreturn qualquer tokens que seu aplicativo tenha solicitado.</span><span class="sxs-lookup"><span data-stu-id="d7b13-128">**Redirect Uri** is a scheme and string combination that Azure AD uses tooreturn any tokens that your app has requested.</span></span> <span data-ttu-id="d7b13-129">Digite `https://localhost:44321/` para esse valor.</span><span class="sxs-lookup"><span data-stu-id="d7b13-129">Enter `https://localhost:44321/` for this value.</span></span>

6. <span data-ttu-id="d7b13-130">De saudação **configurações** -> **propriedades** página para seu aplicativo, Olá URI da ID do aplicativo de atualização.</span><span class="sxs-lookup"><span data-stu-id="d7b13-130">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="d7b13-131">Insira um identificador específico ao locatário.</span><span class="sxs-lookup"><span data-stu-id="d7b13-131">Enter a tenant-specific identifier.</span></span> <span data-ttu-id="d7b13-132">Por exemplo, insira: `https://contoso.onmicrosoft.com/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="d7b13-132">For example, enter `https://contoso.onmicrosoft.com/TodoListService`.</span></span>

7. <span data-ttu-id="d7b13-133">Salve a configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="d7b13-133">Save hello configuration.</span></span> <span data-ttu-id="d7b13-134">Deixe o portal Olá aberto, porque você também precisará tooregister seu aplicativo cliente em breve.</span><span class="sxs-lookup"><span data-stu-id="d7b13-134">Leave hello portal open, because you'll also need tooregister your client application shortly.</span></span>

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a><span data-ttu-id="d7b13-135">Etapa 2: Configurar o pipeline de autenticação Olá aplicativo toouse Olá OWIN</span><span class="sxs-lookup"><span data-stu-id="d7b13-135">Step 2: Set up hello app toouse hello OWIN authentication pipeline</span></span>
<span data-ttu-id="d7b13-136">solicitações de entrada toovalidate e tokens, é necessário tooset backup toocommunicate seu aplicativo com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7b13-136">toovalidate incoming requests and tokens, you need tooset up your application toocommunicate with Azure AD.</span></span>

1. <span data-ttu-id="d7b13-137">toobegin, abra a solução de saudação e adicionar projeto de TodoListService toohello de pacotes NuGet de middleware OWIN de saudação usando Olá Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="d7b13-137">toobegin, open hello solution and add hello OWIN middleware NuGet packages toohello TodoListService project by using hello Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. <span data-ttu-id="d7b13-138">Adicionar um projeto TodoListService do toohello da classe de inicialização OWIN chamado `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="d7b13-138">Add an OWIN Startup class toohello TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="d7b13-139">Projeto de saudação com o botão direito, selecione **adicionar** > **Novo Item**e, em seguida, procure **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="d7b13-139">Right-click hello project, select **Add** > **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="d7b13-140">Olá OWIN middleware invocará Olá `Configuration(…)` método quando seu aplicativo é iniciado.</span><span class="sxs-lookup"><span data-stu-id="d7b13-140">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

3. <span data-ttu-id="d7b13-141">Altere a declaração de classe Olá muito`public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="d7b13-141">Change hello class declaration too`public partial class Startup`.</span></span> <span data-ttu-id="d7b13-142">Já implementamos parte dessa classe para você em outro arquivo.</span><span class="sxs-lookup"><span data-stu-id="d7b13-142">We’ve already implemented part of this class for you in another file.</span></span> <span data-ttu-id="d7b13-143">Em Olá `Configuration(…)` método, fazer uma chamada muito`ConfgureAuth(…)` tooset a autenticação para seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="d7b13-143">In hello `Configuration(…)` method, make a call too`ConfgureAuth(…)` tooset up authentication for your web app.</span></span>

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. <span data-ttu-id="d7b13-144">Arquivo hello abrir `App_Start\Startup.Auth.cs` e implementar Olá `ConfigureAuth(…)` método.</span><span class="sxs-lookup"><span data-stu-id="d7b13-144">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(…)` method.</span></span> <span data-ttu-id="d7b13-145">Olá parâmetros que você fornece em `WindowsAzureActiveDirectoryBearerAuthenticationOptions` servirá como coordenadas para toocommunicate seu aplicativo com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7b13-145">hello parameters that you provide in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>

    ```C#
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
            });
    }
    ```

5. <span data-ttu-id="d7b13-146">Agora você pode usar `[Authorize]` atributos toohelp proteger seus controladores e ações com autenticação do portador do JSON Web Token (JWT).</span><span class="sxs-lookup"><span data-stu-id="d7b13-146">Now you can use `[Authorize]` attributes toohelp protect your controllers and actions with JSON Web Token (JWT) bearer authentication.</span></span> <span data-ttu-id="d7b13-147">Decore Olá `Controllers\TodoListController.cs` classe com uma marca de autorização.</span><span class="sxs-lookup"><span data-stu-id="d7b13-147">Decorate hello `Controllers\TodoListController.cs` class with an authorize tag.</span></span> <span data-ttu-id="d7b13-148">Isso forçará Olá usuário toosign em antes de acessar essa página.</span><span class="sxs-lookup"><span data-stu-id="d7b13-148">This will force hello user toosign in before accessing that page.</span></span>

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    <span data-ttu-id="d7b13-149">Quando um chamador autorizado com êxito invoca uma saudação `TodoListController` APIs, ação Olá pode precisar acessar tooinformation sobre chamador hello.</span><span class="sxs-lookup"><span data-stu-id="d7b13-149">When an authorized caller successfully invokes one of hello `TodoListController` APIs, hello action might need access tooinformation about hello caller.</span></span> <span data-ttu-id="d7b13-150">OWIN fornece acesso toohello declarações no token de portador Olá via Olá `ClaimsPrincpal` objeto.</span><span class="sxs-lookup"><span data-stu-id="d7b13-150">OWIN provides access toohello claims inside hello bearer token via hello `ClaimsPrincpal` object.</span></span>  

6. <span data-ttu-id="d7b13-151">Um requisito comum para APIs da web é toovalidate hello "escopos" presentes no token de saudação.</span><span class="sxs-lookup"><span data-stu-id="d7b13-151">A common requirement for web APIs is toovalidate hello "scopes" present in hello token.</span></span> <span data-ttu-id="d7b13-152">Isso garante que o usuário Olá consentiu toohello permissões tooaccess necessário Olá tooDo serviço da lista.</span><span class="sxs-lookup"><span data-stu-id="d7b13-152">This ensures that hello user has consented toohello permissions required tooaccess hello tooDo List Service.</span></span>

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is hello default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "hello Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. <span data-ttu-id="d7b13-153">Olá abrir `web.config` na raiz de saudação do projeto TodoListService de saudação do arquivo e insira os valores de configuração no hello `<appSettings>` seção.</span><span class="sxs-lookup"><span data-stu-id="d7b13-153">Open hello `web.config` file in hello root of hello TodoListService project, and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="d7b13-154">`ida:Tenant`é o nome de saudação do seu locatário do AD do Azure – por exemplo, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="d7b13-154">`ida:Tenant` is hello name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="d7b13-155">`ida:Audience`é Olá URI de ID de aplicativo do aplicativo hello que você inseriu na Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d7b13-155">`ida:Audience` is hello App ID URI of hello application that you entered in hello Azure portal.</span></span>

## <a name="step-3-configure-a-client-application-and-run-hello-service"></a><span data-ttu-id="d7b13-156">Etapa 3: Configurar um aplicativo cliente e executar o serviço de saudação</span><span class="sxs-lookup"><span data-stu-id="d7b13-156">Step 3: Configure a client application and run hello service</span></span>
<span data-ttu-id="d7b13-157">Antes de poder ver Olá tooDo serviço da lista em ação, você precisa cliente da lista tooconfigure Olá tooDo para que possa obter tokens do AD do Azure e fazer chamadas toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="d7b13-157">Before you can see hello tooDo List Service in action, you need tooconfigure hello tooDo List client so it can get tokens from Azure AD and make calls toohello service.</span></span>

1. <span data-ttu-id="d7b13-158">Voltar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d7b13-158">Go back toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="d7b13-159">Criar um novo aplicativo no seu locatário do AD do Azure e selecione **aplicativo cliente nativo** no prompt de saudação resultante.</span><span class="sxs-lookup"><span data-stu-id="d7b13-159">Create a new application in your Azure AD tenant, and select **Native Client Application** in hello resulting prompt.</span></span>
  * <span data-ttu-id="d7b13-160">**Nome** descreve toousers seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d7b13-160">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="d7b13-161">Digite `http://TodoListClient/` para Olá **Uri de redirecionamento** valor.</span><span class="sxs-lookup"><span data-stu-id="d7b13-161">Enter `http://TodoListClient/` for hello **Redirect Uri** value.</span></span>

3. <span data-ttu-id="d7b13-162">Depois de concluir o registro, o Azure AD atribui a um aplicativo de tooyour de ID de aplicativo único.</span><span class="sxs-lookup"><span data-stu-id="d7b13-162">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span> <span data-ttu-id="d7b13-163">Você precisará desse valor nas etapas da próximas hello, portanto copie-o da página de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d7b13-163">You’ll need this value in hello next steps, so copy it from hello application page.</span></span>

4. <span data-ttu-id="d7b13-164">De saudação **configurações** página, selecione **permissões necessárias**e, em seguida, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d7b13-164">From hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span> <span data-ttu-id="d7b13-165">Localize e selecione Olá tooDo serviço da lista, adicione Olá **acesso TodoListService** permissão em **permissões delegadas**e, em seguida, clique em **feito**.</span><span class="sxs-lookup"><span data-stu-id="d7b13-165">Locate and select hello tooDo List Service, add hello **Access TodoListService** permission under **Delegated Permissions**, and then click **Done**.</span></span>

5. <span data-ttu-id="d7b13-166">No Visual Studio, abra `App.config` Olá TodoListClient projeto e, em seguida, insira os valores de configuração no hello `<appSettings>` seção.</span><span class="sxs-lookup"><span data-stu-id="d7b13-166">In Visual Studio, open `App.config` in hello TodoListClient project, and then enter your configuration values in hello `<appSettings>` section.</span></span>

  * <span data-ttu-id="d7b13-167">`ida:Tenant`é o nome de saudação do seu locatário do AD do Azure – por exemplo, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="d7b13-167">`ida:Tenant` is hello name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="d7b13-168">`ida:ClientId`é a ID do aplicativo hello que você copiou da saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d7b13-168">`ida:ClientId` is hello app ID that you copied from hello Azure portal.</span></span>
  * <span data-ttu-id="d7b13-169">`todo:TodoListResourceId`é hello URI de ID do aplicativo de saudação tooDo aplicativo de serviço de lista que você inseriu na Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d7b13-169">`todo:TodoListResourceId` is hello App ID URI of hello tooDo List Service application that you entered in hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7b13-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d7b13-170">Next steps</span></span>
<span data-ttu-id="d7b13-171">Por fim, limpe, compile e execute cada projeto.</span><span class="sxs-lookup"><span data-stu-id="d7b13-171">Finally, clean, build, and run each project.</span></span> <span data-ttu-id="d7b13-172">Se você ainda não fez isso, agora é Olá tempo toocreate um novo usuário em seu locatário com um *. c o m domínio.</span><span class="sxs-lookup"><span data-stu-id="d7b13-172">If you haven’t already, now is hello time toocreate a new user in your tenant with a *.onmicrosoft.com domain.</span></span> <span data-ttu-id="d7b13-173">Entrar no cliente da lista tooDo toohello com esse usuário e adicionar a lista de tarefas do usuário toohello algumas tarefas.</span><span class="sxs-lookup"><span data-stu-id="d7b13-173">Sign in toohello tooDo List client with that user, and add some tasks toohello user's to-do list.</span></span>

<span data-ttu-id="d7b13-174">Para referência, o exemplo hello concluída (sem os valores de configuração) está disponível em [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="d7b13-174">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="d7b13-175">Agora você pode mover toomore cenários de identidade.</span><span class="sxs-lookup"><span data-stu-id="d7b13-175">You can now move on toomore identity scenarios.</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
