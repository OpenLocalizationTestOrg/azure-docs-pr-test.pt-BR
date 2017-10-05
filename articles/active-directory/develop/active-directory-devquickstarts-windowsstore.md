---
title: "Introdução à Windows Store no Azure AD | Microsoft Docs"
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
ms.openlocfilehash: 6b5189dc06d7f8b0ed4426944948b904feba847e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a><span data-ttu-id="53956-103">Integrar o Azure AD com aplicativos da Windows Store</span><span class="sxs-lookup"><span data-stu-id="53956-103">Integrate Azure AD with Windows Store apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="53956-104">Não há suporte para projetos da Windows Store 8.1 e de versões anteriores no Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="53956-104">Windows Store 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="53956-105">Para obter mais informações, consulte [Direcionamento e compatibilidade da plataforma Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="53956-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="53956-106">Se você estiver desenvolvendo aplicativos para a Windows Store, o Azure AD (Azure Active Directory) tornará simples e direto autenticar os usuários com suas contas do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="53956-106">If you're developing apps for the Windows Store, Azure Active Directory (Azure AD) makes it simple and straightforward to authenticate your users with their Active Directory accounts.</span></span> <span data-ttu-id="53956-107">Ao integrar-se com o Azure AD, um aplicativo pode consumir com segurança qualquer API Web protegida pelo Azure AD, por exemplo as APIs do Office 365 ou a API do Azure.</span><span class="sxs-lookup"><span data-stu-id="53956-107">By integrating with Azure AD, an app can securely consume any web API that's protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="53956-108">Para aplicativos de área de trabalho da Windows Store que precisam acessar recursos protegidos, o Azure AD fornece a ADAL (biblioteca de autenticação do Active Directory).</span><span class="sxs-lookup"><span data-stu-id="53956-108">For Windows Store desktop apps that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="53956-109">A única finalidade da ADAL é tornar mais fácil para o aplicativo obter tokens de acesso.</span><span class="sxs-lookup"><span data-stu-id="53956-109">The sole purpose of ADAL is to make it easy for the app to get access tokens.</span></span> <span data-ttu-id="53956-110">Para demonstrar como isso é fácil, este artigo mostra como criar um aplicativo da Windows Store DirectorySearcher que:</span><span class="sxs-lookup"><span data-stu-id="53956-110">To demonstrate how easy it is, this article shows how to build a DirectorySearcher Windows Store app that:</span></span>

* <span data-ttu-id="53956-111">Obtém tokens de acesso para chamar a API do Graph do Azure AD usando o [protocolo de autenticação OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="53956-111">Gets access tokens for calling the Azure AD Graph API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="53956-112">Pesquisa por usuários com um determinado nome UPN em um diretório.</span><span class="sxs-lookup"><span data-stu-id="53956-112">Searches a directory for users with a given user principal name (UPN).</span></span>
* <span data-ttu-id="53956-113">Desconecta usuários.</span><span class="sxs-lookup"><span data-stu-id="53956-113">Signs users out.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="53956-114">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="53956-114">Before you get started</span></span>
* <span data-ttu-id="53956-115">Baixe um [projeto de esqueleto](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip) ou baixe a [amostra concluída](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="53956-115">Download the [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), or download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span></span> <span data-ttu-id="53956-116">Cada download é uma solução do Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="53956-116">Each download is a Visual Studio 2015 solution.</span></span>
* <span data-ttu-id="53956-117">Você também precisará de um locatário do Azure AD no qual criar usuários e registrar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="53956-117">You also need an Azure AD tenant in which to create users and register the app.</span></span> <span data-ttu-id="53956-118">Se você ainda não tiver um locatário [saiba como obter um](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="53956-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="53956-119">Quando estiver pronto, siga os procedimentos nas próximas três seções.</span><span class="sxs-lookup"><span data-stu-id="53956-119">When you are ready, follow the procedures in the next three sections.</span></span>

## <a name="step-1-register-the-directorysearcher-app"></a><span data-ttu-id="53956-120">Etapa 1: registrar o aplicativo DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="53956-120">Step 1: Register the DirectorySearcher app</span></span>
<span data-ttu-id="53956-121">Para habilitar o aplicativo para obter tokens, primeiro será necessário registrá-lo no seu locatário do Azure AD e conceder permissão para acessar a API do Graph do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53956-121">To enable the app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API.</span></span> <span data-ttu-id="53956-122">Faça assim:</span><span class="sxs-lookup"><span data-stu-id="53956-122">Here's how:</span></span>

1. <span data-ttu-id="53956-123">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="53956-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="53956-124">Na barra superior, clique em sua conta.</span><span class="sxs-lookup"><span data-stu-id="53956-124">On the top bar, click your account.</span></span> <span data-ttu-id="53956-125">Em seguida, na lista **Diretório**, selecione o locatário do Active Directory em que você deseja registrar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="53956-125">Then, under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="53956-126">Clique em **Mais Serviços** no painel esquerdo e selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="53956-126">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="53956-127">Clique em **Registros do aplicativo** e, em seguida, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="53956-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="53956-128">Siga os prompts para criar um **aplicativo cliente nativo**.</span><span class="sxs-lookup"><span data-stu-id="53956-128">Follow the prompts to create a **Native Client Application**.</span></span>
  * <span data-ttu-id="53956-129">**Nome** descreve o aplicativo aos usuários.</span><span class="sxs-lookup"><span data-stu-id="53956-129">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="53956-130">O **URI de redirecionamento** é uma combinação de esquema e de cadeia de caracteres que o Azure AD usará para retornar respostas de tokens.</span><span class="sxs-lookup"><span data-stu-id="53956-130">**Redirect URI** is a scheme and string combination that Azure AD uses to return token responses.</span></span> <span data-ttu-id="53956-131">Insira um valor de espaço reservado por enquanto (por exemplo, **http://DirectorySearcher**).</span><span class="sxs-lookup"><span data-stu-id="53956-131">Enter a placeholder value for now (for example, **http://DirectorySearcher**).</span></span> <span data-ttu-id="53956-132">Substituiremos este valor posteriormente.</span><span class="sxs-lookup"><span data-stu-id="53956-132">You'll replace the value later.</span></span>
6. <span data-ttu-id="53956-133">Depois de você concluir o registro, o Azure AD atribui uma ID do aplicativo exclusiva ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="53956-133">After you’ve completed the registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="53956-134">Copie o valor na guia **Aplicativo**, pois você precisará dele mais tarde.</span><span class="sxs-lookup"><span data-stu-id="53956-134">Copy the value on the **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="53956-135">Na página **Configurações**, selecione **Permissões necessárias** e escolha **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="53956-135">On the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="53956-136">Para o aplicativo do **Azure Active Directory**, selecione **Microsoft Graph** como a API.</span><span class="sxs-lookup"><span data-stu-id="53956-136">For the **Azure Active Directory** app, select **Microsoft Graph** as the API.</span></span>
9. <span data-ttu-id="53956-137">Em **Permissões Delegadas**, adicione a permissão **Acessar o diretório como o usuário conectado**.</span><span class="sxs-lookup"><span data-stu-id="53956-137">Under **Delegated Permissions**, add the **Access the directory as the signed-in user** permission.</span></span> <span data-ttu-id="53956-138">Fazer isso permite que o aplicativo consulte a API do Graph para usuários.</span><span class="sxs-lookup"><span data-stu-id="53956-138">Doing so enables the app to query the Graph API for users.</span></span>

## <a name="step-2-install-and-configure-adal"></a><span data-ttu-id="53956-139">Etapa 2: instalar e configurar a ADAL</span><span class="sxs-lookup"><span data-stu-id="53956-139">Step 2: Install and configure ADAL</span></span>
<span data-ttu-id="53956-140">Agora que você tem um aplicativo no Azure AD, você pode instalar a ADAL e escrever seu código relacionado à identidade.</span><span class="sxs-lookup"><span data-stu-id="53956-140">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="53956-141">Para permitir que a ADAL se comunique com o Azure AD, dê a ela algumas informações sobre o registro do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="53956-141">To enable ADAL to communicate with Azure AD, give it some information about the app registration.</span></span>

1. <span data-ttu-id="53956-142">Adicione a ADAL ao projeto DirectorySearcher usando o Console do Gerenciador de Pacotes.</span><span class="sxs-lookup"><span data-stu-id="53956-142">Add ADAL to the DirectorySearcher project by using the Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. <span data-ttu-id="53956-143">No projeto DirectorySearcher, abra MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="53956-143">In the DirectorySearcher project, open MainPage.xaml.cs.</span></span>
3. <span data-ttu-id="53956-144">Substitua os valores na região **Config Values** pelos valores que você inseriu no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="53956-144">Replace the values in the **Config Values** region with the values that you entered in the Azure portal.</span></span> <span data-ttu-id="53956-145">Seu código fará referência a esses valores sempre que ele usar a ADAL.</span><span class="sxs-lookup"><span data-stu-id="53956-145">Your code refers to these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="53956-146">O *tenant* é o domínio do seu locatário do Azure AD, por exemplo, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="53956-146">The *tenant* is the domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="53956-147">A *clientId* é a ID do cliente do aplicativo, que você copiou do portal.</span><span class="sxs-lookup"><span data-stu-id="53956-147">The *clientId* is the client ID of the app, which you copied from the portal.</span></span>
4. <span data-ttu-id="53956-148">Agora você precisa descobrir o URI de retorno de chamada para seu aplicativo da Windows Store.</span><span class="sxs-lookup"><span data-stu-id="53956-148">You now need to discover the callback URI for your Windows Store app.</span></span> <span data-ttu-id="53956-149">Defina um ponto de interrupção nessa linha no método `MainPage` :</span><span class="sxs-lookup"><span data-stu-id="53956-149">Set a breakpoint on this line in the `MainPage` method:</span></span>
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. <span data-ttu-id="53956-150">Compile a solução, certificando-se de que todas as referências do pacote sejam restauradas.</span><span class="sxs-lookup"><span data-stu-id="53956-150">Build the solution, making sure that all package references are restored.</span></span> <span data-ttu-id="53956-151">Se houver pacotes ausentes, abra o Gerenciador de Pacotes NuGet e restaure-os.</span><span class="sxs-lookup"><span data-stu-id="53956-151">If any packages are missing, open the NuGet Package Manager and restore them.</span></span>
6. <span data-ttu-id="53956-152">Execute o aplicativo e copie separadamente o valor de `redirectUri` quando o ponto de interrupção for atingido.</span><span class="sxs-lookup"><span data-stu-id="53956-152">Run the app, and copy the value of `redirectUri` when the breakpoint is hit.</span></span> <span data-ttu-id="53956-153">O valor deve ter uma aparência semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="53956-153">The value should look something like the following:</span></span>

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. <span data-ttu-id="53956-154">De volta à guia **Configurações** do seu aplicativo no Portal do Azure, adicione um **RedirectUri** com o valor precedente.</span><span class="sxs-lookup"><span data-stu-id="53956-154">Back on the **Settings** tab of the app in the Azure portal, add a **RedirectUri** with the preceding value.</span></span>  

## <a name="step-3-use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="53956-155">Etapa 3: usar a ADAL para obter tokens do Azure AD</span><span class="sxs-lookup"><span data-stu-id="53956-155">Step 3: Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="53956-156">O princípio básico da ADAL é que sempre que o aplicativo precisa de um token de acesso, ele simplesmente chama `authContext.AcquireToken(…)` e a ADAL faz o resto.</span><span class="sxs-lookup"><span data-stu-id="53956-156">The basic principle behind ADAL is that whenever the app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does the rest.</span></span>  

1. <span data-ttu-id="53956-157">Inicialize o aplicativo `AuthenticationContext`, que é a classe primária da ADAL.</span><span class="sxs-lookup"><span data-stu-id="53956-157">Initialize the app’s `AuthenticationContext`, which is the primary class of ADAL.</span></span> <span data-ttu-id="53956-158">Essa ação passa à ADAL as coordenadas necessárias para se comunicar com o Azure AD e informar a ele como armazenar tokens em cache.</span><span class="sxs-lookup"><span data-stu-id="53956-158">This action passes ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. <span data-ttu-id="53956-159">Localize o método `Search(...)`, que é invocado quando os usuários clicam no botão **Pesquisa** na interface do usuário do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="53956-159">Locate the `Search(...)` method, which is invoked when users click the **Search** button on the app's UI.</span></span> <span data-ttu-id="53956-160">Esse método faz uma solicitação get para que a API do Graph do Azure AD consulte usuários cujo UPN comece com o termo de pesquisa fornecido.</span><span class="sxs-lookup"><span data-stu-id="53956-160">This method makes a get request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span> <span data-ttu-id="53956-161">Para consultar a API do Graph, inclua um token de acesso no cabeçalho **Authorization** da solicitação.</span><span class="sxs-lookup"><span data-stu-id="53956-161">To query the Graph API, include an access token in the request's **Authorization** header.</span></span> <span data-ttu-id="53956-162">É aí que a ADAL entra em cena.</span><span class="sxs-lookup"><span data-stu-id="53956-162">This is where ADAL comes in.</span></span>

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
                ShowAuthError(string.Format("If the error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    <span data-ttu-id="53956-163">Quando o aplicativo solicita um token chamando `AcquireTokenAsync(...)`, a ADAL tenta retornar um token sem pedir as credenciais ao usuário.</span><span class="sxs-lookup"><span data-stu-id="53956-163">When the app requests a token by calling `AcquireTokenAsync(...)`, ADAL attempts to return a token without asking the user for credentials.</span></span> <span data-ttu-id="53956-164">Se a ADAL determinar que o usuário precisa entrar para obter um token, ela exibirá uma caixa de diálogo de entrada, coletará as credenciais do usuário e retornar um token após uma autenticação bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="53956-164">If ADAL determines that the user needs to sign in to get a token, it displays a sign-in dialog box, collects the user's credentials, and returns a token after authentication succeeds.</span></span> <span data-ttu-id="53956-165">Se a ADAL não puder retornar um token por qualquer motivo, o status *AuthenticationResult* será um erro.</span><span class="sxs-lookup"><span data-stu-id="53956-165">If ADAL is unable to return a token for any reason, the *AuthenticationResult* status is an error.</span></span>
3. <span data-ttu-id="53956-166">Agora é hora de usar o token de acesso que você acabou de adquirir.</span><span class="sxs-lookup"><span data-stu-id="53956-166">Now it's time to use the access token you just acquired.</span></span> <span data-ttu-id="53956-167">Além disso, no método `Search(...)`, anexe o token para a solicitação get de API do Graph no cabeçalho **Authorization**:</span><span class="sxs-lookup"><span data-stu-id="53956-167">Also in the `Search(...)` method, attach the token to the Graph API get request in the **Authorization** header:</span></span>

    ```C#
    // Add the access token to the Authorization header of the call to the Graph API, and call the Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. <span data-ttu-id="53956-168">Você pode usar o objeto `AuthenticationResult` para exibir informações sobre o usuário no aplicativo, por exemplo a ID do usuário:</span><span class="sxs-lookup"><span data-stu-id="53956-168">You can use the `AuthenticationResult` object to display information about the user in the app, such as the user's ID:</span></span>

    ```C#
    // Update the page UI to represent the signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. <span data-ttu-id="53956-169">Você também pode usar a ADAL para fazer com que os usuários saiam do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="53956-169">You can also use ADAL to sign users out of the app.</span></span> <span data-ttu-id="53956-170">Quando o usuário clica no botão **Sair**, certifique-se de que a próxima chamada para `AcquireTokenAsync(...)` mostre um modo de exibição de entrada.</span><span class="sxs-lookup"><span data-stu-id="53956-170">When the user clicks the **Sign Out** button, ensure that the next call to `AcquireTokenAsync(...)` shows a sign-in view.</span></span> <span data-ttu-id="53956-171">Com a ADAL, essa ação é tão fácil quanto limpar o cache de tokens:</span><span class="sxs-lookup"><span data-stu-id="53956-171">With ADAL, this action is as easy as clearing the token cache:</span></span>

    ```C#
    private void SignOut()
    {
        // Clear session state from the token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a><span data-ttu-id="53956-172">O que vem a seguir</span><span class="sxs-lookup"><span data-stu-id="53956-172">What's next</span></span>
<span data-ttu-id="53956-173">Agora você tem um aplicativo da Windows Store que pode autenticar usuários, chamar APIs Web com segurança usando OAuth 2.0 e obter informações básicas sobre o usuário.</span><span class="sxs-lookup"><span data-stu-id="53956-173">You now have a working Windows Store app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about the user.</span></span>

<span data-ttu-id="53956-174">Se você ainda não fez isso, agora é o momento de popular seu locatário com alguns usuários.</span><span class="sxs-lookup"><span data-stu-id="53956-174">If you haven’t already populated your tenant with users, now is the time to do so.</span></span>
1. <span data-ttu-id="53956-175">Execute o aplicativo DirectorySearcher e então entre com um dos usuários.</span><span class="sxs-lookup"><span data-stu-id="53956-175">Run your DirectorySearcher app, and then sign in with one of the users.</span></span>
2. <span data-ttu-id="53956-176">Procure por outros usuários com base em seus UPNs.</span><span class="sxs-lookup"><span data-stu-id="53956-176">Search for other users based on their UPN.</span></span>
3. <span data-ttu-id="53956-177">Feche o aplicativo e execute-o novamente.</span><span class="sxs-lookup"><span data-stu-id="53956-177">Close the app, and rerun it.</span></span> <span data-ttu-id="53956-178">Observe como a sessão do usuário permanece intacta.</span><span class="sxs-lookup"><span data-stu-id="53956-178">Notice how the user’s session remains intact.</span></span>
4. <span data-ttu-id="53956-179">Saia clicando com o botão direito do mouse para mostrar a barra inferior e entre novamente como outro usuário.</span><span class="sxs-lookup"><span data-stu-id="53956-179">Sign out by right-clicking to display the bottom bar, and then sign back in as another user.</span></span>

<span data-ttu-id="53956-180">A ADAL facilita a incorporar todos esses recursos de identidade comuns no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="53956-180">ADAL makes it easy to incorporate all these common identity features into the app.</span></span> <span data-ttu-id="53956-181">Ele se encarrega de todo o trabalho difícil para você, por exemplo, gerenciamento de cache, suporte a protocolo OAuth, apresentação de uma interface do usuário de logon ao usuário e atualização de tokens expirados.</span><span class="sxs-lookup"><span data-stu-id="53956-181">It takes care of all the dirty work for you, such as cache management, OAuth protocol support, presenting the user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="53956-182">Você precisa conhecer apenas uma única chamada à API, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="53956-182">You need to know only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="53956-183">Para referência, baixe a [amostra concluída](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (sem seus valores de configuração).</span><span class="sxs-lookup"><span data-stu-id="53956-183">For reference, download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="53956-184">Agora você pode passar para cenários de identidade adicionais.</span><span class="sxs-lookup"><span data-stu-id="53956-184">You can now move on to additional identity scenarios.</span></span> <span data-ttu-id="53956-185">Por exemplo, experimente [Proteger uma API Web .NET com o Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="53956-185">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
