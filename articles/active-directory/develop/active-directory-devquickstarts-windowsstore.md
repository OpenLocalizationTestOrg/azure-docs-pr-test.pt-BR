---
title: "aaaAzure AD Windows Store Introdução | Microsoft Docs"
description: Crie aplicativos da Windows Store que se integrem ao Azure AD para entrar e chame APIs protegidas do Azure AD usando OAuth.
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 3b96a6d1-270b-4ac1-b9b5-58070c896a68
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 09/16/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 1d12c7b928bc0e94fb823f8db4a09ff416205e2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a><span data-ttu-id="8f3e6-103">Integrar o Azure AD com aplicativos da Windows Store</span><span class="sxs-lookup"><span data-stu-id="8f3e6-103">Integrate Azure AD with Windows Store apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="8f3e6-104">Não há suporte para projetos da Windows Store 8.1 e de versões anteriores no Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-104">Windows Store 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="8f3e6-105">Para saber mais, confira [Direcionamento e compatibilidade da plataforma Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="8f3e6-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="8f3e6-106">Se você estiver desenvolvendo aplicativos para saudação da Windows Store, Azure Active Directory (AD do Azure) torna simple e direto tooauthenticate os usuários com suas contas do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-106">If you're developing apps for hello Windows Store, Azure Active Directory (Azure AD) makes it simple and straightforward tooauthenticate your users with their Active Directory accounts.</span></span> <span data-ttu-id="8f3e6-107">Com a integração com o AD do Azure, um aplicativo pode consumir com segurança qualquer API que é protegido pelo AD do Azure, como Olá APIs do Office 365 ou hello Azure API da web.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-107">By integrating with Azure AD, an app can securely consume any web API that's protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="8f3e6-108">Para aplicativos da área de trabalho da Windows Store que precisam de recursos de tooaccess protegido, o AD do Azure fornece Olá biblioteca de autenticação do Active Directory (ADAL).</span><span class="sxs-lookup"><span data-stu-id="8f3e6-108">For Windows Store desktop apps that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="8f3e6-109">Olá única finalidade ADAL é toomake fácil para tokens de acesso de tooget de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-109">hello sole purpose of ADAL is toomake it easy for hello app tooget access tokens.</span></span> <span data-ttu-id="8f3e6-110">toodemonstrate como é, este artigo mostra como toobuild Windows DirectorySearcher armazenam fácil aplicativos que:</span><span class="sxs-lookup"><span data-stu-id="8f3e6-110">toodemonstrate how easy it is, this article shows how toobuild a DirectorySearcher Windows Store app that:</span></span>

* <span data-ttu-id="8f3e6-111">Obtém acesso tokens para chamar a API do Azure AD Graph Olá usando Olá [protocolo de autenticação OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="8f3e6-111">Gets access tokens for calling hello Azure AD Graph API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="8f3e6-112">Pesquisa por usuários com um determinado nome UPN em um diretório.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-112">Searches a directory for users with a given user principal name (UPN).</span></span>
* <span data-ttu-id="8f3e6-113">Desconecta usuários.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-113">Signs users out.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="8f3e6-114">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="8f3e6-114">Before you get started</span></span>
* <span data-ttu-id="8f3e6-115">Baixar Olá [projeto esqueleto](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), ou baixar Olá [exemplo concluído](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="8f3e6-115">Download hello [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), or download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span></span> <span data-ttu-id="8f3e6-116">Cada download é uma solução do Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-116">Each download is a Visual Studio 2015 solution.</span></span>
* <span data-ttu-id="8f3e6-117">Também é necessário um locatário Azure AD no qual usuários toocreate e registrar o aplicativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-117">You also need an Azure AD tenant in which toocreate users and register hello app.</span></span> <span data-ttu-id="8f3e6-118">Se você ainda não tiver um locatário, [Saiba como tooget uma](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="8f3e6-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="8f3e6-119">Quando você estiver pronto, siga Olá procedimentos Olá três próximas seções.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-119">When you are ready, follow hello procedures in hello next three sections.</span></span>

## <a name="step-1-register-hello-directorysearcher-app"></a><span data-ttu-id="8f3e6-120">Etapa 1: Registrar o aplicativo de DirectorySearcher Olá</span><span class="sxs-lookup"><span data-stu-id="8f3e6-120">Step 1: Register hello DirectorySearcher app</span></span>
<span data-ttu-id="8f3e6-121">tokens de tooget do tooenable Olá aplicativo, primeiro é necessário tooregistê-lo no AD do Azure locatário e conceda a ela Olá tooaccess de permissão do Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-121">tooenable hello app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API.</span></span> <span data-ttu-id="8f3e6-122">Faça assim:</span><span class="sxs-lookup"><span data-stu-id="8f3e6-122">Here's how:</span></span>

1. <span data-ttu-id="8f3e6-123">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8f3e6-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8f3e6-124">Na barra superior do hello, clique em sua conta.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-124">On hello top bar, click your account.</span></span> <span data-ttu-id="8f3e6-125">Em seguida, em Olá **diretório** lista, o locatário do Active Directory hello selecione onde você deseja que o aplicativo de saudação tooregister.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-125">Then, under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="8f3e6-126">Clique em **mais serviços** Olá painel esquerdo e, em seguida, selecione **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-126">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="8f3e6-127">Clique em **Registros do aplicativo** e, em seguida, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="8f3e6-128">Siga Olá prompts toocreate um **aplicativo cliente nativo**.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-128">Follow hello prompts toocreate a **Native Client Application**.</span></span>
  * <span data-ttu-id="8f3e6-129">**Nome** descreve Olá toousers de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-129">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="8f3e6-130">**URI de redirecionamento** é uma combinação de esquema e a cadeia de caracteres que o AD do Azure usa tooreturn respostas de token.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-130">**Redirect URI** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span> <span data-ttu-id="8f3e6-131">Insira um valor de espaço reservado por enquanto (por exemplo, **http://DirectorySearcher**).</span><span class="sxs-lookup"><span data-stu-id="8f3e6-131">Enter a placeholder value for now (for example, **http://DirectorySearcher**).</span></span> <span data-ttu-id="8f3e6-132">Posteriormente, você substituirá o valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-132">You'll replace hello value later.</span></span>
6. <span data-ttu-id="8f3e6-133">Depois de concluir o registro de saudação, o Azure AD atribui aplicativo hello uma ID exclusiva do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-133">After you’ve completed hello registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="8f3e6-134">Copie o valor Olá Olá **aplicativo** guia, pois você precisará dele mais tarde.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-134">Copy hello value on hello **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="8f3e6-135">Em Olá **configurações** página, selecione **permissões necessárias**e, em seguida, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-135">On hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="8f3e6-136">Para Olá **Active Directory do Azure** aplicativo, selecione **Microsoft Graph** como Olá API.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-136">For hello **Azure Active Directory** app, select **Microsoft Graph** as hello API.</span></span>
9. <span data-ttu-id="8f3e6-137">Em **permissões delegadas**, adicionar Olá **acessar o diretório de hello como o usuário conectado Olá** permissão.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-137">Under **Delegated Permissions**, add hello **Access hello directory as hello signed-in user** permission.</span></span> <span data-ttu-id="8f3e6-138">Isso permite que o hello tooquery aplicativo hello Graph API para os usuários.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-138">Doing so enables hello app tooquery hello Graph API for users.</span></span>

## <a name="step-2-install-and-configure-adal"></a><span data-ttu-id="8f3e6-139">Etapa 2: instalar e configurar a ADAL</span><span class="sxs-lookup"><span data-stu-id="8f3e6-139">Step 2: Install and configure ADAL</span></span>
<span data-ttu-id="8f3e6-140">Agora que você tem um aplicativo no Azure AD, você pode instalar a ADAL e escrever seu código relacionado à identidade.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-140">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="8f3e6-141">tooenable toocommunicate ADAL com o Azure AD, dê a ele algumas informações sobre o registro do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-141">tooenable ADAL toocommunicate with Azure AD, give it some information about hello app registration.</span></span>

1. <span data-ttu-id="8f3e6-142">Adicione projeto de DirectorySearcher toohello ADAL usando Olá Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-142">Add ADAL toohello DirectorySearcher project by using hello Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. <span data-ttu-id="8f3e6-143">No projeto de DirectorySearcher hello, abra MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-143">In hello DirectorySearcher project, open MainPage.xaml.cs.</span></span>
3. <span data-ttu-id="8f3e6-144">Substituir valores Olá Olá **valores de configuração** região com valores de saudação que você inseriu no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-144">Replace hello values in hello **Config Values** region with hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="8f3e6-145">O código se refere a valores toothese sempre que ele usa ADAL.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-145">Your code refers toothese values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="8f3e6-146">Olá *locatário* é o domínio de saudação do seu locatário do AD do Azure (por exemplo, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="8f3e6-146">hello *tenant* is hello domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="8f3e6-147">Olá *clientId* é a ID do cliente de saudação do aplicativo hello, o que você copiou do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-147">hello *clientId* is hello client ID of hello app, which you copied from hello portal.</span></span>
4. <span data-ttu-id="8f3e6-148">Agora, você precisa toodiscover o retorno de chamada de saudação URI para seu aplicativo da Windows Store.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-148">You now need toodiscover hello callback URI for your Windows Store app.</span></span> <span data-ttu-id="8f3e6-149">Defina um ponto de interrupção nessa linha em Olá `MainPage` método:</span><span class="sxs-lookup"><span data-stu-id="8f3e6-149">Set a breakpoint on this line in hello `MainPage` method:</span></span>
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. <span data-ttu-id="8f3e6-150">Compile a solução de hello, certificando-se de que todas as referências de pacote são restauradas.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-150">Build hello solution, making sure that all package references are restored.</span></span> <span data-ttu-id="8f3e6-151">Se todos os pacotes estiverem ausentes, abra Olá NuGet Package Manager e restaurá-los.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-151">If any packages are missing, open hello NuGet Package Manager and restore them.</span></span>
6. <span data-ttu-id="8f3e6-152">Executar o aplicativo hello e copie o valor de saudação do `redirectUri` quando Olá ponto de interrupção.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-152">Run hello app, and copy hello value of `redirectUri` when hello breakpoint is hit.</span></span> <span data-ttu-id="8f3e6-153">valor de saudação deve ser semelhante a saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f3e6-153">hello value should look something like hello following:</span></span>

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. <span data-ttu-id="8f3e6-154">Em Olá **configurações** guia do aplicativo Olá Olá portal do Azure, adicione um **RedirectUri** com hello precede o valor.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-154">Back on hello **Settings** tab of hello app in hello Azure portal, add a **RedirectUri** with hello preceding value.</span></span>  

## <a name="step-3-use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="8f3e6-155">Etapa 3: Tokens ADAL tooget uso do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="8f3e6-155">Step 3: Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="8f3e6-156">Olá princípio básico de ADAL é que sempre que o aplicativo hello precisa de um token de acesso, ele simplesmente chama `authContext.AcquireToken(…)`, e ADAL Olá rest.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-156">hello basic principle behind ADAL is that whenever hello app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does hello rest.</span></span>  

1. <span data-ttu-id="8f3e6-157">Inicialização do aplicativo hello `AuthenticationContext`, que é a classe principal de saudação do ADAL.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-157">Initialize hello app’s `AuthenticationContext`, which is hello primary class of ADAL.</span></span> <span data-ttu-id="8f3e6-158">Essa ação passa coordenadas Olá ADAL ele precisa toocommunicate com o Azure AD e informe como toocache tokens.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-158">This action passes ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. <span data-ttu-id="8f3e6-159">Localizar Olá `Search(...)` método, que é invocado quando os usuários clicarem Olá **pesquisa** botão na interface de usuário do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-159">Locate hello `Search(...)` method, which is invoked when users click hello **Search** button on hello app's UI.</span></span> <span data-ttu-id="8f3e6-160">Esse método torna um tooquery de toohello do Azure AD Graph API de solicitação get para usuários cujo UPN começa com hello dado o termo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-160">This method makes a get request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span> <span data-ttu-id="8f3e6-161">Olá tooquery API do Graph, incluir um token de acesso na solicitação de saudação **autorização** cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-161">tooquery hello Graph API, include an access token in hello request's **Authorization** header.</span></span> <span data-ttu-id="8f3e6-162">É aí que a ADAL entra em cena.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-162">This is where ADAL comes in.</span></span>

    ```C#
    private async void Search(object sender, RoutedEventArgs e)
    {
        ...
        AuthenticationResult result = null;
        try
        {
            result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectURI, new PlatformParameters(PromptBehavior.Auto, false));
        }
        catch (AdalException ex)
        {
            if (ex.ErrorCode != "authentication_canceled")
            {
                ShowAuthError(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    <span data-ttu-id="8f3e6-163">Quando o aplicativo hello solicita um token chamando `AcquireTokenAsync(...)`, ADAL tentativas tooreturn um token sem solicitar credenciais de usuário hello.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-163">When hello app requests a token by calling `AcquireTokenAsync(...)`, ADAL attempts tooreturn a token without asking hello user for credentials.</span></span> <span data-ttu-id="8f3e6-164">Se ADAL determina que o usuário Olá precisa toosign em tooget um token, ele exibe uma caixa de diálogo de logon, coleta as credenciais do usuário hello e retorna um token depois que a autenticação seja bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-164">If ADAL determines that hello user needs toosign in tooget a token, it displays a sign-in dialog box, collects hello user's credentials, and returns a token after authentication succeeds.</span></span> <span data-ttu-id="8f3e6-165">Se o ADAL está tooreturn não é possível um token por qualquer motivo, Olá *AuthenticationResult* status é um erro.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-165">If ADAL is unable tooreturn a token for any reason, hello *AuthenticationResult* status is an error.</span></span>
3. <span data-ttu-id="8f3e6-166">Agora é o token de acesso do tempo toouse Olá que você acabou de adquirir.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-166">Now it's time toouse hello access token you just acquired.</span></span> <span data-ttu-id="8f3e6-167">Também no hello `Search(...)` método, anexar Olá toohello token de solicitação de obtenção de API do Graph em Olá **autorização** cabeçalho:</span><span class="sxs-lookup"><span data-stu-id="8f3e6-167">Also in hello `Search(...)` method, attach hello token toohello Graph API get request in hello **Authorization** header:</span></span>

    ```C#
    // Add hello access token toohello Authorization header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. <span data-ttu-id="8f3e6-168">Você pode usar o hello `AuthenticationResult` toodisplay informações sobre usuário Olá no aplicativo hello, como ID do usuário de saudação do objeto:</span><span class="sxs-lookup"><span data-stu-id="8f3e6-168">You can use hello `AuthenticationResult` object toodisplay information about hello user in hello app, such as hello user's ID:</span></span>

    ```C#
    // Update hello page UI toorepresent hello signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. <span data-ttu-id="8f3e6-169">Você também pode usar o ADAL toosign usuários fora do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-169">You can also use ADAL toosign users out of hello app.</span></span> <span data-ttu-id="8f3e6-170">Quando o usuário Olá clica Olá **sair** botão, certifique-se de que chamam Avançar Olá muito`AcquireTokenAsync(...)` mostra uma exibição de entrada.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-170">When hello user clicks hello **Sign Out** button, ensure that hello next call too`AcquireTokenAsync(...)` shows a sign-in view.</span></span> <span data-ttu-id="8f3e6-171">Com a ADAL, essa ação é tão fácil quanto limpar o cache de token hello:</span><span class="sxs-lookup"><span data-stu-id="8f3e6-171">With ADAL, this action is as easy as clearing hello token cache:</span></span>

    ```C#
    private void SignOut()
    {
        // Clear session state from hello token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a><span data-ttu-id="8f3e6-172">O que vem a seguir</span><span class="sxs-lookup"><span data-stu-id="8f3e6-172">What's next</span></span>
<span data-ttu-id="8f3e6-173">Agora você tem um aplicativo da Windows Store que pode autenticar os usuários, com segurança chamar APIs usando OAuth 2.0 da web e obter informações básicas sobre o usuário de saudação do trabalho.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-173">You now have a working Windows Store app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about hello user.</span></span>

<span data-ttu-id="8f3e6-174">Se você já não tiver populado seu locatário com usuários, agora é Olá tempo toodo assim.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-174">If you haven’t already populated your tenant with users, now is hello time toodo so.</span></span>
1. <span data-ttu-id="8f3e6-175">Executar seu aplicativo DirectorySearcher e, em seguida, entrar com um dos usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-175">Run your DirectorySearcher app, and then sign in with one of hello users.</span></span>
2. <span data-ttu-id="8f3e6-176">Procure por outros usuários com base em seus UPNs.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-176">Search for other users based on their UPN.</span></span>
3. <span data-ttu-id="8f3e6-177">Feche o aplicativo hello e executá-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-177">Close hello app, and rerun it.</span></span> <span data-ttu-id="8f3e6-178">Observe como a sessão do usuário Olá permanece intacta.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-178">Notice how hello user’s session remains intact.</span></span>
4. <span data-ttu-id="8f3e6-179">Sair clicando toodisplay Olá barra inferior e, em seguida, entrar novamente como outro usuário.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-179">Sign out by right-clicking toodisplay hello bottom bar, and then sign back in as another user.</span></span>

<span data-ttu-id="8f3e6-180">ADAL torna fácil tooincorporate todos esses recursos de identidade comum para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-180">ADAL makes it easy tooincorporate all these common identity features into hello app.</span></span> <span data-ttu-id="8f3e6-181">Cuida de todo o trabalho sujo Olá para você, como gerenciamento de cache, suporte ao protocolo OAuth, apresentando usuário Olá com um logon de interface do usuário, e a atualização expirou tokens.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-181">It takes care of all hello dirty work for you, such as cache management, OAuth protocol support, presenting hello user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="8f3e6-182">Você precisa tooknow apenas uma única API chamada, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-182">You need tooknow only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="8f3e6-183">Para referência, baixe Olá [exemplo concluído](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (sem os valores de configuração).</span><span class="sxs-lookup"><span data-stu-id="8f3e6-183">For reference, download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="8f3e6-184">Agora você pode mover tooadditional cenários de identidade.</span><span class="sxs-lookup"><span data-stu-id="8f3e6-184">You can now move on tooadditional identity scenarios.</span></span> <span data-ttu-id="8f3e6-185">Por exemplo, experimente [Proteger uma API Web .NET com o Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="8f3e6-185">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
