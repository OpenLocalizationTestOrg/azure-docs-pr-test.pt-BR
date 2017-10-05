---
title: "Introdução à API Web .NET do Azure AD | Microsoft Docs"
description: "Como compilar uma API Web do .NET MVC que se integre ao Azure AD para autenticação e autorização."
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
ms.openlocfilehash: f44d75f45073a5d9aa9b1863ed227aba4efcf785
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a><span data-ttu-id="eaf39-103">Proteger uma API Web usando os tokens de portador do Azure AD</span><span class="sxs-lookup"><span data-stu-id="eaf39-103">Help protect a web API by using bearer tokens from Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="eaf39-104">Se você estiver criando um aplicativo que fornece acesso a recursos protegidos, você precisará saber como proteger esses recursos de acessos não garantidos.</span><span class="sxs-lookup"><span data-stu-id="eaf39-104">If you’re building an application that provides access to protected resources, you need to know how to prevent unwarranted access to those resources.</span></span>
<span data-ttu-id="eaf39-105">O Azure AD (Azure Active Directory) faz com que seja simples e direto ajudar a proteger uma API Web usando tokens de acesso de portador do OAuth 2.0 com apenas algumas linhas de código.</span><span class="sxs-lookup"><span data-stu-id="eaf39-105">Azure Active Directory (Azure AD) makes it simple and straightforward to help protect a web API by using OAuth 2.0 bearer access tokens with only a few lines of code.</span></span>

<span data-ttu-id="eaf39-106">Em aplicativos Web ASP.NET, você pode executar essa proteção usando a implementação da Microsoft do middleware OWIN voltado à comunidade, incluído no .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="eaf39-106">In ASP.NET web apps, you can accomplish this protection by using the Microsoft implementation of the community-driven OWIN middleware included in .NET Framework 4.5.</span></span> <span data-ttu-id="eaf39-107">Aqui, você usará o OWIN para compilar uma API Web de “Lista de Tarefas Pendentes” que:</span><span class="sxs-lookup"><span data-stu-id="eaf39-107">Here we’ll use OWIN to build a "To Do List" web API that:</span></span>

* <span data-ttu-id="eaf39-108">Designa quais APIs estão protegidas.</span><span class="sxs-lookup"><span data-stu-id="eaf39-108">Designates which APIs are protected.</span></span>
* <span data-ttu-id="eaf39-109">Valida que as chamadas à API Web contêm um token de acesso válido.</span><span class="sxs-lookup"><span data-stu-id="eaf39-109">Validates that the web API calls contain a valid access token.</span></span>

<span data-ttu-id="eaf39-110">Para criar a API de lista de tarefas pendentes, você precisa primeiro:</span><span class="sxs-lookup"><span data-stu-id="eaf39-110">To build the To Do List API, you first need to:</span></span>

1. <span data-ttu-id="eaf39-111">Registrar um aplicativo com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eaf39-111">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="eaf39-112">Configurar o aplicativo para usar o pipeline de autenticação OWIN.</span><span class="sxs-lookup"><span data-stu-id="eaf39-112">Set up the app to use the OWIN authentication pipeline.</span></span>
3. <span data-ttu-id="eaf39-113">Configurar um aplicativo cliente para chamar a API Web.</span><span class="sxs-lookup"><span data-stu-id="eaf39-113">Configure a client application to call the web API.</span></span>

<span data-ttu-id="eaf39-114">Para começar, [baixe o esqueleto do aplicativo](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) ou [baixe o exemplo concluído](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="eaf39-114">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="eaf39-115">Cada um é uma solução do Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="eaf39-115">Each is a Visual Studio 2013 solution.</span></span> <span data-ttu-id="eaf39-116">Você também precisa de um locatário do Azure AD no qual registrar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eaf39-116">You also need an Azure AD tenant in which to register your application.</span></span> <span data-ttu-id="eaf39-117">Se você ainda não tiver um locatário, [saiba como obter um](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="eaf39-117">If you don't have one already, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="eaf39-118">Etapa 1: registrar um aplicativo com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="eaf39-118">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="eaf39-119">Para proteger seu aplicativo, você primeiro precisará criar um aplicativo em seu locatário e fornecer algumas informações cruciais ao Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eaf39-119">To help secure your application, you first need to create an application in your tenant and provide Azure AD with a few key pieces of information.</span></span>

1. <span data-ttu-id="eaf39-120">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="eaf39-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="eaf39-121">Na barra superior, clique em sua conta.</span><span class="sxs-lookup"><span data-stu-id="eaf39-121">On the top bar, click your account.</span></span> <span data-ttu-id="eaf39-122">Na lista **Diretório**, escolha o locatário do Azure AD no qual você quer registrar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eaf39-122">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>

3. <span data-ttu-id="eaf39-123">Clique em **Mais Serviços** no painel esquerdo e selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="eaf39-123">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="eaf39-124">Clique em **Registros do aplicativo** e, em seguida, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="eaf39-124">Click **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="eaf39-125">Siga os prompts e crie um novo **aplicativo Web e/ou API Web**.</span><span class="sxs-lookup"><span data-stu-id="eaf39-125">Follow the prompts and create a new **Web Application and/or Web API**.</span></span>
  * <span data-ttu-id="eaf39-126">**Nome** descreve seu aplicativo para os usuários.</span><span class="sxs-lookup"><span data-stu-id="eaf39-126">**Name** describes your application to users.</span></span> <span data-ttu-id="eaf39-127">Digite **Serviço de Lista de Tarefas Pendentes**.</span><span class="sxs-lookup"><span data-stu-id="eaf39-127">Enter **To Do List Service**.</span></span>
  * <span data-ttu-id="eaf39-128">O **URI de redirecionamento** é uma combinação de esquema e de cadeia de caracteres que o Azure AD usa para retornar tokens solicitados pelo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eaf39-128">**Redirect Uri** is a scheme and string combination that Azure AD uses to return any tokens that your app has requested.</span></span> <span data-ttu-id="eaf39-129">Digite `https://localhost:44321/` para esse valor.</span><span class="sxs-lookup"><span data-stu-id="eaf39-129">Enter `https://localhost:44321/` for this value.</span></span>

6. <span data-ttu-id="eaf39-130">Na página **Configurações** -> **Propriedades** do aplicativo, atualize o URI da ID do Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eaf39-130">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="eaf39-131">Insira um identificador específico ao locatário.</span><span class="sxs-lookup"><span data-stu-id="eaf39-131">Enter a tenant-specific identifier.</span></span> <span data-ttu-id="eaf39-132">Por exemplo, insira: `https://contoso.onmicrosoft.com/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="eaf39-132">For example, enter `https://contoso.onmicrosoft.com/TodoListService`.</span></span>

7. <span data-ttu-id="eaf39-133">Salve a configuração.</span><span class="sxs-lookup"><span data-stu-id="eaf39-133">Save the configuration.</span></span> <span data-ttu-id="eaf39-134">Deixe o portal aberto, pois você também precisará registrar seu aplicativo cliente em breve.</span><span class="sxs-lookup"><span data-stu-id="eaf39-134">Leave the portal open, because you'll also need to register your client application shortly.</span></span>

## <a name="step-2-set-up-the-app-to-use-the-owin-authentication-pipeline"></a><span data-ttu-id="eaf39-135">Etapa 2: configurar o aplicativo para usar o pipeline de autenticação OWIN</span><span class="sxs-lookup"><span data-stu-id="eaf39-135">Step 2: Set up the app to use the OWIN authentication pipeline</span></span>
<span data-ttu-id="eaf39-136">Para validar tokens e solicitações de entrada, você precisa configurar seu aplicativo para se comunicar com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eaf39-136">To validate incoming requests and tokens, you need to set up your application to communicate with Azure AD.</span></span>

1. <span data-ttu-id="eaf39-137">Para começar, abra a solução e adicione os pacotes do NuGet de middleware OWIN ao projeto TodoListService usando o Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="eaf39-137">To begin, open the solution and add the OWIN middleware NuGet packages to the TodoListService project by using the Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. <span data-ttu-id="eaf39-138">Adicionar uma classe de inicialização OWIN no projeto TodoListService chamado `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="eaf39-138">Add an OWIN Startup class to the TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="eaf39-139">Clique com o botão direito do mouse no projeto, selecione **Adicionar** > **Novo Item** e pesquise por **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="eaf39-139">Right-click the project, select **Add** > **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="eaf39-140">O middleware OWIN invocará o método `Configuration(…)` quando seu aplicativo for iniciado.</span><span class="sxs-lookup"><span data-stu-id="eaf39-140">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

3. <span data-ttu-id="eaf39-141">Altere a declaração de classe para `public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="eaf39-141">Change the class declaration to `public partial class Startup`.</span></span> <span data-ttu-id="eaf39-142">Já implementamos parte dessa classe para você em outro arquivo.</span><span class="sxs-lookup"><span data-stu-id="eaf39-142">We’ve already implemented part of this class for you in another file.</span></span> <span data-ttu-id="eaf39-143">No método `Configuration(…)`, faça uma chamada para `ConfgureAuth(…)` para configurar a autenticação para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="eaf39-143">In the `Configuration(…)` method, make a call to `ConfgureAuth(…)` to set up authentication for your web app.</span></span>

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. <span data-ttu-id="eaf39-144">Abra o arquivo `App_Start\Startup.Auth.cs` e implemente o método `ConfigureAuth(…)`.</span><span class="sxs-lookup"><span data-stu-id="eaf39-144">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(…)` method.</span></span> <span data-ttu-id="eaf39-145">Os parâmetros que você fornecer em `WindowsAzureActiveDirectoryBearerAuthenticationOptions` servirão como coordenadas para seu aplicativo para se comunicar com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eaf39-145">The parameters that you provide in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>

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

5. <span data-ttu-id="eaf39-146">Agora você pode usar atributos `[Authorize]` para proteger os controladores e ações com a autenticação de portador JWT (Token Web JSON).</span><span class="sxs-lookup"><span data-stu-id="eaf39-146">Now you can use `[Authorize]` attributes to help protect your controllers and actions with JSON Web Token (JWT) bearer authentication.</span></span> <span data-ttu-id="eaf39-147">Decore a classe `Controllers\TodoListController.cs` com uma marca de autorização.</span><span class="sxs-lookup"><span data-stu-id="eaf39-147">Decorate the `Controllers\TodoListController.cs` class with an authorize tag.</span></span> <span data-ttu-id="eaf39-148">Isso forçará o usuário a entrar antes de acessar essa página.</span><span class="sxs-lookup"><span data-stu-id="eaf39-148">This will force the user to sign in before accessing that page.</span></span>

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    <span data-ttu-id="eaf39-149">Quando um chamador autorizado invoca com êxito uma das `TodoListController` APIs, a ação pode precisar ter acesso às informações sobre o chamador.</span><span class="sxs-lookup"><span data-stu-id="eaf39-149">When an authorized caller successfully invokes one of the `TodoListController` APIs, the action might need access to information about the caller.</span></span> <span data-ttu-id="eaf39-150">O OWIN fornece acesso às declarações dentro do token de portador por meio do objeto `ClaimsPrincpal` .</span><span class="sxs-lookup"><span data-stu-id="eaf39-150">OWIN provides access to the claims inside the bearer token via the `ClaimsPrincpal` object.</span></span>  

6. <span data-ttu-id="eaf39-151">Um requisito comum para APIs Web é validar os “escopos” presentes no token.</span><span class="sxs-lookup"><span data-stu-id="eaf39-151">A common requirement for web APIs is to validate the "scopes" present in the token.</span></span> <span data-ttu-id="eaf39-152">Isso garante que o usuário consentiu em conceder as permissões necessárias para acessar o serviço de Lista de Tarefas Pendentes.</span><span class="sxs-lookup"><span data-stu-id="eaf39-152">This ensures that the user has consented to the permissions required to access the To Do List Service.</span></span>

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is the default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "The Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. <span data-ttu-id="eaf39-153">Abra o arquivo `web.config` na raiz do projeto TodoListService e insira os valores de configuração na seção `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="eaf39-153">Open the `web.config` file in the root of the TodoListService project, and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="eaf39-154">`ida:Tenant` é o nome do seu locatário do Azure AD – por exemplo, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="eaf39-154">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="eaf39-155">`ida:Audience` é o URI de ID do aplicativo que você inseriu no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf39-155">`ida:Audience` is the App ID URI of the application that you entered in the Azure portal.</span></span>

## <a name="step-3-configure-a-client-application-and-run-the-service"></a><span data-ttu-id="eaf39-156">Etapa 3: Configurar um aplicativo cliente e executar o serviço</span><span class="sxs-lookup"><span data-stu-id="eaf39-156">Step 3: Configure a client application and run the service</span></span>
<span data-ttu-id="eaf39-157">Antes de poder ver o serviço de Lista de Tarefas Pendentes funcionando, você precisa configurar o cliente de Lista de Tarefas Pendentes para que ele possa obter tokens do Azure AD e fazer chamadas para o serviço.</span><span class="sxs-lookup"><span data-stu-id="eaf39-157">Before you can see the To Do List Service in action, you need to configure the To Do List client so it can get tokens from Azure AD and make calls to the service.</span></span>

1. <span data-ttu-id="eaf39-158">Retorne ao [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="eaf39-158">Go back to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="eaf39-159">Crie um novo aplicativo no locatário do AD do Azure e selecione **aplicativo cliente nativo** no prompt resultante.</span><span class="sxs-lookup"><span data-stu-id="eaf39-159">Create a new application in your Azure AD tenant, and select **Native Client Application** in the resulting prompt.</span></span>
  * <span data-ttu-id="eaf39-160">**Nome** descreve seu aplicativo para os usuários.</span><span class="sxs-lookup"><span data-stu-id="eaf39-160">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="eaf39-161">Digite `http://TodoListClient/` para o valor **URI de redirecionamento** .</span><span class="sxs-lookup"><span data-stu-id="eaf39-161">Enter `http://TodoListClient/` for the **Redirect Uri** value.</span></span>

3. <span data-ttu-id="eaf39-162">Depois de concluir o registro, o Azure AD atribui uma identificação exclusiva do aplicativo ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eaf39-162">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span> <span data-ttu-id="eaf39-163">Você precisará desse valor nas próximas etapas, portanto, copie-o da página do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eaf39-163">You’ll need this value in the next steps, so copy it from the application page.</span></span>

4. <span data-ttu-id="eaf39-164">Na página **Configurações**, selecione **Permissões necessárias** e escolha **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="eaf39-164">From the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span> <span data-ttu-id="eaf39-165">Localize e selecione o serviço de Lista de Tarefas Pendentes, adicione a permissão **Acessar TodoListService** em **Permissões Delegadas** e clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="eaf39-165">Locate and select the To Do List Service, add the **Access TodoListService** permission under **Delegated Permissions**, and then click **Done**.</span></span>

5. <span data-ttu-id="eaf39-166">No Visual Studio, abra `App.config` no projeto TodoListClient e insira seus valores de configuração na seção `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="eaf39-166">In Visual Studio, open `App.config` in the TodoListClient project, and then enter your configuration values in the `<appSettings>` section.</span></span>

  * <span data-ttu-id="eaf39-167">`ida:Tenant` é o nome do seu locatário do Azure AD – por exemplo, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="eaf39-167">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="eaf39-168">`ida:ClientId` é a ID do aplicativo que você copiou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf39-168">`ida:ClientId` is the app ID that you copied from the Azure portal.</span></span>
  * <span data-ttu-id="eaf39-169">`todo:TodoListResourceId` é o URI da ID do aplicativo de serviço de Lista de Tarefas Pendentes que você inseriu no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="eaf39-169">`todo:TodoListResourceId` is the App ID URI of the To Do List Service application that you entered in the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eaf39-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eaf39-170">Next steps</span></span>
<span data-ttu-id="eaf39-171">Por fim, limpe, compile e execute cada projeto.</span><span class="sxs-lookup"><span data-stu-id="eaf39-171">Finally, clean, build, and run each project.</span></span> <span data-ttu-id="eaf39-172">Se você ainda não fez isso, agora é o momento de criar um novo usuário em seu locatário com um domínio *.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="eaf39-172">If you haven’t already, now is the time to create a new user in your tenant with a *.onmicrosoft.com domain.</span></span> <span data-ttu-id="eaf39-173">Entre no cliente de lista de tarefas com esse usuário e adicione algumas tarefas na lista de tarefas pendentes do usuário.</span><span class="sxs-lookup"><span data-stu-id="eaf39-173">Sign in to the To Do List client with that user, and add some tasks to the user's to-do list.</span></span>

<span data-ttu-id="eaf39-174">Para referência, a amostra concluída (sem seus valores de configuração) está disponível no [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="eaf39-174">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="eaf39-175">Agora, você pode seguir para cenários de identidade.</span><span class="sxs-lookup"><span data-stu-id="eaf39-175">You can now move on to more identity scenarios.</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
