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
# <a name="integrate-azure-ad-with-windows-store-apps"></a>Integrar o Azure AD com aplicativos da Windows Store
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> Não há suporte para projetos da Windows Store 8.1 e de versões anteriores no Visual Studio 2017.  Para saber mais, confira [Direcionamento e compatibilidade da plataforma Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

Se você estiver desenvolvendo aplicativos para saudação da Windows Store, Azure Active Directory (AD do Azure) torna simple e direto tooauthenticate os usuários com suas contas do Active Directory. Com a integração com o AD do Azure, um aplicativo pode consumir com segurança qualquer API que é protegido pelo AD do Azure, como Olá APIs do Office 365 ou hello Azure API da web.

Para aplicativos da área de trabalho da Windows Store que precisam de recursos de tooaccess protegido, o AD do Azure fornece Olá biblioteca de autenticação do Active Directory (ADAL). Olá única finalidade ADAL é toomake fácil para tokens de acesso de tooget de aplicativo hello. toodemonstrate como é, este artigo mostra como toobuild Windows DirectorySearcher armazenam fácil aplicativos que:

* Obtém acesso tokens para chamar a API do Azure AD Graph Olá usando Olá [protocolo de autenticação OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Pesquisa por usuários com um determinado nome UPN em um diretório.
* Desconecta usuários.

## <a name="before-you-get-started"></a>Antes de começar
* Baixar Olá [projeto esqueleto](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), ou baixar Olá [exemplo concluído](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip). Cada download é uma solução do Visual Studio 2015.
* Também é necessário um locatário Azure AD no qual usuários toocreate e registrar o aplicativo de saudação. Se você ainda não tiver um locatário, [Saiba como tooget uma](active-directory-howto-tenant.md).

Quando você estiver pronto, siga Olá procedimentos Olá três próximas seções.

## <a name="step-1-register-hello-directorysearcher-app"></a>Etapa 1: Registrar o aplicativo de DirectorySearcher Olá
tokens de tooget do tooenable Olá aplicativo, primeiro é necessário tooregistê-lo no AD do Azure locatário e conceda a ela Olá tooaccess de permissão do Azure AD Graph API. Faça assim:

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Na barra superior do hello, clique em sua conta. Em seguida, em Olá **diretório** lista, o locatário do Active Directory hello selecione onde você deseja que o aplicativo de saudação tooregister.
3. Clique em **mais serviços** Olá painel esquerdo e, em seguida, selecione **Active Directory do Azure**.
4. Clique em **Registros do aplicativo** e, em seguida, selecione **Adicionar**.
5. Siga Olá prompts toocreate um **aplicativo cliente nativo**.
  * **Nome** descreve Olá toousers de aplicativo.
  * **URI de redirecionamento** é uma combinação de esquema e a cadeia de caracteres que o AD do Azure usa tooreturn respostas de token. Insira um valor de espaço reservado por enquanto (por exemplo, **http://DirectorySearcher**). Posteriormente, você substituirá o valor de saudação.
6. Depois de concluir o registro de saudação, o Azure AD atribui aplicativo hello uma ID exclusiva do aplicativo. Copie o valor Olá Olá **aplicativo** guia, pois você precisará dele mais tarde.
7. Em Olá **configurações** página, selecione **permissões necessárias**e, em seguida, selecione **adicionar**.
8. Para Olá **Active Directory do Azure** aplicativo, selecione **Microsoft Graph** como Olá API.
9. Em **permissões delegadas**, adicionar Olá **acessar o diretório de hello como o usuário conectado Olá** permissão. Isso permite que o hello tooquery aplicativo hello Graph API para os usuários.

## <a name="step-2-install-and-configure-adal"></a>Etapa 2: instalar e configurar a ADAL
Agora que você tem um aplicativo no Azure AD, você pode instalar a ADAL e escrever seu código relacionado à identidade. tooenable toocommunicate ADAL com o Azure AD, dê a ele algumas informações sobre o registro do aplicativo hello.

1. Adicione projeto de DirectorySearcher toohello ADAL usando Olá Package Manager Console.

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. No projeto de DirectorySearcher hello, abra MainPage.xaml.cs.
3. Substituir valores Olá Olá **valores de configuração** região com valores de saudação que você inseriu no hello portal do Azure. O código se refere a valores toothese sempre que ele usa ADAL.
  * Olá *locatário* é o domínio de saudação do seu locatário do AD do Azure (por exemplo, contoso.onmicrosoft.com).
  * Olá *clientId* é a ID do cliente de saudação do aplicativo hello, o que você copiou do portal de saudação.
4. Agora, você precisa toodiscover o retorno de chamada de saudação URI para seu aplicativo da Windows Store. Defina um ponto de interrupção nessa linha em Olá `MainPage` método:
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. Compile a solução de hello, certificando-se de que todas as referências de pacote são restauradas. Se todos os pacotes estiverem ausentes, abra Olá NuGet Package Manager e restaurá-los.
6. Executar o aplicativo hello e copie o valor de saudação do `redirectUri` quando Olá ponto de interrupção. valor de saudação deve ser semelhante a saudação a seguir:

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. Em Olá **configurações** guia do aplicativo Olá Olá portal do Azure, adicione um **RedirectUri** com hello precede o valor.  

## <a name="step-3-use-adal-tooget-tokens-from-azure-ad"></a>Etapa 3: Tokens ADAL tooget uso do AD do Azure
Olá princípio básico de ADAL é que sempre que o aplicativo hello precisa de um token de acesso, ele simplesmente chama `authContext.AcquireToken(…)`, e ADAL Olá rest.  

1. Inicialização do aplicativo hello `AuthenticationContext`, que é a classe principal de saudação do ADAL. Essa ação passa coordenadas Olá ADAL ele precisa toocommunicate com o Azure AD e informe como toocache tokens.

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. Localizar Olá `Search(...)` método, que é invocado quando os usuários clicarem Olá **pesquisa** botão na interface de usuário do aplicativo hello. Esse método torna um tooquery de toohello do Azure AD Graph API de solicitação get para usuários cujo UPN começa com hello dado o termo de pesquisa. Olá tooquery API do Graph, incluir um token de acesso na solicitação de saudação **autorização** cabeçalho. É aí que a ADAL entra em cena.

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
    Quando o aplicativo hello solicita um token chamando `AcquireTokenAsync(...)`, ADAL tentativas tooreturn um token sem solicitar credenciais de usuário hello. Se ADAL determina que o usuário Olá precisa toosign em tooget um token, ele exibe uma caixa de diálogo de logon, coleta as credenciais do usuário hello e retorna um token depois que a autenticação seja bem-sucedida. Se o ADAL está tooreturn não é possível um token por qualquer motivo, Olá *AuthenticationResult* status é um erro.
3. Agora é o token de acesso do tempo toouse Olá que você acabou de adquirir. Também no hello `Search(...)` método, anexar Olá toohello token de solicitação de obtenção de API do Graph em Olá **autorização** cabeçalho:

    ```C#
    // Add hello access token toohello Authorization header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. Você pode usar o hello `AuthenticationResult` toodisplay informações sobre usuário Olá no aplicativo hello, como ID do usuário de saudação do objeto:

    ```C#
    // Update hello page UI toorepresent hello signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. Você também pode usar o ADAL toosign usuários fora do aplicativo hello. Quando o usuário Olá clica Olá **sair** botão, certifique-se de que chamam Avançar Olá muito`AcquireTokenAsync(...)` mostra uma exibição de entrada. Com a ADAL, essa ação é tão fácil quanto limpar o cache de token hello:

    ```C#
    private void SignOut()
    {
        // Clear session state from hello token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a>O que vem a seguir
Agora você tem um aplicativo da Windows Store que pode autenticar os usuários, com segurança chamar APIs usando OAuth 2.0 da web e obter informações básicas sobre o usuário de saudação do trabalho.

Se você já não tiver populado seu locatário com usuários, agora é Olá tempo toodo assim.
1. Executar seu aplicativo DirectorySearcher e, em seguida, entrar com um dos usuários de saudação.
2. Procure por outros usuários com base em seus UPNs.
3. Feche o aplicativo hello e executá-lo novamente. Observe como a sessão do usuário Olá permanece intacta.
4. Sair clicando toodisplay Olá barra inferior e, em seguida, entrar novamente como outro usuário.

ADAL torna fácil tooincorporate todos esses recursos de identidade comum para o aplicativo hello. Cuida de todo o trabalho sujo Olá para você, como gerenciamento de cache, suporte ao protocolo OAuth, apresentando usuário Olá com um logon de interface do usuário, e a atualização expirou tokens. Você precisa tooknow apenas uma única API chamada, `authContext.AcquireToken*(…)`.

Para referência, baixe Olá [exemplo concluído](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (sem os valores de configuração).

Agora você pode mover tooadditional cenários de identidade. Por exemplo, experimente [Proteger uma API Web .NET com o Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
