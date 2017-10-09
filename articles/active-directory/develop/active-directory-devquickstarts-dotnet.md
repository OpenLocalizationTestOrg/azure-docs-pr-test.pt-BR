---
title: ".NET aaaAzure AD Introdução | Microsoft Docs"
description: Como toobuild um aplicativo de Desktop do Windows .NET que se integra ao AD do Azure para entrar e chama o AD do Azure usando o OAuth APIs protegidas.
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
ms.openlocfilehash: c09b358f24c7bfb371b34cf72ca48c0a45042f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a><span data-ttu-id="4908b-103">Integrar o AD do Azure em um aplicativo WPF de área de trabalho do Windows</span><span class="sxs-lookup"><span data-stu-id="4908b-103">Integrate Azure AD into a Windows Desktop WPF App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="4908b-104">Se você estiver desenvolvendo um aplicativo de área de trabalho, o AD do Azure torna simples e direta para você tooauthenticate os usuários com suas contas do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4908b-104">If you're developing a desktop application, Azure AD makes it simple and straightforward for you tooauthenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="4908b-105">Ele também permite que seu aplicativo toosecurely consumir qualquer web API protegida pelo AD do Azure, como Olá APIs do Office 365 ou Olá API do Azure.</span><span class="sxs-lookup"><span data-stu-id="4908b-105">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="4908b-106">Para clientes nativos .NET que necessitam de recursos tooaccess protegido, o AD do Azure fornece Olá biblioteca de autenticação do Active Directory ou ADAL.</span><span class="sxs-lookup"><span data-stu-id="4908b-106">For .NET native clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="4908b-107">Única finalidade do ADAL é toomake fácil para seus tokens de acesso do aplicativo tooget.</span><span class="sxs-lookup"><span data-stu-id="4908b-107">ADAL's sole purpose in life is toomake it easy for your app tooget access tokens.</span></span>  <span data-ttu-id="4908b-108">toodemonstrate facilidade é, aqui, criaremos um aplicativo de lista de tarefas do .NET WPF que:</span><span class="sxs-lookup"><span data-stu-id="4908b-108">toodemonstrate just how easy it is, here we'll build a .NET WPF To-Do List application that:</span></span>

* <span data-ttu-id="4908b-109">Obtém acesso tokens para chamar a API do Azure AD Graph hello usando Olá [protocolo de autenticação OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="4908b-109">Gets access tokens for calling hello Azure AD Graph API using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="4908b-110">Pesquisa um diretório para usuários com um determinado alias.</span><span class="sxs-lookup"><span data-stu-id="4908b-110">Searches a directory for users with a given alias.</span></span>
* <span data-ttu-id="4908b-111">Desconecta usuários.</span><span class="sxs-lookup"><span data-stu-id="4908b-111">Signs users out.</span></span>

<span data-ttu-id="4908b-112">aplicativo de trabalho concluída hello de toobuild, você precisará:</span><span class="sxs-lookup"><span data-stu-id="4908b-112">toobuild hello complete working application, you'll need to:</span></span>

1. <span data-ttu-id="4908b-113">Registrar seu aplicativo no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4908b-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="4908b-114">Instalar e configurar a ADAL.</span><span class="sxs-lookup"><span data-stu-id="4908b-114">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="4908b-115">Use ADAL tooget tokens do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4908b-115">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="4908b-116">tooget iniciado, [baixar o esqueleto do aplicativo hello](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) ou [baixar exemplo hello concluída](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="4908b-116">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="4908b-117">Você também precisará de um locatário do AD do Azure no qual você possa criar usuários e registrar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4908b-117">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="4908b-118">Se você ainda não tiver um locatário, [Saiba como tooget uma](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="4908b-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-hello-directorysearcher-application"></a><span data-ttu-id="4908b-119">1. Registrar Olá DirectorySearcher aplicativo</span><span class="sxs-lookup"><span data-stu-id="4908b-119">1. Register hello DirectorySearcher Application</span></span>
<span data-ttu-id="4908b-120">tooenable tokens de tooget seu aplicativo, primeiro será necessário tooregistê-lo no AD do Azure locatário e atribuí-lo Olá tooaccess de permissão do Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="4908b-120">tooenable your app tooget tokens, you'll first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="4908b-121">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4908b-121">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4908b-122">Na barra superior do hello, clique em sua conta e em Olá **diretório** , escolha um locatário do Active Directory Olá onde você deseja tooregister seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4908b-122">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="4908b-123">Clique em **mais serviços** Olá navegação à esquerda e escolha **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="4908b-123">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="4908b-124">Clique em **Registros do Aplicativo** e escolha **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4908b-124">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="4908b-125">Siga os prompts de saudação e criar um novo **aplicativo cliente nativo**.</span><span class="sxs-lookup"><span data-stu-id="4908b-125">Follow hello prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="4908b-126">Olá **nome** da saudação aplicativo descrevem os usuários tooend de aplicativos</span><span class="sxs-lookup"><span data-stu-id="4908b-126">hello **Name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="4908b-127">Olá **Uri de redirecionamento** é uma combinação de esquema e a cadeia de caracteres que o AD do Azure usará tooreturn respostas de token.</span><span class="sxs-lookup"><span data-stu-id="4908b-127">hello **Redirect Uri** is a scheme and string combination that Azure AD will use tooreturn token responses.</span></span>  <span data-ttu-id="4908b-128">Insira um aplicativo de tooyour específico de valor, por exemplo, `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="4908b-128">Enter a value specific tooyour application, e.g. `http://DirectorySearcher`.</span></span>
6. <span data-ttu-id="4908b-129">Depois de concluir o registro, o AAD atribuirá a seu aplicativo uma ID do Aplicativo única.</span><span class="sxs-lookup"><span data-stu-id="4908b-129">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="4908b-130">Você precisará desse valor nas seções de Avançar Olá, portanto copie-o da página de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="4908b-130">You'll need this value in hello next sections, so copy it from hello application page.</span></span>
7. <span data-ttu-id="4908b-131">De saudação **configurações** escolha **permissões necessárias** e escolha **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4908b-131">From hello **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="4908b-132">Selecione Olá **Microsoft Graph** como Olá API e adicione Olá **ler dados do diretório** permissão em **permissões delegadas**.</span><span class="sxs-lookup"><span data-stu-id="4908b-132">Select hello **Microsoft Graph** as hello API and add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="4908b-133">Isso permitirá a saudação de tooquery aplicativo Graph API para os usuários.</span><span class="sxs-lookup"><span data-stu-id="4908b-133">This will enable your application tooquery hello Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="4908b-134">2. Instalar e Configurar o ADAL</span><span class="sxs-lookup"><span data-stu-id="4908b-134">2. Install & Configure ADAL</span></span>
<span data-ttu-id="4908b-135">Agora que você tem um aplicativo no AD do Azure, você pode instalar a ADAL e escrever seu código relacionado à identidade.</span><span class="sxs-lookup"><span data-stu-id="4908b-135">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="4908b-136">Para toocommunicate capaz de toobe ADAL com o Azure AD, é necessário tooprovide-lo com algumas informações sobre o registro do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4908b-136">In order for ADAL toobe able toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="4908b-137">Comece adicionando o projeto de DirectorySearcher toohello ADAL usando Olá Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="4908b-137">Begin by adding ADAL toohello DirectorySearcher project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="4908b-138">No projeto de DirectorySearcher hello, abra `app.config`.</span><span class="sxs-lookup"><span data-stu-id="4908b-138">In hello DirectorySearcher project, open `app.config`.</span></span>  <span data-ttu-id="4908b-139">Substituir valores de saudação de elementos Olá Olá `<appSettings>` Olá de tooreflect seção valores de entrada hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4908b-139">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values you input into hello Azure Portal.</span></span>  <span data-ttu-id="4908b-140">Seu código fará referência a esses valores sempre que ele usar a ADAL.</span><span class="sxs-lookup"><span data-stu-id="4908b-140">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="4908b-141">Olá `ida:Tenant` é o domínio de saudação do seu locatário do AD do Azure, por exemplo, contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="4908b-141">hello `ida:Tenant` is hello domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="4908b-142">Olá `ida:ClientId` é Olá clientId do aplicativo é copiada do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="4908b-142">hello `ida:ClientId` is hello clientId of your application you copied from hello portal.</span></span>
  * <span data-ttu-id="4908b-143">Olá `ida:RedirectUri` é hello registrado no portal de saudação do url de redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="4908b-143">hello `ida:RedirectUri` is hello redirect url you registered in hello portal.</span></span>

## <a name="3----use-adal-tooget-tokens-from-aad"></a><span data-ttu-id="4908b-144">3.    Usar Tokens tooGet ADAL do AAD</span><span class="sxs-lookup"><span data-stu-id="4908b-144">3.    Use ADAL tooGet Tokens from AAD</span></span>
<span data-ttu-id="4908b-145">Olá princípio básico de ADAL é que sempre que seu aplicativo precisa de um token de acesso, ele simplesmente chama `authContext.AcquireTokenAsync(...)`, e ADAL Olá rest.</span><span class="sxs-lookup"><span data-stu-id="4908b-145">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireTokenAsync(...)`, and ADAL does hello rest.</span></span>  

* <span data-ttu-id="4908b-146">Em Olá `DirectorySearcher` projeto, abra `MainWindow.xaml.cs` e localize Olá `MainWindow()` método.</span><span class="sxs-lookup"><span data-stu-id="4908b-146">In hello `DirectorySearcher` project, open `MainWindow.xaml.cs` and locate hello `MainWindow()` method.</span></span>  <span data-ttu-id="4908b-147">primeira etapa de saudação é tooinitialize seu aplicativo `AuthenticationContext` -ADAL da classe principal.</span><span class="sxs-lookup"><span data-stu-id="4908b-147">hello first step is tooinitialize your app's `AuthenticationContext` - ADAL's primary class.</span></span>  <span data-ttu-id="4908b-148">Isso é onde você passa ADAL Olá coordenadas necessárias toocommunicate com o Azure AD e informe como toocache tokens.</span><span class="sxs-lookup"><span data-stu-id="4908b-148">This is where you pass ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* <span data-ttu-id="4908b-149">Localizar agora Olá `Search(...)` método, que será invocado quando Olá usuário cliks hello "Pesquisar" botão na interface de usuário do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="4908b-149">Now locate hello `Search(...)` method, which will be invoked when hello user cliks hello "Search" button in hello app's UI.</span></span>  <span data-ttu-id="4908b-150">Esse método torna um tooquery de toohello do Azure AD Graph API de solicitação GET para usuários cujo UPN começa com hello dado o termo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="4908b-150">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="4908b-151">Mas em Olá de tooquery ordem API do Graph, você precisa tooinclude um access_token no hello `Authorization` cabeçalho da saudação solicitar - onde ADAL é.</span><span class="sxs-lookup"><span data-stu-id="4908b-151">But in order tooquery hello Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate hello Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for hello tooDo item name");
        return;
    }

    // Get an Access Token for hello Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled hello sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* <span data-ttu-id="4908b-152">Quando o aplicativo solicita um token chamando `AcquireTokenAsync(...)`, ADAL tentará tooreturn um token sem solicitar credenciais de usuário hello.</span><span class="sxs-lookup"><span data-stu-id="4908b-152">When your app requests a token by calling `AcquireTokenAsync(...)`, ADAL will attempt tooreturn a token without asking hello user for credentials.</span></span>  <span data-ttu-id="4908b-153">Se ADAL determina que o usuário Olá precisa toosign em tooget um token, ele exibe uma caixa de diálogo de logon, coletar credenciais de saudação do usuário e retorna um token após a autenticação bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="4908b-153">If ADAL determines that hello user needs toosign in tooget a token, it will display a login dialog, collect hello user's credentials, and return a token upon successful authentication.</span></span>  <span data-ttu-id="4908b-154">Se o ADAL está tooreturn não é possível um token por qualquer motivo, ela irá gerar um `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="4908b-154">If ADAL is unable tooreturn a token for any reason, it will throw an `AdalException`.</span></span>
* <span data-ttu-id="4908b-155">Observe que Olá `AuthenticationResult` objeto contém um `UserInfo` objeto que pode ser usado toocollect informações seu aplicativo pode ser necessário.</span><span class="sxs-lookup"><span data-stu-id="4908b-155">Notice that hello `AuthenticationResult` object contains a `UserInfo` object that can be used toocollect information your app may need.</span></span>  <span data-ttu-id="4908b-156">Em Olá DirectorySearcher, `UserInfo` é a interface do usuário do aplicativo de saudação toocustomize usado com a id de saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="4908b-156">In hello DirectorySearcher, `UserInfo` is used toocustomize hello app's UI with hello user's id.</span></span>
* <span data-ttu-id="4908b-157">Quando o usuário Olá clica hello "Sair" botão, queremos tooensure que Olá próxima chamada muito`AcquireTokenAsync(...)` pedirá Olá usuário toosign no.</span><span class="sxs-lookup"><span data-stu-id="4908b-157">When hello user clicks hello "Sign Out" button, we want tooensure that hello next call too`AcquireTokenAsync(...)` will ask hello user toosign in.</span></span>  <span data-ttu-id="4908b-158">ADAL, isso é tão fácil quanto limpar o cache de token hello:</span><span class="sxs-lookup"><span data-stu-id="4908b-158">With ADAL, this is as easy as clearing hello token cache:</span></span>

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear hello token cache
    authContext.TokenCache.Clear();

    ...
}
```

* <span data-ttu-id="4908b-159">No entanto, se o usuário Olá não botão hello "Sair", você desejará toomaintain Olá sessão de usuário para Olá próxima vez que executar Olá DirectorySearcher.</span><span class="sxs-lookup"><span data-stu-id="4908b-159">However, if hello user does not click hello "Sign Out" button, you will want toomaintain hello user's session for hello next time they run hello DirectorySearcher.</span></span>  <span data-ttu-id="4908b-160">Quando o aplicativo hello é iniciado, você pode verificar o cache de token do ADAL para um token existente e atualize o hello da interface do usuário adequadamente.</span><span class="sxs-lookup"><span data-stu-id="4908b-160">When hello app launches, you can check ADAL's token cache for an existing token and update hello UI accordingly.</span></span>  <span data-ttu-id="4908b-161">Em Olá `CheckForCachedToken()` método, fazer outra chamada muito`AcquireTokenAsync(...)`, desta vez passando Olá `PromptBehavior.Never` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="4908b-161">In hello `CheckForCachedToken()` method, make another call too`AcquireTokenAsync(...)`, this time passing in hello `PromptBehavior.Never` parameter.</span></span>  <span data-ttu-id="4908b-162">`PromptBehavior.Never`informará ADAL que usuário Olá não deve ser solicitado para entrar e ADAL em vez disso, gerar uma exceção se for tooreturn não é possível um token.</span><span class="sxs-lookup"><span data-stu-id="4908b-162">`PromptBehavior.Never` will tell ADAL that hello user should not be prompted for sign in, and ADAL should instead throw an exception if it is unable tooreturn a token.</span></span>

```C#
public async void CheckForCachedToken() 
{
    // As hello application starts, try tooget an access token without prompting hello user.  If one exists, show hello user as signed in.
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

        // If user interaction is required, proceed toomain page without singing hello user in.
        return;
    }

    // A valid token is in hello cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

<span data-ttu-id="4908b-163">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="4908b-163">Congratulations!</span></span> <span data-ttu-id="4908b-164">Você agora tem um aplicativo .NET WPF que tem Olá capacidade tooauthenticate usuários de trabalho, com segurança chamar APIs da Web usando o OAuth 2.0 e obter informações básicas sobre o usuário Olá.</span><span class="sxs-lookup"><span data-stu-id="4908b-164">You now have a working .NET WPF application that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="4908b-165">Se você ainda não fez isso, agora é Olá tempo toopopulate seu locatário com alguns usuários.</span><span class="sxs-lookup"><span data-stu-id="4908b-165">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="4908b-166">Execute o aplicativo DirectorySearcher e faça logon com um desses usuários.</span><span class="sxs-lookup"><span data-stu-id="4908b-166">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="4908b-167">Procure por outros usuários com base em seus UPNs.</span><span class="sxs-lookup"><span data-stu-id="4908b-167">Search for other users based on their UPN.</span></span>  <span data-ttu-id="4908b-168">Feche o aplicativo hello e execute-a novamente.</span><span class="sxs-lookup"><span data-stu-id="4908b-168">Close hello app, and re-run it.</span></span>  <span data-ttu-id="4908b-169">Observe como a sessão do usuário Olá permanece intacta.</span><span class="sxs-lookup"><span data-stu-id="4908b-169">Notice how hello user's session remains intact.</span></span>  <span data-ttu-id="4908b-170">Saia e faça logon novamente como outro usuário.</span><span class="sxs-lookup"><span data-stu-id="4908b-170">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="4908b-171">ADAL torna fácil tooincorporate todos esses recursos comuns de identidade em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4908b-171">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="4908b-172">Cuida de todo o trabalho sujo Olá para você - gerenciamento de cache, suporte ao protocolo OAuth, apresentando usuário Olá com um logon de interface do usuário, atualizando tokens expirados e muito mais.</span><span class="sxs-lookup"><span data-stu-id="4908b-172">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="4908b-173">Tudo o que você realmente precisa de tooknow é uma única chamada de API, `authContext.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="4908b-173">All you really need tooknow is a single API call, `authContext.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="4908b-174">Para referência, o exemplo hello concluída (sem os valores de configuração) é fornecido [aqui](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="4908b-174">For reference, hello completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="4908b-175">Agora você pode mover tooadditional cenários.</span><span class="sxs-lookup"><span data-stu-id="4908b-175">You can now move on tooadditional scenarios.</span></span>  <span data-ttu-id="4908b-176">Você pode desejar tootry:</span><span class="sxs-lookup"><span data-stu-id="4908b-176">You may want tootry:</span></span>

[<span data-ttu-id="4908b-177">Proteger uma API da Web .NET com o Azure AD >></span><span class="sxs-lookup"><span data-stu-id="4908b-177">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

