---
title: v 2.0 do Active Directory aaaAzure aplicativo nativo do .NET | Microsoft Docs
description: "Como toobuild um aplicativo nativo do .NET que assina os usuários com ambos os Account pessoal da Microsoft e contas corporativa ou escolar."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 46d81e09-bad0-44ce-9026-881805976e72
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/30/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 9418eeba02b800feee5cb00219574eb16506f0a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-windows-desktop-app"></a><span data-ttu-id="22466-103">Adicionar entrada tooa aplicativo de área de trabalho do Windows</span><span class="sxs-lookup"><span data-stu-id="22466-103">Add sign-in tooa Windows Desktop app</span></span>
<span data-ttu-id="22466-104">Com o ponto de extremidade de Olá Olá v 2.0, você pode adicionar rapidamente aplicativos de área de trabalho tooyour autenticação com suporte para ambas as contas Microsoft pessoais e contas corporativa ou escolar.</span><span class="sxs-lookup"><span data-stu-id="22466-104">With hello hello v2.0 endpoint, you can quickly add authentication tooyour desktop apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="22466-105">Ele também permite que seu aplicativo toosecurely se comunicar com um back-end da web api, bem como [Olá Microsoft Graph](https://graph.microsoft.io) e alguns Olá [Unified APIs do Office 365](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span><span class="sxs-lookup"><span data-stu-id="22466-105">It also enables your app toosecurely communicate with a backend web api, as well as [hello Microsoft Graph](https://graph.microsoft.io) and a few of hello [Office 365 Unified APIs](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span></span>

> [!NOTE]
> <span data-ttu-id="22466-106">Nem todos os recursos e cenários do Azure AD (Active Directory) têm suporte pelo ponto de extremidade do hello v 2.0.</span><span class="sxs-lookup"><span data-stu-id="22466-106">Not all Azure Active Directory (AD) scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="22466-107">toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="22466-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="22466-108">Para [.NET aplicativos nativos que são executados em um dispositivo](active-directory-v2-flows.md#mobile-and-native-apps), o AD do Azure fornece Olá biblioteca de autenticação de identidade do Microsoft ou MSAL.</span><span class="sxs-lookup"><span data-stu-id="22466-108">For [.NET native apps that run on a device](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD provides hello Microsoft Identity Authentication Library, or MSAL.</span></span>  <span data-ttu-id="22466-109">Única finalidade do MSAL é toomake fácil para seu aplicativo tooget tokens para chamar serviços da web.</span><span class="sxs-lookup"><span data-stu-id="22466-109">MSAL's sole purpose in life is toomake it easy for your app tooget tokens for calling web services.</span></span>  <span data-ttu-id="22466-110">toodemonstrate facilidade é, aqui, criaremos um aplicativo de lista de tarefas do .NET WPF que:</span><span class="sxs-lookup"><span data-stu-id="22466-110">toodemonstrate just how easy it is, here we'll build a .NET WPF To-Do List app that:</span></span>

* <span data-ttu-id="22466-111">Sinais Olá usuário no & obtém acesso tokens usando Olá [protocolo de autenticação OAuth 2.0](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="22466-111">Signs hello user in & gets access tokens using hello [OAuth 2.0 authentication protocol](active-directory-v2-protocols.md).</span></span>
* <span data-ttu-id="22466-112">Chama com segurança um serviço da Web de Lista de Tarefas back-end, que também é protegido pelo OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="22466-112">Securely calls a backend To-Do List web service, which is also secured by OAuth 2.0.</span></span>
* <span data-ttu-id="22466-113">Usuário de saudação sinais out.</span><span class="sxs-lookup"><span data-stu-id="22466-113">Signs hello user out.</span></span>

## <a name="download-sample-code"></a><span data-ttu-id="22466-114">Baixar código de exemplo</span><span class="sxs-lookup"><span data-stu-id="22466-114">Download sample code</span></span>
<span data-ttu-id="22466-115">código de saudação para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="22466-115">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span></span>  <span data-ttu-id="22466-116">toofollow ao longo, você pode [baixar o esqueleto do aplicativo hello como. zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) ou esqueleto de saudação do clone:</span><span class="sxs-lookup"><span data-stu-id="22466-116">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

<span data-ttu-id="22466-117">aplicativo Hello concluída é fornecido no final da saudação deste tutorial também.</span><span class="sxs-lookup"><span data-stu-id="22466-117">hello completed app is provided at hello end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="22466-118">Registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="22466-118">Register an app</span></span>
<span data-ttu-id="22466-119">Crie um novo aplicativo em [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ou siga estas [etapas detalhadas](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="22466-119">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="22466-120">Não se esqueça de:</span><span class="sxs-lookup"><span data-stu-id="22466-120">Make sure to:</span></span>

* <span data-ttu-id="22466-121">Cópia para baixo Olá **Id do aplicativo** atribuído tooyour aplicativo, você precisará dele em breve.</span><span class="sxs-lookup"><span data-stu-id="22466-121">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="22466-122">Adicionar Olá **Mobile** plataforma para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="22466-122">Add hello **Mobile** platform for your app.</span></span>

## <a name="install--configure-msal"></a><span data-ttu-id="22466-123">Instalar e Configurar o MSAL</span><span class="sxs-lookup"><span data-stu-id="22466-123">Install & Configure MSAL</span></span>
<span data-ttu-id="22466-124">Agora que você tem um aplicativo registrado na Microsoft, pode instalar o MSAL e gravar seu código relacionado à identidade.</span><span class="sxs-lookup"><span data-stu-id="22466-124">Now that you have an app registered with Microsoft, you can install MSAL and write your identity-related code.</span></span>  <span data-ttu-id="22466-125">Ponto de extremidade do MSAL toobe toocommunicate capaz de saudação v 2.0, é necessário tooprovide-lo com algumas informações sobre o registro do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="22466-125">In order for MSAL toobe able toocommunicate hello v2.0 endpoint, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="22466-126">Comece adicionando MSAL toohello TodoListClient projeto usando Olá Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="22466-126">Begin by adding MSAL toohello TodoListClient project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* <span data-ttu-id="22466-127">No projeto de TodoListClient hello, abra `app.config`.</span><span class="sxs-lookup"><span data-stu-id="22466-127">In hello TodoListClient project, open `app.config`.</span></span>  <span data-ttu-id="22466-128">Substituir valores de saudação de elementos Olá Olá `<appSettings>` Olá de tooreflect seção valores entrada no portal de registro de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="22466-128">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values you input into hello app registration portal.</span></span>  <span data-ttu-id="22466-129">Seu código fará referência a esses valores sempre que ele usar a MSAL.</span><span class="sxs-lookup"><span data-stu-id="22466-129">Your code will reference these values whenever it uses MSAL.</span></span>
  
  * <span data-ttu-id="22466-130">Olá `ida:ClientId` é hello **Id do aplicativo** do seu aplicativo é copiada do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="22466-130">hello `ida:ClientId` is hello **Application Id** of your app you copied from hello portal.</span></span>
* <span data-ttu-id="22466-131">No hello serviço TodoList projeto, abra `web.config` na raiz de saudação do projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="22466-131">In hello TodoList-Service project, open `web.config` in hello root of hello project.</span></span>  
  
  * <span data-ttu-id="22466-132">Substituir saudação `ida:Audience` valor com hello mesmo **Id do aplicativo** do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="22466-132">Replace hello `ida:Audience` value with hello same **Application Id** from hello portal.</span></span>

## <a name="use-msal-tooget-tokens"></a><span data-ttu-id="22466-133">Usar os tokens de tooget MSAL</span><span class="sxs-lookup"><span data-stu-id="22466-133">Use MSAL tooget tokens</span></span>
<span data-ttu-id="22466-134">Olá MSAL de princípio básico é que sempre que seu aplicativo precisa de um token de acesso, você simplesmente chamar `app.AcquireToken(...)`, e MSAL Olá rest.</span><span class="sxs-lookup"><span data-stu-id="22466-134">hello basic principle behind MSAL is that whenever your app needs an access token, you simply call `app.AcquireToken(...)`, and MSAL does hello rest.</span></span>  

* <span data-ttu-id="22466-135">Em Olá `TodoListClient` projeto, abra `MainWindow.xaml.cs` e localize Olá `OnInitialized(...)` método.</span><span class="sxs-lookup"><span data-stu-id="22466-135">In hello `TodoListClient` project, open `MainWindow.xaml.cs` and locate hello `OnInitialized(...)` method.</span></span>  <span data-ttu-id="22466-136">primeira etapa de saudação é tooinitialize seu aplicativo `PublicClientApplication` -classe principal do MSAL, que representa a aplicativos nativos.</span><span class="sxs-lookup"><span data-stu-id="22466-136">hello first step is tooinitialize your app's `PublicClientApplication` - MSAL's primary class representing native applications.</span></span>  <span data-ttu-id="22466-137">Isso é onde você passa MSAL Olá coordenadas necessárias toocommunicate com o Azure AD e informe como toocache tokens.</span><span class="sxs-lookup"><span data-stu-id="22466-137">This is where you pass MSAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* <span data-ttu-id="22466-138">Quando o aplicativo hello é iniciado, podemos deseja toocheck e veja se o usuário Olá já está conectado em aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="22466-138">When hello app starts up, we want toocheck and see if hello user is already signed into hello app.</span></span>  <span data-ttu-id="22466-139">No entanto, nós não desejamos tooinvoke uma entrada da interface do usuário ainda - faremos usuário Olá clique em "Entrar" toodo assim.</span><span class="sxs-lookup"><span data-stu-id="22466-139">However, we don't want tooinvoke a sign-in UI just yet - we'll make hello user click "Sign In" toodo so.</span></span>  <span data-ttu-id="22466-140">Também no hello `OnInitialized(...)` método:</span><span class="sxs-lookup"><span data-stu-id="22466-140">Also in hello `OnInitialized(...)` method:</span></span>

```C#
// As hello app starts, we want toocheck toosee if hello user is already signed in.
// You can do so by trying tooget a token from MSAL, using hello method
// AcquireTokenSilent.  This forces MSAL toothrow an exception if it cannot
// get a token for hello user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in hello cache - or MSAL was able tooget a new oen via refresh token.
    // Proceed toofetch hello user's tasks from hello TodoListService via hello GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, hello app should take no action,
        // and simply show hello user hello sign in button.
    }
    else
    {
        // Here, we catch all other MsalExceptions
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
}

```

* <span data-ttu-id="22466-141">Se o usuário Olá não está conectado e eles botão hello "Entrar", é deseja tooinvoke um interface de usuário de logon e usuário Olá inserir suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="22466-141">If hello user is not signed in and they click hello "Sign In" button, we want tooinvoke a login UI and have hello user enter their credentials.</span></span>  <span data-ttu-id="22466-142">Implementar o manipulador de botão Olá entrar:</span><span class="sxs-lookup"><span data-stu-id="22466-142">Implement hello Sign-In button handler:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign hello user out if they clicked hello "Clear Cache" button

// If hello user clicked hello 'Sign-In' button, force
// MSAL tooprompt hello user for credentials by using
// AcquireTokenAsync, a method that is guaranteed tooshow a prompt toohello user.
// MSAL will get a token for hello TodoListService and cache it for you.

AuthenticationResult result = null;
try
{
    result = await app.AcquireTokenAsync(new string[] { clientId });
    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    // If MSAL cannot get a token, it will throw an exception.
    // If hello user canceled hello login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by hello user");
    }
    else
    {
        // An unexpected error occurred.
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }

        MessageBox.Show(message);
    }

    return;
}


}
```

* <span data-ttu-id="22466-143">Se Olá usuário com êxito entrar, MSAL receberá e um token de cache para você, e você poderá continuar Olá toocall `GetTodoList()` método com confiança.</span><span class="sxs-lookup"><span data-stu-id="22466-143">If hello user successfully signs-in, MSAL will receive and cache a token for you, and you can proceed toocall hello `GetTodoList()` method with confidence.</span></span>  <span data-ttu-id="22466-144">Tudo o que saiu tooget tarefas do usuário é Olá tooimplement `GetTodoList()` método.</span><span class="sxs-lookup"><span data-stu-id="22466-144">All that's left tooget a user's tasks is tooimplement hello `GetTodoList()` method.</span></span>

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try tooget an access token toocall hello TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL toothrow an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show hello user a message
    // and let them click hello Sign-In button.

    if (ex.ErrorCode == "user_interaction_required")
    {
        MessageBox.Show("Please sign in first");
        SignInButton.Content = "Sign In";
    }
    else
    {
        // In any other case, an unexpected error occurred.

        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }

    return;
}

// Once hello token has been returned by MSAL,
// add it toohello http authorization header,
// before making hello call tooaccess hello tooDo list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When hello user is done managing their To-Do List, they may finally sign out of hello app by clicking hello "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If hello user clicked hello 'clear cache' button,
        // clear hello MSAL token cache and show hello user as signed out.
        // It's also necessary tooclear hello cookies from hello browser
        // control so hello next user has a chance toosign in.

        if (SignInButton.Content.ToString() == "Clear Cache")
        {
                TodoList.ItemsSource = string.Empty;
                app.UserTokenCache.Clear(app.ClientId);
                ClearCookies();
                SignInButton.Content = "Sign In";
                return;
        }

        ...
```

## <a name="run"></a><span data-ttu-id="22466-145">Executar</span><span class="sxs-lookup"><span data-stu-id="22466-145">Run</span></span>
<span data-ttu-id="22466-146">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="22466-146">Congratulations!</span></span> <span data-ttu-id="22466-147">Você agora tem um aplicativo .NET WPF que possua Olá capacidade tooauthenticate usuários de trabalho & seguro chamar APIs da Web usando o OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="22466-147">You now have a working .NET WPF app that has hello ability tooauthenticate users & securely call Web APIs using OAuth 2.0.</span></span>  <span data-ttu-id="22466-148">Execute os dois projetos e entre com uma conta da Microsoft pessoal ou uma conta corporativa ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="22466-148">Run your both projects, and sign in with either a personal Microsoft account or a work or school account.</span></span>  <span data-ttu-id="22466-149">Adicione lista de tarefas do usuário do toothat de tarefas.</span><span class="sxs-lookup"><span data-stu-id="22466-149">Add tasks toothat user's To-Do list.</span></span>  <span data-ttu-id="22466-150">Saia e entre novamente como tooview de outro usuário sua lista de tarefas pendentes.</span><span class="sxs-lookup"><span data-stu-id="22466-150">Sign out, and sign back in as another user tooview their To-Do list.</span></span>  <span data-ttu-id="22466-151">Feche o aplicativo hello e execute-a novamente.</span><span class="sxs-lookup"><span data-stu-id="22466-151">Close hello app, and re-run it.</span></span>  <span data-ttu-id="22466-152">Observe como a sessão do usuário Olá permanece intacto – isso ocorre porque o aplicativo hello armazena em cache os tokens em um arquivo local.</span><span class="sxs-lookup"><span data-stu-id="22466-152">Notice how hello user's session remains intact - that is because hello app caches tokens in a local file.</span></span>

<span data-ttu-id="22466-153">MSAL torna fácil tooincorporate recursos comuns de identidade em seu aplicativo, usando contas pessoais e corporativas.</span><span class="sxs-lookup"><span data-stu-id="22466-153">MSAL makes it easy tooincorporate common identity features into your app, using both personal and work accounts.</span></span>  <span data-ttu-id="22466-154">Cuida de todo o trabalho sujo Olá para você - gerenciamento de cache, suporte ao protocolo OAuth, apresentando usuário Olá com um logon de interface do usuário, atualizando tokens expirados e muito mais.</span><span class="sxs-lookup"><span data-stu-id="22466-154">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="22466-155">Tudo o que você realmente precisa de tooknow é uma única chamada de API, `app.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="22466-155">All you really need tooknow is a single API call, `app.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="22466-156">Para referência, Olá concluída exemplo (sem os valores de configuração) [é fornecido como. zip aqui](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), ou você pode cloná-lo do GitHub:</span><span class="sxs-lookup"><span data-stu-id="22466-156">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="22466-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="22466-157">Next steps</span></span>
<span data-ttu-id="22466-158">Agora você pode ir para tópicos mais avançados.</span><span class="sxs-lookup"><span data-stu-id="22466-158">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="22466-159">Você pode desejar tootry:</span><span class="sxs-lookup"><span data-stu-id="22466-159">You may want tootry:</span></span>

* [<span data-ttu-id="22466-160">Proteger a saudação TodoListService Web API com o ponto de extremidade do hello v 2.0</span><span class="sxs-lookup"><span data-stu-id="22466-160">Securing hello TodoListService Web API with hello v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-dotnet-api.md)

<span data-ttu-id="22466-161">Para obter recursos adicionais, consulte:</span><span class="sxs-lookup"><span data-stu-id="22466-161">For additional resources, check out:</span></span>  

* [<span data-ttu-id="22466-162">Guia do desenvolvedor v 2.0 Olá >></span><span class="sxs-lookup"><span data-stu-id="22466-162">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="22466-163">Marca "msal" de StackOverflow >></span><span class="sxs-lookup"><span data-stu-id="22466-163">StackOverflow "msal" tag >></span></span>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="22466-164">Obter atualizações de segurança para nossos produtos</span><span class="sxs-lookup"><span data-stu-id="22466-164">Get security updates for our products</span></span>
<span data-ttu-id="22466-165">Recomendamos que você tooget as notificações quando os incidentes de segurança ocorrem visitando [essa página](https://technet.microsoft.com/security/dd252948) e assinando tooSecurity alertas de aviso.</span><span class="sxs-lookup"><span data-stu-id="22466-165">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

