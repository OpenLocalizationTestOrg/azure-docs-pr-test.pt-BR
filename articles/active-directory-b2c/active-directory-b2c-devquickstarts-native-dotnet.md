---
title: Azure Active Directory B2C | Microsoft Docs
description: "Como compilar um aplicativo Web com gerenciamento de entrada, de inscrição e de perfis usando o Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9da14362-8216-4485-960e-af17cd5ba3bd
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: 8e2b5c704230ee2ba1395dc76a1551aaa8e7af7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a><span data-ttu-id="56bc7-103">Azure AD B2C: criar um aplicativo da área de trabalho do Windows</span><span class="sxs-lookup"><span data-stu-id="56bc7-103">Azure AD B2C: Build a Windows desktop app</span></span>
<span data-ttu-id="56bc7-104">Ao usar o Azure Active Directory B2C (Azure AD), você poderá adicionar recursos poderosos de gerenciamento de identidades de autoatendimento para seu aplicativo da área de trabalho em poucas etapas.</span><span class="sxs-lookup"><span data-stu-id="56bc7-104">By using Azure Active Directory (Azure AD) B2C, you can add powerful self-service identity management features to your desktop app in a few short steps.</span></span> <span data-ttu-id="56bc7-105">Este artigo mostra como criar um aplicativo “lista de tarefas pendentes” do WPF (Windows Presentation Foundation) do .NET que inclui a inscrição, a entrada e o gerenciamento de perfil de usuário.</span><span class="sxs-lookup"><span data-stu-id="56bc7-105">This article will show you how to create a .NET Windows Presentation Foundation (WPF) "to-do list" app that includes user sign-up, sign-in, and profile management.</span></span> <span data-ttu-id="56bc7-106">O aplicativo inclui suporte para a inscrição e a entrada usando um nome de usuário ou um email.</span><span class="sxs-lookup"><span data-stu-id="56bc7-106">The app will include support for sign-up and sign-in by using a user name or email.</span></span> <span data-ttu-id="56bc7-107">Ele também incluirá o suporte para a inscrição e a entrada usando contas sociais como o Facebook e o Google.</span><span class="sxs-lookup"><span data-stu-id="56bc7-107">It will also include support for sign-up and sign-in by using social accounts such as Facebook and Google.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="56bc7-108">Obter um diretório AD B2C do Azure</span><span class="sxs-lookup"><span data-stu-id="56bc7-108">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="56bc7-109">Antes de usar AD B2C do Azure, você deve criar um diretório ou locatário.</span><span class="sxs-lookup"><span data-stu-id="56bc7-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="56bc7-110">Um diretório é um contêiner para todos os seus usuários, aplicativos, grupos etc.</span><span class="sxs-lookup"><span data-stu-id="56bc7-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="56bc7-111">Se você ainda não tiver um, [crie um diretório B2C](active-directory-b2c-get-started.md) antes de prosseguir neste guia.</span><span class="sxs-lookup"><span data-stu-id="56bc7-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="56bc7-112">Criar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="56bc7-112">Create an application</span></span>
<span data-ttu-id="56bc7-113">Em seguida, você precisa criar um aplicativo em seu diretório B2C.</span><span class="sxs-lookup"><span data-stu-id="56bc7-113">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="56bc7-114">Isso fornece ao AD do Azure as informações de que ele precisa para se comunicar de forma segura com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="56bc7-114">This gives Azure AD information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="56bc7-115">Para criar um aplicativo, [siga estas instruções](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="56bc7-115">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span>  <span data-ttu-id="56bc7-116">É necessário que você:</span><span class="sxs-lookup"><span data-stu-id="56bc7-116">Be sure to:</span></span>

* <span data-ttu-id="56bc7-117">Inclua um **cliente nativo** no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="56bc7-117">Include a **native client** in the application.</span></span>
* <span data-ttu-id="56bc7-118">Copie o **URI de redirecionamento** `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="56bc7-118">Copy the **Redirect URI** `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="56bc7-119">É a URL padrão deste exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="56bc7-119">It is the default URL for this code sample.</span></span>
* <span data-ttu-id="56bc7-120">Copie a **ID do Aplicativo** atribuída ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="56bc7-120">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="56bc7-121">Você precisará dela mais tarde.</span><span class="sxs-lookup"><span data-stu-id="56bc7-121">You will need it later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="56bc7-122">Criar suas políticas</span><span class="sxs-lookup"><span data-stu-id="56bc7-122">Create your policies</span></span>
<span data-ttu-id="56bc7-123">No Azure AD B2C, cada experiência do usuário é definida por uma [política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="56bc7-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="56bc7-124">Este exemplo de código contém três experiências de identidade: perfil de inscrição, entrada e edição.</span><span class="sxs-lookup"><span data-stu-id="56bc7-124">This code sample contains three identity experiences: sign up, sign in, and edit profile.</span></span> <span data-ttu-id="56bc7-125">Você precisa criar uma política para cada tipo, como descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="56bc7-125">You need to create a policy for each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="56bc7-126">Ao criar as três políticas, não se esqueça de:</span><span class="sxs-lookup"><span data-stu-id="56bc7-126">When you create the three policies, be sure to:</span></span>

* <span data-ttu-id="56bc7-127">Escolher a **Inscrição de ID de usuário** ou a **Inscrição de email** na folha de provedores de identidade.</span><span class="sxs-lookup"><span data-stu-id="56bc7-127">Choose either **User ID sign-up** or **Email sign-up** in the identity providers blade.</span></span>
* <span data-ttu-id="56bc7-128">Escolher **Nome de exibição** e outros atributos de inscrição na política de inscrição.</span><span class="sxs-lookup"><span data-stu-id="56bc7-128">Choose **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="56bc7-129">Escolher as declarações **Nome de exibição** e **ID de objeto** como declarações de aplicativo para cada política.</span><span class="sxs-lookup"><span data-stu-id="56bc7-129">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="56bc7-130">Você pode escolher outras declarações também.</span><span class="sxs-lookup"><span data-stu-id="56bc7-130">You can choose other claims as well.</span></span>
* <span data-ttu-id="56bc7-131">Copie o **Nome** de cada política depois de criá-la.</span><span class="sxs-lookup"><span data-stu-id="56bc7-131">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="56bc7-132">Ele deve ter o prefixo `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="56bc7-132">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="56bc7-133">Você precisará esses nomes de política mais tarde.</span><span class="sxs-lookup"><span data-stu-id="56bc7-133">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="56bc7-134">Depois de criar suas três políticas, você estará pronto para compilar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="56bc7-134">After you have successfully created the three policies, you're ready to build your app.</span></span>

## <a name="download-the-code"></a><span data-ttu-id="56bc7-135">Baixar o código</span><span class="sxs-lookup"><span data-stu-id="56bc7-135">Download the code</span></span>
<span data-ttu-id="56bc7-136">O código para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="56bc7-136">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span></span> <span data-ttu-id="56bc7-137">Para compilar o exemplo à medida que avançar, [baixe um projeto de esqueleto como um arquivo .zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="56bc7-137">To build the sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span></span> <span data-ttu-id="56bc7-138">Também é possível clonar o esqueleto:</span><span class="sxs-lookup"><span data-stu-id="56bc7-138">You can also clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

<span data-ttu-id="56bc7-139">O aplicativo completo também está [disponível como um arquivo .zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) ou na ramificação `complete` do mesmo repositório.</span><span class="sxs-lookup"><span data-stu-id="56bc7-139">The completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) or on the `complete` branch of the same repository.</span></span>

<span data-ttu-id="56bc7-140">Depois de baixar o código de exemplo, abra o arquivo .sln do Visual Studio para começar.</span><span class="sxs-lookup"><span data-stu-id="56bc7-140">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="56bc7-141">O projeto do `TaskClient` é o aplicativo de área de trabalho do WPF com o qual usuário interage.</span><span class="sxs-lookup"><span data-stu-id="56bc7-141">The `TaskClient` project is the WPF desktop application that the user interacts with.</span></span> <span data-ttu-id="56bc7-142">Para os fins deste tutorial, ele chama uma API Web de tarefa de back-end, hospedada no Azure, que armazena a lista de tarefas de cada usuário.</span><span class="sxs-lookup"><span data-stu-id="56bc7-142">For the purposes of this tutorial, it calls a back-end task web API, hosted in Azure, that stores each user's to-do list.</span></span>  <span data-ttu-id="56bc7-143">Você não precisa criar a API Web; ela já está em execução para você.</span><span class="sxs-lookup"><span data-stu-id="56bc7-143">You do not need to build the web API, we already have it running for you.</span></span>

<span data-ttu-id="56bc7-144">Para saber como a API Web autentica solicitações com segurança usando o Azure AD B2C, confira nosso [artigo de introdução à API Web](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="56bc7-144">To learn how a web API securely authenticates requests by using Azure AD B2C, check out the [web API getting started article](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="execute-policies"></a><span data-ttu-id="56bc7-145">Executar políticas</span><span class="sxs-lookup"><span data-stu-id="56bc7-145">Execute policies</span></span>
<span data-ttu-id="56bc7-146">Seu aplicativo se comunica com o Azure AD B2C enviando mensagens de autenticação que especificam a política que desejam executar como parte da solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="56bc7-146">Your app communicates with Azure AD B2C by sending authentication messages that specify the policy they want to execute as part of the HTTP request.</span></span> <span data-ttu-id="56bc7-147">Para aplicativos da área de trabalho do .NET, você pode usar a visualização da MSAL (Biblioteca de Autenticação da Microsoft) para enviar mensagens de autenticação OAuth 2.0, executar políticas e obter tokens que chamam APIs Web.</span><span class="sxs-lookup"><span data-stu-id="56bc7-147">For .NET desktop applications, you can use the preview Microsoft Authentication Library (MSAL) to send OAuth 2.0 authentication messages, execute policies, and get tokens that call web APIs.</span></span>

### <a name="install-msal"></a><span data-ttu-id="56bc7-148">Instalar MSAL</span><span class="sxs-lookup"><span data-stu-id="56bc7-148">Install MSAL</span></span>
<span data-ttu-id="56bc7-149">Adicione MSAL ao projeto `TaskClient` usando o Visual Studio Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="56bc7-149">Add MSAL to the `TaskClient` project by using the Visual Studio Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a><span data-ttu-id="56bc7-150">Insira seus detalhes B2C</span><span class="sxs-lookup"><span data-stu-id="56bc7-150">Enter your B2C details</span></span>
<span data-ttu-id="56bc7-151">Abra o arquivo `Globals.cs` e substitua cada um dos valores da propriedade pelos seus próprios.</span><span class="sxs-lookup"><span data-stu-id="56bc7-151">Open the file `Globals.cs` and replace each of the property values with your own.</span></span> <span data-ttu-id="56bc7-152">Essa classe é usada em todo o `TaskClient` para referenciar os valores comumente usados.</span><span class="sxs-lookup"><span data-stu-id="56bc7-152">This class is used throughout `TaskClient` to reference commonly used values.</span></span>

```C#
public static class Globals
{
    ...

    // TODO: Replace these five default with your own configuration values
    public static string tenant = "fabrikamb2c.onmicrosoft.com";
    public static string clientId = "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6";
    public static string signInPolicy = "b2c_1_sign_in";
    public static string signUpPolicy = "b2c_1_sign_up";
    public static string editProfilePolicy = "b2c_1_edit_profile";

    ...
}
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="create-the-publicclientapplication"></a><span data-ttu-id="56bc7-153">Criar o PublicClientApplication</span><span class="sxs-lookup"><span data-stu-id="56bc7-153">Create the PublicClientApplication</span></span>
<span data-ttu-id="56bc7-154">A classe primária da MSAL é `PublicClientApplication`.</span><span class="sxs-lookup"><span data-stu-id="56bc7-154">The primary class of MSAL is `PublicClientApplication`.</span></span> <span data-ttu-id="56bc7-155">Essa classe representa o aplicativo no sistema Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="56bc7-155">This class represents your application in the Azure AD B2C system.</span></span> <span data-ttu-id="56bc7-156">Quando o aplicativo é inicializado, cria uma instância de `PublicClientApplication` em `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="56bc7-156">When the app initalizes, create an instance of `PublicClientApplication` in `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="56bc7-157">Isso pode ser usado em toda a janela.</span><span class="sxs-lookup"><span data-stu-id="56bc7-157">This can be used throughout the window.</span></span>

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens to persist when the user closes the app,
        // we've extended the MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a><span data-ttu-id="56bc7-158">Iniciar um fluxo de inscrição</span><span class="sxs-lookup"><span data-stu-id="56bc7-158">Initiate a sign-up flow</span></span>
<span data-ttu-id="56bc7-159">Quando um usuário opta por se inscrever, você deseja iniciar um fluxo de inscrição que use a política de inscrição criada.</span><span class="sxs-lookup"><span data-stu-id="56bc7-159">When a user opts to signs up, you want to initiate a sign-up flow that uses the sign-up policy you created.</span></span> <span data-ttu-id="56bc7-160">Usando a MSAL, você apenas chama `pca.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="56bc7-160">By using MSAL, you just call `pca.AcquireTokenAsync(...)`.</span></span> <span data-ttu-id="56bc7-161">Os parâmetros que você passa para o `AcquireTokenAsync(...)` determinam qual token receber, a política usada na solicitação de autenticação e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="56bc7-161">The parameters you pass to `AcquireTokenAsync(...)` determine which token you receive, the policy used in the authentication request, and more.</span></span>

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use the app's clientId here as the scope parameter, indicating that
        // you want a token to the your app's backend web API (represented by
        // the cloud hosted task API).  Use the UiOptions.ForceLogin flag to
        // indicate to MSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in the app that the user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When the request completes successfully, you can get user
        // information from the AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After the sign up successfully completes, display the user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of the policy.
    catch (MsalException ex)
    {
        if (ex.ErrorCode != "authentication_canceled")
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

### <a name="initiate-a-sign-in-flow"></a><span data-ttu-id="56bc7-162">Iniciar um fluxo de entrada</span><span class="sxs-lookup"><span data-stu-id="56bc7-162">Initiate a sign-in flow</span></span>
<span data-ttu-id="56bc7-163">Você pode iniciar um fluxo de entrada da mesma maneira que inicia um fluxo de inscrição.</span><span class="sxs-lookup"><span data-stu-id="56bc7-163">You can initiate a sign-in flow in the same way that you initiate a sign-up flow.</span></span> <span data-ttu-id="56bc7-164">Quando um usuário entrar, faça a mesma chamada a MSAL, dessa vez usando a política de entrada:</span><span class="sxs-lookup"><span data-stu-id="56bc7-164">When a user signs in, make the same call to MSAL, this time by using your sign-in policy:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.signInPolicy);
        ...
```

### <a name="initiate-an-edit-profile-flow"></a><span data-ttu-id="56bc7-165">Iniciar um fluxo de edição de perfil</span><span class="sxs-lookup"><span data-stu-id="56bc7-165">Initiate an edit-profile flow</span></span>
<span data-ttu-id="56bc7-166">Novamente, você pode executar uma política de edição de perfil da mesma maneira:</span><span class="sxs-lookup"><span data-stu-id="56bc7-166">Again, you can execute an edit-profile policy in the same fashion:</span></span>

```C#
private async void EditProfile(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.editProfilePolicy);
```

<span data-ttu-id="56bc7-167">Em todos esses casos, MSAL retornará um token em `AuthenticationResult` ou gerará uma exceção.</span><span class="sxs-lookup"><span data-stu-id="56bc7-167">In all of these cases, MSAL either returns a token in `AuthenticationResult` or throws an exception.</span></span> <span data-ttu-id="56bc7-168">Sempre que obtiver um token do MSA, você poderá usar o `AuthenticationResult.User` objeto para atualizar os dados do usuário no aplicativo, como a interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="56bc7-168">Each time you get a token from MSAL, you can use the `AuthenticationResult.User` object to update the user data in the app, such as the UI.</span></span> <span data-ttu-id="56bc7-169">A ADAL também armazena o token em cache para uso em outras partes do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="56bc7-169">ADAL also caches the token for use in other parts of the application.</span></span>

### <a name="check-for-tokens-on-app-start"></a><span data-ttu-id="56bc7-170">Verificar se há tokens na inicialização do aplicativo</span><span class="sxs-lookup"><span data-stu-id="56bc7-170">Check for tokens on app start</span></span>
<span data-ttu-id="56bc7-171">Você também pode usar a MSAL para controlar o estado de entrada do usuário.</span><span class="sxs-lookup"><span data-stu-id="56bc7-171">You can also use MSAL to keep track of the user's sign-in state.</span></span>  <span data-ttu-id="56bc7-172">Neste aplicativo, queremos que o usuário permaneça conectado mesmo depois que fechar o aplicativo e o abrir novamente.</span><span class="sxs-lookup"><span data-stu-id="56bc7-172">In this app, we want the user to remain signed in even after they close the app & re-open it.</span></span>  <span data-ttu-id="56bc7-173">De volta à substituição `OnInitialized`, use o método `AcquireTokenSilent` da MSAL para verificar se há tokens em cache:</span><span class="sxs-lookup"><span data-stu-id="56bc7-173">Back inside the `OnInitialized` override, use MSAL's `AcquireTokenSilent` method to check for cached tokens:</span></span>

```C#
AuthenticationResult result = null;
try
{
    // If the user has has a token cached with any policy, we'll display them as signed-in.
    TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
    string existingPolicy = tci == null ? null : tci.Policy;
    result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    SignInButton.Visibility = Visibility.Collapsed;
    SignUpButton.Visibility = Visibility.Collapsed;
    EditProfileButton.Visibility = Visibility.Visible;
    SignOutButton.Visibility = Visibility.Visible;
    UsernameLabel.Content = result.User.Name;
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "failed_to_acquire_token_silently")
    {
        // There are no tokens in the cache.  Proceed without calling the To Do list service.
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
```

## <a name="call-the-task-api"></a><span data-ttu-id="56bc7-174">Chamar a API de tarefa</span><span class="sxs-lookup"><span data-stu-id="56bc7-174">Call the task API</span></span>
<span data-ttu-id="56bc7-175">Agora você já usou MSAL para executar políticas e para obter tokens.</span><span class="sxs-lookup"><span data-stu-id="56bc7-175">You have now used MSAL to execute policies and get tokens.</span></span>  <span data-ttu-id="56bc7-176">Quando você quiser usar um desses tokens para chamar a API de tarefa, você pode usar novamente da MSAL `AcquireTokenSilent` método para verificar tokens armazenados em cache:</span><span class="sxs-lookup"><span data-stu-id="56bc7-176">When you want to use one these tokens to call the task API, you can again use MSAL's `AcquireTokenSilent` method to check for cached tokens:</span></span>

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want to check for a cached token, independent of whatever policy was used to acquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent to indicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch the exception and show the user a message.
    catch (MsalException ex)
    {
        // There is no access token in the cache, so prompt the user to sign-in.
        if (ex.ErrorCode == "failed_to_acquire_token_silently")
        {
            MessageBox.Show("Please sign up or sign in first");
            SignInButton.Visibility = Visibility.Visible;
            SignUpButton.Visibility = Visibility.Visible;
            EditProfileButton.Visibility = Visibility.Collapsed;
            SignOutButton.Visibility = Visibility.Collapsed;
            UsernameLabel.Content = string.Empty;
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
    ...
```

<span data-ttu-id="56bc7-177">Quando a chamada para `AcquireTokenSilentAsync(...)` é bem-sucedida e um token é encontrado no cache, você pode adicionar o token ao cabeçalho `Authorization` da solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="56bc7-177">When the call to `AcquireTokenSilentAsync(...)` succeeds and a token is found in the cache, you can add the token to the `Authorization` header of the HTTP request.</span></span> <span data-ttu-id="56bc7-178">A API Web da tarefa usará esse cabeçalho para autenticar a solicitação para ler a lista de tarefas pendentes do usuário:</span><span class="sxs-lookup"><span data-stu-id="56bc7-178">The task web API will use this header to authenticate the request to read the user's to-do list:</span></span>

```C#
    ...
    // Once the token has been returned by MSAL, add it to the http authorization header, before making the call to access the To Do list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call the To Do list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-the-user-out"></a><span data-ttu-id="56bc7-179">Desconectar o usuário</span><span class="sxs-lookup"><span data-stu-id="56bc7-179">Sign the user out</span></span>
<span data-ttu-id="56bc7-180">Finalmente, você pode usar MSAL para encerrar a sessão do usuário com o aplicativo, quando o usuário seleciona **Sair**.</span><span class="sxs-lookup"><span data-stu-id="56bc7-180">Finally, you can use MSAL to end a user's session with the app when the user selects **Sign out**.</span></span>  <span data-ttu-id="56bc7-181">Ao se usar MSAL, isso é feito por meio da limpeza de todos os tokens no cache de tokens:</span><span class="sxs-lookup"><span data-stu-id="56bc7-181">When using MSAL, this is accomplished by clearing all of the tokens from the token cache:</span></span>

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of the user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in the browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update the UI to show the user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-the-sample-app"></a><span data-ttu-id="56bc7-182">Executar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="56bc7-182">Run the sample app</span></span>
<span data-ttu-id="56bc7-183">Por fim, compile e execute o exemplo.</span><span class="sxs-lookup"><span data-stu-id="56bc7-183">Finally, build and run the sample.</span></span>  <span data-ttu-id="56bc7-184">Inscreva-se no aplicativo usando um endereço de email ou um nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="56bc7-184">Sign up for the app by using an email address or user name.</span></span> <span data-ttu-id="56bc7-185">Saia e entre novamente como o mesmo usuário.</span><span class="sxs-lookup"><span data-stu-id="56bc7-185">Sign out and sign back in as the same user.</span></span> <span data-ttu-id="56bc7-186">Edite perfil do usuário.</span><span class="sxs-lookup"><span data-stu-id="56bc7-186">Edit that user's profile.</span></span> <span data-ttu-id="56bc7-187">Saia e entre novamente como outro usuário.</span><span class="sxs-lookup"><span data-stu-id="56bc7-187">Sign out and sign up by using a different user.</span></span>

## <a name="add-social-idps"></a><span data-ttu-id="56bc7-188">Adicionar IDPs sociais</span><span class="sxs-lookup"><span data-stu-id="56bc7-188">Add social IDPs</span></span>
<span data-ttu-id="56bc7-189">Atualmente, o aplicativo só dá suporte à inscrição e à entrada do usuário com **contas locais**.</span><span class="sxs-lookup"><span data-stu-id="56bc7-189">Currently, the app supports only user sign-up and sign-in that use **local accounts**.</span></span> <span data-ttu-id="56bc7-190">Essas são as contas armazenadas em seu diretório do B2C que usam um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="56bc7-190">These are accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="56bc7-191">Com o Azure AD B2C, você pode adicionar suporte a outros provedores de identidade (IDPs), sem alterar qualquer código.</span><span class="sxs-lookup"><span data-stu-id="56bc7-191">By using Azure AD B2C, you can add support for other identity providers (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="56bc7-192">Para adicionar IDPs sociais ao seu aplicativo, comece seguindo as instruções detalhadas nestes artigos.</span><span class="sxs-lookup"><span data-stu-id="56bc7-192">To add social IDPs to your app, begin by following the detailed instructions in these articles.</span></span> <span data-ttu-id="56bc7-193">Para cada IDP ao qual deseja oferecer suporte, você precisa registrar um aplicativo no sistema e obter uma ID de cliente.</span><span class="sxs-lookup"><span data-stu-id="56bc7-193">For each IDP you want to support, you need to register an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="56bc7-194">Configurar o Facebook como um IDP</span><span class="sxs-lookup"><span data-stu-id="56bc7-194">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="56bc7-195">Configurar o Google como um IDP</span><span class="sxs-lookup"><span data-stu-id="56bc7-195">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="56bc7-196">Configurar o Amazon como um IDP</span><span class="sxs-lookup"><span data-stu-id="56bc7-196">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="56bc7-197">Configurar o LinkedIn como um IDP</span><span class="sxs-lookup"><span data-stu-id="56bc7-197">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="56bc7-198">Após a adição dos provedores de identidade ao seu diretório B2C, você precisará editar cada uma das suas três políticas para incluir os novos IDPs, como descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="56bc7-198">After you add the identity providers to your B2C directory, you need to edit each of your three policies to include the new IDPs, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="56bc7-199">Depois de salvar as políticas, execute o aplicativo novamente.</span><span class="sxs-lookup"><span data-stu-id="56bc7-199">After you save your policies, run the app again.</span></span> <span data-ttu-id="56bc7-200">Você deve ver os novos IDPs adicionados como opções de entrada e de inscrição em cada experiência de identidade.</span><span class="sxs-lookup"><span data-stu-id="56bc7-200">You should see the new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="56bc7-201">Você pode fazer experiências com suas políticas e observar os efeitos no aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="56bc7-201">You can experiment with your policies and observe the effects on your sample app.</span></span> <span data-ttu-id="56bc7-202">Adicione ou remova IDPs, manipule declarações de aplicativo ou altere os atributos de inscrição.</span><span class="sxs-lookup"><span data-stu-id="56bc7-202">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="56bc7-203">Experimente até conseguir entender como as políticas, as solicitações de autenticação e MSAL funcionam juntos.</span><span class="sxs-lookup"><span data-stu-id="56bc7-203">Experiment until you can see how policies, authentication requests, and MSAL tie together.</span></span>

<span data-ttu-id="56bc7-204">Para referência, o exemplo completo [é fornecido como um arquivo .zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="56bc7-204">For reference, the completed sample [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="56bc7-205">Você também pode cloná-lo do GitHub:</span><span class="sxs-lookup"><span data-stu-id="56bc7-205">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
