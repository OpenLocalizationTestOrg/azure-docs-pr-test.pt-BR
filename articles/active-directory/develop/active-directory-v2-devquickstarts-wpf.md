---
title: Aplicativo nativo .NET do Azure Active Directory v2.0 | Microsoft Docs
description: "Como criar um aplicativo nativo .NET que conecte usuários com a conta pessoal da Microsoft e as contas corporativas ou de estudante."
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
ms.openlocfilehash: 7389f55ee6fef9548abb0ca4ac1bbd0399868d47
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-a-windows-desktop-app"></a><span data-ttu-id="d0580-103">Adicionar credenciais a um aplicativo da Área de Trabalho do Windows</span><span class="sxs-lookup"><span data-stu-id="d0580-103">Add sign-in to a Windows Desktop app</span></span>
<span data-ttu-id="d0580-104">Com o ponto de extremidade v2.0, você pode adicionar autenticação rapidamente a seus aplicativos do área de trabalho com suporte a contas pessoais da Microsoft e contas corporativas ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="d0580-104">With the the v2.0 endpoint, you can quickly add authentication to your desktop apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="d0580-105">Ele também permite que seu aplicativo se comunique de forma segura com uma API Web de back-end, bem como com o [Microsoft Graph](https://graph.microsoft.io) e algumas das [APIs Unificadas do Office 365](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span><span class="sxs-lookup"><span data-stu-id="d0580-105">It also enables your app to securely communicate with a backend web api, as well as [the Microsoft Graph](https://graph.microsoft.io) and a few of the [Office 365 Unified APIs](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span></span>

> [!NOTE]
> <span data-ttu-id="d0580-106">Nem todos os recursos e cenários do Azure Active Directory (AD) têm suporte no ponto de extremidade v2.0.</span><span class="sxs-lookup"><span data-stu-id="d0580-106">Not all Azure Active Directory (AD) scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="d0580-107">Para determinar se você deve usar o ponto de extremidade v2.0, leia sobre as [limitações da v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="d0580-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="d0580-108">Para [clientes nativos .NET que precisam executar um dispositivo](active-directory-v2-flows.md#mobile-and-native-apps), o Azure AD fornece a Biblioteca de Autenticação do Microsoft Identity, ou MSAL.</span><span class="sxs-lookup"><span data-stu-id="d0580-108">For [.NET native apps that run on a device](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD provides the Microsoft Identity Authentication Library, or MSAL.</span></span>  <span data-ttu-id="d0580-109">Única finalidade da MSAL é tornar mais fácil a obtenção de tokens de acesso para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d0580-109">MSAL's sole purpose in life is to make it easy for your app to get tokens for calling web services.</span></span>  <span data-ttu-id="d0580-110">Para demonstrar como é fácil, vamos compilar aqui um aplicativo de Lista de Tarefas para .NET WPF que:</span><span class="sxs-lookup"><span data-stu-id="d0580-110">To demonstrate just how easy it is, here we'll build a .NET WPF To-Do List app that:</span></span>

* <span data-ttu-id="d0580-111">Conecta o usuário e obtém tokens de acesso usando o [protocolo de autenticação OAuth 2.0](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="d0580-111">Signs the user in & gets access tokens using the [OAuth 2.0 authentication protocol](active-directory-v2-protocols.md).</span></span>
* <span data-ttu-id="d0580-112">Chama com segurança um serviço da Web de Lista de Tarefas back-end, que também é protegido pelo OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d0580-112">Securely calls a backend To-Do List web service, which is also secured by OAuth 2.0.</span></span>
* <span data-ttu-id="d0580-113">Desconecta o usuário.</span><span class="sxs-lookup"><span data-stu-id="d0580-113">Signs the user out.</span></span>

## <a name="download-sample-code"></a><span data-ttu-id="d0580-114">Baixar código de exemplo</span><span class="sxs-lookup"><span data-stu-id="d0580-114">Download sample code</span></span>
<span data-ttu-id="d0580-115">O código para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="d0580-115">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span></span>  <span data-ttu-id="d0580-116">Para acompanhar, você pode [baixar o esqueleto do aplicativo como um .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) ou clonar o esqueleto:</span><span class="sxs-lookup"><span data-stu-id="d0580-116">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

<span data-ttu-id="d0580-117">O aplicativo concluído é fornecido também no final desse tutorial.</span><span class="sxs-lookup"><span data-stu-id="d0580-117">The completed app is provided at the end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="d0580-118">Registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="d0580-118">Register an app</span></span>
<span data-ttu-id="d0580-119">Crie um novo aplicativo em [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ou siga estas [etapas detalhadas](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="d0580-119">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="d0580-120">Não se esqueça de:</span><span class="sxs-lookup"><span data-stu-id="d0580-120">Make sure to:</span></span>

* <span data-ttu-id="d0580-121">Copiar a **ID do Aplicativo** designada ao seu aplicativo, você precisará dela logo.</span><span class="sxs-lookup"><span data-stu-id="d0580-121">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="d0580-122">Adicione a plataforma **Móvel** de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d0580-122">Add the **Mobile** platform for your app.</span></span>

## <a name="install--configure-msal"></a><span data-ttu-id="d0580-123">Instalar e Configurar o MSAL</span><span class="sxs-lookup"><span data-stu-id="d0580-123">Install & Configure MSAL</span></span>
<span data-ttu-id="d0580-124">Agora que você tem um aplicativo registrado na Microsoft, pode instalar o MSAL e gravar seu código relacionado à identidade.</span><span class="sxs-lookup"><span data-stu-id="d0580-124">Now that you have an app registered with Microsoft, you can install MSAL and write your identity-related code.</span></span>  <span data-ttu-id="d0580-125">Para que o MSAL possa comunicar o ponto de extremidade v2.0, forneça a ele algumas informações sobre o registro de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d0580-125">In order for MSAL to be able to communicate the v2.0 endpoint, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="d0580-126">Comece adicionando o MSAL ao projeto TodoListClient usando o Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="d0580-126">Begin by adding MSAL to the TodoListClient project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* <span data-ttu-id="d0580-127">No projeto TodoListClient, abra `app.config`.</span><span class="sxs-lookup"><span data-stu-id="d0580-127">In the TodoListClient project, open `app.config`.</span></span>  <span data-ttu-id="d0580-128">Substitua os valores dos elementos na seção `<appSettings>` para refletir os valores inseridos no portal de registro do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d0580-128">Replace the values of the elements in the `<appSettings>` section to reflect the values you input into the app registration portal.</span></span>  <span data-ttu-id="d0580-129">Seu código fará referência a esses valores sempre que ele usar a MSAL.</span><span class="sxs-lookup"><span data-stu-id="d0580-129">Your code will reference these values whenever it uses MSAL.</span></span>
  
  * <span data-ttu-id="d0580-130">O `ida:ClientId` é a **ID do Aplicativo** do seu aplicativo que você copiou do portal.</span><span class="sxs-lookup"><span data-stu-id="d0580-130">The `ida:ClientId` is the **Application Id** of your app you copied from the portal.</span></span>
* <span data-ttu-id="d0580-131">No projeto do Serviço de Lista de Tarefas, abra `web.config` na raiz do projeto.</span><span class="sxs-lookup"><span data-stu-id="d0580-131">In the TodoList-Service project, open `web.config` in the root of the project.</span></span>  
  
  * <span data-ttu-id="d0580-132">Substitua o `ida:Audience` valor com a mesma **ID do Aplicativo** no portal.</span><span class="sxs-lookup"><span data-stu-id="d0580-132">Replace the `ida:Audience` value with the same **Application Id** from the portal.</span></span>

## <a name="use-msal-to-get-tokens"></a><span data-ttu-id="d0580-133">Usar MSAL para obter tokens</span><span class="sxs-lookup"><span data-stu-id="d0580-133">Use MSAL to get tokens</span></span>
<span data-ttu-id="d0580-134">O princípio básico da ADAL é que sempre que seu aplicativo precisar de um token de acesso, você simplesmente chamará `app.AcquireToken(...)`e a MSAL fará o resto.</span><span class="sxs-lookup"><span data-stu-id="d0580-134">The basic principle behind MSAL is that whenever your app needs an access token, you simply call `app.AcquireToken(...)`, and MSAL does the rest.</span></span>  

* <span data-ttu-id="d0580-135">No projeto `TodoListClient`, abra `MainWindow.xaml.cs` e localize o método `OnInitialized(...)`.</span><span class="sxs-lookup"><span data-stu-id="d0580-135">In the `TodoListClient` project, open `MainWindow.xaml.cs` and locate the `OnInitialized(...)` method.</span></span>  <span data-ttu-id="d0580-136">A primeira etapa é inicializar o `PublicClientApplication` de seu aplicativo - classe principal da MSAL representando aplicativos nativos.</span><span class="sxs-lookup"><span data-stu-id="d0580-136">The first step is to initialize your app's `PublicClientApplication` - MSAL's primary class representing native applications.</span></span>  <span data-ttu-id="d0580-137">É aqui que você passa à MSAL as coordenadas necessárias para se comunicar com o Azure AD e informar a ele como armazenar tokens em cache.</span><span class="sxs-lookup"><span data-stu-id="d0580-137">This is where you pass MSAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* <span data-ttu-id="d0580-138">Quando o aplicativo é iniciado, queremos verificar e ver se o usuário já está conectado ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d0580-138">When the app starts up, we want to check and see if the user is already signed into the app.</span></span>  <span data-ttu-id="d0580-139">No entanto, não queremos chamar uma entrada na interface do usuário ainda – vamos fazer o usuário clicar em "Entrar" para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="d0580-139">However, we don't want to invoke a sign-in UI just yet - we'll make the user click "Sign In" to do so.</span></span>  <span data-ttu-id="d0580-140">Também no método `OnInitialized(...)` :</span><span class="sxs-lookup"><span data-stu-id="d0580-140">Also in the `OnInitialized(...)` method:</span></span>

```C#
// As the app starts, we want to check to see if the user is already signed in.
// You can do so by trying to get a token from MSAL, using the method
// AcquireTokenSilent.  This forces MSAL to throw an exception if it cannot
// get a token for the user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in the cache - or MSAL was able to get a new oen via refresh token.
    // Proceed to fetch the user's tasks from the TodoListService via the GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, the app should take no action,
        // and simply show the user the sign in button.
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

* <span data-ttu-id="d0580-141">Se o usuário não está conectado e clica no botão "Entrar", queremos chamar uma interface de usuário de logon para que o usuário insira suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="d0580-141">If the user is not signed in and they click the "Sign In" button, we want to invoke a login UI and have the user enter their credentials.</span></span>  <span data-ttu-id="d0580-142">Implemente o manipulador do botão Entrar:</span><span class="sxs-lookup"><span data-stu-id="d0580-142">Implement the Sign-In button handler:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign the user out if they clicked the "Clear Cache" button

// If the user clicked the 'Sign-In' button, force
// MSAL to prompt the user for credentials by using
// AcquireTokenAsync, a method that is guaranteed to show a prompt to the user.
// MSAL will get a token for the TodoListService and cache it for you.

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
    // If the user canceled the login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by the user");
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

* <span data-ttu-id="d0580-143">Se o usuário entrar com êxito, a MSAL receberá e armazenará em cache um token para você, e você poderá prosseguir e chamar o método `GetTodoList()` com confiança.</span><span class="sxs-lookup"><span data-stu-id="d0580-143">If the user successfully signs-in, MSAL will receive and cache a token for you, and you can proceed to call the `GetTodoList()` method with confidence.</span></span>  <span data-ttu-id="d0580-144">Tudo o que resta para obter as tarefas do usuário é implementar o `GetTodoList()` método.</span><span class="sxs-lookup"><span data-stu-id="d0580-144">All that's left to get a user's tasks is to implement the `GetTodoList()` method.</span></span>

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try to get an access token to call the TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL to throw an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show the user a message
    // and let them click the Sign-In button.

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

// Once the token has been returned by MSAL,
// add it to the http authorization header,
// before making the call to access the To Do list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When the user is done managing their To-Do List, they may finally sign out of the app by clicking the "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If the user clicked the 'clear cache' button,
        // clear the MSAL token cache and show the user as signed out.
        // It's also necessary to clear the cookies from the browser
        // control so the next user has a chance to sign in.

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

## <a name="run"></a><span data-ttu-id="d0580-145">Executar</span><span class="sxs-lookup"><span data-stu-id="d0580-145">Run</span></span>
<span data-ttu-id="d0580-146">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="d0580-146">Congratulations!</span></span> <span data-ttu-id="d0580-147">Agora você tem um aplicativo WPF .NET de trabalho que pode autenticar usuários e chamar com segurança APIs Web usando Oauth</span><span class="sxs-lookup"><span data-stu-id="d0580-147">You now have a working .NET WPF app that has the ability to authenticate users & securely call Web APIs using OAuth 2.0.</span></span>  <span data-ttu-id="d0580-148">Execute os dois projetos e entre com uma conta da Microsoft pessoal ou uma conta corporativa ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="d0580-148">Run your both projects, and sign in with either a personal Microsoft account or a work or school account.</span></span>  <span data-ttu-id="d0580-149">Adicione tarefas à lista Tarefas Pendentes daquele usuário. </span><span class="sxs-lookup"><span data-stu-id="d0580-149">Add tasks to that user's To-Do list.</span></span>  <span data-ttu-id="d0580-150">Saia e entre novamente como outro usuário para ver a lista Tarefas Pendentes.</span><span class="sxs-lookup"><span data-stu-id="d0580-150">Sign out, and sign back in as another user to view their To-Do list.</span></span>  <span data-ttu-id="d0580-151">Feche o aplicativo e execute-o novamente.</span><span class="sxs-lookup"><span data-stu-id="d0580-151">Close the app, and re-run it.</span></span>  <span data-ttu-id="d0580-152">Observe que a sessão do usuário permanece intacta, isso ocorre porque o aplicativo armazena em cache tokens em um arquivo local.</span><span class="sxs-lookup"><span data-stu-id="d0580-152">Notice how the user's session remains intact - that is because the app caches tokens in a local file.</span></span>

<span data-ttu-id="d0580-153">A MSAL facilita a incorporação de recursos de identidade comuns em seu aplicativo, usando tanto a conta corporativa quanto a pessoal.</span><span class="sxs-lookup"><span data-stu-id="d0580-153">MSAL makes it easy to incorporate common identity features into your app, using both personal and work accounts.</span></span>  <span data-ttu-id="d0580-154">Ele se encarrega de todo o trabalho difícil para você - gerenciamento de cache, suporte a protocolo OAuth, apresentação de uma IU de logon ao usuário, atualização de tokens expirados e mais.</span><span class="sxs-lookup"><span data-stu-id="d0580-154">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="d0580-155">Tudo o que você realmente precisa saber é uma única chamada à API, `app.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="d0580-155">All you really need to know is a single API call, `app.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="d0580-156">Para referência, o exemplo concluído (sem os valores de configuração) [é fornecido como um .zip aqui](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), ou você pode cloná-lo do GitHub:</span><span class="sxs-lookup"><span data-stu-id="d0580-156">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="d0580-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d0580-157">Next steps</span></span>
<span data-ttu-id="d0580-158">Agora você pode ir para tópicos mais avançados.</span><span class="sxs-lookup"><span data-stu-id="d0580-158">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="d0580-159">Você pode desejar experimentar:</span><span class="sxs-lookup"><span data-stu-id="d0580-159">You may want to try:</span></span>

* [<span data-ttu-id="d0580-160">Proteção da API Web TodoListService com o ponto de extremidade v2.0</span><span class="sxs-lookup"><span data-stu-id="d0580-160">Securing the TodoListService Web API with the v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-dotnet-api.md)

<span data-ttu-id="d0580-161">Para obter recursos adicionais, consulte:</span><span class="sxs-lookup"><span data-stu-id="d0580-161">For additional resources, check out:</span></span>  

* [<span data-ttu-id="d0580-162">Guia do desenvolvedor do v2.0 >></span><span class="sxs-lookup"><span data-stu-id="d0580-162">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="d0580-163">Marca "msal" de StackOverflow >></span><span class="sxs-lookup"><span data-stu-id="d0580-163">StackOverflow "msal" tag >></span></span>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="d0580-164">Obter atualizações de segurança para nossos produtos</span><span class="sxs-lookup"><span data-stu-id="d0580-164">Get security updates for our products</span></span>
<span data-ttu-id="d0580-165">Recomendamos que você obtenha notificações sobre a ocorrência de incidentes de segurança visitando [esta página](https://technet.microsoft.com/security/dd252948) e assinando os alertas do Security Advisory.</span><span class="sxs-lookup"><span data-stu-id="d0580-165">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

