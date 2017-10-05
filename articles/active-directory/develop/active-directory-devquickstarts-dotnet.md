---
title: "Introdução ao .NET do Azure AD | Microsoft Docs"
description: "Como compilar um aplicativo .NET de área de trabalho do Windows que se integre ao AD do Azure para entrada e que chame APIs protegidas do AD do Azure usando OAuth."
services: active-directory
documentationcenter: .net
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: ed33574f-6fa3-402c-b030-fae76fba84e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 7a252e0e5243c7b7489373845531cb913ca1f6aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a><span data-ttu-id="f6866-103">Integrar o AD do Azure em um aplicativo WPF de área de trabalho do Windows</span><span class="sxs-lookup"><span data-stu-id="f6866-103">Integrate Azure AD into a Windows Desktop WPF App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="f6866-104">Se você estiver desenvolvendo um aplicativo de desktop, o AD do Azure torna a autenticação dos usuários com suas contas do Active Directory simples e direta.</span><span class="sxs-lookup"><span data-stu-id="f6866-104">If you're developing a desktop application, Azure AD makes it simple and straightforward for you to authenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="f6866-105">Ele também permite que seu aplicativo consuma com segurança qualquer API da Web protegida pelo AD do Azure, como as APIs do Office 365 ou a API do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6866-105">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="f6866-106">Para clientes nativos .NET que precisam acessar recursos protegidos, o AD do Azure fornece a biblioteca de autenticação do Active Directory, ou ADAL.</span><span class="sxs-lookup"><span data-stu-id="f6866-106">For .NET native clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="f6866-107">A única finalidade da ADAL é tornar mais fácil para seu aplicativo obter tokens de acesso.</span><span class="sxs-lookup"><span data-stu-id="f6866-107">ADAL's sole purpose in life is to make it easy for your app to get access tokens.</span></span>  <span data-ttu-id="f6866-108">Para demonstrar como é fácil, vamos compilar aqui um aplicativo de lista de tarefas pendentes para .NET WPF que:</span><span class="sxs-lookup"><span data-stu-id="f6866-108">To demonstrate just how easy it is, here we'll build a .NET WPF To-Do List application that:</span></span>

* <span data-ttu-id="f6866-109">Obtém tokens de acesso para chamar a Graph API do AD do Azure usando o [protocolo de autenticação OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="f6866-109">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="f6866-110">Pesquisa um diretório para usuários com um determinado alias.</span><span class="sxs-lookup"><span data-stu-id="f6866-110">Searches a directory for users with a given alias.</span></span>
* <span data-ttu-id="f6866-111">Desconecta usuários.</span><span class="sxs-lookup"><span data-stu-id="f6866-111">Signs users out.</span></span>

<span data-ttu-id="f6866-112">Para compilar o aplicativo em funcionamento completo, você precisará:</span><span class="sxs-lookup"><span data-stu-id="f6866-112">To build the complete working application, you'll need to:</span></span>

1. <span data-ttu-id="f6866-113">Registrar seu aplicativo no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6866-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="f6866-114">Instalar e configurar a ADAL.</span><span class="sxs-lookup"><span data-stu-id="f6866-114">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="f6866-115">Usar a ADAL para obter tokens do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6866-115">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="f6866-116">Para começar, [baixe o esqueleto do aplicativo](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) ou [baixe o exemplo concluído](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="f6866-116">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="f6866-117">Você também precisará de um locatário do AD do Azure no qual você possa criar usuários e registrar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f6866-117">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="f6866-118">Se você ainda não tiver um locatário [saiba como obter um](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="f6866-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-the-directorysearcher-application"></a><span data-ttu-id="f6866-119">1. Registrar o aplicativo DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="f6866-119">1. Register the DirectorySearcher Application</span></span>
<span data-ttu-id="f6866-120">Para habilitar seu aplicativo para obter tokens, primeiro será necessário registrá-lo no seu locatário do AD do Azure e conceder permissão para acessar a Graph API do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="f6866-120">To enable your app to get tokens, you'll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="f6866-121">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f6866-121">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f6866-122">Na barra superior, clique na sua conta e, na lista **Diretório**, escolha o locatário do Active Directory em que você deseja registrar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f6866-122">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="f6866-123">Clique em **Mais Serviços** no painel de navegação à esquerda e escolha **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f6866-123">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="f6866-124">Clique em **Registros do Aplicativo** e escolha **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f6866-124">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="f6866-125">Siga os prompts e crie um novo **Aplicativo cliente nativo**.</span><span class="sxs-lookup"><span data-stu-id="f6866-125">Follow the prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="f6866-126">O **Nome** do aplicativo descreverá seu aplicativo para os usuários finais</span><span class="sxs-lookup"><span data-stu-id="f6866-126">The **Name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="f6866-127">O **URI de redirecionamento** é uma combinação de esquema e de cadeia de caracteres que o AD do Azure usará para retornar respostas de tokens.</span><span class="sxs-lookup"><span data-stu-id="f6866-127">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span></span>  <span data-ttu-id="f6866-128">Insira um valor específico para seu aplicativo, por exemplo, `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="f6866-128">Enter a value specific to your application, e.g. `http://DirectorySearcher`.</span></span>
6. <span data-ttu-id="f6866-129">Depois de concluir o registro, o AAD atribuirá a seu aplicativo uma ID do Aplicativo única.</span><span class="sxs-lookup"><span data-stu-id="f6866-129">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="f6866-130">Você precisará desse valor nas próximas seções, então copie-o da página do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f6866-130">You'll need this value in the next sections, so copy it from the application page.</span></span>
7. <span data-ttu-id="f6866-131">Na página **Configurações**, escolha **Permissões Necessárias** e escolha **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f6866-131">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="f6866-132">Escolha o **Microsoft Graph** como a API e adicione a permissão **Ler Dados do Diretório** em **Permissões Delegadas**.</span><span class="sxs-lookup"><span data-stu-id="f6866-132">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="f6866-133">Isso permitirá que seu aplicativo consulte a Graph API para usuários.</span><span class="sxs-lookup"><span data-stu-id="f6866-133">This will enable your application to query the Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="f6866-134">2. Instalar e Configurar o ADAL</span><span class="sxs-lookup"><span data-stu-id="f6866-134">2. Install & Configure ADAL</span></span>
<span data-ttu-id="f6866-135">Agora que você tem um aplicativo no AD do Azure, você pode instalar a ADAL e escrever seu código relacionado à identidade.</span><span class="sxs-lookup"><span data-stu-id="f6866-135">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="f6866-136">Para que a ADAL possa se comunicar com o Azure AD, é necessário fornecer a ela algumas informações sobre o registro do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f6866-136">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="f6866-137">Comece adicionando o ADAL ao projeto DirectorySearcher usando o Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="f6866-137">Begin by adding ADAL to the DirectorySearcher project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="f6866-138">No projeto DirectorySearcher, abra `app.config`.</span><span class="sxs-lookup"><span data-stu-id="f6866-138">In the DirectorySearcher project, open `app.config`.</span></span>  <span data-ttu-id="f6866-139">Substitua os valores dos elementos na seção `<appSettings>` para refletir os valores inseridos por você no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6866-139">Replace the values of the elements in the `<appSettings>` section to reflect the values you input into the Azure Portal.</span></span>  <span data-ttu-id="f6866-140">Seu código fará referência a esses valores sempre que ele usar a ADAL.</span><span class="sxs-lookup"><span data-stu-id="f6866-140">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="f6866-141">O `ida:Tenant` é o domínio do seu locatário do AD do Azure, por exemplo, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="f6866-141">The `ida:Tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="f6866-142">O `ida:ClientId` é a clientId do seu aplicativo que você copiou do portal.</span><span class="sxs-lookup"><span data-stu-id="f6866-142">The `ida:ClientId` is the clientId of your application you copied from the portal.</span></span>
  * <span data-ttu-id="f6866-143">O `ida:RedirectUri` é a URL de redirecionamento registrada no portal.</span><span class="sxs-lookup"><span data-stu-id="f6866-143">The `ida:RedirectUri` is the redirect url you registered in the portal.</span></span>

## <a name="3----use-adal-to-get-tokens-from-aad"></a><span data-ttu-id="f6866-144">3.    Usar o ADAL para obter tokens do AAD</span><span class="sxs-lookup"><span data-stu-id="f6866-144">3.    Use ADAL to Get Tokens from AAD</span></span>
<span data-ttu-id="f6866-145">O princípio básico da ADAL é que sempre que seu aplicativo precisa de um token de acesso, ele simplesmente chama `authContext.AcquireTokenAsync(...)`, e a ADAL faz o resto.</span><span class="sxs-lookup"><span data-stu-id="f6866-145">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireTokenAsync(...)`, and ADAL does the rest.</span></span>  

* <span data-ttu-id="f6866-146">No projeto `DirectorySearcher`, abra `MainWindow.xaml.cs` e localize o método `MainWindow()`.</span><span class="sxs-lookup"><span data-stu-id="f6866-146">In the `DirectorySearcher` project, open `MainWindow.xaml.cs` and locate the `MainWindow()` method.</span></span>  <span data-ttu-id="f6866-147">A primeira etapa é inicializar o `AuthenticationContext` de seu aplicativo: a classe principal da ADAL.</span><span class="sxs-lookup"><span data-stu-id="f6866-147">The first step is to initialize your app's `AuthenticationContext` - ADAL's primary class.</span></span>  <span data-ttu-id="f6866-148">É aqui que você passa à ADAL as coordenadas necessárias para se comunicar com o AD do Azure e informar a ele como armazenar tokens em cache.</span><span class="sxs-lookup"><span data-stu-id="f6866-148">This is where you pass ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* <span data-ttu-id="f6866-149">Agora localize o método `Search(...)` , que será chamado quando os usuário clicar no botão "Pesquisar" na interface do usuário do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f6866-149">Now locate the `Search(...)` method, which will be invoked when the user cliks the "Search" button in the app's UI.</span></span>  <span data-ttu-id="f6866-150">Esse método faz uma solicitação GET para que a Graph API do AD do Azure procure por usuários cujo UPN começa com o termo de pesquisa fornecido.</span><span class="sxs-lookup"><span data-stu-id="f6866-150">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="f6866-151">Mas para consultar a Graph API, você precisa incluir um access_token no cabeçalho `Authorization` da solicitação - é aí que entra a ADAL.</span><span class="sxs-lookup"><span data-stu-id="f6866-151">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate the Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for the To Do item name");
        return;
    }

    // Get an Access Token for the Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled the sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* <span data-ttu-id="f6866-152">Quando o aplicativo solicita um token chamando `AcquireTokenAsync(...)`, a ADAL tentará retornar um token sem pedir as credenciais ao usuário.</span><span class="sxs-lookup"><span data-stu-id="f6866-152">When your app requests a token by calling `AcquireTokenAsync(...)`, ADAL will attempt to return a token without asking the user for credentials.</span></span>  <span data-ttu-id="f6866-153">Se a ADAL determina que o usuário precisa entrar para obter um token, exibirá uma caixa de diálogo de logon, coletar as credenciais do usuário e retornar um token após uma autenticação bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="f6866-153">If ADAL determines that the user needs to sign in to get a token, it will display a login dialog, collect the user's credentials, and return a token upon successful authentication.</span></span>  <span data-ttu-id="f6866-154">Se a ADAL não puder retornar um token por qualquer motivo, o status exibirá `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="f6866-154">If ADAL is unable to return a token for any reason, it will throw an `AdalException`.</span></span>
* <span data-ttu-id="f6866-155">Observe que o objeto `AuthenticationResult` contém um objeto `UserInfo` que pode ser usado para coletar informações que seu aplicativo pode precisar.</span><span class="sxs-lookup"><span data-stu-id="f6866-155">Notice that the `AuthenticationResult` object contains a `UserInfo` object that can be used to collect information your app may need.</span></span>  <span data-ttu-id="f6866-156">Em DirectorySearcher, `UserInfo` é usado para personalizar a interface do usuário do aplicativo com a ID do usuário.</span><span class="sxs-lookup"><span data-stu-id="f6866-156">In the DirectorySearcher, `UserInfo` is used to customize the app's UI with the user's id.</span></span>
* <span data-ttu-id="f6866-157">Quando o usuário clica no botão "Sair", queremos garantir que a próxima chamada para `AcquireTokenAsync(...)` solicitará que o usuário entre.</span><span class="sxs-lookup"><span data-stu-id="f6866-157">When the user clicks the "Sign Out" button, we want to ensure that the next call to `AcquireTokenAsync(...)` will ask the user to sign in.</span></span>  <span data-ttu-id="f6866-158">Com a ADAL, isso é tão fácil quanto limpar o cache de tokens:</span><span class="sxs-lookup"><span data-stu-id="f6866-158">With ADAL, this is as easy as clearing the token cache:</span></span>

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear the token cache
    authContext.TokenCache.Clear();

    ...
}
```

* <span data-ttu-id="f6866-159">No entanto, se o usuário não clicar no botão "Sair", convém manter a sessão do usuário para a próxima vez que ele executar o DirectorySearcher.</span><span class="sxs-lookup"><span data-stu-id="f6866-159">However, if the user does not click the "Sign Out" button, you will want to maintain the user's session for the next time they run the DirectorySearcher.</span></span>  <span data-ttu-id="f6866-160">Quando o aplicativo for iniciado, você pode verificar o cache de token da ADAL e procurar um token existente e atualizar a interface do usuário de acordo.</span><span class="sxs-lookup"><span data-stu-id="f6866-160">When the app launches, you can check ADAL's token cache for an existing token and update the UI accordingly.</span></span>  <span data-ttu-id="f6866-161">No método `CheckForCachedToken()`, faça outra chamada para `AcquireTokenAsync(...)`, desta vez, aprovando o parâmetro `PromptBehavior.Never`.</span><span class="sxs-lookup"><span data-stu-id="f6866-161">In the `CheckForCachedToken()` method, make another call to `AcquireTokenAsync(...)`, this time passing in the `PromptBehavior.Never` parameter.</span></span>  <span data-ttu-id="f6866-162">`PromptBehavior.Never` informará à ADAL que não se deve solicitar a entrada do usuário e a ADAL, em vez disso, deve emitir uma exceção se não for possível retornar um token.</span><span class="sxs-lookup"><span data-stu-id="f6866-162">`PromptBehavior.Never` will tell ADAL that the user should not be prompted for sign in, and ADAL should instead throw an exception if it is unable to return a token.</span></span>

```C#
public async void CheckForCachedToken() 
{
    // As the application starts, try to get an access token without prompting the user.  If one exists, show the user as signed in.
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Never));
    }
    catch (AdalException ex)
    {
        if (ex.ErrorCode != "user_interaction_required")
        {
            // An unexpected error occurred.
            MessageBox.Show(ex.Message);
        }

        // If user interaction is required, proceed to main page without singing the user in.
        return;
    }

    // A valid token is in the cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

<span data-ttu-id="f6866-163">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="f6866-163">Congratulations!</span></span> <span data-ttu-id="f6866-164">Agora você tem um aplicativo .NET WPF que tem a capacidade de autenticar usuários, chamar APIs da Web com segurança usando OAuth 2.0 e obter informações básicas sobre o usuário.</span><span class="sxs-lookup"><span data-stu-id="f6866-164">You now have a working .NET WPF application that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="f6866-165">Se você ainda não fez isso, agora é o momento de preencher seu locatário com alguns usuários.</span><span class="sxs-lookup"><span data-stu-id="f6866-165">If you haven't already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="f6866-166">Execute o aplicativo DirectorySearcher e entre com um desses usuários.</span><span class="sxs-lookup"><span data-stu-id="f6866-166">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="f6866-167">Procure por outros usuários com base em seus UPNs.</span><span class="sxs-lookup"><span data-stu-id="f6866-167">Search for other users based on their UPN.</span></span>  <span data-ttu-id="f6866-168">Feche o aplicativo e execute-o novamente.</span><span class="sxs-lookup"><span data-stu-id="f6866-168">Close the app, and re-run it.</span></span>  <span data-ttu-id="f6866-169">Observe como a sessão do usuário permanece intacta.</span><span class="sxs-lookup"><span data-stu-id="f6866-169">Notice how the user's session remains intact.</span></span>  <span data-ttu-id="f6866-170">Saia e entre novamente como outro usuário.</span><span class="sxs-lookup"><span data-stu-id="f6866-170">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="f6866-171">A ADAL facilita a incorporar todos esses recursos comuns de identidade em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f6866-171">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="f6866-172">Ele se encarrega de todo o trabalho difícil para você - gerenciamento de cache, suporte a protocolo OAuth, apresentação de uma IU de logon ao usuário, atualização de tokens expirados e mais.</span><span class="sxs-lookup"><span data-stu-id="f6866-172">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="f6866-173">Tudo o que você realmente precisa saber é uma única chamada à API, `authContext.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="f6866-173">All you really need to know is a single API call, `authContext.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="f6866-174">Para referência, o exemplo concluído (sem seus valores de configuração) é fornecido [aqui](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="f6866-174">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="f6866-175">Agora você pode passar para cenários de adicionais.</span><span class="sxs-lookup"><span data-stu-id="f6866-175">You can now move on to additional scenarios.</span></span>  <span data-ttu-id="f6866-176">Você pode desejar experimentar:</span><span class="sxs-lookup"><span data-stu-id="f6866-176">You may want to try:</span></span>

[<span data-ttu-id="f6866-177">Proteger uma API da Web .NET com o Azure AD >></span><span class="sxs-lookup"><span data-stu-id="f6866-177">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

