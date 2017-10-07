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
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a>Azure AD B2C: criar um aplicativo da área de trabalho do Windows
Usando B2C do Azure Active Directory (AD do Azure), você pode adicionar o aplicativo de área de trabalho do identidade de autoatendimento poderoso gerenciamento recursos tooyour em poucas etapas. Este artigo mostra como toocreate um aplicativo .NET Windows Presentation Foundation (WPF) "lista de tarefas" que inclui a inscrição, entrada de usuário e gerenciamento de perfil. aplicativo Hello inclui suporte para inscrição e entrar usando um nome de usuário ou email. Ele também incluirá o suporte para a inscrição e a entrada usando contas sociais como o Facebook e o Google.

## <a name="get-an-azure-ad-b2c-directory"></a>Obter um diretório AD B2C do Azure
Antes de usar AD B2C do Azure, você deve criar um diretório ou locatário.  Um diretório é um contêiner para todos os seus usuários, aplicativos, grupos etc. Se você ainda não tiver um, [crie um diretório B2C](active-directory-b2c-get-started.md) antes de prosseguir neste guia.

## <a name="create-an-application"></a>Criar um aplicativo
Em seguida, você precisa toocreate um aplicativo no seu diretório do B2C. Isso fornece informações do AD do Azure que ele precisa toosecurely se comunicar com seu aplicativo. toocreate um aplicativo, siga [estas instruções](active-directory-b2c-app-registration.md).  É necessário que você:

* Incluir um **cliente nativo** no aplicativo hello.
* Saudação de cópia **URI de redirecionamento** `urn:ietf:wg:oauth:2.0:oob`. É saudação padrão URL para este exemplo de código.
* Saudação de cópia **ID do aplicativo** que é atribuído tooyour aplicativo. Você precisará dela mais tarde.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Criar suas políticas
No Azure AD B2C, cada experiência do usuário é definida por uma [política](active-directory-b2c-reference-policies.md). Este exemplo de código contém três experiências de identidade: perfil de inscrição, entrada e edição. Você precisa toocreate uma política para cada tipo, conforme descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Quando você criar políticas de três hello, certifique-se a:

* Escolha **ID de usuário se inscreve** ou **Email inscrição** na folha de provedores de identidade hello.
* Escolher **Nome de exibição** e outros atributos de inscrição na política de inscrição.
* Escolher as declarações **Nome de exibição** e **ID de objeto** como declarações de aplicativo para cada política. Você pode escolher outras declarações também.
* Saudação de cópia **nome** de cada política depois de criá-lo. Ele deve ter o prefixo Olá `b2c_1_`.  Você precisará esses nomes de política mais tarde.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Depois que você criou com êxito Olá três políticas, você está pronto toobuild seu aplicativo.

## <a name="download-hello-code"></a>Baixar o código de saudação
Olá código para este tutorial [é mantida no GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet). exemplo de hello toobuild que você vá, você pode [baixar um projeto de esqueleto como um arquivo. zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip). Também é possível clonar o esqueleto do hello:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

aplicativo Hello concluída também é [disponível como um arquivo. zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) ou em Olá `complete` ramificação da saudação mesmo repositório.

Depois de baixar o código de exemplo hello, Olá abra o Visual Studio. sln arquivo tooget é iniciado. Olá `TaskClient` projeto é Olá aplicativo de área de trabalho do WPF que Olá usuário interage com. Para fins de saudação deste tutorial, ele chama uma tarefa de back-end API da web, hospedado no Azure, que armazena a lista de tarefas de cada usuário.  Você não precisa toobuild Olá web API, já está em execução para você.

toolearn como uma API da web com segurança autentica solicitações usando o Azure AD B2C, confira o [API da web Introdução artigo](active-directory-b2c-devquickstarts-api-dotnet.md).

## <a name="execute-policies"></a>Executar políticas
Seu aplicativo se comunica com o Azure AD B2C enviando mensagens de autenticação que especificam a diretiva Olá quiserem tooexecute como parte da solicitação HTTP de saudação. .NET para aplicativos de desktop, você pode usar o hello visualizar mensagens de autenticação OAuth 2.0 do toosend biblioteca de autenticação da Microsoft (MSAL), execute as políticas e obter tokens que chamam APIs web.

### <a name="install-msal"></a>Instalar MSAL
Adicionar MSAL toohello `TaskClient` projeto usando Olá Visual Studio Package Manager Console.

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a>Insira seus detalhes B2C
Arquivo hello abra `Globals.cs` e substitua cada um dos valores de propriedade Olá com seus próprios. Essa classe é usada em todo `TaskClient` tooreference usado valores.

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

### <a name="create-hello-publicclientapplication"></a>Criar hello PublicClientApplication
a classe principal Olá de MSAL é `PublicClientApplication`. Essa classe representa o aplicativo no sistema de saudação do Azure AD B2C. Quando hello inicializa do aplicativo, crie uma instância de `PublicClientApplication` em `MainWindow.xaml.cs`. Isso pode ser usado em toda a janela de saudação.

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

### <a name="initiate-a-sign-up-flow"></a>Iniciar um fluxo de inscrição
Quando um usuário opta por toosigns backup, você deseja tooinitiate um fluxo de inscrição que usa a política de inscrição Olá criado por você. Usando a MSAL, você apenas chama `pca.AcquireTokenAsync(...)`. Olá parâmetros que você passa muito`AcquireTokenAsync(...)` determinar qual token receber, política de saudação usada na solicitação de autenticação hello e muito mais.

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

### <a name="initiate-a-sign-in-flow"></a>Iniciar um fluxo de entrada
Você pode iniciar um fluxo de entrada hello mesma maneira que você inicia um fluxo de inscrição. Quando um usuário faz logon, verifique Olá mesmo chamar tooMSAL, desta vez usando sua política de entrada:

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

### <a name="initiate-an-edit-profile-flow"></a>Iniciar um fluxo de edição de perfil
Novamente, você pode executar uma política de edição de perfil em Olá mesmo modo:

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

Em todos esses casos, MSAL retornará um token em `AuthenticationResult` ou gerará uma exceção. Cada vez que você obtém um token de MSAL, você pode usar o hello `AuthenticationResult.User` tooupdate Olá usuário dados no aplicativo hello, como saudação da interface do usuário do objeto. O ADAL também caches Olá token para uso em outras partes do aplicativo hello.

### <a name="check-for-tokens-on-app-start"></a>Verificar se há tokens na inicialização do aplicativo
Você também pode usar o controle de tookeep MSAL Olá da entrada de estado do usuário.  Neste aplicativo, queremos Olá usuário tooremain conectado mesmo depois que fechar o aplicativo hello e abri-la novamente.  Dentro de saudação `OnInitialized` substituir, use do MSAL `AcquireTokenSilent` método toocheck para tokens em cache:

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

## <a name="call-hello-task-api"></a>Chamar API de tarefa Olá
Você agora usaram políticas de tooexecute MSAL e obter tokens.  Quando você quiser toouse uma API de tarefa esses tokens toocall hello, você pode usar novamente do MSAL `AcquireTokenSilent` método toocheck para tokens em cache:

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

Olá quando chamada muito`AcquireTokenSilentAsync(...)` for bem-sucedido e um token é encontrada no cache de saudação, você pode adicionar toohello token Olá `Authorization` cabeçalho de solicitação HTTP de saudação. API da web de tarefa Olá usará a lista de tarefas pendentes de cabeçalho tooauthenticate Olá solicitação tooread saudação do usuário:

```C#
    ...
    // Once hello token has been returned by MSAL, add it toohello http authorization header, before making hello call tooaccess hello tooDo list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call hello tooDo list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-hello-user-out"></a>Usuário de saudação Sign-out
Finalmente, você pode usar MSAL tooend uma sessão do usuário com o aplicativo hello quando Olá usuário seleciona **sair**.  Ao usar MSAL, isso é feito ao desmarcar todos os tokens de saudação do cache de token de saudação de:

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

## <a name="run-hello-sample-app"></a>Execute o aplicativo de exemplo hello
Por fim, compilar e executar o exemplo hello.  Inscreva-se para o aplicativo hello usando um nome de usuário ou endereço de email. Sair e entrar novamente como Olá mesmo usuário. Edite perfil do usuário. Saia e entre novamente como outro usuário.

## <a name="add-social-idps"></a>Adicionar IDPs sociais
Atualmente, o aplicativo hello dá suporte apenas inscrição de usuário e entrar que usam **contas locais**. Essas são as contas armazenadas em seu diretório do B2C que usam um nome de usuário e senha. Com o Azure AD B2C, você pode adicionar suporte a outros provedores de identidade (IDPs), sem alterar qualquer código.

tooadd social IDPs tooyour aplicativo, comece seguindo Olá detalhadas as instruções neste artigo. Para cada IDP toosupport desejado, você precisa tooregister um aplicativo no sistema e obter uma ID de cliente.

* [Configurar o Facebook como um IDP](active-directory-b2c-setup-fb-app.md)
* [Configurar o Google como um IDP](active-directory-b2c-setup-goog-app.md)
* [Configurar o Amazon como um IDP](active-directory-b2c-setup-amzn-app.md)
* [Configurar o LinkedIn como um IDP](active-directory-b2c-setup-li-app.md)

Depois de adicionar o diretório de tooyour B2C de provedores de identidade hello, você precisa tooedit cada um dos seus três políticas tooinclude Olá IDPs novo, como descrita em Olá [artigo de referência de política](active-directory-b2c-reference-policies.md). Depois de salvar suas políticas, execute novamente o aplicativo hello. Você deve ver Olá que idps novo são adicionados como opções de entrada e inscreva-se em cada uma das suas experiências de identidade.

Você pode fazer experiências com suas políticas e observar os efeitos de saudação em seu aplicativo de exemplo. Adicione ou remova IDPs, manipule declarações de aplicativo ou altere os atributos de inscrição. Experimente até conseguir entender como as políticas, as solicitações de autenticação e MSAL funcionam juntos.

Para referência, Olá concluída exemplo [é fornecido como um arquivo. zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip). Você também pode cloná-lo do GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
