---
title: "aaaAzure do Windows Phone AD Introdução | Microsoft Docs"
description: Como toobuild um aplicativo do Windows Phone que se integra ao AD do Azure para entrar e chama o AD do Azure usando o OAuth APIs protegidas.
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
ms.openlocfilehash: e766bfcdfae10483772154f4b5facdec05fc846f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a><span data-ttu-id="a1063-103">Integrar o AD do Azure com um aplicativo do Windows Phone</span><span class="sxs-lookup"><span data-stu-id="a1063-103">Integrate Azure AD with a Windows Phone App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="a1063-104">Não há suporte para projetos do Windows Phone 8.1 e de versões anteriores no Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="a1063-104">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="a1063-105">Para saber mais, confira [Direcionamento e compatibilidade da plataforma Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="a1063-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="a1063-106">Se você estiver desenvolvendo um aplicativo do Windows Phone 8.1, o AD do Azure torna simples e direta para você tooauthenticate os usuários com suas contas do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a1063-106">If you're developing a Windows Phone 8.1 app, Azure AD makes it simple and straightforward for you tooauthenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="a1063-107">Ele também permite que seu aplicativo toosecurely consumir qualquer web API protegida pelo AD do Azure, como Olá APIs do Office 365 ou Olá API do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1063-107">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

> [!NOTE]
> <span data-ttu-id="a1063-108">Este exemplo de código usa ADAL v2.0.</span><span class="sxs-lookup"><span data-stu-id="a1063-108">This code sample uses ADAL v2.0.</span></span>  <span data-ttu-id="a1063-109">Para a tecnologia mais recente do hello, convém tooinstead tente nosso [Tutorial Universal do Windows usando v 3.0 ADAL](active-directory-devquickstarts-windowsstore.md).</span><span class="sxs-lookup"><span data-stu-id="a1063-109">For hello latest technology, you may want tooinstead try our [Windows Universal Tutorial using ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span></span>  <span data-ttu-id="a1063-110">Se, na verdade, você estiver criando um aplicativo para Windows Phone 8.1, esse é o lugar certo hello.</span><span class="sxs-lookup"><span data-stu-id="a1063-110">If you are indeed building an app for Windows Phone 8.1, this is hello right place.</span></span>  <span data-ttu-id="a1063-111">V 2.0 ADAL ainda tem suporte total e é hello forma recomendada de agianst desenvolvimento de aplicativos Windows Phone 8.1 usando o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1063-111">ADAL v2.0 is still fully supported, and is hello recommended way of developing apps agianst Windows Phone 8.1 using Azure AD.</span></span>
> 
> 

<span data-ttu-id="a1063-112">Para clientes nativos .NET que necessitam de recursos tooaccess protegido, o AD do Azure fornece Olá biblioteca de autenticação do Active Directory ou ADAL.</span><span class="sxs-lookup"><span data-stu-id="a1063-112">For .NET native clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="a1063-113">Única finalidade do ADAL é toomake fácil para seus tokens de acesso do aplicativo tooget.</span><span class="sxs-lookup"><span data-stu-id="a1063-113">ADAL’s sole purpose in life is toomake it easy for your app tooget access tokens.</span></span>  <span data-ttu-id="a1063-114">toodemonstrate facilidade é, aqui, criaremos um "Pesquisador de diretório" aplicativo do Windows Phone 8.1 que:</span><span class="sxs-lookup"><span data-stu-id="a1063-114">toodemonstrate just how easy it is, here we’ll build a "Directory Searcher" Windows Phone 8.1 app that:</span></span>

* <span data-ttu-id="a1063-115">Obtém acesso tokens para chamar a API do Azure AD Graph hello usando Olá [protocolo de autenticação OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="a1063-115">Gets access tokens for calling hello Azure AD Graph API using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="a1063-116">Pesquisa um diretório para usuários com um determinado UPN.</span><span class="sxs-lookup"><span data-stu-id="a1063-116">Searches a directory for users with a given UPN.</span></span>
* <span data-ttu-id="a1063-117">Desconecta usuários.</span><span class="sxs-lookup"><span data-stu-id="a1063-117">Signs users out.</span></span>

<span data-ttu-id="a1063-118">aplicativo de trabalho concluída hello de toobuild, você precisará:</span><span class="sxs-lookup"><span data-stu-id="a1063-118">toobuild hello complete working application, you’ll need to:</span></span>

1. <span data-ttu-id="a1063-119">Registrar seu aplicativo no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1063-119">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="a1063-120">Instalar e configurar a ADAL.</span><span class="sxs-lookup"><span data-stu-id="a1063-120">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="a1063-121">Use ADAL tooget tokens do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1063-121">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="a1063-122">tooget iniciado, [baixar um projeto de esqueleto](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) ou [baixar exemplo hello concluída](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="a1063-122">tooget started, [download a skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="a1063-123">Cada um é uma solução do Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="a1063-123">Each is a Visual Studio 2013 solution.</span></span>  <span data-ttu-id="a1063-124">Você também precisará de um locatário do AD do Azure no qual você possa criar usuários e registrar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a1063-124">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="a1063-125">Se você ainda não tiver um locatário, [Saiba como tooget uma](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="a1063-125">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-hello-directory-searcher-application"></a><span data-ttu-id="a1063-126">1. Registrar Olá aplicativo do Pesquisador de diretório</span><span class="sxs-lookup"><span data-stu-id="a1063-126">1. Register hello Directory Searcher Application</span></span>
<span data-ttu-id="a1063-127">tooenable tokens de tooget seu aplicativo, primeiro será necessário tooregistê-lo no AD do Azure locatário e atribuí-lo Olá tooaccess de permissão do Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="a1063-127">tooenable your app tooget tokens, you’ll first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="a1063-128">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a1063-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a1063-129">Na barra superior do hello, clique em sua conta e em Olá **diretório** , escolha um locatário do Active Directory Olá onde você deseja tooregister seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a1063-129">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="a1063-130">Clique em **mais serviços** Olá navegação à esquerda e escolha **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="a1063-130">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="a1063-131">Clique em **Registros do Aplicativo** e escolha **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a1063-131">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="a1063-132">Siga os prompts de saudação e criar um novo **aplicativo cliente nativo**.</span><span class="sxs-lookup"><span data-stu-id="a1063-132">Follow hello prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="a1063-133">Olá **nome** da saudação aplicativo descrevem os usuários tooend de aplicativos</span><span class="sxs-lookup"><span data-stu-id="a1063-133">hello **Name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="a1063-134">Olá **Uri de redirecionamento** é uma combinação de esquema e a cadeia de caracteres que o AD do Azure usará tooreturn respostas de token.</span><span class="sxs-lookup"><span data-stu-id="a1063-134">hello **Redirect Uri** is a scheme and string combination that Azure AD will use tooreturn token responses.</span></span>  <span data-ttu-id="a1063-135">Insira um valor de espaço reservado por enquanto, por exemplo, `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="a1063-135">Enter a placeholder value for now, e.g. `http://DirectorySearcher`.</span></span>  <span data-ttu-id="a1063-136">Substituiremos este valor posteriormente.</span><span class="sxs-lookup"><span data-stu-id="a1063-136">We'll replace this value later.</span></span>
6. <span data-ttu-id="a1063-137">Depois de concluir o registro, o AAD atribuirá a seu aplicativo uma ID do Aplicativo única.</span><span class="sxs-lookup"><span data-stu-id="a1063-137">Once you’ve completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="a1063-138">Você precisará desse valor nas seções de Avançar hello, portanto copiá-lo do guia do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a1063-138">You’ll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="a1063-139">De saudação **configurações** escolha **permissões necessárias** e escolha **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a1063-139">From hello **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="a1063-140">Selecione Olá **Microsoft Graph** como Olá API e adicione Olá **ler dados do diretório** permissão em **permissões delegadas**.</span><span class="sxs-lookup"><span data-stu-id="a1063-140">Select hello **Microsoft Graph** as hello API and add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="a1063-141">Isso permitirá a saudação de tooquery aplicativo Graph API para os usuários.</span><span class="sxs-lookup"><span data-stu-id="a1063-141">This will enable your application tooquery hello Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="a1063-142">2. Instalar e Configurar o ADAL</span><span class="sxs-lookup"><span data-stu-id="a1063-142">2. Install & Configure ADAL</span></span>
<span data-ttu-id="a1063-143">Agora que você tem um aplicativo no AD do Azure, você pode instalar a ADAL e escrever seu código relacionado à identidade.</span><span class="sxs-lookup"><span data-stu-id="a1063-143">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="a1063-144">Para toocommunicate capaz de toobe ADAL com o Azure AD, é necessário tooprovide-lo com algumas informações sobre o registro do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a1063-144">In order for ADAL toobe able toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="a1063-145">Comece adicionando o projeto de DirectorySearcher toohello ADAL usando Olá Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="a1063-145">Begin by adding ADAL toohello DirectorySearcher project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="a1063-146">No projeto de DirectorySearcher hello, abra `MainPage.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="a1063-146">In hello DirectorySearcher project, open `MainPage.xaml.cs`.</span></span>  <span data-ttu-id="a1063-147">Substituir valores Olá Olá `Config Values` Olá de tooreflect região valores de entrada hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1063-147">Replace hello values in hello `Config Values` region tooreflect hello values you input into hello Azure Portal.</span></span>  <span data-ttu-id="a1063-148">Seu código fará referência a esses valores sempre que ele usar a ADAL.</span><span class="sxs-lookup"><span data-stu-id="a1063-148">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="a1063-149">Olá `tenant` é o domínio de saudação do seu locatário do AD do Azure, por exemplo, contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="a1063-149">hello `tenant` is hello domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="a1063-150">Olá `clientId` é Olá clientId do aplicativo é copiada do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="a1063-150">hello `clientId` is hello clientId of your application you copied from hello portal.</span></span>
* <span data-ttu-id="a1063-151">Uri de retorno de chamada de saudação toodiscover agora é necessário para seu aplicativo do Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="a1063-151">You now need toodiscover hello callback uri for your Windows Phone app.</span></span>  <span data-ttu-id="a1063-152">Defina um ponto de interrupção nessa linha em Olá `MainPage` método:</span><span class="sxs-lookup"><span data-stu-id="a1063-152">Set a breakpoint on this line in hello `MainPage` method:</span></span>

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* <span data-ttu-id="a1063-153">Executar o aplicativo hello e separar copiar valor de saudação do `redirectUri` quando Olá ponto de interrupção.</span><span class="sxs-lookup"><span data-stu-id="a1063-153">Run hello app, and copy aside hello value of `redirectUri` when hello breakpoint is hit.</span></span>  <span data-ttu-id="a1063-154">O resultado deve ser semelhante a</span><span class="sxs-lookup"><span data-stu-id="a1063-154">It should look something like</span></span>

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* <span data-ttu-id="a1063-155">Em Olá **configurar** guia do seu aplicativo em Olá Portal de gerenciamento do Azure, substitua o valor de saudação de saudação **RedirectUri** com esse valor.</span><span class="sxs-lookup"><span data-stu-id="a1063-155">Back on hello **Configure** tab of your application in hello Azure Management Portal, replace hello value of hello **RedirectUri** with this value.</span></span>  

## <a name="3-use-adal-tooget-tokens-from-aad"></a><span data-ttu-id="a1063-156">3. Usar Tokens tooGet ADAL do AAD</span><span class="sxs-lookup"><span data-stu-id="a1063-156">3. Use ADAL tooGet Tokens from AAD</span></span>
<span data-ttu-id="a1063-157">Olá princípio básico de ADAL é que sempre que seu aplicativo precisa de um token de acesso, ele simplesmente chama `authContext.AcquireToken(…)`, e ADAL Olá rest.</span><span class="sxs-lookup"><span data-stu-id="a1063-157">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does hello rest.</span></span>  

* <span data-ttu-id="a1063-158">primeira etapa de saudação é tooinitialize seu aplicativo `AuthenticationContext` -ADAL da classe principal.</span><span class="sxs-lookup"><span data-stu-id="a1063-158">hello first step is tooinitialize your app’s `AuthenticationContext` - ADAL’s primary class.</span></span>  <span data-ttu-id="a1063-159">Isso é onde você passa ADAL Olá coordenadas necessárias toocommunicate com o Azure AD e informe como toocache tokens.</span><span class="sxs-lookup"><span data-stu-id="a1063-159">This is where you pass ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* <span data-ttu-id="a1063-160">Localizar agora Olá `Search(...)` método, que será invocado quando Olá usuário cliks hello "Pesquisar" botão na interface de usuário do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a1063-160">Now locate hello `Search(...)` method, which will be invoked when hello user cliks hello "Search" button in hello app's UI.</span></span>  <span data-ttu-id="a1063-161">Esse método torna um tooquery de toohello do Azure AD Graph API de solicitação GET para usuários cujo UPN começa com hello dado o termo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="a1063-161">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="a1063-162">Mas em Olá de tooquery ordem API do Graph, você precisa tooinclude um access_token no hello `Authorization` cabeçalho da saudação solicitar - onde ADAL é.</span><span class="sxs-lookup"><span data-stu-id="a1063-162">But in order tooquery hello Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try tooget a token without triggering any user prompt.
    // ADAL will check whether hello requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained hello QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* <span data-ttu-id="a1063-163">Se a autenticação interativa é necessária, ADAL usará o agente de autenticação de Web (WAB) do Windows Phone e [modelo continuação](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) na página de logon toodisplay Olá AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1063-163">If interactive authentication is necessary, ADAL will use Windows Phone's Web Authentication Broker (WAB) and [continuation model](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) toodisplay hello Azure AD sign in page.</span></span>  <span data-ttu-id="a1063-164">Quando Olá usuário faz logon, seu aplicativo precisa resultados de saudação ADAL toopass de interação de WAB hello.</span><span class="sxs-lookup"><span data-stu-id="a1063-164">When hello user signs in, your app needs toopass ADAL hello results of hello WAB interaction.</span></span>  <span data-ttu-id="a1063-165">Isso é tão simple quanto implementando Olá `ContinueWebAuthentication` interface:</span><span class="sxs-lookup"><span data-stu-id="a1063-165">This is as simple as implementing hello `ContinueWebAuthentication` interface:</span></span>

```C#
// This method is automatically invoked when hello application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass hello authentication interaction results tooADAL, which will
    // conclude hello token acquisition operation and invoke hello callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* <span data-ttu-id="a1063-166">Agora é saudação do tempo toouse `AuthenticationResult` que ADAL retornado tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a1063-166">Now it's time toouse hello `AuthenticationResult` that ADAL returned tooyour app.</span></span>  <span data-ttu-id="a1063-167">Em Olá `QueryGraph(...)` retorno de chamada, anexar access_token Olá adquirido toohello GET solicitação no cabeçalho de autorização hello:</span><span class="sxs-lookup"><span data-stu-id="a1063-167">In hello `QueryGraph(...)` callback, attach hello access_token you acquired toohello GET request in hello Authorization header:</span></span>

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add hello access token toohello Authorization Header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* <span data-ttu-id="a1063-168">Você também pode usar o hello `AuthenticationResult` toodisplay informações sobre o usuário Olá em seu aplicativo do objeto.</span><span class="sxs-lookup"><span data-stu-id="a1063-168">You can also use hello `AuthenticationResult` object toodisplay information about hello user in your app.</span></span> <span data-ttu-id="a1063-169">Em Olá `QueryGraph(...)` método, a id do usuário do hello tooshow resultados use Olá na página de saudação:</span><span class="sxs-lookup"><span data-stu-id="a1063-169">In hello `QueryGraph(...)` method, use hello result tooshow hello user's id on hello page:</span></span>

```C#
// Update hello Page UI toorepresent hello signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* <span data-ttu-id="a1063-170">Por fim, você pode usar o usuário de saudação toosign ADAL do aplicativo também.</span><span class="sxs-lookup"><span data-stu-id="a1063-170">Finally, you can use ADAL toosign hello user out of hte application as well.</span></span>  <span data-ttu-id="a1063-171">Quando o usuário Olá clica hello "Sair" botão, queremos tooensure que Olá próxima chamada muito`AcquireTokenSilentAsync(...)` falhará.</span><span class="sxs-lookup"><span data-stu-id="a1063-171">When hello user clicks hello "Sign Out" button, we want tooensure that hello next call too`AcquireTokenSilentAsync(...)` will fail.</span></span>  <span data-ttu-id="a1063-172">ADAL, isso é tão fácil quanto limpar o cache de token hello:</span><span class="sxs-lookup"><span data-stu-id="a1063-172">With ADAL, this is as easy as clearing hello token cache:</span></span>

```C#
private void SignOut()
{
    // Clear session state from hello token cache.
    authContext.TokenCache.Clear();

    ...
}
```

<span data-ttu-id="a1063-173">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="a1063-173">Congratulations!</span></span> <span data-ttu-id="a1063-174">Você agora tem um aplicativo do Windows Phone que tem Olá capacidade tooauthenticate usuários de trabalho com segurança chamar APIs da Web usando o OAuth 2.0 e obter informações básicas sobre o usuário hello.</span><span class="sxs-lookup"><span data-stu-id="a1063-174">You now have a working Windows Phone app that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="a1063-175">Se você ainda não fez isso, agora é Olá tempo toopopulate seu locatário com alguns usuários.</span><span class="sxs-lookup"><span data-stu-id="a1063-175">If you haven’t already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="a1063-176">Execute o aplicativo DirectorySearcher e faça logon com um desses usuários.</span><span class="sxs-lookup"><span data-stu-id="a1063-176">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="a1063-177">Procure por outros usuários com base em seus UPNs.</span><span class="sxs-lookup"><span data-stu-id="a1063-177">Search for other users based on their UPN.</span></span>  <span data-ttu-id="a1063-178">Feche o aplicativo hello e execute-a novamente.</span><span class="sxs-lookup"><span data-stu-id="a1063-178">Close hello app, and re-run it.</span></span>  <span data-ttu-id="a1063-179">Observe como a sessão do usuário Olá permanece intacta.</span><span class="sxs-lookup"><span data-stu-id="a1063-179">Notice how hello user’s session remains intact.</span></span>  <span data-ttu-id="a1063-180">Saia e faça logon novamente como outro usuário.</span><span class="sxs-lookup"><span data-stu-id="a1063-180">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="a1063-181">ADAL torna fácil tooincorporate todos esses recursos comuns de identidade em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a1063-181">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="a1063-182">Cuida de todo o trabalho sujo Olá para você - gerenciamento de cache, suporte ao protocolo OAuth, apresentando usuário Olá com um logon de interface do usuário, atualizando tokens expirados e muito mais.</span><span class="sxs-lookup"><span data-stu-id="a1063-182">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="a1063-183">Tudo o que você realmente precisa de tooknow é uma única chamada de API, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="a1063-183">All you really need tooknow is a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="a1063-184">Para referência, o exemplo hello concluída (sem os valores de configuração) é fornecido [aqui](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="a1063-184">For reference, hello completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="a1063-185">Agora você pode mover tooadditional cenários de identidade.</span><span class="sxs-lookup"><span data-stu-id="a1063-185">You can now move on tooadditional identity scenarios.</span></span>  <span data-ttu-id="a1063-186">Você pode desejar tootry:</span><span class="sxs-lookup"><span data-stu-id="a1063-186">You may want tootry:</span></span>

[<span data-ttu-id="a1063-187">Proteger uma API da Web .NET com o Azure AD >></span><span class="sxs-lookup"><span data-stu-id="a1063-187">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

