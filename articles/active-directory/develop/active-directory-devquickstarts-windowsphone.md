---
title: "aaaAzure do Windows Phone AD Introdução | Microsoft Docs"
description: Como toobuild um aplicativo do Windows Phone que se integra ao AD do Azure para entrar e chama o AD do Azure usando o OAuth APIs protegidas.
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 66f5ac20-5e1f-4b9d-bb99-9b3305e26416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: e766bfcdfae10483772154f4b5facdec05fc846f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a>Integrar o AD do Azure com um aplicativo do Windows Phone
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> Não há suporte para projetos do Windows Phone 8.1 e de versões anteriores no Visual Studio 2017.  Para saber mais, confira [Direcionamento e compatibilidade da plataforma Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

Se você estiver desenvolvendo um aplicativo do Windows Phone 8.1, o AD do Azure torna simples e direta para você tooauthenticate os usuários com suas contas do Active Directory.  Ele também permite que seu aplicativo toosecurely consumir qualquer web API protegida pelo AD do Azure, como Olá APIs do Office 365 ou Olá API do Azure.

> [!NOTE]
> Este exemplo de código usa ADAL v2.0.  Para a tecnologia mais recente do hello, convém tooinstead tente nosso [Tutorial Universal do Windows usando v 3.0 ADAL](active-directory-devquickstarts-windowsstore.md).  Se, na verdade, você estiver criando um aplicativo para Windows Phone 8.1, esse é o lugar certo hello.  V 2.0 ADAL ainda tem suporte total e é hello forma recomendada de agianst desenvolvimento de aplicativos Windows Phone 8.1 usando o Azure AD.
> 
> 

Para clientes nativos .NET que necessitam de recursos tooaccess protegido, o AD do Azure fornece Olá biblioteca de autenticação do Active Directory ou ADAL.  Única finalidade do ADAL é toomake fácil para seus tokens de acesso do aplicativo tooget.  toodemonstrate facilidade é, aqui, criaremos um "Pesquisador de diretório" aplicativo do Windows Phone 8.1 que:

* Obtém acesso tokens para chamar a API do Azure AD Graph hello usando Olá [protocolo de autenticação OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Pesquisa um diretório para usuários com um determinado UPN.
* Desconecta usuários.

aplicativo de trabalho concluída hello de toobuild, você precisará:

1. Registrar seu aplicativo no Azure AD.
2. Instalar e configurar a ADAL.
3. Use ADAL tooget tokens do AD do Azure.

tooget iniciado, [baixar um projeto de esqueleto](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) ou [baixar exemplo hello concluída](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).  Cada um é uma solução do Visual Studio 2013.  Você também precisará de um locatário do AD do Azure no qual você possa criar usuários e registrar um aplicativo.  Se você ainda não tiver um locatário, [Saiba como tooget uma](active-directory-howto-tenant.md).

## <a name="1-register-hello-directory-searcher-application"></a>1. Registrar Olá aplicativo do Pesquisador de diretório
tooenable tokens de tooget seu aplicativo, primeiro será necessário tooregistê-lo no AD do Azure locatário e atribuí-lo Olá tooaccess de permissão do Azure AD Graph API:

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Na barra superior do hello, clique em sua conta e em Olá **diretório** , escolha um locatário do Active Directory Olá onde você deseja tooregister seu aplicativo.
3. Clique em **mais serviços** Olá navegação à esquerda e escolha **Active Directory do Azure**.
4. Clique em **Registros do Aplicativo** e escolha **Adicionar**.
5. Siga os prompts de saudação e criar um novo **aplicativo cliente nativo**.
  * Olá **nome** da saudação aplicativo descrevem os usuários tooend de aplicativos
  * Olá **Uri de redirecionamento** é uma combinação de esquema e a cadeia de caracteres que o AD do Azure usará tooreturn respostas de token.  Insira um valor de espaço reservado por enquanto, por exemplo, `http://DirectorySearcher`.  Substituiremos este valor posteriormente.
6. Depois de concluir o registro, o AAD atribuirá a seu aplicativo uma ID do Aplicativo única.  Você precisará desse valor nas seções de Avançar hello, portanto copiá-lo do guia do aplicativo hello.
7. De saudação **configurações** escolha **permissões necessárias** e escolha **adicionar**. Selecione Olá **Microsoft Graph** como Olá API e adicione Olá **ler dados do diretório** permissão em **permissões delegadas**.  Isso permitirá a saudação de tooquery aplicativo Graph API para os usuários.

## <a name="2-install--configure-adal"></a>2. Instalar e Configurar o ADAL
Agora que você tem um aplicativo no AD do Azure, você pode instalar a ADAL e escrever seu código relacionado à identidade.  Para toocommunicate capaz de toobe ADAL com o Azure AD, é necessário tooprovide-lo com algumas informações sobre o registro do seu aplicativo.

* Comece adicionando o projeto de DirectorySearcher toohello ADAL usando Olá Package Manager Console.

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* No projeto de DirectorySearcher hello, abra `MainPage.xaml.cs`.  Substituir valores Olá Olá `Config Values` Olá de tooreflect região valores de entrada hello Portal do Azure.  Seu código fará referência a esses valores sempre que ele usar a ADAL.
  * Olá `tenant` é o domínio de saudação do seu locatário do AD do Azure, por exemplo, contoso.onmicrosoft.com
  * Olá `clientId` é Olá clientId do aplicativo é copiada do portal de saudação.
* Uri de retorno de chamada de saudação toodiscover agora é necessário para seu aplicativo do Windows Phone.  Defina um ponto de interrupção nessa linha em Olá `MainPage` método:

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* Executar o aplicativo hello e separar copiar valor de saudação do `redirectUri` quando Olá ponto de interrupção.  O resultado deve ser semelhante a

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* Em Olá **configurar** guia do seu aplicativo em Olá Portal de gerenciamento do Azure, substitua o valor de saudação de saudação **RedirectUri** com esse valor.  

## <a name="3-use-adal-tooget-tokens-from-aad"></a>3. Usar Tokens tooGet ADAL do AAD
Olá princípio básico de ADAL é que sempre que seu aplicativo precisa de um token de acesso, ele simplesmente chama `authContext.AcquireToken(…)`, e ADAL Olá rest.  

* primeira etapa de saudação é tooinitialize seu aplicativo `AuthenticationContext` -ADAL da classe principal.  Isso é onde você passa ADAL Olá coordenadas necessárias toocommunicate com o Azure AD e informe como toocache tokens.

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* Localizar agora Olá `Search(...)` método, que será invocado quando Olá usuário cliks hello "Pesquisar" botão na interface de usuário do aplicativo hello.  Esse método torna um tooquery de toohello do Azure AD Graph API de solicitação GET para usuários cujo UPN começa com hello dado o termo de pesquisa.  Mas em Olá de tooquery ordem API do Graph, você precisa tooinclude um access_token no hello `Authorization` cabeçalho da saudação solicitar - onde ADAL é.

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try tooget a token without triggering any user prompt.
    // ADAL will check whether hello requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained hello QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* Se a autenticação interativa é necessária, ADAL usará o agente de autenticação de Web (WAB) do Windows Phone e [modelo continuação](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) na página de logon toodisplay Olá AD do Azure.  Quando Olá usuário faz logon, seu aplicativo precisa resultados de saudação ADAL toopass de interação de WAB hello.  Isso é tão simple quanto implementando Olá `ContinueWebAuthentication` interface:

```C#
// This method is automatically invoked when hello application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass hello authentication interaction results tooADAL, which will
    // conclude hello token acquisition operation and invoke hello callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* Agora é saudação do tempo toouse `AuthenticationResult` que ADAL retornado tooyour aplicativo.  Em Olá `QueryGraph(...)` retorno de chamada, anexar access_token Olá adquirido toohello GET solicitação no cabeçalho de autorização hello:

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add hello access token toohello Authorization Header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* Você também pode usar o hello `AuthenticationResult` toodisplay informações sobre o usuário Olá em seu aplicativo do objeto. Em Olá `QueryGraph(...)` método, a id do usuário do hello tooshow resultados use Olá na página de saudação:

```C#
// Update hello Page UI toorepresent hello signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* Por fim, você pode usar o usuário de saudação toosign ADAL do aplicativo também.  Quando o usuário Olá clica hello "Sair" botão, queremos tooensure que Olá próxima chamada muito`AcquireTokenSilentAsync(...)` falhará.  ADAL, isso é tão fácil quanto limpar o cache de token hello:

```C#
private void SignOut()
{
    // Clear session state from hello token cache.
    authContext.TokenCache.Clear();

    ...
}
```

Parabéns! Você agora tem um aplicativo do Windows Phone que tem Olá capacidade tooauthenticate usuários de trabalho com segurança chamar APIs da Web usando o OAuth 2.0 e obter informações básicas sobre o usuário hello.  Se você ainda não fez isso, agora é Olá tempo toopopulate seu locatário com alguns usuários.  Execute o aplicativo DirectorySearcher e faça logon com um desses usuários.  Procure por outros usuários com base em seus UPNs.  Feche o aplicativo hello e execute-a novamente.  Observe como a sessão do usuário Olá permanece intacta.  Saia e faça logon novamente como outro usuário.

ADAL torna fácil tooincorporate todos esses recursos comuns de identidade em seu aplicativo.  Cuida de todo o trabalho sujo Olá para você - gerenciamento de cache, suporte ao protocolo OAuth, apresentando usuário Olá com um logon de interface do usuário, atualizando tokens expirados e muito mais.  Tudo o que você realmente precisa de tooknow é uma única chamada de API, `authContext.AcquireToken*(…)`.

Para referência, o exemplo hello concluída (sem os valores de configuração) é fornecido [aqui](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).  Agora você pode mover tooadditional cenários de identidade.  Você pode desejar tootry:

[Proteger uma API da Web .NET com o Azure AD >>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

