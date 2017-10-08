---
title: "aaaAzure AD AngularJS Introdução | Microsoft Docs"
description: "Como toobuild um aplicativo de página única AngularJS que se integra ao AD do Azure para entrar e chama as APIs de protegidos pelo AD do Azure usando o OAuth."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: f2991054-8146-4718-a5f7-59b892230ad7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: eca5e1c9662186dfae4f96ca3041f9350583cf79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a>Ajudar a proteger aplicativos de página única AngularJS usando o AD do Azure

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure Active Directory (AD do Azure) torna simples e direta para você tooadd entrada, saída e chamadas de API de OAuth seguro tooyour aplicativos de única página.  Ele permite que os usuários de tooauthenticate aplicativos com suas contas do Active Directory do Windows Server e consumir qualquer API do AD do Azure ajuda a proteger, como Olá APIs do Office 365 ou hello Azure API da web.

Para aplicativos de JavaScript em execução em um navegador, o AD do Azure fornece Olá biblioteca de autenticação do Active Directory (ADAL) ou adal.js. Olá única finalidade adal.js é toomake fácil para seus tokens de acesso do aplicativo tooget. toodemonstrate facilidade é, aqui é possível compilar um aplicativo de lista de tooDo do AngularJS:

* Sinais Olá usuário no aplicativo toohello usando o AD do Azure como provedor de identidade hello.

* Exibe algumas informações sobre o usuário hello.
* Com segurança chamadas Olá tooDo do aplicativo lista API usando tokens de portador do AD do Azure.
* Sinais Olá usuário fora do aplicativo hello.

aplicativo toobuild hello de concluído, trabalho, você precisa:

1. Registrar um aplicativo no Azure AD.
2. Instalar o ADAL e configurar o aplicativo de página única hello.
3. Use páginas seguras toohelp ADAL no aplicativo de página única hello.

tooget iniciado, [baixar o esqueleto do aplicativo hello](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) ou [baixar exemplo hello concluída](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip). Você também precisará de um locatário do Azure AD no qual possa criar usuários e registrar um aplicativo. Se você ainda não tiver um locatário, [Saiba como tooget uma](active-directory-howto-tenant.md).

## <a name="step-1-register-hello-directorysearcher-application"></a>Etapa 1: Registrar o aplicativo de DirectorySearcher hello
tooenable aplicativo tooauthenticate usuários e tokens de get, primeiro é necessário tooregistê-lo no AD do Azure locatário:

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Se você tiver entrado em diretórios toomultiple, talvez seja necessário tooensure que você está exibindo o diretório correto hello. toodo assim, na barra superior do hello, clique em sua conta. Em Olá **diretório** , escolha o locatário de saudação do AD do Azure onde deseja tooregister seu aplicativo.
3. Clique em **mais serviços** Olá painel esquerdo e, em seguida, selecione **Active Directory do Azure**.
4. Clique em **Registros do aplicativo** e, em seguida, selecione **Adicionar**.
5. Siga os prompts de saudação e criar um novo aplicativo web e/ou API da web:
  * **Nome** descreve toousers seu aplicativo.
  * **Uri de redirecionamento** é Olá local toowhich AD do Azure retornará tokens. saudação padrão local para este exemplo é `https://localhost:44326/`.
6. Depois de concluir o registro, o Azure AD atribui a um aplicativo de tooyour de ID de aplicativo único.  Você precisará desse valor nas seções de Avançar hello, portanto copiá-lo do guia do aplicativo hello.
7. O Adal.js usa toocommunicate de fluxo implícitos OAuth Olá com o Azure AD. Você deve habilitar o fluxo implícito Olá para seu aplicativo:
  1. Clique em aplicativo hello e selecione **manifesto** editor de manifesto tooopen Olá embutido.
  2. Localizar Olá `oauth2AllowImplicitFlow` propriedade. Defina seu valor muito`true`.
  3. Clique em **salvar** toosave manifesto de saudação.
8. Conceda permissões em seu locatário para seu aplicativo. Vá muito**configurações** > **propriedades** > **permissões necessárias**e clique em Olá **conceder permissões**botão na barra superior hello. Clique em **Sim** tooconfirm.

## <a name="step-2-install-adal-and-configure-hello-single-page-app"></a>Etapa 2: Instalar ADAL e configurar o aplicativo de página única Olá
Agora que você tem um aplicativo no AD do Azure, você pode instalar a adal.js e escrever seu código relacionado à identidade.

### <a name="configure-hello-javascript-client"></a>Configurar o cliente de JavaScript Olá
Começar adicionando adal.js toohello TodoSPA projeto usando Olá Package Manager Console:
  1. Baixar [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) e adicioná-lo toohello `App/Scripts/` diretório do projeto.
  2. Baixar [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) e adicioná-lo toohello `App/Scripts/` diretório do projeto.
  3. Carregar cada script antes final Olá Olá `</body>` em `index.html`:

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-hello-back-end-server"></a>Configurar o servidor de back-end Olá
Para tokens de tooaccept do aplicativo de página única Olá tooDo de back-end API da lista de navegador hello, back-end Olá precisa de informações de configuração sobre o registro do aplicativo hello. No projeto de TodoSPA hello, abra `web.config`. Substituir valores de saudação de elementos Olá Olá `<appSettings>` Olá a seção tooreflect Olá os valores que você usou no portal do Azure. Seu código fará referência a esses valores sempre que ele usar a ADAL.
  * `ida:Tenant`é o domínio de saudação do seu locatário do AD do Azure – por exemplo, contoso.onmicrosoft.com.
  * `ida:Audience`é Olá ID do cliente do aplicativo que você copiou do portal de saudação.

## <a name="step-3-use-adal-toohelp-secure-pages-in-hello-single-page-app"></a>Etapa 3: Use ADAL toohelp seguras páginas Olá aplicativo de página única
O Adal.js integra-se ao roteiro AngularJS e aos provedores HTTP e, portanto, você pode ajudar a proteger exibições individuais em seu aplicativo de página única.

1. Em `App/Scripts/app.js`, Avançar no módulo de adal.js hello:

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. Inicializar `adalProvider` usando valores de configuração de saudação de seu registro de aplicativo, também no `App/Scripts/app.js`:

    ```js
    adalProvider.init(
      {
          instance: 'https://login.microsoftonline.com/',
          tenant: 'Enter your tenant name here e.g. contoso.onmicrosoft.com',
          clientId: 'Enter your client ID here e.g. e9a5a8b6-8af7-4719-9821-0deef255f68e',
          extraQueryParameter: 'nux=1',
          //cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
      },
      $httpProvider
    );
    ```
3. Ajudar a proteger Olá `TodoList` exibição no aplicativo hello usando apenas uma linha de código: `requireADLogin`.

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a>Resumo
Agora você tem um aplicativo de única página seguro que pode entrar em usuários e emitir solicitações protegidas de token de portador tooits back-end API. Quando um usuário clica Olá **TodoList** link, o adal.js será automaticamente redirecionada tooAzure AD para entrar se necessário. Além disso, o adal.js anexa automaticamente um acesso token tooany Ajax solicitações que são enviadas de back-end do aplicativo toohello.  

Olá etapas anteriores são Olá bare mínimo necessário toobuild um aplicativo de página única usando o adal.js. Mas alguns outros recursos são úteis no aplicativo de página única:

* tooexplicitly emitir solicitações de entrada e saídas, você pode definir funções em seus controladores que invocam adal.js.  Em `App/Scripts/homeCtrl.js`:

    ```js
    ...
    $scope.login = function () {
        adalService.login();
    };
    $scope.logout = function () {
        adalService.logOut();
    };
    ...
    ```
* Talvez você queira toopresent informações do usuário na interface de usuário do aplicativo hello. Olá ADAL serviço já foi adicionado toohello `userDataCtrl` controlador, para que você possa acessar Olá `userInfo` exibição, associada ao objeto no hello `App/Views/UserData.html`:

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* Há muitos cenários em que você desejará tooknow se Olá usuário está conectado ou não. Você também pode usar o hello `userInfo` objeto toogather essas informações.  Por exemplo, em `index.html`, você pode mostrar o hello **Login** ou **Logout** botão com base no status de autenticação:

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

O aplicativo de página única integrado ao AD do Azure pode autenticar os usuários, com segurança chamar seu back-end usando OAuth 2.0 e obter informações básicas sobre o usuário hello. Se você ainda não fez isso, agora é Olá tempo toopopulate seu locatário com alguns usuários. Executar seu aplicativo de página única lista tooDo e entrar com um desses usuários. Adicionar lista de tarefas do usuário do tarefas toohello, sair e entrar novamente.

Adal.js torna fácil tooincorporate recursos comuns de identidade em seu aplicativo. Cuida de todo o trabalho sujo Olá para você: gerenciamento de cache, suporte ao protocolo OAuth, apresentando usuário Olá com uma entrada da interface do usuário, atualizando tokens expirados e muito mais.

Para referência, o exemplo hello concluída (sem os valores de configuração) está disponível em [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).

## <a name="next-steps"></a>Próximas etapas
Agora você pode mover tooadditional cenários. Talvez você queira tootry: [chamar uma API da web CORS de um aplicativo de página única](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
