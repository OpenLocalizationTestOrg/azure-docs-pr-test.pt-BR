---
title: aaaAzure B2C do Active Directory | Microsoft Docs
description: "Como toobuild um aplicativo de área de trabalho do Windows que inclui entrar, se inscrever e criar o perfil de gerenciamento usando o Azure Active Directory B2C."
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
ms.openlocfilehash: f22b0299ff74bfba2f3fea88f006da609859dda5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a><span data-ttu-id="58fe4-103">Azure AD B2C: criar um aplicativo da área de trabalho do Windows</span><span class="sxs-lookup"><span data-stu-id="58fe4-103">Azure AD B2C: Build a Windows desktop app</span></span>
<span data-ttu-id="58fe4-104">Usando B2C do Azure Active Directory (AD do Azure), você pode adicionar o aplicativo de área de trabalho do identidade de autoatendimento poderoso gerenciamento recursos tooyour em poucas etapas.</span><span class="sxs-lookup"><span data-stu-id="58fe4-104">By using Azure Active Directory (Azure AD) B2C, you can add powerful self-service identity management features tooyour desktop app in a few short steps.</span></span> <span data-ttu-id="58fe4-105">Este artigo mostra como toocreate um aplicativo .NET Windows Presentation Foundation (WPF) "lista de tarefas" que inclui a inscrição, entrada de usuário e gerenciamento de perfil.</span><span class="sxs-lookup"><span data-stu-id="58fe4-105">This article will show you how toocreate a .NET Windows Presentation Foundation (WPF) "to-do list" app that includes user sign-up, sign-in, and profile management.</span></span> <span data-ttu-id="58fe4-106">aplicativo Hello inclui suporte para inscrição e entrar usando um nome de usuário ou email.</span><span class="sxs-lookup"><span data-stu-id="58fe4-106">hello app will include support for sign-up and sign-in by using a user name or email.</span></span> <span data-ttu-id="58fe4-107">Ele também incluirá o suporte para a inscrição e a entrada usando contas sociais como o Facebook e o Google.</span><span class="sxs-lookup"><span data-stu-id="58fe4-107">It will also include support for sign-up and sign-in by using social accounts such as Facebook and Google.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="58fe4-108">Obter um diretório AD B2C do Azure</span><span class="sxs-lookup"><span data-stu-id="58fe4-108">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="58fe4-109">Antes de usar AD B2C do Azure, você deve criar um diretório ou locatário.</span><span class="sxs-lookup"><span data-stu-id="58fe4-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="58fe4-110">Um diretório é um contêiner para todos os seus usuários, aplicativos, grupos etc.</span><span class="sxs-lookup"><span data-stu-id="58fe4-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="58fe4-111">Se você ainda não tiver um, [crie um diretório B2C](active-directory-b2c-get-started.md) antes de prosseguir neste guia.</span><span class="sxs-lookup"><span data-stu-id="58fe4-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="58fe4-112">Criar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="58fe4-112">Create an application</span></span>
<span data-ttu-id="58fe4-113">Em seguida, você precisa toocreate um aplicativo no seu diretório do B2C.</span><span class="sxs-lookup"><span data-stu-id="58fe4-113">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="58fe4-114">Isso fornece informações do AD do Azure que ele precisa toosecurely se comunicar com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="58fe4-114">This gives Azure AD information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="58fe4-115">toocreate um aplicativo, siga [estas instruções](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="58fe4-115">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span>  <span data-ttu-id="58fe4-116">É necessário que você:</span><span class="sxs-lookup"><span data-stu-id="58fe4-116">Be sure to:</span></span>

* <span data-ttu-id="58fe4-117">Incluir um **cliente nativo** no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="58fe4-117">Include a **native client** in hello application.</span></span>
* <span data-ttu-id="58fe4-118">Saudação de cópia **URI de redirecionamento** `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="58fe4-118">Copy hello **Redirect URI** `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="58fe4-119">É saudação padrão URL para este exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="58fe4-119">It is hello default URL for this code sample.</span></span>
* <span data-ttu-id="58fe4-120">Saudação de cópia **ID do aplicativo** que é atribuído tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="58fe4-120">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="58fe4-121">Você precisará dela mais tarde.</span><span class="sxs-lookup"><span data-stu-id="58fe4-121">You will need it later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="58fe4-122">Criar suas políticas</span><span class="sxs-lookup"><span data-stu-id="58fe4-122">Create your policies</span></span>
<span data-ttu-id="58fe4-123">No Azure AD B2C, cada experiência do usuário é definida por uma [política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="58fe4-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="58fe4-124">Este exemplo de código contém três experiências de identidade: perfil de inscrição, entrada e edição.</span><span class="sxs-lookup"><span data-stu-id="58fe4-124">This code sample contains three identity experiences: sign up, sign in, and edit profile.</span></span> <span data-ttu-id="58fe4-125">Você precisa toocreate uma política para cada tipo, conforme descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="58fe4-125">You need toocreate a policy for each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="58fe4-126">Quando você criar políticas de três hello, certifique-se a:</span><span class="sxs-lookup"><span data-stu-id="58fe4-126">When you create hello three policies, be sure to:</span></span>

* <span data-ttu-id="58fe4-127">Escolha **ID de usuário se inscreve** ou **Email inscrição** na folha de provedores de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="58fe4-127">Choose either **User ID sign-up** or **Email sign-up** in hello identity providers blade.</span></span>
* <span data-ttu-id="58fe4-128">Escolher **Nome de exibição** e outros atributos de inscrição na política de inscrição.</span><span class="sxs-lookup"><span data-stu-id="58fe4-128">Choose **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="58fe4-129">Escolher as declarações **Nome de exibição** e **ID de objeto** como declarações de aplicativo para cada política.</span><span class="sxs-lookup"><span data-stu-id="58fe4-129">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="58fe4-130">Você pode escolher outras declarações também.</span><span class="sxs-lookup"><span data-stu-id="58fe4-130">You can choose other claims as well.</span></span>
* <span data-ttu-id="58fe4-131">Saudação de cópia **nome** de cada política depois de criá-lo.</span><span class="sxs-lookup"><span data-stu-id="58fe4-131">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="58fe4-132">Ele deve ter o prefixo Olá `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="58fe4-132">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="58fe4-133">Você precisará esses nomes de política mais tarde.</span><span class="sxs-lookup"><span data-stu-id="58fe4-133">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="58fe4-134">Depois que você criou com êxito Olá três políticas, você está pronto toobuild seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="58fe4-134">After you have successfully created hello three policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="58fe4-135">Baixar o código de saudação</span><span class="sxs-lookup"><span data-stu-id="58fe4-135">Download hello code</span></span>
<span data-ttu-id="58fe4-136">Olá código para este tutorial [é mantida no GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="58fe4-136">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span></span> <span data-ttu-id="58fe4-137">exemplo de hello toobuild que você vá, você pode [baixar um projeto de esqueleto como um arquivo. zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="58fe4-137">toobuild hello sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span></span> <span data-ttu-id="58fe4-138">Também é possível clonar o esqueleto do hello:</span><span class="sxs-lookup"><span data-stu-id="58fe4-138">You can also clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

<span data-ttu-id="58fe4-139">aplicativo Hello concluída também é [disponível como um arquivo. zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) ou em Olá `complete` ramificação da saudação mesmo repositório.</span><span class="sxs-lookup"><span data-stu-id="58fe4-139">hello completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) or on hello `complete` branch of hello same repository.</span></span>

<span data-ttu-id="58fe4-140">Depois de baixar o código de exemplo hello, Olá abra o Visual Studio. sln arquivo tooget é iniciado.</span><span class="sxs-lookup"><span data-stu-id="58fe4-140">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="58fe4-141">Olá `TaskClient` projeto é Olá aplicativo de área de trabalho do WPF que Olá usuário interage com.</span><span class="sxs-lookup"><span data-stu-id="58fe4-141">hello `TaskClient` project is hello WPF desktop application that hello user interacts with.</span></span> <span data-ttu-id="58fe4-142">Para fins de saudação deste tutorial, ele chama uma tarefa de back-end API da web, hospedado no Azure, que armazena a lista de tarefas de cada usuário.</span><span class="sxs-lookup"><span data-stu-id="58fe4-142">For hello purposes of this tutorial, it calls a back-end task web API, hosted in Azure, that stores each user's to-do list.</span></span>  <span data-ttu-id="58fe4-143">Você não precisa toobuild Olá web API, já está em execução para você.</span><span class="sxs-lookup"><span data-stu-id="58fe4-143">You do not need toobuild hello web API, we already have it running for you.</span></span>

<span data-ttu-id="58fe4-144">toolearn como uma API da web com segurança autentica solicitações usando o Azure AD B2C, confira o [API da web Introdução artigo](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="58fe4-144">toolearn how a web API securely authenticates requests by using Azure AD B2C, check out the [web API getting started article](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="execute-policies"></a><span data-ttu-id="58fe4-145">Executar políticas</span><span class="sxs-lookup"><span data-stu-id="58fe4-145">Execute policies</span></span>
<span data-ttu-id="58fe4-146">Seu aplicativo se comunica com o Azure AD B2C enviando mensagens de autenticação que especificam a diretiva Olá quiserem tooexecute como parte da solicitação HTTP de saudação.</span><span class="sxs-lookup"><span data-stu-id="58fe4-146">Your app communicates with Azure AD B2C by sending authentication messages that specify hello policy they want tooexecute as part of hello HTTP request.</span></span> <span data-ttu-id="58fe4-147">.NET para aplicativos de desktop, você pode usar o hello visualizar mensagens de autenticação OAuth 2.0 do toosend biblioteca de autenticação da Microsoft (MSAL), execute as políticas e obter tokens que chamam APIs web.</span><span class="sxs-lookup"><span data-stu-id="58fe4-147">For .NET desktop applications, you can use hello preview Microsoft Authentication Library (MSAL) toosend OAuth 2.0 authentication messages, execute policies, and get tokens that call web APIs.</span></span>

### <a name="install-msal"></a><span data-ttu-id="58fe4-148">Instalar MSAL</span><span class="sxs-lookup"><span data-stu-id="58fe4-148">Install MSAL</span></span>
<span data-ttu-id="58fe4-149">Adicionar MSAL toohello `TaskClient` projeto usando Olá Visual Studio Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="58fe4-149">Add MSAL toohello `TaskClient` project by using hello Visual Studio Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a><span data-ttu-id="58fe4-150">Insira seus detalhes B2C</span><span class="sxs-lookup"><span data-stu-id="58fe4-150">Enter your B2C details</span></span>
<span data-ttu-id="58fe4-151">Arquivo hello abra `Globals.cs` e substitua cada um dos valores de propriedade Olá com seus próprios.</span><span class="sxs-lookup"><span data-stu-id="58fe4-151">Open hello file `Globals.cs` and replace each of hello property values with your own.</span></span> <span data-ttu-id="58fe4-152">Essa classe é usada em todo `TaskClient` tooreference usado valores.</span><span class="sxs-lookup"><span data-stu-id="58fe4-152">This class is used throughout `TaskClient` tooreference commonly used values.</span></span>

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

### <a name="create-hello-publicclientapplication"></a><span data-ttu-id="58fe4-153">Criar hello PublicClientApplication</span><span class="sxs-lookup"><span data-stu-id="58fe4-153">Create hello PublicClientApplication</span></span>
<span data-ttu-id="58fe4-154">a classe principal Olá de MSAL é `PublicClientApplication`.</span><span class="sxs-lookup"><span data-stu-id="58fe4-154">hello primary class of MSAL is `PublicClientApplication`.</span></span> <span data-ttu-id="58fe4-155">Essa classe representa o aplicativo no sistema de saudação do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="58fe4-155">This class represents your application in hello Azure AD B2C system.</span></span> <span data-ttu-id="58fe4-156">Quando hello inicializa do aplicativo, crie uma instância de `PublicClientApplication` em `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="58fe4-156">When hello app initalizes, create an instance of `PublicClientApplication` in `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="58fe4-157">Isso pode ser usado em toda a janela de saudação.</span><span class="sxs-lookup"><span data-stu-id="58fe4-157">This can be used throughout hello window.</span></span>

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens toopersist when hello user closes hello app,
        // we've extended hello MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a><span data-ttu-id="58fe4-158">Iniciar um fluxo de inscrição</span><span class="sxs-lookup"><span data-stu-id="58fe4-158">Initiate a sign-up flow</span></span>
<span data-ttu-id="58fe4-159">Quando um usuário opta por toosigns backup, você deseja tooinitiate um fluxo de inscrição que usa a política de inscrição Olá criado por você.</span><span class="sxs-lookup"><span data-stu-id="58fe4-159">When a user opts toosigns up, you want tooinitiate a sign-up flow that uses hello sign-up policy you created.</span></span> <span data-ttu-id="58fe4-160">Usando a MSAL, você apenas chama `pca.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="58fe4-160">By using MSAL, you just call `pca.AcquireTokenAsync(...)`.</span></span> <span data-ttu-id="58fe4-161">Olá parâmetros que você passa muito`AcquireTokenAsync(...)` determinar qual token receber, política de saudação usada na solicitação de autenticação hello e muito mais.</span><span class="sxs-lookup"><span data-stu-id="58fe4-161">hello parameters you pass too`AcquireTokenAsync(...)` determine which token you receive, hello policy used in hello authentication request, and more.</span></span>

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use hello app's clientId here as hello scope parameter, indicating that
        // you want a token toohello your app's backend web API (represented by
        // hello cloud hosted task API).  Use hello UiOptions.ForceLogin flag to
        // indicate tooMSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in hello app that hello user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When hello request completes successfully, you can get user
        // information from hello AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After hello sign up successfully completes, display hello user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of hello policy.
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

### <a name="initiate-a-sign-in-flow"></a><span data-ttu-id="58fe4-162">Iniciar um fluxo de entrada</span><span class="sxs-lookup"><span data-stu-id="58fe4-162">Initiate a sign-in flow</span></span>
<span data-ttu-id="58fe4-163">Você pode iniciar um fluxo de entrada hello mesma maneira que você inicia um fluxo de inscrição.</span><span class="sxs-lookup"><span data-stu-id="58fe4-163">You can initiate a sign-in flow in hello same way that you initiate a sign-up flow.</span></span> <span data-ttu-id="58fe4-164">Quando um usuário faz logon, verifique Olá mesmo chamar tooMSAL, desta vez usando sua política de entrada:</span><span class="sxs-lookup"><span data-stu-id="58fe4-164">When a user signs in, make hello same call tooMSAL, this time by using your sign-in policy:</span></span>

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

### <a name="initiate-an-edit-profile-flow"></a><span data-ttu-id="58fe4-165">Iniciar um fluxo de edição de perfil</span><span class="sxs-lookup"><span data-stu-id="58fe4-165">Initiate an edit-profile flow</span></span>
<span data-ttu-id="58fe4-166">Novamente, você pode executar uma política de edição de perfil em Olá mesmo modo:</span><span class="sxs-lookup"><span data-stu-id="58fe4-166">Again, you can execute an edit-profile policy in hello same fashion:</span></span>

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

<span data-ttu-id="58fe4-167">Em todos esses casos, MSAL retornará um token em `AuthenticationResult` ou gerará uma exceção.</span><span class="sxs-lookup"><span data-stu-id="58fe4-167">In all of these cases, MSAL either returns a token in `AuthenticationResult` or throws an exception.</span></span> <span data-ttu-id="58fe4-168">Cada vez que você obtém um token de MSAL, você pode usar o hello `AuthenticationResult.User` tooupdate Olá usuário dados no aplicativo hello, como saudação da interface do usuário do objeto.</span><span class="sxs-lookup"><span data-stu-id="58fe4-168">Each time you get a token from MSAL, you can use hello `AuthenticationResult.User` object tooupdate hello user data in hello app, such as hello UI.</span></span> <span data-ttu-id="58fe4-169">O ADAL também caches Olá token para uso em outras partes do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="58fe4-169">ADAL also caches hello token for use in other parts of hello application.</span></span>

### <a name="check-for-tokens-on-app-start"></a><span data-ttu-id="58fe4-170">Verificar se há tokens na inicialização do aplicativo</span><span class="sxs-lookup"><span data-stu-id="58fe4-170">Check for tokens on app start</span></span>
<span data-ttu-id="58fe4-171">Você também pode usar o controle de tookeep MSAL Olá da entrada de estado do usuário.</span><span class="sxs-lookup"><span data-stu-id="58fe4-171">You can also use MSAL tookeep track of hello user's sign-in state.</span></span>  <span data-ttu-id="58fe4-172">Neste aplicativo, queremos Olá usuário tooremain conectado mesmo depois que fechar o aplicativo hello e abri-la novamente.</span><span class="sxs-lookup"><span data-stu-id="58fe4-172">In this app, we want hello user tooremain signed in even after they close hello app & re-open it.</span></span>  <span data-ttu-id="58fe4-173">Dentro de saudação `OnInitialized` substituir, use do MSAL `AcquireTokenSilent` método toocheck para tokens em cache:</span><span class="sxs-lookup"><span data-stu-id="58fe4-173">Back inside hello `OnInitialized` override, use MSAL's `AcquireTokenSilent` method toocheck for cached tokens:</span></span>

```C#
AuthenticationResult result = null;
try
{
    // If hello user has has a token cached with any policy, we'll display them as signed-in.
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
        // There are no tokens in hello cache.  Proceed without calling hello tooDo list service.
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

## <a name="call-hello-task-api"></a><span data-ttu-id="58fe4-174">Chamar API de tarefa Olá</span><span class="sxs-lookup"><span data-stu-id="58fe4-174">Call hello task API</span></span>
<span data-ttu-id="58fe4-175">Você agora usaram políticas de tooexecute MSAL e obter tokens.</span><span class="sxs-lookup"><span data-stu-id="58fe4-175">You have now used MSAL tooexecute policies and get tokens.</span></span>  <span data-ttu-id="58fe4-176">Quando você quiser toouse uma API de tarefa esses tokens toocall hello, você pode usar novamente do MSAL `AcquireTokenSilent` método toocheck para tokens em cache:</span><span class="sxs-lookup"><span data-stu-id="58fe4-176">When you want toouse one these tokens toocall hello task API, you can again use MSAL's `AcquireTokenSilent` method toocheck for cached tokens:</span></span>

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want toocheck for a cached token, independent of whatever policy was used tooacquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent tooindicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch hello exception and show hello user a message.
    catch (MsalException ex)
    {
        // There is no access token in hello cache, so prompt hello user toosign-in.
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

<span data-ttu-id="58fe4-177">Olá quando chamada muito`AcquireTokenSilentAsync(...)` for bem-sucedido e um token é encontrada no cache de saudação, você pode adicionar toohello token Olá `Authorization` cabeçalho de solicitação HTTP de saudação.</span><span class="sxs-lookup"><span data-stu-id="58fe4-177">When hello call too`AcquireTokenSilentAsync(...)` succeeds and a token is found in hello cache, you can add hello token toohello `Authorization` header of hello HTTP request.</span></span> <span data-ttu-id="58fe4-178">API da web de tarefa Olá usará a lista de tarefas pendentes de cabeçalho tooauthenticate Olá solicitação tooread saudação do usuário:</span><span class="sxs-lookup"><span data-stu-id="58fe4-178">hello task web API will use this header tooauthenticate hello request tooread hello user's to-do list:</span></span>

```C#
    ...
    // Once hello token has been returned by MSAL, add it toohello http authorization header, before making hello call tooaccess hello tooDo list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call hello tooDo list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-hello-user-out"></a><span data-ttu-id="58fe4-179">Usuário de saudação Sign-out</span><span class="sxs-lookup"><span data-stu-id="58fe4-179">Sign hello user out</span></span>
<span data-ttu-id="58fe4-180">Finalmente, você pode usar MSAL tooend uma sessão do usuário com o aplicativo hello quando Olá usuário seleciona **sair**.  Ao usar MSAL, isso é feito ao desmarcar todos os tokens de saudação do cache de token de saudação de:</span><span class="sxs-lookup"><span data-stu-id="58fe4-180">Finally, you can use MSAL tooend a user's session with hello app when hello user selects **Sign out**.  When using MSAL, this is accomplished by clearing all of hello tokens from hello token cache:</span></span>

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of hello user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in hello browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update hello UI tooshow hello user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-hello-sample-app"></a><span data-ttu-id="58fe4-181">Execute o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="58fe4-181">Run hello sample app</span></span>
<span data-ttu-id="58fe4-182">Por fim, compilar e executar o exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="58fe4-182">Finally, build and run hello sample.</span></span>  <span data-ttu-id="58fe4-183">Inscreva-se para o aplicativo hello usando um nome de usuário ou endereço de email.</span><span class="sxs-lookup"><span data-stu-id="58fe4-183">Sign up for hello app by using an email address or user name.</span></span> <span data-ttu-id="58fe4-184">Sair e entrar novamente como Olá mesmo usuário.</span><span class="sxs-lookup"><span data-stu-id="58fe4-184">Sign out and sign back in as hello same user.</span></span> <span data-ttu-id="58fe4-185">Edite perfil do usuário.</span><span class="sxs-lookup"><span data-stu-id="58fe4-185">Edit that user's profile.</span></span> <span data-ttu-id="58fe4-186">Saia e entre novamente como outro usuário.</span><span class="sxs-lookup"><span data-stu-id="58fe4-186">Sign out and sign up by using a different user.</span></span>

## <a name="add-social-idps"></a><span data-ttu-id="58fe4-187">Adicionar IDPs sociais</span><span class="sxs-lookup"><span data-stu-id="58fe4-187">Add social IDPs</span></span>
<span data-ttu-id="58fe4-188">Atualmente, o aplicativo hello dá suporte apenas inscrição de usuário e entrar que usam **contas locais**.</span><span class="sxs-lookup"><span data-stu-id="58fe4-188">Currently, hello app supports only user sign-up and sign-in that use **local accounts**.</span></span> <span data-ttu-id="58fe4-189">Essas são as contas armazenadas em seu diretório do B2C que usam um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="58fe4-189">These are accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="58fe4-190">Com o Azure AD B2C, você pode adicionar suporte a outros provedores de identidade (IDPs), sem alterar qualquer código.</span><span class="sxs-lookup"><span data-stu-id="58fe4-190">By using Azure AD B2C, you can add support for other identity providers (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="58fe4-191">tooadd social IDPs tooyour aplicativo, comece seguindo Olá detalhadas as instruções neste artigo.</span><span class="sxs-lookup"><span data-stu-id="58fe4-191">tooadd social IDPs tooyour app, begin by following hello detailed instructions in these articles.</span></span> <span data-ttu-id="58fe4-192">Para cada IDP toosupport desejado, você precisa tooregister um aplicativo no sistema e obter uma ID de cliente.</span><span class="sxs-lookup"><span data-stu-id="58fe4-192">For each IDP you want toosupport, you need tooregister an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="58fe4-193">Configurar o Facebook como um IDP</span><span class="sxs-lookup"><span data-stu-id="58fe4-193">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="58fe4-194">Configurar o Google como um IDP</span><span class="sxs-lookup"><span data-stu-id="58fe4-194">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="58fe4-195">Configurar o Amazon como um IDP</span><span class="sxs-lookup"><span data-stu-id="58fe4-195">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="58fe4-196">Configurar o LinkedIn como um IDP</span><span class="sxs-lookup"><span data-stu-id="58fe4-196">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="58fe4-197">Depois de adicionar o diretório de tooyour B2C de provedores de identidade hello, você precisa tooedit cada um dos seus três políticas tooinclude Olá IDPs novo, como descrita em Olá [artigo de referência de política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="58fe4-197">After you add hello identity providers tooyour B2C directory, you need tooedit each of your three policies tooinclude hello new IDPs, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="58fe4-198">Depois de salvar suas políticas, execute novamente o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="58fe4-198">After you save your policies, run hello app again.</span></span> <span data-ttu-id="58fe4-199">Você deve ver Olá que idps novo são adicionados como opções de entrada e inscreva-se em cada uma das suas experiências de identidade.</span><span class="sxs-lookup"><span data-stu-id="58fe4-199">You should see hello new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="58fe4-200">Você pode fazer experiências com suas políticas e observar os efeitos de saudação em seu aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="58fe4-200">You can experiment with your policies and observe hello effects on your sample app.</span></span> <span data-ttu-id="58fe4-201">Adicione ou remova IDPs, manipule declarações de aplicativo ou altere os atributos de inscrição.</span><span class="sxs-lookup"><span data-stu-id="58fe4-201">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="58fe4-202">Experimente até conseguir entender como as políticas, as solicitações de autenticação e MSAL funcionam juntos.</span><span class="sxs-lookup"><span data-stu-id="58fe4-202">Experiment until you can see how policies, authentication requests, and MSAL tie together.</span></span>

<span data-ttu-id="58fe4-203">Para referência, Olá concluída exemplo [é fornecido como um arquivo. zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="58fe4-203">For reference, hello completed sample [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="58fe4-204">Você também pode cloná-lo do GitHub:</span><span class="sxs-lookup"><span data-stu-id="58fe4-204">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
