---
title: v 2.0 do Active Directory aaaAzure aplicativo nativo do .NET | Microsoft Docs
description: "Como toobuild um aplicativo nativo do .NET que assina os usuários com ambos os Account pessoal da Microsoft e contas corporativa ou escolar."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 46d81e09-bad0-44ce-9026-881805976e72
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/30/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 9418eeba02b800feee5cb00219574eb16506f0a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-windows-desktop-app"></a>Adicionar entrada tooa aplicativo de área de trabalho do Windows
Com o ponto de extremidade de Olá Olá v 2.0, você pode adicionar rapidamente aplicativos de área de trabalho tooyour autenticação com suporte para ambas as contas Microsoft pessoais e contas corporativa ou escolar.  Ele também permite que seu aplicativo toosecurely se comunicar com um back-end da web api, bem como [Olá Microsoft Graph](https://graph.microsoft.io) e alguns Olá [Unified APIs do Office 365](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).

> [!NOTE]
> Nem todos os recursos e cenários do Azure AD (Active Directory) têm suporte pelo ponto de extremidade do hello v 2.0.  toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).
> 
> 

Para [.NET aplicativos nativos que são executados em um dispositivo](active-directory-v2-flows.md#mobile-and-native-apps), o AD do Azure fornece Olá biblioteca de autenticação de identidade do Microsoft ou MSAL.  Única finalidade do MSAL é toomake fácil para seu aplicativo tooget tokens para chamar serviços da web.  toodemonstrate facilidade é, aqui, criaremos um aplicativo de lista de tarefas do .NET WPF que:

* Sinais Olá usuário no & obtém acesso tokens usando Olá [protocolo de autenticação OAuth 2.0](active-directory-v2-protocols.md).
* Chama com segurança um serviço da Web de Lista de Tarefas back-end, que também é protegido pelo OAuth 2.0.
* Usuário de saudação sinais out.

## <a name="download-sample-code"></a>Baixar código de exemplo
código de saudação para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).  toofollow ao longo, você pode [baixar o esqueleto do aplicativo hello como. zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) ou esqueleto de saudação do clone:

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

aplicativo Hello concluída é fornecido no final da saudação deste tutorial também.

## <a name="register-an-app"></a>Registrar um aplicativo
Crie um novo aplicativo em [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ou siga estas [etapas detalhadas](active-directory-v2-app-registration.md).  Não se esqueça de:

* Cópia para baixo Olá **Id do aplicativo** atribuído tooyour aplicativo, você precisará dele em breve.
* Adicionar Olá **Mobile** plataforma para seu aplicativo.

## <a name="install--configure-msal"></a>Instalar e Configurar o MSAL
Agora que você tem um aplicativo registrado na Microsoft, pode instalar o MSAL e gravar seu código relacionado à identidade.  Ponto de extremidade do MSAL toobe toocommunicate capaz de saudação v 2.0, é necessário tooprovide-lo com algumas informações sobre o registro do seu aplicativo.

* Comece adicionando MSAL toohello TodoListClient projeto usando Olá Package Manager Console.

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* No projeto de TodoListClient hello, abra `app.config`.  Substituir valores de saudação de elementos Olá Olá `<appSettings>` Olá de tooreflect seção valores entrada no portal de registro de aplicativo hello.  Seu código fará referência a esses valores sempre que ele usar a MSAL.
  
  * Olá `ida:ClientId` é hello **Id do aplicativo** do seu aplicativo é copiada do portal de saudação.
* No hello serviço TodoList projeto, abra `web.config` na raiz de saudação do projeto de saudação.  
  
  * Substituir saudação `ida:Audience` valor com hello mesmo **Id do aplicativo** do portal de saudação.

## <a name="use-msal-tooget-tokens"></a>Usar os tokens de tooget MSAL
Olá MSAL de princípio básico é que sempre que seu aplicativo precisa de um token de acesso, você simplesmente chamar `app.AcquireToken(...)`, e MSAL Olá rest.  

* Em Olá `TodoListClient` projeto, abra `MainWindow.xaml.cs` e localize Olá `OnInitialized(...)` método.  primeira etapa de saudação é tooinitialize seu aplicativo `PublicClientApplication` -classe principal do MSAL, que representa a aplicativos nativos.  Isso é onde você passa MSAL Olá coordenadas necessárias toocommunicate com o Azure AD e informe como toocache tokens.

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* Quando o aplicativo hello é iniciado, podemos deseja toocheck e veja se o usuário Olá já está conectado em aplicativo hello.  No entanto, nós não desejamos tooinvoke uma entrada da interface do usuário ainda - faremos usuário Olá clique em "Entrar" toodo assim.  Também no hello `OnInitialized(...)` método:

```C#
// As hello app starts, we want toocheck toosee if hello user is already signed in.
// You can do so by trying tooget a token from MSAL, using hello method
// AcquireTokenSilent.  This forces MSAL toothrow an exception if it cannot
// get a token for hello user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in hello cache - or MSAL was able tooget a new oen via refresh token.
    // Proceed toofetch hello user's tasks from hello TodoListService via hello GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, hello app should take no action,
        // and simply show hello user hello sign in button.
    }
    else
    {
        // Here, we catch all other MsalExceptions
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
}

```

* Se o usuário Olá não está conectado e eles botão hello "Entrar", é deseja tooinvoke um interface de usuário de logon e usuário Olá inserir suas credenciais.  Implementar o manipulador de botão Olá entrar:

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign hello user out if they clicked hello "Clear Cache" button

// If hello user clicked hello 'Sign-In' button, force
// MSAL tooprompt hello user for credentials by using
// AcquireTokenAsync, a method that is guaranteed tooshow a prompt toohello user.
// MSAL will get a token for hello TodoListService and cache it for you.

AuthenticationResult result = null;
try
{
    result = await app.AcquireTokenAsync(new string[] { clientId });
    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    // If MSAL cannot get a token, it will throw an exception.
    // If hello user canceled hello login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by hello user");
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


}
```

* Se Olá usuário com êxito entrar, MSAL receberá e um token de cache para você, e você poderá continuar Olá toocall `GetTodoList()` método com confiança.  Tudo o que saiu tooget tarefas do usuário é Olá tooimplement `GetTodoList()` método.

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try tooget an access token toocall hello TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL toothrow an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show hello user a message
    // and let them click hello Sign-In button.

    if (ex.ErrorCode == "user_interaction_required")
    {
        MessageBox.Show("Please sign in first");
        SignInButton.Content = "Sign In";
    }
    else
    {
        // In any other case, an unexpected error occurred.

        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }

    return;
}

// Once hello token has been returned by MSAL,
// add it toohello http authorization header,
// before making hello call tooaccess hello tooDo list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When hello user is done managing their To-Do List, they may finally sign out of hello app by clicking hello "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If hello user clicked hello 'clear cache' button,
        // clear hello MSAL token cache and show hello user as signed out.
        // It's also necessary tooclear hello cookies from hello browser
        // control so hello next user has a chance toosign in.

        if (SignInButton.Content.ToString() == "Clear Cache")
        {
                TodoList.ItemsSource = string.Empty;
                app.UserTokenCache.Clear(app.ClientId);
                ClearCookies();
                SignInButton.Content = "Sign In";
                return;
        }

        ...
```

## <a name="run"></a>Executar
Parabéns! Você agora tem um aplicativo .NET WPF que possua Olá capacidade tooauthenticate usuários de trabalho & seguro chamar APIs da Web usando o OAuth 2.0.  Execute os dois projetos e entre com uma conta da Microsoft pessoal ou uma conta corporativa ou de estudante.  Adicione lista de tarefas do usuário do toothat de tarefas.  Saia e entre novamente como tooview de outro usuário sua lista de tarefas pendentes.  Feche o aplicativo hello e execute-a novamente.  Observe como a sessão do usuário Olá permanece intacto – isso ocorre porque o aplicativo hello armazena em cache os tokens em um arquivo local.

MSAL torna fácil tooincorporate recursos comuns de identidade em seu aplicativo, usando contas pessoais e corporativas.  Cuida de todo o trabalho sujo Olá para você - gerenciamento de cache, suporte ao protocolo OAuth, apresentando usuário Olá com um logon de interface do usuário, atualizando tokens expirados e muito mais.  Tudo o que você realmente precisa de tooknow é uma única chamada de API, `app.AcquireTokenAsync(...)`.

Para referência, Olá concluída exemplo (sem os valores de configuração) [é fornecido como. zip aqui](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), ou você pode cloná-lo do GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a>Próximas etapas
Agora você pode ir para tópicos mais avançados.  Você pode desejar tootry:

* [Proteger a saudação TodoListService Web API com o ponto de extremidade do hello v 2.0](active-directory-v2-devquickstarts-dotnet-api.md)

Para obter recursos adicionais, consulte:  

* [Guia do desenvolvedor v 2.0 Olá >>](active-directory-appmodel-v2-overview.md)
* [Marca "msal" de StackOverflow >>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a>Obter atualizações de segurança para nossos produtos
Recomendamos que você tooget as notificações quando os incidentes de segurança ocorrem visitando [essa página](https://technet.microsoft.com/security/dd252948) e assinando tooSecurity alertas de aviso.

