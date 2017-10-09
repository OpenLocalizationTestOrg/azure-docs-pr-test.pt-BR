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
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a>Integrar o AD do Azure em um aplicativo WPF de área de trabalho do Windows
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Se você estiver desenvolvendo um aplicativo de área de trabalho, o AD do Azure torna simples e direta para você tooauthenticate os usuários com suas contas do Active Directory.  Ele também permite que seu aplicativo toosecurely consumir qualquer web API protegida pelo AD do Azure, como Olá APIs do Office 365 ou Olá API do Azure.

Para clientes nativos .NET que necessitam de recursos tooaccess protegido, o AD do Azure fornece Olá biblioteca de autenticação do Active Directory ou ADAL.  Única finalidade do ADAL é toomake fácil para seus tokens de acesso do aplicativo tooget.  toodemonstrate facilidade é, aqui, criaremos um aplicativo de lista de tarefas do .NET WPF que:

* Obtém acesso tokens para chamar a API do Azure AD Graph hello usando Olá [protocolo de autenticação OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Pesquisa um diretório para usuários com um determinado alias.
* Desconecta usuários.

aplicativo de trabalho concluída hello de toobuild, você precisará:

1. Registrar seu aplicativo no Azure AD.
2. Instalar e configurar a ADAL.
3. Use ADAL tooget tokens do AD do Azure.

tooget iniciado, [baixar o esqueleto do aplicativo hello](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) ou [baixar exemplo hello concluída](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).  Você também precisará de um locatário do AD do Azure no qual você possa criar usuários e registrar um aplicativo.  Se você ainda não tiver um locatário, [Saiba como tooget uma](active-directory-howto-tenant.md).

## <a name="1-register-hello-directorysearcher-application"></a>1. Registrar Olá DirectorySearcher aplicativo
tooenable tokens de tooget seu aplicativo, primeiro será necessário tooregistê-lo no AD do Azure locatário e atribuí-lo Olá tooaccess de permissão do Azure AD Graph API:

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Na barra superior do hello, clique em sua conta e em Olá **diretório** , escolha um locatário do Active Directory Olá onde você deseja tooregister seu aplicativo.
3. Clique em **mais serviços** Olá navegação à esquerda e escolha **Active Directory do Azure**.
4. Clique em **Registros do Aplicativo** e escolha **Adicionar**.
5. Siga os prompts de saudação e criar um novo **aplicativo cliente nativo**.
  * Olá **nome** da saudação aplicativo descrevem os usuários tooend de aplicativos
  * Olá **Uri de redirecionamento** é uma combinação de esquema e a cadeia de caracteres que o AD do Azure usará tooreturn respostas de token.  Insira um aplicativo de tooyour específico de valor, por exemplo, `http://DirectorySearcher`.
6. Depois de concluir o registro, o AAD atribuirá a seu aplicativo uma ID do Aplicativo única.  Você precisará desse valor nas seções de Avançar Olá, portanto copie-o da página de aplicativo hello.
7. De saudação **configurações** escolha **permissões necessárias** e escolha **adicionar**. Selecione Olá **Microsoft Graph** como Olá API e adicione Olá **ler dados do diretório** permissão em **permissões delegadas**.  Isso permitirá a saudação de tooquery aplicativo Graph API para os usuários.

## <a name="2-install--configure-adal"></a>2. Instalar e Configurar o ADAL
Agora que você tem um aplicativo no AD do Azure, você pode instalar a ADAL e escrever seu código relacionado à identidade.  Para toocommunicate capaz de toobe ADAL com o Azure AD, é necessário tooprovide-lo com algumas informações sobre o registro do seu aplicativo.

* Comece adicionando o projeto de DirectorySearcher toohello ADAL usando Olá Package Manager Console.

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* No projeto de DirectorySearcher hello, abra `app.config`.  Substituir valores de saudação de elementos Olá Olá `<appSettings>` Olá de tooreflect seção valores de entrada hello Portal do Azure.  Seu código fará referência a esses valores sempre que ele usar a ADAL.
  * Olá `ida:Tenant` é o domínio de saudação do seu locatário do AD do Azure, por exemplo, contoso.onmicrosoft.com
  * Olá `ida:ClientId` é Olá clientId do aplicativo é copiada do portal de saudação.
  * Olá `ida:RedirectUri` é hello registrado no portal de saudação do url de redirecionamento.

## <a name="3----use-adal-tooget-tokens-from-aad"></a>3.    Usar Tokens tooGet ADAL do AAD
Olá princípio básico de ADAL é que sempre que seu aplicativo precisa de um token de acesso, ele simplesmente chama `authContext.AcquireTokenAsync(...)`, e ADAL Olá rest.  

* Em Olá `DirectorySearcher` projeto, abra `MainWindow.xaml.cs` e localize Olá `MainWindow()` método.  primeira etapa de saudação é tooinitialize seu aplicativo `AuthenticationContext` -ADAL da classe principal.  Isso é onde você passa ADAL Olá coordenadas necessárias toocommunicate com o Azure AD e informe como toocache tokens.

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* Localizar agora Olá `Search(...)` método, que será invocado quando Olá usuário cliks hello "Pesquisar" botão na interface de usuário do aplicativo hello.  Esse método torna um tooquery de toohello do Azure AD Graph API de solicitação GET para usuários cujo UPN começa com hello dado o termo de pesquisa.  Mas em Olá de tooquery ordem API do Graph, você precisa tooinclude um access_token no hello `Authorization` cabeçalho da saudação solicitar - onde ADAL é.

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
* Quando o aplicativo solicita um token chamando `AcquireTokenAsync(...)`, ADAL tentará tooreturn um token sem solicitar credenciais de usuário hello.  Se ADAL determina que o usuário Olá precisa toosign em tooget um token, ele exibe uma caixa de diálogo de logon, coletar credenciais de saudação do usuário e retorna um token após a autenticação bem-sucedida.  Se o ADAL está tooreturn não é possível um token por qualquer motivo, ela irá gerar um `AdalException`.
* Observe que Olá `AuthenticationResult` objeto contém um `UserInfo` objeto que pode ser usado toocollect informações seu aplicativo pode ser necessário.  Em Olá DirectorySearcher, `UserInfo` é a interface do usuário do aplicativo de saudação toocustomize usado com a id de saudação do usuário.
* Quando o usuário Olá clica hello "Sair" botão, queremos tooensure que Olá próxima chamada muito`AcquireTokenAsync(...)` pedirá Olá usuário toosign no.  ADAL, isso é tão fácil quanto limpar o cache de token hello:

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear hello token cache
    authContext.TokenCache.Clear();

    ...
}
```

* No entanto, se o usuário Olá não botão hello "Sair", você desejará toomaintain Olá sessão de usuário para Olá próxima vez que executar Olá DirectorySearcher.  Quando o aplicativo hello é iniciado, você pode verificar o cache de token do ADAL para um token existente e atualize o hello da interface do usuário adequadamente.  Em Olá `CheckForCachedToken()` método, fazer outra chamada muito`AcquireTokenAsync(...)`, desta vez passando Olá `PromptBehavior.Never` parâmetro.  `PromptBehavior.Never`informará ADAL que usuário Olá não deve ser solicitado para entrar e ADAL em vez disso, gerar uma exceção se for tooreturn não é possível um token.

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

Parabéns! Você agora tem um aplicativo .NET WPF que tem Olá capacidade tooauthenticate usuários de trabalho, com segurança chamar APIs da Web usando o OAuth 2.0 e obter informações básicas sobre o usuário Olá.  Se você ainda não fez isso, agora é Olá tempo toopopulate seu locatário com alguns usuários.  Execute o aplicativo DirectorySearcher e faça logon com um desses usuários.  Procure por outros usuários com base em seus UPNs.  Feche o aplicativo hello e execute-a novamente.  Observe como a sessão do usuário Olá permanece intacta.  Saia e faça logon novamente como outro usuário.

ADAL torna fácil tooincorporate todos esses recursos comuns de identidade em seu aplicativo.  Cuida de todo o trabalho sujo Olá para você - gerenciamento de cache, suporte ao protocolo OAuth, apresentando usuário Olá com um logon de interface do usuário, atualizando tokens expirados e muito mais.  Tudo o que você realmente precisa de tooknow é uma única chamada de API, `authContext.AcquireTokenAsync(...)`.

Para referência, o exemplo hello concluída (sem os valores de configuração) é fornecido [aqui](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).  Agora você pode mover tooadditional cenários.  Você pode desejar tootry:

[Proteger uma API da Web .NET com o Azure AD >>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

