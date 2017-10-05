---
title: "Introdução ao Windows Phone no Azure AD | Microsoft Docs"
description: Como criar um aplicativo do Windows Phone que se integre ao AD do Azure para entrar e chame APIs protegidas do AD do Azure usando OAuth.
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 66f5ac20-5e1f-4b9d-bb99-9b3305e26416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 03c4b6d225dce99d79ef6c1ba2af43af8dea3eae
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a><span data-ttu-id="cf984-103">Integrar o AD do Azure com um aplicativo do Windows Phone</span><span class="sxs-lookup"><span data-stu-id="cf984-103">Integrate Azure AD with a Windows Phone App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="cf984-104">Não há suporte para projetos do Windows Phone 8.1 e de versões anteriores no Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="cf984-104">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="cf984-105">Para obter mais informações, consulte [Direcionamento e compatibilidade da plataforma Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="cf984-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="cf984-106">Se você estiver desenvolvendo um aplicativo do Windows Phone 8.1, o Azure AD torna simples e direto autenticar os usuários com suas contas do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cf984-106">If you're developing a Windows Phone 8.1 app, Azure AD makes it simple and straightforward for you to authenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="cf984-107">Ele também permite que seu aplicativo consuma com segurança qualquer API da Web protegida pelo AD do Azure, como as APIs do Office 365 ou a API do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf984-107">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

> [!NOTE]
> <span data-ttu-id="cf984-108">Este exemplo de código usa ADAL v2.0.</span><span class="sxs-lookup"><span data-stu-id="cf984-108">This code sample uses ADAL v2.0.</span></span>  <span data-ttu-id="cf984-109">Para a tecnologia mais recente, é aconselhável experimentar nosso [Tutorial Universal do Windows usando o ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span><span class="sxs-lookup"><span data-stu-id="cf984-109">For the latest technology, you may want to instead try our [Windows Universal Tutorial using ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span></span>  <span data-ttu-id="cf984-110">Se você realmente estiver criando um aplicativo para Windows Phone 8.1, esse é o lugar certo.</span><span class="sxs-lookup"><span data-stu-id="cf984-110">If you are indeed building an app for Windows Phone 8.1, this is the right place.</span></span>  <span data-ttu-id="cf984-111">O ADAL v2.0 ainda é totalmente suportado e é a maneira recomendada de desenvolvimento de aplicativos para o Windows Phone 8.1 usando o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf984-111">ADAL v2.0 is still fully supported, and is the recommended way of developing apps agianst Windows Phone 8.1 using Azure AD.</span></span>
> 
> 

<span data-ttu-id="cf984-112">Para clientes nativos .NET que precisam acessar recursos protegidos, o AD do Azure fornece a biblioteca de autenticação do Active Directory, ou ADAL.</span><span class="sxs-lookup"><span data-stu-id="cf984-112">For .NET native clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="cf984-113">Única finalidade da ADAL é tornar mais fácil para seu aplicativo obter tokens de acesso.</span><span class="sxs-lookup"><span data-stu-id="cf984-113">ADAL’s sole purpose in life is to make it easy for your app to get access tokens.</span></span>  <span data-ttu-id="cf984-114">Para demonstrar como isso é fácil, aqui vamos criar um aplicativo "Directory Searcher" do Windows Phone 8.1 que:</span><span class="sxs-lookup"><span data-stu-id="cf984-114">To demonstrate just how easy it is, here we’ll build a "Directory Searcher" Windows Phone 8.1 app that:</span></span>

* <span data-ttu-id="cf984-115">Obtém tokens de acesso para chamar a Graph API do AD do Azure usando o [protocolo de autenticação OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf984-115">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="cf984-116">Pesquisa um diretório para usuários com um determinado UPN.</span><span class="sxs-lookup"><span data-stu-id="cf984-116">Searches a directory for users with a given UPN.</span></span>
* <span data-ttu-id="cf984-117">Desconecta usuários.</span><span class="sxs-lookup"><span data-stu-id="cf984-117">Signs users out.</span></span>

<span data-ttu-id="cf984-118">Para compilar o aplicativo em funcionamento completo, você precisará:</span><span class="sxs-lookup"><span data-stu-id="cf984-118">To build the complete working application, you’ll need to:</span></span>

1. <span data-ttu-id="cf984-119">Registrar seu aplicativo no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf984-119">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="cf984-120">Instalar e configurar a ADAL.</span><span class="sxs-lookup"><span data-stu-id="cf984-120">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="cf984-121">Usar a ADAL para obter tokens do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf984-121">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="cf984-122">Para começar, [baixe um projeto de esqueleto](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) ou [baixe o exemplo concluído](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="cf984-122">To get started, [download a skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="cf984-123">Cada um é uma solução do Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="cf984-123">Each is a Visual Studio 2013 solution.</span></span>  <span data-ttu-id="cf984-124">Você também precisará de um locatário do AD do Azure no qual você possa criar usuários e registrar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf984-124">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="cf984-125">Se você ainda não tiver um locatário [saiba como obter um](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="cf984-125">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-the-directory-searcher-application"></a><span data-ttu-id="cf984-126">1. Registrar o aplicativo Directory Searcher</span><span class="sxs-lookup"><span data-stu-id="cf984-126">1. Register the Directory Searcher Application</span></span>
<span data-ttu-id="cf984-127">Para habilitar seu aplicativo para obter tokens, primeiro será necessário registrá-lo no seu locatário do AD do Azure e conceder permissão para acessar a Graph API do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="cf984-127">To enable your app to get tokens, you’ll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="cf984-128">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cf984-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cf984-129">Na barra superior, clique na sua conta e, na lista **Diretório**, escolha o locatário do Active Directory em que você deseja registrar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf984-129">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="cf984-130">Clique em **Mais Serviços** no painel de navegação à esquerda e escolha **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cf984-130">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="cf984-131">Clique em **Registros do Aplicativo** e escolha **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cf984-131">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="cf984-132">Siga os prompts e crie um novo **Aplicativo cliente nativo**.</span><span class="sxs-lookup"><span data-stu-id="cf984-132">Follow the prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="cf984-133">O **Nome** do aplicativo descreverá seu aplicativo para os usuários finais</span><span class="sxs-lookup"><span data-stu-id="cf984-133">The **Name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="cf984-134">O **URI de redirecionamento** é uma combinação de esquema e de cadeia de caracteres que o AD do Azure usará para retornar respostas de tokens.</span><span class="sxs-lookup"><span data-stu-id="cf984-134">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span></span>  <span data-ttu-id="cf984-135">Insira um valor de espaço reservado por enquanto, por exemplo, `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="cf984-135">Enter a placeholder value for now, e.g. `http://DirectorySearcher`.</span></span>  <span data-ttu-id="cf984-136">Substituiremos este valor posteriormente.</span><span class="sxs-lookup"><span data-stu-id="cf984-136">We'll replace this value later.</span></span>
6. <span data-ttu-id="cf984-137">Depois de concluir o registro, o AAD atribuirá a seu aplicativo uma ID do Aplicativo única.</span><span class="sxs-lookup"><span data-stu-id="cf984-137">Once you’ve completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="cf984-138">Você precisará desse valor nas próximas seções, portanto, copie-o da guia do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf984-138">You’ll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="cf984-139">Na página **Configurações**, escolha **Permissões Necessárias** e escolha **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cf984-139">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="cf984-140">Escolha o **Microsoft Graph** como a API e adicione a permissão **Ler Dados do Diretório** em **Permissões Delegadas**.</span><span class="sxs-lookup"><span data-stu-id="cf984-140">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="cf984-141">Isso permitirá que seu aplicativo consulte a Graph API para usuários.</span><span class="sxs-lookup"><span data-stu-id="cf984-141">This will enable your application to query the Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="cf984-142">2. Instalar e Configurar o ADAL</span><span class="sxs-lookup"><span data-stu-id="cf984-142">2. Install & Configure ADAL</span></span>
<span data-ttu-id="cf984-143">Agora que você tem um aplicativo no AD do Azure, você pode instalar a ADAL e escrever seu código relacionado à identidade.</span><span class="sxs-lookup"><span data-stu-id="cf984-143">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="cf984-144">Para que a ADAL possa se comunicar com o Azure AD, é necessário fornecer a ela algumas informações sobre o registro do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf984-144">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="cf984-145">Comece adicionando o ADAL ao projeto DirectorySearcher usando o Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="cf984-145">Begin by adding ADAL to the DirectorySearcher project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="cf984-146">No projeto DirectorySearcher, abra `MainPage.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="cf984-146">In the DirectorySearcher project, open `MainPage.xaml.cs`.</span></span>  <span data-ttu-id="cf984-147">Substitua os valores na região `Config Values` para refletir os valores inseridos por você no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf984-147">Replace the values in the `Config Values` region to reflect the values you input into the Azure Portal.</span></span>  <span data-ttu-id="cf984-148">Seu código fará referência a esses valores sempre que ele usar a ADAL.</span><span class="sxs-lookup"><span data-stu-id="cf984-148">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="cf984-149">O `tenant` é o domínio do seu locatário do AD do Azure, por exemplo, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="cf984-149">The `tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="cf984-150">O `clientId` é a clientId do seu aplicativo que você copiou do portal.</span><span class="sxs-lookup"><span data-stu-id="cf984-150">The `clientId` is the clientId of your application you copied from the portal.</span></span>
* <span data-ttu-id="cf984-151">Agora você precisa descobrir o URI de retorno de chamada para seu aplicativo do Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="cf984-151">You now need to discover the callback uri for your Windows Phone app.</span></span>  <span data-ttu-id="cf984-152">Defina um ponto de interrupção nessa linha no método `MainPage` :</span><span class="sxs-lookup"><span data-stu-id="cf984-152">Set a breakpoint on this line in the `MainPage` method:</span></span>

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* <span data-ttu-id="cf984-153">Execute o aplicativo e copie separadamente o valor de `redirectUri` quando o ponto de interrupção for atingido.</span><span class="sxs-lookup"><span data-stu-id="cf984-153">Run the app, and copy aside the value of `redirectUri` when the breakpoint is hit.</span></span>  <span data-ttu-id="cf984-154">O resultado deve ser semelhante a</span><span class="sxs-lookup"><span data-stu-id="cf984-154">It should look something like</span></span>

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* <span data-ttu-id="cf984-155">De volta à guia **Configurar** do seu aplicativo no Portal de Gerenciamento do Azure, substitua o valor de **RedirectUri** por esse valor.</span><span class="sxs-lookup"><span data-stu-id="cf984-155">Back on the **Configure** tab of your application in the Azure Management Portal, replace the value of the **RedirectUri** with this value.</span></span>  

## <a name="3-use-adal-to-get-tokens-from-aad"></a><span data-ttu-id="cf984-156">3. Usar o ADAL para obter tokens do AAD</span><span class="sxs-lookup"><span data-stu-id="cf984-156">3. Use ADAL to Get Tokens from AAD</span></span>
<span data-ttu-id="cf984-157">O princípio básico da ADAL é que sempre que seu aplicativo precisa de um token de acesso, ele simplesmente chama `authContext.AcquireToken(…)`, e a ADAL faz o resto.</span><span class="sxs-lookup"><span data-stu-id="cf984-157">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does the rest.</span></span>  

* <span data-ttu-id="cf984-158">A primeira etapa é inicializar o `AuthenticationContext` de seu aplicativo - classe principal da ADAL.</span><span class="sxs-lookup"><span data-stu-id="cf984-158">The first step is to initialize your app’s `AuthenticationContext` - ADAL’s primary class.</span></span>  <span data-ttu-id="cf984-159">É aqui que você passa à ADAL as coordenadas necessárias para se comunicar com o AD do Azure e informar a ele como armazenar tokens em cache.</span><span class="sxs-lookup"><span data-stu-id="cf984-159">This is where you pass ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* <span data-ttu-id="cf984-160">Agora localize o método `Search(...)` , que será chamado quando os usuário clicar no botão "Pesquisar" na interface do usuário do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf984-160">Now locate the `Search(...)` method, which will be invoked when the user cliks the "Search" button in the app's UI.</span></span>  <span data-ttu-id="cf984-161">Esse método faz uma solicitação GET para que a Graph API do AD do Azure procure por usuários cujo UPN começa com o termo de pesquisa fornecido.</span><span class="sxs-lookup"><span data-stu-id="cf984-161">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="cf984-162">Mas para consultar a Graph API, você precisa incluir um access_token no cabeçalho `Authorization` da solicitação - é aí que entra a ADAL.</span><span class="sxs-lookup"><span data-stu-id="cf984-162">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try to get a token without triggering any user prompt.
    // ADAL will check whether the requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained the QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* <span data-ttu-id="cf984-163">Se for necessário usar autenticação interativa, a ADAL usará o WAB (Web Authentication Broker, agenciador de autenticação da Web) do Windows Phone e [modelo de continuação](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) para exibir a página de logon do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf984-163">If interactive authentication is necessary, ADAL will use Windows Phone's Web Authentication Broker (WAB) and [continuation model](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) to display the Azure AD sign in page.</span></span>  <span data-ttu-id="cf984-164">Quando o usuário faz logon, seu aplicativo precisa passar à ADAL os resultados da interação com o WAB.</span><span class="sxs-lookup"><span data-stu-id="cf984-164">When the user signs in, your app needs to pass ADAL the results of the WAB interaction.</span></span>  <span data-ttu-id="cf984-165">Isso é tão simples quanto implementar a interface `ContinueWebAuthentication` :</span><span class="sxs-lookup"><span data-stu-id="cf984-165">This is as simple as implementing the `ContinueWebAuthentication` interface:</span></span>

```C#
// This method is automatically invoked when the application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass the authentication interaction results to ADAL, which will
    // conclude the token acquisition operation and invoke the callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* <span data-ttu-id="cf984-166">Agora é hora de usar o `AuthenticationResult` que a ADAL retornou ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf984-166">Now it's time to use the `AuthenticationResult` that ADAL returned to your app.</span></span>  <span data-ttu-id="cf984-167">No retorno de chamada `QueryGraph(...)`, anexe o access_token que você adquiriu à solicitação GET, no cabeçalho Autorização:</span><span class="sxs-lookup"><span data-stu-id="cf984-167">In the `QueryGraph(...)` callback, attach the access_token you acquired to the GET request in the Authorization header:</span></span>

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If the error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add the access token to the Authorization Header of the call to the Graph API, and call the Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* <span data-ttu-id="cf984-168">Você também pode usar o objeto `AuthenticationResult` para exibir informações sobre o usuário em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf984-168">You can also use the `AuthenticationResult` object to display information about the user in your app.</span></span> <span data-ttu-id="cf984-169">No método `QueryGraph(...)` , use o resultado para mostrar a id do usuário na página:</span><span class="sxs-lookup"><span data-stu-id="cf984-169">In the `QueryGraph(...)` method, use the result to show the user's id on the page:</span></span>

```C#
// Update the Page UI to represent the signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* <span data-ttu-id="cf984-170">Por fim, você também pode usar a ADAL para realizar o logout do usuário do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf984-170">Finally, you can use ADAL to sign the user out of hte application as well.</span></span>  <span data-ttu-id="cf984-171">Quando o usuário clica no botão "Sair", queremos garantir que a próxima chamada para `AcquireTokenSilentAsync(...)` falhará.</span><span class="sxs-lookup"><span data-stu-id="cf984-171">When the user clicks the "Sign Out" button, we want to ensure that the next call to `AcquireTokenSilentAsync(...)` will fail.</span></span>  <span data-ttu-id="cf984-172">Com a ADAL, isso é tão fácil quanto limpar o cache de tokens:</span><span class="sxs-lookup"><span data-stu-id="cf984-172">With ADAL, this is as easy as clearing the token cache:</span></span>

```C#
private void SignOut()
{
    // Clear session state from the token cache.
    authContext.TokenCache.Clear();

    ...
}
```

<span data-ttu-id="cf984-173">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="cf984-173">Congratulations!</span></span> <span data-ttu-id="cf984-174">Agora você tem um aplicativo do Windows Phone que tem a capacidade de autenticar usuários, chamar APIs da Web com segurança usando OAuth 2.0 e obter informações básicas sobre o usuário.</span><span class="sxs-lookup"><span data-stu-id="cf984-174">You now have a working Windows Phone app that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="cf984-175">Se você ainda não fez isso, agora é o momento de preencher seu locatário com alguns usuários.</span><span class="sxs-lookup"><span data-stu-id="cf984-175">If you haven’t already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="cf984-176">Execute o aplicativo DirectorySearcher e faça logon com um desses usuários.</span><span class="sxs-lookup"><span data-stu-id="cf984-176">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="cf984-177">Procure por outros usuários com base em seus UPNs.</span><span class="sxs-lookup"><span data-stu-id="cf984-177">Search for other users based on their UPN.</span></span>  <span data-ttu-id="cf984-178">Feche o aplicativo e execute-o novamente.</span><span class="sxs-lookup"><span data-stu-id="cf984-178">Close the app, and re-run it.</span></span>  <span data-ttu-id="cf984-179">Observe como a sessão do usuário permanece intacta.</span><span class="sxs-lookup"><span data-stu-id="cf984-179">Notice how the user’s session remains intact.</span></span>  <span data-ttu-id="cf984-180">Saia e faça logon novamente como outro usuário.</span><span class="sxs-lookup"><span data-stu-id="cf984-180">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="cf984-181">A ADAL facilita a incorporar todos esses recursos comuns de identidade em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf984-181">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="cf984-182">Ele se encarrega de todo o trabalho difícil para você - gerenciamento de cache, suporte a protocolo OAuth, apresentação de uma IU de logon ao usuário, atualização de tokens expirados e mais.</span><span class="sxs-lookup"><span data-stu-id="cf984-182">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="cf984-183">Tudo o que você realmente precisa saber é uma única chamada à API, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="cf984-183">All you really need to know is a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="cf984-184">Para referência, o exemplo concluído (sem seus valores de configuração) é fornecido [aqui](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="cf984-184">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="cf984-185">Agora você pode passar para cenários de identidade adicionais.</span><span class="sxs-lookup"><span data-stu-id="cf984-185">You can now move on to additional identity scenarios.</span></span>  <span data-ttu-id="cf984-186">Você pode desejar experimentar:</span><span class="sxs-lookup"><span data-stu-id="cf984-186">You may want to try:</span></span>

[<span data-ttu-id="cf984-187">Proteger uma API da Web .NET com o Azure AD >></span><span class="sxs-lookup"><span data-stu-id="cf984-187">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

