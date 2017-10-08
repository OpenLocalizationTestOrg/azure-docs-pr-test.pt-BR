---
title: "aaaAzure AD v 2.0 NodeJS AngularJS aplicativos de única página Introdução | Microsoft Docs"
description: "Como a toobuild um aplicativo Angular JS única página que conecta os usuários com Microsoft pessoal contas e de trabalho ou escolares."
services: active-directory
documentationcenter: 
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: d286aa33-8a94-452f-beb7-ddc6c6daa5c8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/23/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 1ab450caf08ab05fba140b94b1b8de652e99cbc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-angularjs-single-page-app---nodejs"></a>Adicionar o aplicativo de página única entrada tooan AngularJS - NodeJS
Neste artigo, adicionaremos entrar com Microsoft alimentado contas tooan AngularJS aplicativo usando o ponto de extremidade do hello Active Directory do Azure v 2.0. o ponto de extremidade do Hello v 2.0 permitem que você tooperform uma integração único em seu aplicativo e autenticar usuários com contas pessoais e de trabalho/escola.

Este exemplo é um aplicativo de página única de uma simples lista de tarefas pendentes que armazena as tarefas em uma API REST back-end. Ele é escrito em NodeJS e protegido usando tokens de portador OAuth do AD do Azure.  Olá AngularJS aplicativo usará nossa biblioteca de autenticação de JavaScript do código-fonte aberto [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle Olá todo processo de entrada e adquirir tokens para chamar hello API REST.  Olá mesmo padrão pode ser aplicadas tooauthenticate tooother APIs REST, como Olá [Microsoft Graph](https://graph.microsoft.com) ou Olá APIs do Gerenciador de recursos do Azure.

> [!NOTE]
> Nem todos os recursos e cenários de Active Directory do Azure têm suporte pelo ponto de extremidade do hello v 2.0.  toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="download"></a>Baixar
tooget iniciado, você precisará toodownload & instalar [node.js](https://nodejs.org).  Em seguida, você pode clonar ou [baixar](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) um aplicativo de esqueleto:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS.git
```

aplicativo de esqueleto Olá inclui todos os códigos de boilerplate Olá para um aplicativo simples do AngularJS, mas não tem todas as partes relacionadas à identidade de saudação.  Se você não quiser toofollow ao longo, em vez disso, você pode clonar ou [baixar](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) exemplo hello concluída.

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-NodeJS.git
```

## <a name="register-an-app"></a>Registrar um aplicativo
Primeiro, crie um aplicativo no hello [Portal de registro de aplicativo](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou siga estas [etapas detalhadas](active-directory-v2-app-registration.md).  Não se esqueça de:

* Adicionar Olá **Web** plataforma para seu aplicativo.
* Digite hello correto **URI de redirecionamento**. saudação padrão para este exemplo é `http://localhost:8080`.
* Deixe Olá **permitir fluxo implícito** caixa de seleção habilitada. 

Cópia para baixo Olá **ID do aplicativo** que é atribuído tooyour aplicativo, você precisará dele em breve. 

## <a name="install-adaljs"></a>Instalar o adal.js
toostart, navegue tooproject você fez o download e instale o adal.js.  Se o [bower](http://bower.io/) estiver instalado, basta executar este comando.  Para qualquer incompatibilidade de versão de dependência, basta escolha uma versão superior hello.

```
bower install adal-angular#experimental
```

Como alternativa, você pode baixar manualmente o [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) e o [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).  Adicione os dois arquivos toohello `app/lib/adal-angular-experimental/dist` directory.

Agora, abra o projeto Olá em seu editor de texto favorito e carregar adal.js final de saudação do corpo da página de saudação:

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a>Configurar Olá API REST
Enquanto estamos configurando tudo, permite o trabalho de API REST de back-end get hello.  Em um prompt de comando, instale todos os pacotes necessários de saudação executando (Verifique se você está no diretório de nível superior de saudação do projeto Olá):

```
npm install
```

Agora, abra `config.js` e substitua Olá `audience` valor:

```js
exports.creds = {

     // TODO: Replace this value with hello Application ID from hello registration portal
     audience: '<Your-application-id>',

     ...
}
```

Olá API REST usará tokens de toovalidate esse valor recebe do aplicativo Angular de saudação em solicitações do AJAX.  Observe que essa API REST simples armazena dados na memória - para cada servidor de saudação do toostop de tempo, você perderá todas as tarefas criadas anteriormente.

Isso é tudo que vamos toospend discussão de como funciona a saudação API REST de tempo de saudação.  Sinta-se livre toopoke ao redor no código hello, mas se você quiser toolearn mais sobre como proteger APIs com o Azure AD da web, check-out [neste artigo](active-directory-v2-devquickstarts-node-api.md). 

## <a name="sign-users-in"></a>Entrada de usuários
Tempo toowrite algum código de identidade.  Talvez você já tenha notado que o adal.js contém um provedor AngularJS, que funciona perfeitamente com o mecanismo de roteamento Angular.  Inicie adicionando Olá módulo adal toohello aplicativo:

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

Agora você pode inicializar Olá `adalProvider` com a ID do aplicativo:

```js
// app/scripts/app.js

...

adalProvider.init({

        // Use this value for hello public instance of Azure AD
        instance: 'https://login.microsoftonline.com/', 

        // hello 'common' endpoint is used for multi-tenant applications like this one
        tenant: 'common',

        // Your application id from hello registration portal
        clientId: '<Your-application-id>',

        // If you're using IE, uncommment this line - hello default HTML5 sessionStorage does not work for localhost.
        //cacheLocation: 'localStorage',

    }, $httpProvider);
```

Ótimo, agora o adal.js todas as informações de saudação precisa toosecure os usuários do aplicativo e entrar no.  tooforce de entrada para uma rota específica no aplicativo hello, tudo é uma linha de código:

```js
// app/scripts/app.js

...

}).when("/TodoList", {
    controller: "todoListCtrl",
    templateUrl: "/static/views/TodoList.html",
    requireADLogin: true, // Ensures that hello user must be logged in tooaccess hello route
})

...
```

Agora, quando um usuário clica Olá `TodoList` link, o adal.js será automaticamente redirecionada tooAzure AD para entrar se necessário.  Também é possível enviar de forma explícita as solicitações de entrada e saída chamando o adal.js em seus controladores:

```js
// app/scripts/homeCtrl.js

angular.module('todoApp')
// Load adal.js hello same way for use in controllers and views   
.controller('homeCtrl', ['$scope', 'adalAuthenticationService','$location', function ($scope, adalService, $location) {
    $scope.login = function () {

        // Redirect hello user toosign in
        adalService.login();

    };
    $scope.logout = function () {

        // Redirect hello user toolog out    
        adalService.logOut();

    };
...
```

## <a name="display-user-info"></a>Exibir informações do usuário
Agora que hello usuário está conectado, você provavelmente precisará tooaccess Olá conectado autenticação dados de usuário em seu aplicativo.  Adal.js expõe essas informações para você em Olá `userInfo` objeto.  tooaccess esse objeto em uma exibição, primeiro adicione o adal.js toohello escopo de raiz do controlador correspondente hello:

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

Então enfrentam Olá `userInfo` objeto no modo de exibição: 

```html
<!--app/views/UserData.html-->

...

    <!--Get hello user's profile information from hello ADAL userInfo object-->
    <tr ng-repeat="(key, value) in userInfo.profile">
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
...
```

Você também pode usar o hello `userInfo` toodetermine do objeto se Olá usuário está conectado ou não.

```html
<!--index.html-->

...

    <!--Use hello ADAL userInfo object tooshow hello right login/logout button-->
    <ul class="nav navbar-nav navbar-right">
        <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
        <li><a class="btn btn-link" ng-hide="userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    </ul>
...
```

## <a name="call-hello-rest-api"></a>Saudação de chamada de API REST
Por fim, é hora tooget alguns tokens e chamada hello toocreate da API REST, ler, atualizam e excluir tarefas.  E sabe o que mais?  Você não tem toodo *algo*.  O Adal.js se encarregará automaticamente de obter, armazenar em cache e atualizar os tokens.  Ele também tome cuidado de anexar esses tokens que AJAX toooutgoing solicita que você envie toohello API REST.  

Como isso funciona exatamente? É toda Obrigado toohello mágica do [AngularJS interceptores](https://docs.angularjs.org/api/ng/service/$http), que permite o adal.js tootransform mensagens http de entrada e saída.  Além disso, adal.js pressupõe que todas as solicitações enviam toohello mesmo domínio como a janela Olá deve usar tokens destinados Olá mesma ID de aplicativo como Olá aplicativo AngularJS.  Isso é porque usamos Olá mesma ID de aplicativo em ambos os aplicativos de saudação Angular em Olá NodeJS REST API.  Obviamente, você pode substituir esse comportamento e informar o adal.js tooget tokens para outras APIs REST, se necessário - mas para Olá este cenário simples padrões fará.

Aqui está um trecho de código que mostra como é fácil toosend solicitações com tokens de portador do AD do Azure:

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

Parabéns!  Seu aplicativo de página única integrado ao Azure AD está concluído.  Vá em frente, receba os aplausos.  Ele pode autenticar os usuários, com segurança chamar sua API REST usando o OpenID Connect de back-end e obter informações básicas sobre o usuário hello.  Fora da caixa Olá, ele oferece suporte a qualquer usuário com um Account pessoal da Microsoft ou uma conta de trabalho/escola do AD do Azure.  Experimente aplicativo hello executando:

```
node server.js
```

Em um navegador, navegue muito`http://localhost:8080`.  Entre usando uma conta pessoal da Microsoft ou uma conta corporativa/de estudante.  Adicionar lista de tarefas do usuário de toohello tarefas e sair.  Tente entrar com hello outro tipo de conta. Se você precisar de usuários do AD do Azure locatário toocreate trabalho/escola, [Saiba como um aqui tooget](active-directory-howto-tenant.md) (é gratuito).

toocontinue aprendendo sobre Olá Olá v 2.0 de ponto de extremidade, head back tooour [guia do desenvolvedor v 2.0](active-directory-appmodel-v2-overview.md).  Para obter recursos adicionais, consulte:

* [Exemplos do Azure no GitHub >>](https://github.com/Azure-Samples)
* [Azure AD no Stack Overflow >>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* Documentação do Azure AD no [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)

## <a name="get-security-updates-for-our-products"></a>Obter atualizações de segurança para nossos produtos
Recomendamos que você tooget as notificações quando os incidentes de segurança ocorrem visitando [essa página](https://technet.microsoft.com/security/dd252948) e assinando tooSecurity alertas de aviso.

