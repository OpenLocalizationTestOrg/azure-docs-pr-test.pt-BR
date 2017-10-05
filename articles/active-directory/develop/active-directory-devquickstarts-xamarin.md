---
title: "Introdução ao Xamarin do Azure AD | Microsoft Docs"
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
ms.openlocfilehash: 54ee403f283bc5dc79911e2e813dd513ff595828
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a><span data-ttu-id="c49e3-103">Integrar o Azure AD com aplicativos Xamarin</span><span class="sxs-lookup"><span data-stu-id="c49e3-103">Integrate Azure AD with Xamarin apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="c49e3-104">Com o Xamarin, você pode gravar aplicativos móveis em C# que podem ser executados no iOS, no Android e no Windows (dispositivos móveis e computadores).</span><span class="sxs-lookup"><span data-stu-id="c49e3-104">With Xamarin, you can write mobile apps in C# that can run on iOS, Android, and Windows (mobile devices and PCs).</span></span> <span data-ttu-id="c49e3-105">Se você estiver criando um aplicativo usando o Xamarin, o Azure Active Directory (Azure AD) facilita autenticar usuários com suas contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c49e3-105">If you're building an app using Xamarin, Azure Active Directory (Azure AD) makes it simple to authenticate users with their Azure AD accounts.</span></span> <span data-ttu-id="c49e3-106">O aplicativo também pode consumir com segurança qualquer API Web protegida pelo Azure AD, por exemplo as APIs do Office 365 ou a API do Azure.</span><span class="sxs-lookup"><span data-stu-id="c49e3-106">The app can also securely consume any web API that's protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="c49e3-107">Para aplicativos do Xamarin que precisam acessar recursos protegidos, o Azure AD fornece a Biblioteca de Autenticação do Active Directory (ADAL).</span><span class="sxs-lookup"><span data-stu-id="c49e3-107">For Xamarin apps that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="c49e3-108">A única finalidade da ADAL é tornar mais fácil para seus aplicativos obter tokens de acesso.</span><span class="sxs-lookup"><span data-stu-id="c49e3-108">The sole purpose of ADAL is to make it easy for apps to get access tokens.</span></span> <span data-ttu-id="c49e3-109">Para demonstrar como é fácil, este artigo mostra como criar aplicativos DirectorySearcher que:</span><span class="sxs-lookup"><span data-stu-id="c49e3-109">To demonstrate how easy it is, this article shows how to build DirectorySearcher apps that:</span></span>

* <span data-ttu-id="c49e3-110">Execute no iOS, no Android, na Área de Trabalho do Windows, no Windows Phone e na Windows Store.</span><span class="sxs-lookup"><span data-stu-id="c49e3-110">Run on iOS, Android, Windows Desktop, Windows Phone, and Windows Store.</span></span>
* <span data-ttu-id="c49e3-111">Use uma única PCL (portable class library - biblioteca de classes portátil) para autenticar usuários e obter tokens para a API do Graph do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c49e3-111">Use a single portable class library (PCL) to authenticate users and get tokens for the Azure AD Graph API.</span></span>
* <span data-ttu-id="c49e3-112">Pesquise um diretório para usuários com um determinado UPN.</span><span class="sxs-lookup"><span data-stu-id="c49e3-112">Search a directory for users with a given UPN.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="c49e3-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="c49e3-113">Before you get started</span></span>
* <span data-ttu-id="c49e3-114">Baixe o [projeto de esqueleto](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip) ou baixe o [exemplo concluído](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="c49e3-114">Download the [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), or download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="c49e3-115">Cada download é uma solução do Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="c49e3-115">Each download is a Visual Studio 2013 solution.</span></span>
* <span data-ttu-id="c49e3-116">Você também precisará de um locatário do Azure AD no qual criar usuários e registrar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c49e3-116">You also need an Azure AD tenant in which to create users and register the app.</span></span> <span data-ttu-id="c49e3-117">Se você ainda não tiver um locatário [saiba como obter um](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="c49e3-117">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="c49e3-118">Quando estiver pronto, siga os procedimentos nas próximas quatro seções.</span><span class="sxs-lookup"><span data-stu-id="c49e3-118">When you are ready, follow the procedures in the next four sections.</span></span>

## <a name="step-1-set-up-your-xamarin-development-environment"></a><span data-ttu-id="c49e3-119">Etapa 1: Configurar seu ambiente de desenvolvimento do Xamarin</span><span class="sxs-lookup"><span data-stu-id="c49e3-119">Step 1: Set up your Xamarin development environment</span></span>
<span data-ttu-id="c49e3-120">Como este tutorial inclui projetos para iOS, Android e Windows, são necessários o Visual Studio e o Xamarin.</span><span class="sxs-lookup"><span data-stu-id="c49e3-120">Because this tutorial includes projects for iOS, Android, and Windows, you need both Visual Studio and Xamarin.</span></span> <span data-ttu-id="c49e3-121">Para criar o ambiente necessário, conclua o processo em [definido para cima e instale o Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) no MSDN.</span><span class="sxs-lookup"><span data-stu-id="c49e3-121">To create the necessary environment, complete the process in [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) on MSDN.</span></span> <span data-ttu-id="c49e3-122">Essas instruções incluem material que você pode examinar para saber mais sobre o Xamarin enquanto aguarda a conclusão das instalações.</span><span class="sxs-lookup"><span data-stu-id="c49e3-122">The instructions include material that you can review to learn more about Xamarin while you're waiting for the installations to be completed.</span></span>

<span data-ttu-id="c49e3-123">Depois de concluir a instalação, abra a solução no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c49e3-123">After you've completed the setup, open the solution in Visual Studio.</span></span> <span data-ttu-id="c49e3-124">Lá, você encontrará seis projetos: cinco projetos específicos de plataforma e um PCL, DirectorySearcher.cs, que será compartilhado entre todas as plataformas.</span><span class="sxs-lookup"><span data-stu-id="c49e3-124">There, you will find six projects: five platform-specific projects and one PCL, DirectorySearcher.cs, which will be shared across all platforms.</span></span>

## <a name="step-2-register-the-directorysearcher-app"></a><span data-ttu-id="c49e3-125">Etapa 2: Registrar o aplicativo DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="c49e3-125">Step 2: Register the DirectorySearcher app</span></span>
<span data-ttu-id="c49e3-126">Para habilitar o aplicativo para obter tokens, primeiro será necessário registrá-lo no seu locatário do Azure AD e conceder permissão para acessar a API do Graph do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c49e3-126">To enable the app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API.</span></span> <span data-ttu-id="c49e3-127">Faça assim:</span><span class="sxs-lookup"><span data-stu-id="c49e3-127">Here's how:</span></span>

1. <span data-ttu-id="c49e3-128">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c49e3-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c49e3-129">Na barra superior, clique em sua conta.</span><span class="sxs-lookup"><span data-stu-id="c49e3-129">On the top bar, click your account.</span></span> <span data-ttu-id="c49e3-130">Em seguida, na lista **Diretório**, selecione o locatário do Active Directory em que você deseja registrar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c49e3-130">Then, under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="c49e3-131">Clique em **Mais Serviços** no painel esquerdo e selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c49e3-131">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="c49e3-132">Clique em **Registros do aplicativo**e, em seguida, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c49e3-132">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="c49e3-133">Para criar um novo **Aplicativo Cliente Nativo**, siga os prompts.</span><span class="sxs-lookup"><span data-stu-id="c49e3-133">To create a new **Native Client Application**, follow the prompts.</span></span>
  * <span data-ttu-id="c49e3-134">**Nome** descreve o aplicativo para os usuários.</span><span class="sxs-lookup"><span data-stu-id="c49e3-134">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="c49e3-135">O **URI de redirecionamento** é uma combinação de esquema e de cadeia de caracteres que o Azure AD usará para retornar respostas de tokens.</span><span class="sxs-lookup"><span data-stu-id="c49e3-135">**Redirect URI** is a scheme and string combination that Azure AD uses to return token responses.</span></span> <span data-ttu-id="c49e3-136">Insira um valor (por exemplo, http://DirectorySearcher).</span><span class="sxs-lookup"><span data-stu-id="c49e3-136">Enter a value (for example, http://DirectorySearcher).</span></span>
6. <span data-ttu-id="c49e3-137">Depois que você concluir o registro, o Azure AD atribuirá uma ID do aplicativo exclusiva ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c49e3-137">After you’ve completed registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="c49e3-138">Copie o valor da guia **Aplicativo**, pois você precisará dele mais tarde.</span><span class="sxs-lookup"><span data-stu-id="c49e3-138">Copy the value from the **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="c49e3-139">Na página **Configurações**, selecione **Permissões necessárias** e escolha **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c49e3-139">On the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="c49e3-140">Selecione **Microsoft Graph** como a API.</span><span class="sxs-lookup"><span data-stu-id="c49e3-140">Select **Microsoft Graph** as the API.</span></span> <span data-ttu-id="c49e3-141">Em **permissões delegadas**, adicione o **ler dados do diretório** permissão.</span><span class="sxs-lookup"><span data-stu-id="c49e3-141">Under **Delegated Permissions**, add the **Read Directory Data** permission.</span></span>  
<span data-ttu-id="c49e3-142">Essa ação permite que o aplicativo consulte a API do Graph para usuários.</span><span class="sxs-lookup"><span data-stu-id="c49e3-142">This action enables the app to query the Graph API for users.</span></span>

## <a name="step-3-install-and-configure-adal"></a><span data-ttu-id="c49e3-143">Etapa 3: Instalar e configurar a ADAL</span><span class="sxs-lookup"><span data-stu-id="c49e3-143">Step 3: Install and configure ADAL</span></span>
<span data-ttu-id="c49e3-144">Agora que você tem um aplicativo no Azure AD, você pode instalar a ADAL e escrever seu código relacionado à identidade.</span><span class="sxs-lookup"><span data-stu-id="c49e3-144">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="c49e3-145">Para permitir que a ADAL se comunique com o Azure AD, dê a ela algumas informações sobre o registro do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c49e3-145">To enable ADAL to communicate with Azure AD, give it some information about the app registration.</span></span>

1. <span data-ttu-id="c49e3-146">Adicione a ADAL ao projeto DirectorySearcher usando o Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="c49e3-146">Add ADAL to the DirectorySearcher project by using the Package Manager Console.</span></span>

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

    <span data-ttu-id="c49e3-147">Observe que as duas referências de biblioteca são adicionadas a cada projeto - a parte PCL da ADAL e uma parte específica da plataforma.</span><span class="sxs-lookup"><span data-stu-id="c49e3-147">Note that two library references are added to each project: the PCL portion of ADAL and a platform-specific portion.</span></span>
2. <span data-ttu-id="c49e3-148">No projeto DirectorySearcherLib, abra DirectorySearcher.cs.</span><span class="sxs-lookup"><span data-stu-id="c49e3-148">In the DirectorySearcherLib project, open DirectorySearcher.cs.</span></span>
3. <span data-ttu-id="c49e3-149">Substitua os valores de membro de classe pelos valores que você inseriu no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c49e3-149">Replace the class member values with the values that you entered in the Azure portal.</span></span> <span data-ttu-id="c49e3-150">Seu código fará referência a esses valores sempre que ele usar a ADAL.</span><span class="sxs-lookup"><span data-stu-id="c49e3-150">Your code refers to these values whenever it uses ADAL.</span></span>

  * <span data-ttu-id="c49e3-151">O *tenant* é o domínio do seu locatário do Azure AD, por exemplo, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="c49e3-151">The *tenant* is the domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="c49e3-152">A *clientId* é a ID do cliente do aplicativo, que você copiou do portal.</span><span class="sxs-lookup"><span data-stu-id="c49e3-152">The *clientId* is the client ID of the app, which you copied from the portal.</span></span>
  * <span data-ttu-id="c49e3-153">O *returnUri* é o URI que você inseriu no portal (por exemplo, http://DirectorySearcher) de redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="c49e3-153">The *returnUri* is the redirect URI that you entered in the portal (for example, http://DirectorySearcher).</span></span>

## <a name="step-4-use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="c49e3-154">Etapa 4: Usar a ADAL para obter tokens do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c49e3-154">Step 4: Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="c49e3-155">Quase toda lógica de autenticação do aplicativo está em `DirectorySearcher.SearchByAlias(...)`.</span><span class="sxs-lookup"><span data-stu-id="c49e3-155">Almost all of the app's authentication logic lies in `DirectorySearcher.SearchByAlias(...)`.</span></span> <span data-ttu-id="c49e3-156">Tudo o que é necessário nos projetos específicos da plataforma é passar um parâmetro contextual para o PCL do `DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="c49e3-156">All that's necessary in the platform-specific projects is to pass a contextual parameter to the `DirectorySearcher` PCL.</span></span>

1. <span data-ttu-id="c49e3-157">Abra DirectorySearcher.cs e, em seguida, adicione um novo parâmetro para o `SearchByAlias(...)` método.</span><span class="sxs-lookup"><span data-stu-id="c49e3-157">Open DirectorySearcher.cs, and then add a new parameter to the `SearchByAlias(...)` method.</span></span> <span data-ttu-id="c49e3-158">`IPlatformParameters` é o parâmetro contextual que encapsula os objetos específicos da plataforma de que a ADAL precisa para realizar a autenticação.</span><span class="sxs-lookup"><span data-stu-id="c49e3-158">`IPlatformParameters` is the contextual parameter that encapsulates the platform-specific objects that ADAL needs to perform the authentication.</span></span>

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. <span data-ttu-id="c49e3-159">Inicialize `AuthenticationContext`, que é a classe primária da ADAL.</span><span class="sxs-lookup"><span data-stu-id="c49e3-159">Initialize `AuthenticationContext`, which is the primary class of ADAL.</span></span>  
<span data-ttu-id="c49e3-160">Essa ação passa à ADAL as coordenadas necessárias para se comunicar com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c49e3-160">This action passes ADAL the coordinates it needs to communicate with Azure AD.</span></span>
3. <span data-ttu-id="c49e3-161">Chame `AcquireTokenAsync(...)`, que aceita o objeto `IPlatformParameters` e invoca o fluxo de autenticação necessário para retornar um token para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c49e3-161">Call `AcquireTokenAsync(...)`, which accepts the `IPlatformParameters` object and invokes the authentication flow that's necessary to return a token to the app.</span></span>

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

    <span data-ttu-id="c49e3-162">`AcquireTokenAsync(...)` tenta primeiro retornar um token para o recurso solicitado (a API do Graph neste caso) sem solicitar que os usuários insiram suas credenciais (por meio de caching ou atualizando tokens antigos).</span><span class="sxs-lookup"><span data-stu-id="c49e3-162">`AcquireTokenAsync(...)` first attempts to return a token for the requested resource (the Graph API in this case) without prompting users to enter their credentials (via caching or refreshing old tokens).</span></span> <span data-ttu-id="c49e3-163">Se necessário, ele exibe ao usuário a página de entrada do Azure AD antes de adquirir o token solicitado.</span><span class="sxs-lookup"><span data-stu-id="c49e3-163">As necessary, it shows users the Azure AD sign-in page before acquiring the requested token.</span></span>
4. <span data-ttu-id="c49e3-164">Anexe o token de acesso à solicitação da API do Graph no cabeçalho **Autorização**:</span><span class="sxs-lookup"><span data-stu-id="c49e3-164">Attach the access token to the Graph API request in the **Authorization** header:</span></span>

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

<span data-ttu-id="c49e3-165">Isso é tudo para a PCL do `DirectorySearcher` e o código relacionado à identidade do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c49e3-165">That's all for the `DirectorySearcher` PCL and the app's identity-related code.</span></span> <span data-ttu-id="c49e3-166">Tudo o que resta fazer é chamar o método `SearchByAlias(...)` nos modos de exibição de cada plataforma e, onde necessário, adicionar código para tratar corretamente o ciclo de vida da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="c49e3-166">All that remains is to call the `SearchByAlias(...)` method in each platform's views and, where necessary, to add code for correctly handling the UI lifecycle.</span></span>

### <a name="android"></a><span data-ttu-id="c49e3-167">Android</span><span class="sxs-lookup"><span data-stu-id="c49e3-167">Android</span></span>
1. <span data-ttu-id="c49e3-168">No MainActivity.cs, adicione uma chamada para `SearchByAlias(...)` manipulador de clique do botão:</span><span class="sxs-lookup"><span data-stu-id="c49e3-168">In MainActivity.cs, add a call to `SearchByAlias(...)` in the button click handler:</span></span>

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. <span data-ttu-id="c49e3-169">Substitua o método de ciclo de vida `OnActivityResult` para encaminhar qualquer autenticação, fazendo com que ela seja redirecionada para o método apropriado.</span><span class="sxs-lookup"><span data-stu-id="c49e3-169">Override the `OnActivityResult` lifecycle method to forward any authentication redirects back to the appropriate method.</span></span> <span data-ttu-id="c49e3-170">A ADAL fornece um método auxiliar para isso no Android:</span><span class="sxs-lookup"><span data-stu-id="c49e3-170">ADAL provides a helper method for this in Android:</span></span>

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a><span data-ttu-id="c49e3-171">Área de Trabalho do Windows</span><span class="sxs-lookup"><span data-stu-id="c49e3-171">Windows Desktop</span></span>
<span data-ttu-id="c49e3-172">Em MainWindow.xaml.cs, fazer uma chamada para `SearchByAlias(...)` passando um `WindowInteropHelper` na área de trabalho `PlatformParameters` objeto:</span><span class="sxs-lookup"><span data-stu-id="c49e3-172">In MainWindow.xaml.cs, make a call to `SearchByAlias(...)` by passing a `WindowInteropHelper` in the desktop's `PlatformParameters` object:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a><span data-ttu-id="c49e3-173">iOS</span><span class="sxs-lookup"><span data-stu-id="c49e3-173">iOS</span></span>
<span data-ttu-id="c49e3-174">Em DirSearchClient_iOSViewController.cs, o iOS `PlatformParameters` objeto pega uma referência para o controlador de exibição:</span><span class="sxs-lookup"><span data-stu-id="c49e3-174">In DirSearchClient_iOSViewController.cs, the iOS `PlatformParameters` object takes a reference to the View Controller:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a><span data-ttu-id="c49e3-175">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="c49e3-175">Windows Universal</span></span>
<span data-ttu-id="c49e3-176">No Windows Universal, abra o arquivo MainPage.xaml.cs e implementar o `Search` método.</span><span class="sxs-lookup"><span data-stu-id="c49e3-176">In Windows Universal, open MainPage.xaml.cs, and then implement the `Search` method.</span></span> <span data-ttu-id="c49e3-177">Esse método usa um método auxiliar em um projeto compartilhado para atualizar a interface do usuário conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="c49e3-177">This method uses a helper method in a shared project to update UI as necessary.</span></span>

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a><span data-ttu-id="c49e3-178">O que vem a seguir</span><span class="sxs-lookup"><span data-stu-id="c49e3-178">What's next</span></span>
<span data-ttu-id="c49e3-179">Agora você tem um aplicativo Xamarin em funcionamento que pode autenticar usuários e chamar as APIs de Web com segurança usando OAuth 2.0 em cinco plataformas diferentes.</span><span class="sxs-lookup"><span data-stu-id="c49e3-179">You now have a working Xamarin app that can authenticate users and securely call web APIs by using OAuth 2.0 across five different platforms.</span></span>

<span data-ttu-id="c49e3-180">Se você ainda não fez isso, agora é o momento de popular seu locatário com alguns usuários.</span><span class="sxs-lookup"><span data-stu-id="c49e3-180">If you haven’t already populated your tenant with users, now is the time to do so.</span></span>

1. <span data-ttu-id="c49e3-181">Execute o aplicativo DirectorySearcher e então entre com um dos usuários.</span><span class="sxs-lookup"><span data-stu-id="c49e3-181">Run your DirectorySearcher app, and then sign in with one of the users.</span></span>
2. <span data-ttu-id="c49e3-182">Procure por outros usuários com base em seus UPNs.</span><span class="sxs-lookup"><span data-stu-id="c49e3-182">Search for other users based on their UPN.</span></span>

<span data-ttu-id="c49e3-183">A ADAL facilita a incorporação de recursos comuns de identidade no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c49e3-183">ADAL makes it easy to incorporate common identity features into the app.</span></span> <span data-ttu-id="c49e3-184">Ele se encarrega de todo o trabalho difícil para você, por exemplo, gerenciamento de cache, suporte a protocolo OAuth, apresentação de uma interface do usuário de logon ao usuário e atualização de tokens expirados.</span><span class="sxs-lookup"><span data-stu-id="c49e3-184">It takes care of all the dirty work for you, such as cache management, OAuth protocol support, presenting the user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="c49e3-185">Você precisa conhecer apenas uma única chamada à API, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="c49e3-185">You need to know only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="c49e3-186">Para referência, baixe a [amostra concluída](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (sem seus valores de configuração).</span><span class="sxs-lookup"><span data-stu-id="c49e3-186">For reference, download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="c49e3-187">Agora você pode passar para cenários de identidade adicionais.</span><span class="sxs-lookup"><span data-stu-id="c49e3-187">You can now move on to additional identity scenarios.</span></span> <span data-ttu-id="c49e3-188">Por exemplo, experimente [Proteger uma API Web .NET com o Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c49e3-188">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
