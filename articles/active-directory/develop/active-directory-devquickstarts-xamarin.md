---
title: "aaaAzure AD Xamarin Introdução | Microsoft Docs"
description: Crie aplicativos Xamarin que se integrem ao Azure AD para entrar e chame APIs protegidas do Azure AD usando OAuth.
services: active-directory
documentationcenter: xamarin
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 198cd2c3-f7c8-4ec2-b59d-dfdea9fe7d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 6a0d189648b7071558ac1cf2b908808668960a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a><span data-ttu-id="92533-103">Integrar o Azure AD com aplicativos Xamarin</span><span class="sxs-lookup"><span data-stu-id="92533-103">Integrate Azure AD with Xamarin apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="92533-104">Com o Xamarin, você pode gravar aplicativos móveis em C# que podem ser executados no iOS, no Android e no Windows (dispositivos móveis e computadores).</span><span class="sxs-lookup"><span data-stu-id="92533-104">With Xamarin, you can write mobile apps in C# that can run on iOS, Android, and Windows (mobile devices and PCs).</span></span> <span data-ttu-id="92533-105">Se você estiver criando um aplicativo usando o Xamarin, Azure Active Directory (AD do Azure) torna simples tooauthenticate usuários com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="92533-105">If you're building an app using Xamarin, Azure Active Directory (Azure AD) makes it simple tooauthenticate users with their Azure AD accounts.</span></span> <span data-ttu-id="92533-106">aplicativo Hello também com segurança pode consumir qualquer API da web protegido pelo AD do Azure, como Olá APIs do Office 365 ou hello API do Azure.</span><span class="sxs-lookup"><span data-stu-id="92533-106">hello app can also securely consume any web API that's protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="92533-107">Para aplicativos Xamarin que necessitam de recursos tooaccess protegido, o AD do Azure fornece Olá biblioteca de autenticação do Active Directory (ADAL).</span><span class="sxs-lookup"><span data-stu-id="92533-107">For Xamarin apps that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="92533-108">Olá única finalidade ADAL é toomake fácil para tokens de acesso de tooget de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="92533-108">hello sole purpose of ADAL is toomake it easy for apps tooget access tokens.</span></span> <span data-ttu-id="92533-109">toodemonstrate fácil é, este artigo mostra como toobuild DirectorySearcher aplicativos que:</span><span class="sxs-lookup"><span data-stu-id="92533-109">toodemonstrate how easy it is, this article shows how toobuild DirectorySearcher apps that:</span></span>

* <span data-ttu-id="92533-110">Execute no iOS, no Android, na Área de Trabalho do Windows, no Windows Phone e na Windows Store.</span><span class="sxs-lookup"><span data-stu-id="92533-110">Run on iOS, Android, Windows Desktop, Windows Phone, and Windows Store.</span></span>
* <span data-ttu-id="92533-111">Usar uma única classe portátil biblioteca (PCL) tooauthenticate usuários e obter tokens de saudação do Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="92533-111">Use a single portable class library (PCL) tooauthenticate users and get tokens for hello Azure AD Graph API.</span></span>
* <span data-ttu-id="92533-112">Pesquise um diretório para usuários com um determinado UPN.</span><span class="sxs-lookup"><span data-stu-id="92533-112">Search a directory for users with a given UPN.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="92533-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="92533-113">Before you get started</span></span>
* <span data-ttu-id="92533-114">Baixar Olá [projeto esqueleto](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), ou baixar Olá [exemplo concluído](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="92533-114">Download hello [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), or download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="92533-115">Cada download é uma solução do Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="92533-115">Each download is a Visual Studio 2013 solution.</span></span>
* <span data-ttu-id="92533-116">Também é necessário um locatário Azure AD no qual usuários toocreate e registrar o aplicativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="92533-116">You also need an Azure AD tenant in which toocreate users and register hello app.</span></span> <span data-ttu-id="92533-117">Se você ainda não tiver um locatário, [Saiba como tooget uma](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="92533-117">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="92533-118">Quando você estiver pronto, siga Olá procedimentos Olá quatro seções.</span><span class="sxs-lookup"><span data-stu-id="92533-118">When you are ready, follow hello procedures in hello next four sections.</span></span>

## <a name="step-1-set-up-your-xamarin-development-environment"></a><span data-ttu-id="92533-119">Etapa 1: Configurar seu ambiente de desenvolvimento do Xamarin</span><span class="sxs-lookup"><span data-stu-id="92533-119">Step 1: Set up your Xamarin development environment</span></span>
<span data-ttu-id="92533-120">Como este tutorial inclui projetos para iOS, Android e Windows, são necessários o Visual Studio e o Xamarin.</span><span class="sxs-lookup"><span data-stu-id="92533-120">Because this tutorial includes projects for iOS, Android, and Windows, you need both Visual Studio and Xamarin.</span></span> <span data-ttu-id="92533-121">ambiente necessário toocreate hello, processo Olá completa em [definido para cima e instalar o Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) no MSDN.</span><span class="sxs-lookup"><span data-stu-id="92533-121">toocreate hello necessary environment, complete hello process in [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) on MSDN.</span></span> <span data-ttu-id="92533-122">instruções de saudação incluem material de que você pode examinar toolearn mais sobre Xamarin enquanto você aguarda para Olá instalações toobe concluída.</span><span class="sxs-lookup"><span data-stu-id="92533-122">hello instructions include material that you can review toolearn more about Xamarin while you're waiting for hello installations toobe completed.</span></span>

<span data-ttu-id="92533-123">Depois de concluir a instalação hello, abra a solução de saudação no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="92533-123">After you've completed hello setup, open hello solution in Visual Studio.</span></span> <span data-ttu-id="92533-124">Lá, você encontrará seis projetos: cinco projetos específicos de plataforma e um PCL, DirectorySearcher.cs, que será compartilhado entre todas as plataformas.</span><span class="sxs-lookup"><span data-stu-id="92533-124">There, you will find six projects: five platform-specific projects and one PCL, DirectorySearcher.cs, which will be shared across all platforms.</span></span>

## <a name="step-2-register-hello-directorysearcher-app"></a><span data-ttu-id="92533-125">Etapa 2: Registrar o aplicativo de DirectorySearcher Olá</span><span class="sxs-lookup"><span data-stu-id="92533-125">Step 2: Register hello DirectorySearcher app</span></span>
<span data-ttu-id="92533-126">tokens de tooget do tooenable Olá aplicativo, primeiro é necessário tooregistê-lo no AD do Azure locatário e conceda a ela Olá tooaccess de permissão do Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="92533-126">tooenable hello app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API.</span></span> <span data-ttu-id="92533-127">Faça assim:</span><span class="sxs-lookup"><span data-stu-id="92533-127">Here's how:</span></span>

1. <span data-ttu-id="92533-128">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="92533-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="92533-129">Na barra superior do hello, clique em sua conta.</span><span class="sxs-lookup"><span data-stu-id="92533-129">On hello top bar, click your account.</span></span> <span data-ttu-id="92533-130">Em seguida, em Olá **diretório** lista, o locatário do Active Directory hello selecione onde você deseja que o aplicativo de saudação tooregister.</span><span class="sxs-lookup"><span data-stu-id="92533-130">Then, under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="92533-131">Clique em **mais serviços** Olá painel esquerdo e, em seguida, selecione **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="92533-131">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="92533-132">Clique em **Registros do aplicativo** e, em seguida, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="92533-132">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="92533-133">toocreate um novo **aplicativo cliente nativo**, siga os prompts de saudação.</span><span class="sxs-lookup"><span data-stu-id="92533-133">toocreate a new **Native Client Application**, follow hello prompts.</span></span>
  * <span data-ttu-id="92533-134">**Nome** descreve Olá toousers de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92533-134">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="92533-135">**URI de redirecionamento** é uma combinação de esquema e a cadeia de caracteres que o AD do Azure usa tooreturn respostas de token.</span><span class="sxs-lookup"><span data-stu-id="92533-135">**Redirect URI** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span> <span data-ttu-id="92533-136">Insira um valor (por exemplo, http://DirectorySearcher).</span><span class="sxs-lookup"><span data-stu-id="92533-136">Enter a value (for example, http://DirectorySearcher).</span></span>
6. <span data-ttu-id="92533-137">Depois de concluir o registro, o Azure AD atribui aplicativo hello uma ID exclusiva do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="92533-137">After you’ve completed registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="92533-138">Copie o valor de saudação da saudação **aplicativo** guia, pois você precisará dele mais tarde.</span><span class="sxs-lookup"><span data-stu-id="92533-138">Copy hello value from hello **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="92533-139">Em Olá **configurações** página, selecione **permissões necessárias**e, em seguida, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="92533-139">On hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="92533-140">Selecione **Microsoft Graph** como Olá API.</span><span class="sxs-lookup"><span data-stu-id="92533-140">Select **Microsoft Graph** as hello API.</span></span> <span data-ttu-id="92533-141">Em **permissões delegadas**, adicionar Olá **ler dados do diretório** permissão.</span><span class="sxs-lookup"><span data-stu-id="92533-141">Under **Delegated Permissions**, add hello **Read Directory Data** permission.</span></span>  
<span data-ttu-id="92533-142">Esta ação habilita Olá tooquery aplicativo hello Graph API para os usuários.</span><span class="sxs-lookup"><span data-stu-id="92533-142">This action enables hello app tooquery hello Graph API for users.</span></span>

## <a name="step-3-install-and-configure-adal"></a><span data-ttu-id="92533-143">Etapa 3: Instalar e configurar a ADAL</span><span class="sxs-lookup"><span data-stu-id="92533-143">Step 3: Install and configure ADAL</span></span>
<span data-ttu-id="92533-144">Agora que você tem um aplicativo no Azure AD, você pode instalar a ADAL e escrever seu código relacionado à identidade.</span><span class="sxs-lookup"><span data-stu-id="92533-144">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="92533-145">tooenable toocommunicate ADAL com o Azure AD, dê a ele algumas informações sobre o registro do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="92533-145">tooenable ADAL toocommunicate with Azure AD, give it some information about hello app registration.</span></span>

1. <span data-ttu-id="92533-146">Adicione projeto de DirectorySearcher toohello ADAL usando Olá Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="92533-146">Add ADAL toohello DirectorySearcher project by using hello Package Manager Console.</span></span>

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirectorySearcherLib
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Android
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Desktop
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-iOS
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Universal
    `

    <span data-ttu-id="92533-147">Observe que duas referências de biblioteca são adicionadas tooeach projeto: Olá PCL parte de ADAL e uma parte específica de plataforma.</span><span class="sxs-lookup"><span data-stu-id="92533-147">Note that two library references are added tooeach project: hello PCL portion of ADAL and a platform-specific portion.</span></span>
2. <span data-ttu-id="92533-148">No projeto de DirectorySearcherLib hello, abra DirectorySearcher.cs.</span><span class="sxs-lookup"><span data-stu-id="92533-148">In hello DirectorySearcherLib project, open DirectorySearcher.cs.</span></span>
3. <span data-ttu-id="92533-149">Substitua valores de membro de classe Olá com valores hello que você inseriu na Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="92533-149">Replace hello class member values with hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="92533-150">O código se refere a valores toothese sempre que ele usa ADAL.</span><span class="sxs-lookup"><span data-stu-id="92533-150">Your code refers toothese values whenever it uses ADAL.</span></span>

  * <span data-ttu-id="92533-151">Olá *locatário* é o domínio de saudação do seu locatário do AD do Azure (por exemplo, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="92533-151">hello *tenant* is hello domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="92533-152">Olá *clientId* é a ID do cliente de saudação do aplicativo hello, o que você copiou do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="92533-152">hello *clientId* is hello client ID of hello app, which you copied from hello portal.</span></span>
  * <span data-ttu-id="92533-153">Olá *returnUri* é Olá redirecionamento URI que você inseriu no portal de saudação (por exemplo, http://DirectorySearcher).</span><span class="sxs-lookup"><span data-stu-id="92533-153">hello *returnUri* is hello redirect URI that you entered in hello portal (for example, http://DirectorySearcher).</span></span>

## <a name="step-4-use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="92533-154">Etapa 4: Tokens ADAL tooget uso do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="92533-154">Step 4: Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="92533-155">Quase todos os de lógica de autenticação do aplicativo hello está em `DirectorySearcher.SearchByAlias(...)`.</span><span class="sxs-lookup"><span data-stu-id="92533-155">Almost all of hello app's authentication logic lies in `DirectorySearcher.SearchByAlias(...)`.</span></span> <span data-ttu-id="92533-156">Tudo o que é necessário em projetos do hello específica de plataforma é toopass toohello um parâmetro contextual `DirectorySearcher` PCL.</span><span class="sxs-lookup"><span data-stu-id="92533-156">All that's necessary in hello platform-specific projects is toopass a contextual parameter toohello `DirectorySearcher` PCL.</span></span>

1. <span data-ttu-id="92533-157">Abra DirectorySearcher.cs e, em seguida, adicionar um novo toohello de parâmetro `SearchByAlias(...)` método.</span><span class="sxs-lookup"><span data-stu-id="92533-157">Open DirectorySearcher.cs, and then add a new parameter toohello `SearchByAlias(...)` method.</span></span> <span data-ttu-id="92533-158">`IPlatformParameters`é o parâmetro hello contextuais encapsula específico da plataforma Olá objetos que a autenticação de ADAL necessidades tooperform hello.</span><span class="sxs-lookup"><span data-stu-id="92533-158">`IPlatformParameters` is hello contextual parameter that encapsulates hello platform-specific objects that ADAL needs tooperform hello authentication.</span></span>

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. <span data-ttu-id="92533-159">Inicializar `AuthenticationContext`, que é a classe principal de saudação do ADAL.</span><span class="sxs-lookup"><span data-stu-id="92533-159">Initialize `AuthenticationContext`, which is hello primary class of ADAL.</span></span>  
<span data-ttu-id="92533-160">Este Olá ADAL de passagens de ação ele coordena toocommunicate necessidades com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92533-160">This action passes ADAL hello coordinates it needs toocommunicate with Azure AD.</span></span>
3. <span data-ttu-id="92533-161">Chamar `AcquireTokenAsync(...)`, que aceita Olá `IPlatformParameters` do objeto e invoca o fluxo de autenticação de saudação que é necessário tooreturn um aplicativo toohello token.</span><span class="sxs-lookup"><span data-stu-id="92533-161">Call `AcquireTokenAsync(...)`, which accepts hello `IPlatformParameters` object and invokes hello authentication flow that's necessary tooreturn a token toohello app.</span></span>

    ```C#
    ...
        AuthenticationResult authResult = null;
        try
        {
            AuthenticationContext authContext = new AuthenticationContext(authority);
            authResult = await authContext.AcquireTokenAsync(graphResourceUri, clientId, returnUri, parent);
        }
        catch (Exception ee)
        {
            results.Add(new User { error = ee.Message });
            return results;
        }
    ...
    ```

    <span data-ttu-id="92533-162">`AcquireTokenAsync(...)`primeiro tentativas tooreturn um token para Olá solicitou o recurso (Olá API do Graph neste caso) sem avisar os usuários tooenter suas credenciais (por meio do armazenamento em cache ou atualizar tokens antigos).</span><span class="sxs-lookup"><span data-stu-id="92533-162">`AcquireTokenAsync(...)` first attempts tooreturn a token for hello requested resource (hello Graph API in this case) without prompting users tooenter their credentials (via caching or refreshing old tokens).</span></span> <span data-ttu-id="92533-163">Conforme necessário, ele mostra usuários Olá AD do Azure-página de entrada antes de adquirir o token solicitado hello.</span><span class="sxs-lookup"><span data-stu-id="92533-163">As necessary, it shows users hello Azure AD sign-in page before acquiring hello requested token.</span></span>
4. <span data-ttu-id="92533-164">Anexar a solicitação da API do Graph toohello token Olá acesso no hello **autorização** cabeçalho:</span><span class="sxs-lookup"><span data-stu-id="92533-164">Attach hello access token toohello Graph API request in hello **Authorization** header:</span></span>

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

<span data-ttu-id="92533-165">Isso é tudo para Olá `DirectorySearcher` código de relacionadas à identidade do aplicativo PCL e hello.</span><span class="sxs-lookup"><span data-stu-id="92533-165">That's all for hello `DirectorySearcher` PCL and hello app's identity-related code.</span></span> <span data-ttu-id="92533-166">Tudo o que resta é Olá toocall `SearchByAlias(...)` método nos modos de exibição de cada plataforma e, quando necessário, tooadd código para tratar corretamente Olá do ciclo de vida da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="92533-166">All that remains is toocall hello `SearchByAlias(...)` method in each platform's views and, where necessary, tooadd code for correctly handling hello UI lifecycle.</span></span>

### <a name="android"></a><span data-ttu-id="92533-167">Android</span><span class="sxs-lookup"><span data-stu-id="92533-167">Android</span></span>
1. <span data-ttu-id="92533-168">Em MainActivity.cs, adicione uma chamada muito`SearchByAlias(...)` manipulador de clique no botão de saudação:</span><span class="sxs-lookup"><span data-stu-id="92533-168">In MainActivity.cs, add a call too`SearchByAlias(...)` in hello button click handler:</span></span>

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. <span data-ttu-id="92533-169">Substituir saudação `OnActivityResult` ciclo de vida método tooforward qualquer autenticação redireciona o método apropriado toohello voltar.</span><span class="sxs-lookup"><span data-stu-id="92533-169">Override hello `OnActivityResult` lifecycle method tooforward any authentication redirects back toohello appropriate method.</span></span> <span data-ttu-id="92533-170">A ADAL fornece um método auxiliar para isso no Android:</span><span class="sxs-lookup"><span data-stu-id="92533-170">ADAL provides a helper method for this in Android:</span></span>

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a><span data-ttu-id="92533-171">Área de Trabalho do Windows</span><span class="sxs-lookup"><span data-stu-id="92533-171">Windows Desktop</span></span>
<span data-ttu-id="92533-172">Em MainWindow.xaml.cs, fazer uma chamada muito`SearchByAlias(...)` passando um `WindowInteropHelper` da área de trabalho Olá `PlatformParameters` objeto:</span><span class="sxs-lookup"><span data-stu-id="92533-172">In MainWindow.xaml.cs, make a call too`SearchByAlias(...)` by passing a `WindowInteropHelper` in hello desktop's `PlatformParameters` object:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a><span data-ttu-id="92533-173">iOS</span><span class="sxs-lookup"><span data-stu-id="92533-173">iOS</span></span>
<span data-ttu-id="92533-174">Em DirSearchClient_iOSViewController.cs, Olá iOS `PlatformParameters` objeto assume um controlador de exibição de toohello de referência:</span><span class="sxs-lookup"><span data-stu-id="92533-174">In DirSearchClient_iOSViewController.cs, hello iOS `PlatformParameters` object takes a reference toohello View Controller:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a><span data-ttu-id="92533-175">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="92533-175">Windows Universal</span></span>
<span data-ttu-id="92533-176">No Windows Universal, abra MainPage.xaml.cs e implementar Olá `Search` método.</span><span class="sxs-lookup"><span data-stu-id="92533-176">In Windows Universal, open MainPage.xaml.cs, and then implement hello `Search` method.</span></span> <span data-ttu-id="92533-177">Esse método usa um método auxiliar no tooupdate projeto compartilhado da interface do usuário conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="92533-177">This method uses a helper method in a shared project tooupdate UI as necessary.</span></span>

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a><span data-ttu-id="92533-178">O que vem a seguir</span><span class="sxs-lookup"><span data-stu-id="92533-178">What's next</span></span>
<span data-ttu-id="92533-179">Agora você tem um aplicativo Xamarin em funcionamento que pode autenticar usuários e chamar as APIs de Web com segurança usando OAuth 2.0 em cinco plataformas diferentes.</span><span class="sxs-lookup"><span data-stu-id="92533-179">You now have a working Xamarin app that can authenticate users and securely call web APIs by using OAuth 2.0 across five different platforms.</span></span>

<span data-ttu-id="92533-180">Se você já não tiver populado seu locatário com usuários, agora é Olá tempo toodo assim.</span><span class="sxs-lookup"><span data-stu-id="92533-180">If you haven’t already populated your tenant with users, now is hello time toodo so.</span></span>

1. <span data-ttu-id="92533-181">Executar seu aplicativo DirectorySearcher e, em seguida, entrar com um dos usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="92533-181">Run your DirectorySearcher app, and then sign in with one of hello users.</span></span>
2. <span data-ttu-id="92533-182">Procure por outros usuários com base em seus UPNs.</span><span class="sxs-lookup"><span data-stu-id="92533-182">Search for other users based on their UPN.</span></span>

<span data-ttu-id="92533-183">ADAL torna fácil tooincorporate recursos comuns de identidade para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="92533-183">ADAL makes it easy tooincorporate common identity features into hello app.</span></span> <span data-ttu-id="92533-184">Cuida de todo o trabalho sujo Olá para você, como gerenciamento de cache, suporte ao protocolo OAuth, apresentando usuário Olá com um logon de interface do usuário, e a atualização expirou tokens.</span><span class="sxs-lookup"><span data-stu-id="92533-184">It takes care of all hello dirty work for you, such as cache management, OAuth protocol support, presenting hello user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="92533-185">Você precisa tooknow apenas uma única API chamada, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="92533-185">You need tooknow only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="92533-186">Para referência, baixe Olá [exemplo concluído](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (sem os valores de configuração).</span><span class="sxs-lookup"><span data-stu-id="92533-186">For reference, download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="92533-187">Agora você pode mover tooadditional cenários de identidade.</span><span class="sxs-lookup"><span data-stu-id="92533-187">You can now move on tooadditional identity scenarios.</span></span> <span data-ttu-id="92533-188">Por exemplo, experimente [Proteger uma API Web .NET com o Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="92533-188">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
