---
title: "aplicativo de página única aaaAzure AD v 2.0 AngularJS .NET Introdução | Microsoft Docs"
description: "Como a toobuild um aplicativo Angular JS única página que conecta os usuários com Microsoft pessoal contas e de trabalho ou escolares."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 6a341781-278f-461b-92ca-7572a06e6852
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: bd3fc8dce91eb0bedcbfed47a9b3ef52c5568c6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-angularjs-single-page-app---net"></a><span data-ttu-id="1fcdf-103">Adicionar o aplicativo de página única entrada tooan AngularJS - .NET</span><span class="sxs-lookup"><span data-stu-id="1fcdf-103">Add sign-in tooan AngularJS single page app - .NET</span></span>
<span data-ttu-id="1fcdf-104">Neste artigo, adicionaremos entrar com Microsoft alimentado contas tooan AngularJS aplicativo usando o ponto de extremidade do hello Active Directory do Azure v 2.0.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-104">In this article we'll add sign in with Microsoft powered accounts tooan AngularJS app using hello Azure Active Directory v2.0 endpoint.</span></span>  <span data-ttu-id="1fcdf-105">o ponto de extremidade do Hello v 2.0 permite que você tooperform uma integração único em seu aplicativo e autenticar usuários com contas pessoais e de trabalho/escola.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-105">hello v2.0 endpoint enables you tooperform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="1fcdf-106">Este exemplo é um aplicativo de página única lista de tarefas simples que armazena as tarefas em um back-end API REST, gravadas usando a estrutura do MVC do .NET 4.5 hello e protegido usando tokens de portador OAuth do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written using hello .NET 4.5 MVC framework and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="1fcdf-107">Olá AngularJS aplicativo usará nossa biblioteca de autenticação de JavaScript do código-fonte aberto [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle Olá todo processo de entrada e adquirir tokens para chamar hello API REST.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-107">hello AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello entire sign in process and acquire tokens for calling hello REST API.</span></span>  <span data-ttu-id="1fcdf-108">Olá mesmo padrão pode ser aplicadas tooauthenticate tooother APIs REST, como Olá [Microsoft Graph](https://graph.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="1fcdf-108">hello same pattern can be applied tooauthenticate tooother REST APIs, like hello [Microsoft Graph](https://graph.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="1fcdf-109">Nem todos os recursos e cenários de Active Directory do Azure têm suporte pelo ponto de extremidade do hello v 2.0.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="1fcdf-110">toodetermine se você deve usar o ponto de extremidade de v 2.0 hello, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="1fcdf-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="1fcdf-111">Baixar</span><span class="sxs-lookup"><span data-stu-id="1fcdf-111">Download</span></span>
<span data-ttu-id="1fcdf-112">tooget iniciado, você vai precisar toodownload & instalar o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-112">tooget started, you'll need toodownload & install Visual Studio.</span></span>  <span data-ttu-id="1fcdf-113">Em seguida, você pode clonar ou [baixar](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) um aplicativo de esqueleto:</span><span class="sxs-lookup"><span data-stu-id="1fcdf-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet.git
```

<span data-ttu-id="1fcdf-114">aplicativo de esqueleto Olá inclui todos os códigos de boilerplate Olá para um aplicativo simples do AngularJS, mas não tem todas as partes relacionadas à identidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-114">hello skeleton app includes all hello boilerplate code for a simple AngularJS app, but is missing all of hello identity-related pieces.</span></span>  <span data-ttu-id="1fcdf-115">Se você não quiser toofollow ao longo, em vez disso, você pode clonar ou [baixar](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) exemplo hello concluída.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-115">If you don't want toofollow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) hello completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="1fcdf-116">Registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="1fcdf-116">Register an app</span></span>
<span data-ttu-id="1fcdf-117">Primeiro, crie um aplicativo no hello [Portal de registro de aplicativo](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou siga estas [etapas detalhadas](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="1fcdf-117">First, create an app in hello [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="1fcdf-118">Não se esqueça de:</span><span class="sxs-lookup"><span data-stu-id="1fcdf-118">Make sure to:</span></span>

* <span data-ttu-id="1fcdf-119">Adicionar Olá **Web** plataforma para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-119">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="1fcdf-120">Digite hello correto **URI de redirecionamento**.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-120">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="1fcdf-121">saudação padrão para este exemplo é `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-121">hello default for this sample is `https://localhost:44326/`.</span></span>
* <span data-ttu-id="1fcdf-122">Deixe Olá **permitir fluxo implícito** caixa de seleção habilitada.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-122">Leave hello **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="1fcdf-123">Cópia para baixo Olá **ID do aplicativo** que é atribuído tooyour aplicativo, você precisará dele em breve.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-123">Copy down hello **Application ID** that is assigned tooyour app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="1fcdf-124">Instalar o adal.js</span><span class="sxs-lookup"><span data-stu-id="1fcdf-124">Install adal.js</span></span>
<span data-ttu-id="1fcdf-125">toostart, navegue tooproject você fez o download e instale o adal.js.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-125">toostart, navigate tooproject you downloaded and install adal.js.</span></span>  <span data-ttu-id="1fcdf-126">Se o [bower](http://bower.io/) estiver instalado, basta executar este comando.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="1fcdf-127">Para qualquer incompatibilidade de versão de dependência, basta escolha uma versão superior hello.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-127">For any dependency version mismatches, just choose hello higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="1fcdf-128">Como alternativa, você pode baixar manualmente o [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) e o [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="1fcdf-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="1fcdf-129">Adicione os dois arquivos toohello `app/lib/adal-angular-experimental/dist` diretório de saudação `TodoSPA` projeto.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-129">Add both files toohello `app/lib/adal-angular-experimental/dist` directory of hello `TodoSPA` project.</span></span>

<span data-ttu-id="1fcdf-130">Agora, abra o projeto Olá no Visual Studio e carregar adal.js final Olá do corpo da página principal da saudação:</span><span class="sxs-lookup"><span data-stu-id="1fcdf-130">Now open hello project in Visual Studio, and load adal.js at hello end of hello main page's body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a><span data-ttu-id="1fcdf-131">Configurar Olá API REST</span><span class="sxs-lookup"><span data-stu-id="1fcdf-131">Set up hello REST API</span></span>
<span data-ttu-id="1fcdf-132">Enquanto estamos configurando tudo, vamos trabalhar de API REST do hello back-end.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-132">While we're setting things up, let's get hello backend REST API working.</span></span>  <span data-ttu-id="1fcdf-133">Na raiz de saudação do projeto hello, abra `web.config` e substitua Olá `audience` valor.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-133">In hello root of hello project, open `web.config` and replace hello `audience` value.</span></span>  <span data-ttu-id="1fcdf-134">Olá API REST usará tokens de toovalidate esse valor recebe do aplicativo Angular de saudação em solicitações do AJAX.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-134">hello REST API will use this value toovalidate tokens it receives from hello Angular app on AJAX requests.</span></span>

```xml
<!--web.config-->

...

    <appSettings>
        <add key="ida:Audience" value="[Your-application-id]" />
    </appSettings>

...
```

<span data-ttu-id="1fcdf-135">Isso é tudo que vamos toospend discussão de como funciona a saudação API REST de tempo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-135">That's all hello time we're going toospend discussing how hello REST API works.</span></span>  <span data-ttu-id="1fcdf-136">Sinta-se livre toopoke ao redor no código hello, mas se você quiser toolearn mais sobre como proteger APIs com o Azure AD da web, check-out [neste artigo](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="1fcdf-136">Feel free toopoke around in hello code, but if you want toolearn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-dotnet-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="1fcdf-137">Entrada de usuários</span><span class="sxs-lookup"><span data-stu-id="1fcdf-137">Sign users in</span></span>
<span data-ttu-id="1fcdf-138">Tempo toowrite algum código de identidade.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-138">Time toowrite some identity code.</span></span>  <span data-ttu-id="1fcdf-139">Talvez você já tenha notado que o adal.js contém um provedor AngularJS, que funciona perfeitamente com o mecanismo de roteamento Angular.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-139">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="1fcdf-140">Inicie adicionando Olá módulo adal toohello aplicativo:</span><span class="sxs-lookup"><span data-stu-id="1fcdf-140">Start by adding hello adal module toohello app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="1fcdf-141">Agora você pode inicializar Olá `adalProvider` com a ID do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="1fcdf-141">You can now initialize hello `adalProvider` with your Application ID:</span></span>

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

<span data-ttu-id="1fcdf-142">Ótimo, agora o adal.js todas as informações de saudação precisa toosecure os usuários do aplicativo e entrar no.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-142">Great, now adal.js has all hello information it needs toosecure your app and sign users in.</span></span>  <span data-ttu-id="1fcdf-143">tooforce de entrada para uma rota específica no aplicativo hello, tudo é uma linha de código:</span><span class="sxs-lookup"><span data-stu-id="1fcdf-143">tooforce sign in for a particular route in hello app, all it takes is one line of code:</span></span>

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

<span data-ttu-id="1fcdf-144">Agora, quando um usuário clica Olá `TodoList` link, o adal.js será automaticamente redirecionada tooAzure AD para entrar se necessário.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-144">Now when a user clicks hello `TodoList` link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span>  <span data-ttu-id="1fcdf-145">Também é possível enviar de forma explícita as solicitações de entrada e saída chamando o adal.js em seus controladores:</span><span class="sxs-lookup"><span data-stu-id="1fcdf-145">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

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

## <a name="display-user-info"></a><span data-ttu-id="1fcdf-146">Exibir informações do usuário</span><span class="sxs-lookup"><span data-stu-id="1fcdf-146">Display user info</span></span>
<span data-ttu-id="1fcdf-147">Agora que hello usuário está conectado, você provavelmente precisará tooaccess Olá conectado autenticação dados de usuário em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-147">Now that hello user is signed in, you'll probably need tooaccess hello signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="1fcdf-148">Adal.js expõe essas informações para você em Olá `userInfo` objeto.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-148">Adal.js exposes this information for you in hello `userInfo` object.</span></span>  <span data-ttu-id="1fcdf-149">tooaccess esse objeto em uma exibição, primeiro adicione o adal.js toohello escopo de raiz do controlador correspondente hello:</span><span class="sxs-lookup"><span data-stu-id="1fcdf-149">tooaccess this object in a view, first add adal.js toohello root scope of hello corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="1fcdf-150">Então enfrentam Olá `userInfo` objeto no modo de exibição:</span><span class="sxs-lookup"><span data-stu-id="1fcdf-150">Then you can directly address hello `userInfo` object in your view:</span></span> 

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

<span data-ttu-id="1fcdf-151">Você também pode usar o hello `userInfo` toodetermine do objeto se Olá usuário está conectado ou não.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-151">You can also use hello `userInfo` object toodetermine if hello user is signed in or not.</span></span>

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

## <a name="call-hello-rest-api"></a><span data-ttu-id="1fcdf-152">Saudação de chamada de API REST</span><span class="sxs-lookup"><span data-stu-id="1fcdf-152">Call hello REST API</span></span>
<span data-ttu-id="1fcdf-153">Por fim, é hora tooget alguns tokens e chamada hello toocreate da API REST, ler, atualizam e excluir tarefas.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-153">Finally, it's time tooget some tokens and call hello REST API toocreate, read, update, and delete tasks.</span></span>  <span data-ttu-id="1fcdf-154">E sabe o que mais?</span><span class="sxs-lookup"><span data-stu-id="1fcdf-154">Well guess what?</span></span>  <span data-ttu-id="1fcdf-155">Você não tem toodo *algo*.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-155">You don't have toodo *a thing*.</span></span>  <span data-ttu-id="1fcdf-156">O Adal.js se encarregará automaticamente de obter, armazenar em cache e atualizar os tokens.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-156">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="1fcdf-157">Ele também tome cuidado de anexar esses tokens que AJAX toooutgoing solicita que você envie toohello API REST.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-157">It will also take care of attaching those tokens toooutgoing AJAX requests that you send toohello REST API.</span></span>  

<span data-ttu-id="1fcdf-158">Como isso funciona exatamente?</span><span class="sxs-lookup"><span data-stu-id="1fcdf-158">How exactly does this work?</span></span> <span data-ttu-id="1fcdf-159">É toda Obrigado toohello mágica do [AngularJS interceptores](https://docs.angularjs.org/api/ng/service/$http), que permite o adal.js tootransform mensagens http de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-159">It's all thanks toohello magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js tootransform outgoing and incoming http messages.</span></span>  <span data-ttu-id="1fcdf-160">Além disso, adal.js pressupõe que todas as solicitações enviam toohello mesmo domínio como a janela Olá deve usar tokens destinados Olá mesma ID de aplicativo como Olá aplicativo AngularJS.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-160">Furthermore, adal.js assumes that any requests send toohello same domain as hello window should use tokens intended for hello same Application ID as hello AngularJS app.</span></span>  <span data-ttu-id="1fcdf-161">Isso é porque usamos Olá mesma ID de aplicativo em ambos os aplicativos de saudação Angular em Olá NodeJS REST API.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-161">This is why we used hello same Application ID in both hello Angular app and in hello NodeJS REST API.</span></span>  <span data-ttu-id="1fcdf-162">Obviamente, você pode substituir esse comportamento e informar o adal.js tooget tokens para outras APIs REST, se necessário - mas para Olá este cenário simples padrões fará.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-162">Of course, you can override this behavior and tell adal.js tooget tokens for other REST APIs if necessary - but for this simple scenario hello defaults will do.</span></span>

<span data-ttu-id="1fcdf-163">Aqui está um trecho de código que mostra como é fácil toosend solicitações com tokens de portador do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="1fcdf-163">Here's a snippet that shows how easy it is toosend requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="1fcdf-164">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="1fcdf-164">Congratulations!</span></span>  <span data-ttu-id="1fcdf-165">Seu aplicativo de página única integrado ao Azure AD está concluído.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-165">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="1fcdf-166">Vá em frente, receba os aplausos.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-166">Go ahead, take a bow.</span></span>  <span data-ttu-id="1fcdf-167">Ele pode autenticar os usuários, com segurança chamar sua API REST usando o OpenID Connect de back-end e obter informações básicas sobre o usuário hello.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-167">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about hello user.</span></span>  <span data-ttu-id="1fcdf-168">Fora da caixa Olá, ele oferece suporte a qualquer usuário com um Account pessoal da Microsoft ou uma conta de trabalho/escola do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-168">Out of hello box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="1fcdf-169">Execute o aplicativo hello e em um navegador, navegue muito`https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-169">Run hello app, and in a browser navigate too`https://localhost:44326/`.</span></span>  <span data-ttu-id="1fcdf-170">Entre usando uma conta pessoal da Microsoft ou uma conta corporativa/de estudante.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-170">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="1fcdf-171">Adicionar lista de tarefas do usuário de toohello tarefas e sair.  Tente entrar com hello outro tipo de conta.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-171">Add tasks toohello user's to-do list, and sign out.  Try signing in with hello other type of account.</span></span> <span data-ttu-id="1fcdf-172">Se você precisar de usuários do AD do Azure locatário toocreate trabalho/escola, [Saiba como um aqui tooget](active-directory-howto-tenant.md) (é gratuito).</span><span class="sxs-lookup"><span data-stu-id="1fcdf-172">If you need an Azure AD tenant toocreate work/school users, [learn how tooget one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="1fcdf-173">toocontinue aprendendo sobre Olá v 2.0 ponto de extremidade principal tooour back [guia do desenvolvedor v 2.0](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1fcdf-173">toocontinue learning about hello v2.0 endpoint, head back tooour [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="1fcdf-174">Para obter recursos adicionais, consulte:</span><span class="sxs-lookup"><span data-stu-id="1fcdf-174">For additional resources, check out:</span></span>

* [<span data-ttu-id="1fcdf-175">Exemplos do Azure no GitHub >></span><span class="sxs-lookup"><span data-stu-id="1fcdf-175">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="1fcdf-176">Azure AD no Stack Overflow >></span><span class="sxs-lookup"><span data-stu-id="1fcdf-176">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="1fcdf-177">Documentação do Azure AD no [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="1fcdf-177">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="1fcdf-178">Obter atualizações de segurança para nossos produtos</span><span class="sxs-lookup"><span data-stu-id="1fcdf-178">Get security updates for our products</span></span>
<span data-ttu-id="1fcdf-179">Recomendamos que você tooget as notificações quando os incidentes de segurança ocorrem visitando [essa página](https://technet.microsoft.com/security/dd252948) e assinando tooSecurity alertas de aviso.</span><span class="sxs-lookup"><span data-stu-id="1fcdf-179">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

