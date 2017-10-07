---
title: "aaaAzure AD Xamarin Introdução | Microsoft Docs"
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
ms.openlocfilehash: 6a0d189648b7071558ac1cf2b908808668960a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a>Integrar o Azure AD com aplicativos Xamarin
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Com o Xamarin, você pode gravar aplicativos móveis em C# que podem ser executados no iOS, no Android e no Windows (dispositivos móveis e computadores). Se você estiver criando um aplicativo usando o Xamarin, Azure Active Directory (AD do Azure) torna simples tooauthenticate usuários com suas contas do AD do Azure. aplicativo Hello também com segurança pode consumir qualquer API da web protegido pelo AD do Azure, como Olá APIs do Office 365 ou hello API do Azure.

Para aplicativos Xamarin que necessitam de recursos tooaccess protegido, o AD do Azure fornece Olá biblioteca de autenticação do Active Directory (ADAL). Olá única finalidade ADAL é toomake fácil para tokens de acesso de tooget de aplicativos. toodemonstrate fácil é, este artigo mostra como toobuild DirectorySearcher aplicativos que:

* Execute no iOS, no Android, na Área de Trabalho do Windows, no Windows Phone e na Windows Store.
* Usar uma única classe portátil biblioteca (PCL) tooauthenticate usuários e obter tokens de saudação do Azure AD Graph API.
* Pesquise um diretório para usuários com um determinado UPN.

## <a name="before-you-get-started"></a>Antes de começar
* Baixar Olá [projeto esqueleto](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), ou baixar Olá [exemplo concluído](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip). Cada download é uma solução do Visual Studio 2013.
* Também é necessário um locatário Azure AD no qual usuários toocreate e registrar o aplicativo de saudação. Se você ainda não tiver um locatário, [Saiba como tooget uma](active-directory-howto-tenant.md).

Quando você estiver pronto, siga Olá procedimentos Olá quatro seções.

## <a name="step-1-set-up-your-xamarin-development-environment"></a>Etapa 1: Configurar seu ambiente de desenvolvimento do Xamarin
Como este tutorial inclui projetos para iOS, Android e Windows, são necessários o Visual Studio e o Xamarin. ambiente necessário toocreate hello, processo Olá completa em [definido para cima e instalar o Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) no MSDN. instruções de saudação incluem material de que você pode examinar toolearn mais sobre Xamarin enquanto você aguarda para Olá instalações toobe concluída.

Depois de concluir a instalação hello, abra a solução de saudação no Visual Studio. Lá, você encontrará seis projetos: cinco projetos específicos de plataforma e um PCL, DirectorySearcher.cs, que será compartilhado entre todas as plataformas.

## <a name="step-2-register-hello-directorysearcher-app"></a>Etapa 2: Registrar o aplicativo de DirectorySearcher Olá
tokens de tooget do tooenable Olá aplicativo, primeiro é necessário tooregistê-lo no AD do Azure locatário e conceda a ela Olá tooaccess de permissão do Azure AD Graph API. Faça assim:

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Na barra superior do hello, clique em sua conta. Em seguida, em Olá **diretório** lista, o locatário do Active Directory hello selecione onde você deseja que o aplicativo de saudação tooregister.
3. Clique em **mais serviços** Olá painel esquerdo e, em seguida, selecione **Active Directory do Azure**.
4. Clique em **Registros do aplicativo** e, em seguida, selecione **Adicionar**.
5. toocreate um novo **aplicativo cliente nativo**, siga os prompts de saudação.
  * **Nome** descreve Olá toousers de aplicativo.
  * **URI de redirecionamento** é uma combinação de esquema e a cadeia de caracteres que o AD do Azure usa tooreturn respostas de token. Insira um valor (por exemplo, http://DirectorySearcher).
6. Depois de concluir o registro, o Azure AD atribui aplicativo hello uma ID exclusiva do aplicativo. Copie o valor de saudação da saudação **aplicativo** guia, pois você precisará dele mais tarde.
7. Em Olá **configurações** página, selecione **permissões necessárias**e, em seguida, selecione **adicionar**.
8. Selecione **Microsoft Graph** como Olá API. Em **permissões delegadas**, adicionar Olá **ler dados do diretório** permissão.  
Esta ação habilita Olá tooquery aplicativo hello Graph API para os usuários.

## <a name="step-3-install-and-configure-adal"></a>Etapa 3: Instalar e configurar a ADAL
Agora que você tem um aplicativo no Azure AD, você pode instalar a ADAL e escrever seu código relacionado à identidade. tooenable toocommunicate ADAL com o Azure AD, dê a ele algumas informações sobre o registro do aplicativo hello.

1. Adicione projeto de DirectorySearcher toohello ADAL usando Olá Package Manager Console.

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

    Observe que duas referências de biblioteca são adicionadas tooeach projeto: Olá PCL parte de ADAL e uma parte específica de plataforma.
2. No projeto de DirectorySearcherLib hello, abra DirectorySearcher.cs.
3. Substitua valores de membro de classe Olá com valores hello que você inseriu na Olá portal do Azure. O código se refere a valores toothese sempre que ele usa ADAL.

  * Olá *locatário* é o domínio de saudação do seu locatário do AD do Azure (por exemplo, contoso.onmicrosoft.com).
  * Olá *clientId* é a ID do cliente de saudação do aplicativo hello, o que você copiou do portal de saudação.
  * Olá *returnUri* é Olá redirecionamento URI que você inseriu no portal de saudação (por exemplo, http://DirectorySearcher).

## <a name="step-4-use-adal-tooget-tokens-from-azure-ad"></a>Etapa 4: Tokens ADAL tooget uso do AD do Azure
Quase todos os de lógica de autenticação do aplicativo hello está em `DirectorySearcher.SearchByAlias(...)`. Tudo o que é necessário em projetos do hello específica de plataforma é toopass toohello um parâmetro contextual `DirectorySearcher` PCL.

1. Abra DirectorySearcher.cs e, em seguida, adicionar um novo toohello de parâmetro `SearchByAlias(...)` método. `IPlatformParameters`é o parâmetro hello contextuais encapsula específico da plataforma Olá objetos que a autenticação de ADAL necessidades tooperform hello.

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. Inicializar `AuthenticationContext`, que é a classe principal de saudação do ADAL.  
Este Olá ADAL de passagens de ação ele coordena toocommunicate necessidades com o Azure AD.
3. Chamar `AcquireTokenAsync(...)`, que aceita Olá `IPlatformParameters` do objeto e invoca o fluxo de autenticação de saudação que é necessário tooreturn um aplicativo toohello token.

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

    `AcquireTokenAsync(...)`primeiro tentativas tooreturn um token para Olá solicitou o recurso (Olá API do Graph neste caso) sem avisar os usuários tooenter suas credenciais (por meio do armazenamento em cache ou atualizar tokens antigos). Conforme necessário, ele mostra usuários Olá AD do Azure-página de entrada antes de adquirir o token solicitado hello.
4. Anexar a solicitação da API do Graph toohello token Olá acesso no hello **autorização** cabeçalho:

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

Isso é tudo para Olá `DirectorySearcher` código de relacionadas à identidade do aplicativo PCL e hello. Tudo o que resta é Olá toocall `SearchByAlias(...)` método nos modos de exibição de cada plataforma e, quando necessário, tooadd código para tratar corretamente Olá do ciclo de vida da interface do usuário.

### <a name="android"></a>Android
1. Em MainActivity.cs, adicione uma chamada muito`SearchByAlias(...)` manipulador de clique no botão de saudação:

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. Substituir saudação `OnActivityResult` ciclo de vida método tooforward qualquer autenticação redireciona o método apropriado toohello voltar. A ADAL fornece um método auxiliar para isso no Android:

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a>Área de Trabalho do Windows
Em MainWindow.xaml.cs, fazer uma chamada muito`SearchByAlias(...)` passando um `WindowInteropHelper` da área de trabalho Olá `PlatformParameters` objeto:

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a>iOS
Em DirSearchClient_iOSViewController.cs, Olá iOS `PlatformParameters` objeto assume um controlador de exibição de toohello de referência:

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a>Windows Universal
No Windows Universal, abra MainPage.xaml.cs e implementar Olá `Search` método. Esse método usa um método auxiliar no tooupdate projeto compartilhado da interface do usuário conforme necessário.

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a>O que vem a seguir
Agora você tem um aplicativo Xamarin em funcionamento que pode autenticar usuários e chamar as APIs de Web com segurança usando OAuth 2.0 em cinco plataformas diferentes.

Se você já não tiver populado seu locatário com usuários, agora é Olá tempo toodo assim.

1. Executar seu aplicativo DirectorySearcher e, em seguida, entrar com um dos usuários de saudação.
2. Procure por outros usuários com base em seus UPNs.

ADAL torna fácil tooincorporate recursos comuns de identidade para o aplicativo hello. Cuida de todo o trabalho sujo Olá para você, como gerenciamento de cache, suporte ao protocolo OAuth, apresentando usuário Olá com um logon de interface do usuário, e a atualização expirou tokens. Você precisa tooknow apenas uma única API chamada, `authContext.AcquireToken*(…)`.

Para referência, baixe Olá [exemplo concluído](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (sem os valores de configuração).

Agora você pode mover tooadditional cenários de identidade. Por exemplo, experimente [Proteger uma API Web .NET com o Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
