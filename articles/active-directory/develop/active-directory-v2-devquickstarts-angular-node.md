---
title: "Introdução ao aplicativo de página única AngularJS NodeJS do Azure AD v2.0 | Microsoft Docs"
description: "Como compilar um aplicativo de página única Angular JS que autentica usuários com contas da Microsoft pessoais e contas corporativas ou de estudante."
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
ms.openlocfilehash: 0e90171afd9c4c782fbb18375ab2d147497ef442
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-angularjs-single-page-app---nodejs"></a><span data-ttu-id="5c151-103">Adicionar as credenciais a um aplicativo de página única do AngularJS - NodeJS</span><span class="sxs-lookup"><span data-stu-id="5c151-103">Add sign-in to an AngularJS single page app - NodeJS</span></span>
<span data-ttu-id="5c151-104">Neste artigo, adicionaremos entrada com contas da plataforma Microsoft a um aplicativo AngularJS usando o ponto de extremidade v2.0 do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5c151-104">In this article we'll add sign in with Microsoft powered accounts to an AngularJS app using the Azure Active Directory v2.0 endpoint.</span></span> <span data-ttu-id="5c151-105">O ponto de extremidade v2.0 permite realizar uma integração única em seu aplicativo e autenticar usuários com contas pessoais e corporativas/de estudante.</span><span class="sxs-lookup"><span data-stu-id="5c151-105">the v2.0 endpoint enable you to perform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="5c151-106">Este exemplo é um aplicativo de página única de uma simples lista de tarefas pendentes que armazena as tarefas em uma API REST back-end. Ele é escrito em NodeJS e protegido usando tokens de portador OAuth do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c151-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written in NodeJS and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="5c151-107">O aplicativo AngularJS usará nossa biblioteca de autenticação JavaScript de código aberto [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) para manipular todo o processo de entrada e adquirir tokens para chamar a API REST.</span><span class="sxs-lookup"><span data-stu-id="5c151-107">The AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) to handle the entire sign in process and acquire tokens for calling the REST API.</span></span>  <span data-ttu-id="5c151-108">O mesmo padrão pode ser aplicado para autenticar as outras APIs REST, como o [Microsoft Graph](https://graph.microsoft.com) ou as APIs do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5c151-108">The same pattern can be applied to authenticate to other REST APIs, like the [Microsoft Graph](https://graph.microsoft.com) or the Azure Resource Manager APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="5c151-109">Nem todos os recursos e cenários do Azure Active Directory têm suporte no ponto de extremidade v2.0.</span><span class="sxs-lookup"><span data-stu-id="5c151-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="5c151-110">Para determinar se você deve usar o ponto de extremidade v2.0, leia sobre as [limitações da v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="5c151-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="5c151-111">Baixar</span><span class="sxs-lookup"><span data-stu-id="5c151-111">Download</span></span>
<span data-ttu-id="5c151-112">Para começar, você precisará baixar e instalar o [Node.js](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="5c151-112">To get started, you'll need to download & install [node.js](https://nodejs.org).</span></span>  <span data-ttu-id="5c151-113">Em seguida, você pode clonar ou [baixar](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) um aplicativo de esqueleto:</span><span class="sxs-lookup"><span data-stu-id="5c151-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS.git
```

<span data-ttu-id="5c151-114">O aplicativo de esqueleto inclui todo o código clichê de um aplicativo AngularJS simples, mas não contém as partes relacionadas à identidade.</span><span class="sxs-lookup"><span data-stu-id="5c151-114">The skeleton app includes all the boilerplate code for a simple AngularJS app, but is missing all of the identity-related pieces.</span></span>  <span data-ttu-id="5c151-115">Se você não quiser acompanhar, clone ou [baixe](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) o exemplo completo.</span><span class="sxs-lookup"><span data-stu-id="5c151-115">If you don't want to follow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) the completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-NodeJS.git
```

## <a name="register-an-app"></a><span data-ttu-id="5c151-116">Registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="5c151-116">Register an app</span></span>
<span data-ttu-id="5c151-117">Primeiro, crie um aplicativo no [Portal de Registro de Aplicativos](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ou execute estas [etapas detalhadas](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="5c151-117">First, create an app in the [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="5c151-118">Não se esqueça de:</span><span class="sxs-lookup"><span data-stu-id="5c151-118">Make sure to:</span></span>

* <span data-ttu-id="5c151-119">Adicionar a plataforma **Web** para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5c151-119">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="5c151-120">Inserir o **URI de Redirecionamento**correto.</span><span class="sxs-lookup"><span data-stu-id="5c151-120">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="5c151-121">O padrão para esse exemplo é `http://localhost:8080`</span><span class="sxs-lookup"><span data-stu-id="5c151-121">The default for this sample is `http://localhost:8080`.</span></span>
* <span data-ttu-id="5c151-122">Deixe a caixa de seleção **Permitir Fluxo Implícito** habilitada.</span><span class="sxs-lookup"><span data-stu-id="5c151-122">Leave the **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="5c151-123">Copie a **ID do Aplicativo** designada ao seu aplicativo, você precisará dela em breve.</span><span class="sxs-lookup"><span data-stu-id="5c151-123">Copy down the **Application ID** that is assigned to your app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="5c151-124">Instalar o adal.js</span><span class="sxs-lookup"><span data-stu-id="5c151-124">Install adal.js</span></span>
<span data-ttu-id="5c151-125">Para começar, navegue até o projeto do qual você fez o download e instale o adal.js.</span><span class="sxs-lookup"><span data-stu-id="5c151-125">To start, navigate to project you downloaded and install adal.js.</span></span>  <span data-ttu-id="5c151-126">Se o [bower](http://bower.io/) estiver instalado, basta executar este comando.</span><span class="sxs-lookup"><span data-stu-id="5c151-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="5c151-127">Para qualquer incompatibilidade de versão da dependência, basta escolha a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="5c151-127">For any dependency version mismatches, just choose the higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="5c151-128">Como alternativa, você pode baixar manualmente o [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) e o [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="5c151-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="5c151-129">Adicione os dois arquivos ao diretório `app/lib/adal-angular-experimental/dist` .</span><span class="sxs-lookup"><span data-stu-id="5c151-129">Add both files to the `app/lib/adal-angular-experimental/dist` directory.</span></span>

<span data-ttu-id="5c151-130">Abra o projeto em seu editor de texto favorito e carregue o adal.js no final do corpo da página:</span><span class="sxs-lookup"><span data-stu-id="5c151-130">Now open the project in your favorite text editor, and load adal.js at the end of the page body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-the-rest-api"></a><span data-ttu-id="5c151-131">Configurar a API REST</span><span class="sxs-lookup"><span data-stu-id="5c151-131">Set up the REST API</span></span>
<span data-ttu-id="5c151-132">Enquanto configuramos as coisas, vamos fazer a API REST back-end funcionar.</span><span class="sxs-lookup"><span data-stu-id="5c151-132">While we're setting things up, lets get the backend REST API working.</span></span>  <span data-ttu-id="5c151-133">Em um prompt de comando, instale todos os pacotes necessários executando (verifique se você está no diretório de nível superior do projeto):</span><span class="sxs-lookup"><span data-stu-id="5c151-133">In a command prompt, install all the necessary packages by running (make sure you're in the top-level directory of the project):</span></span>

```
npm install
```

<span data-ttu-id="5c151-134">Agora, abra `config.js` e substitua o valor `audience`:</span><span class="sxs-lookup"><span data-stu-id="5c151-134">Now open `config.js` and replace the `audience` value:</span></span>

```js
exports.creds = {

     // TODO: Replace this value with the Application ID from the registration portal
     audience: '<Your-application-id>',

     ...
}
```

<span data-ttu-id="5c151-135">A API REST usará esse valor para validar tokens que recebe do aplicativo Angular em solicitações AJAX.</span><span class="sxs-lookup"><span data-stu-id="5c151-135">The REST API will use this value to validate tokens it receives from the Angular app on AJAX requests.</span></span>  <span data-ttu-id="5c151-136">Observe que essa API REST simples armazena dados na memória. Portanto, cada vez que você parar o servidor, perderá todas as tarefas criadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5c151-136">Note that this simple REST API stores data in-memory - so each time to stop the server, you will lose all previously created tasks.</span></span>

<span data-ttu-id="5c151-137">Esse é todo o tempo que usaremos para discutir o funcionamento da API REST.</span><span class="sxs-lookup"><span data-stu-id="5c151-137">That's all the time we're going to spend discussing how the REST API works.</span></span>  <span data-ttu-id="5c151-138">Fique à vontade para examinar o código, mas se você quiser saber mais sobre como proteger as APIs Web com o AD do Azure, confira [este artigo](active-directory-v2-devquickstarts-node-api.md).</span><span class="sxs-lookup"><span data-stu-id="5c151-138">Feel free to poke around in the code, but if you want to learn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-node-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="5c151-139">Entrada de usuários</span><span class="sxs-lookup"><span data-stu-id="5c151-139">Sign users in</span></span>
<span data-ttu-id="5c151-140">Hora de escrever um pouco de código de identidade.</span><span class="sxs-lookup"><span data-stu-id="5c151-140">Time to write some identity code.</span></span>  <span data-ttu-id="5c151-141">Talvez você já tenha notado que o adal.js contém um provedor AngularJS, que funciona perfeitamente com o mecanismo de roteamento Angular.</span><span class="sxs-lookup"><span data-stu-id="5c151-141">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="5c151-142">Comece adicionando o módulo adal ao aplicativo:</span><span class="sxs-lookup"><span data-stu-id="5c151-142">Start by adding the adal module to the app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="5c151-143">Agora, você pode inicializar o `adalProvider` com a ID do Aplicativo:</span><span class="sxs-lookup"><span data-stu-id="5c151-143">You can now initialize the `adalProvider` with your Application ID:</span></span>

```js
// app/scripts/app.js

...

adalProvider.init({

        // Use this value for the public instance of Azure AD
        instance: 'https://login.microsoftonline.com/', 

        // The 'common' endpoint is used for multi-tenant applications like this one
        tenant: 'common',

        // Your application id from the registration portal
        clientId: '<Your-application-id>',

        // If you're using IE, uncommment this line - the default HTML5 sessionStorage does not work for localhost.
        //cacheLocation: 'localStorage',

    }, $httpProvider);
```

<span data-ttu-id="5c151-144">Ótimo, agora o adal.js tem todas as informações necessárias para proteger seu aplicativo e autenticar os usuários.</span><span class="sxs-lookup"><span data-stu-id="5c151-144">Great, now adal.js has all the information it needs to secure your app and sign users in.</span></span>  <span data-ttu-id="5c151-145">Para forçar a entrada por uma rota específica no aplicativo, basta uma linha de código:</span><span class="sxs-lookup"><span data-stu-id="5c151-145">To force sign in for a particular route in the app, all it takes is one line of code:</span></span>

```js
// app/scripts/app.js

...

}).when("/TodoList", {
    controller: "todoListCtrl",
    templateUrl: "/static/views/TodoList.html",
    requireADLogin: true, // Ensures that the user must be logged in to access the route
})

...
```

<span data-ttu-id="5c151-146">Quando um usuário clica no link `TodoList` , o adal.js o redireciona automaticamente ao AD do Azure para conexão, se for necessário.</span><span class="sxs-lookup"><span data-stu-id="5c151-146">Now when a user clicks the `TodoList` link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span>  <span data-ttu-id="5c151-147">Também é possível enviar de forma explícita as solicitações de entrada e saída chamando o adal.js em seus controladores:</span><span class="sxs-lookup"><span data-stu-id="5c151-147">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

```js
// app/scripts/homeCtrl.js

angular.module('todoApp')
// Load adal.js the same way for use in controllers and views   
.controller('homeCtrl', ['$scope', 'adalAuthenticationService','$location', function ($scope, adalService, $location) {
    $scope.login = function () {

        // Redirect the user to sign in
        adalService.login();

    };
    $scope.logout = function () {

        // Redirect the user to log out    
        adalService.logOut();

    };
...
```

## <a name="display-user-info"></a><span data-ttu-id="5c151-148">Exibir informações do usuário</span><span class="sxs-lookup"><span data-stu-id="5c151-148">Display user info</span></span>
<span data-ttu-id="5c151-149">Agora que o usuário está conectado, provavelmente você precisará acessar os dados de autenticação do usuário conectado em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5c151-149">Now that the user is signed in, you'll probably need to access the signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="5c151-150">O Adal.js expõe essas informações para você no objeto `userInfo` .</span><span class="sxs-lookup"><span data-stu-id="5c151-150">Adal.js exposes this information for you in the `userInfo` object.</span></span>  <span data-ttu-id="5c151-151">Para acessar este objeto em uma exibição, primeiro adicione adal.js ao escopo raiz do controlador correspondente:</span><span class="sxs-lookup"><span data-stu-id="5c151-151">To access this object in a view, first add adal.js to the root scope of the corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="5c151-152">Em seguida, você pode endereçar diretamente o objeto `userInfo` em seu modo de exibição:</span><span class="sxs-lookup"><span data-stu-id="5c151-152">Then you can directly address the `userInfo` object in your view:</span></span> 

```html
<!--app/views/UserData.html-->

...

    <!--Get the user's profile information from the ADAL userInfo object-->
    <tr ng-repeat="(key, value) in userInfo.profile">
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
...
```

<span data-ttu-id="5c151-153">Você também pode usar o objeto `userInfo` para determinar se o usuário está conectado ou não.</span><span class="sxs-lookup"><span data-stu-id="5c151-153">You can also use the `userInfo` object to determine if the user is signed in or not.</span></span>

```html
<!--index.html-->

...

    <!--Use the ADAL userInfo object to show the right login/logout button-->
    <ul class="nav navbar-nav navbar-right">
        <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
        <li><a class="btn btn-link" ng-hide="userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    </ul>
...
```

## <a name="call-the-rest-api"></a><span data-ttu-id="5c151-154">Chamar a API REST</span><span class="sxs-lookup"><span data-stu-id="5c151-154">Call the REST API</span></span>
<span data-ttu-id="5c151-155">Por fim, é hora de obter alguns tokens e chamar a API REST para criar, ler, atualizar e excluir tarefas.</span><span class="sxs-lookup"><span data-stu-id="5c151-155">Finally, it's time to get some tokens and call the REST API to create, read, update, and delete tasks.</span></span>  <span data-ttu-id="5c151-156">E sabe o que mais?</span><span class="sxs-lookup"><span data-stu-id="5c151-156">Well guess what?</span></span>  <span data-ttu-id="5c151-157">Você não precisa fazer *coisa alguma*.</span><span class="sxs-lookup"><span data-stu-id="5c151-157">You don't have to do *a thing*.</span></span>  <span data-ttu-id="5c151-158">O Adal.js se encarregará automaticamente de obter, armazenar em cache e atualizar os tokens.</span><span class="sxs-lookup"><span data-stu-id="5c151-158">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="5c151-159">Ele também se encarregará de conectar esses tokens às solicitações AJAX de saída que você envia à API REST.</span><span class="sxs-lookup"><span data-stu-id="5c151-159">It will also take care of attaching those tokens to outgoing AJAX requests that you send to the REST API.</span></span>  

<span data-ttu-id="5c151-160">Como isso funciona exatamente?</span><span class="sxs-lookup"><span data-stu-id="5c151-160">How exactly does this work?</span></span> <span data-ttu-id="5c151-161">É tudo graças à mágica dos [interceptores AngularJS](https://docs.angularjs.org/api/ng/service/$http), que permitem ao adal.js transformar as mensagens http de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="5c151-161">It's all thanks to the magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js to transform outgoing and incoming http messages.</span></span>  <span data-ttu-id="5c151-162">Além disso, o adal.js pressupõe que todas as solicitações enviadas ao mesmo domínio que a janela devem usar tokens destinados à mesma ID de Aplicativo que o aplicativo AngularJS.</span><span class="sxs-lookup"><span data-stu-id="5c151-162">Furthermore, adal.js assumes that any requests send to the same domain as the window should use tokens intended for the same Application ID as the AngularJS app.</span></span>  <span data-ttu-id="5c151-163">É por isso que usamos a mesma ID de Aplicativo no aplicativo Angular e na API REST NodeJS.</span><span class="sxs-lookup"><span data-stu-id="5c151-163">This is why we used the same Application ID in both the Angular app and in the NodeJS REST API.</span></span>  <span data-ttu-id="5c151-164">Claro, você pode substituir esse comportamento e instruir o adal.js a obter tokens para outras APIs REST, se for necessário. Mas para este cenário simples, basta os padrão.</span><span class="sxs-lookup"><span data-stu-id="5c151-164">Of course, you can override this behavior and tell adal.js to get tokens for other REST APIs if necessary - but for this simple scenario the defaults will do.</span></span>

<span data-ttu-id="5c151-165">Veja um trecho que mostra como é fácil enviar solicitações com tokens de portador do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="5c151-165">Here's a snippet that shows how easy it is to send requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="5c151-166">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="5c151-166">Congratulations!</span></span>  <span data-ttu-id="5c151-167">Seu aplicativo de página única integrado ao Azure AD está concluído.</span><span class="sxs-lookup"><span data-stu-id="5c151-167">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="5c151-168">Vá em frente, receba os aplausos.</span><span class="sxs-lookup"><span data-stu-id="5c151-168">Go ahead, take a bow.</span></span>  <span data-ttu-id="5c151-169">Ele pode autenticar os usuários, chamar com segurança sua API REST back-end usando OpenID Connect e obter informações básicas sobre o usuário.</span><span class="sxs-lookup"><span data-stu-id="5c151-169">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about the user.</span></span>  <span data-ttu-id="5c151-170">Para uso imediato, ele oferece suporte a qualquer usuário com uma conta pessoal da Microsoft ou uma conta corporativa/de estudante do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c151-170">Out of the box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="5c151-171">Experimente o aplicativo executando:</span><span class="sxs-lookup"><span data-stu-id="5c151-171">Give the app a try by running:</span></span>

```
node server.js
```

<span data-ttu-id="5c151-172">Em um navegador, navegue até `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="5c151-172">In a browser navigate to `http://localhost:8080`.</span></span>  <span data-ttu-id="5c151-173">Entre usando uma conta pessoal da Microsoft ou uma conta corporativa/de estudante.</span><span class="sxs-lookup"><span data-stu-id="5c151-173">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="5c151-174">Adicione tarefas à lista de tarefas pendentes do usuário e saia.</span><span class="sxs-lookup"><span data-stu-id="5c151-174">Add tasks to the user's to-do list, and sign out.</span></span>  <span data-ttu-id="5c151-175">Tente entrar com o outro tipo de conta.</span><span class="sxs-lookup"><span data-stu-id="5c151-175">Try signing in with the other type of account.</span></span> <span data-ttu-id="5c151-176">Se você precisar de um locatário do AD do Azure a fim de criar usuários corporativos/estudantes, [saiba como obter um aqui](active-directory-howto-tenant.md) (é gratuito).</span><span class="sxs-lookup"><span data-stu-id="5c151-176">If you need an Azure AD tenant to create work/school users, [learn how to get one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="5c151-177">Para continuar aprendendo sobre o ponto de extremidade v2.0, retorne ao nosso [guia do desenvolvedor v2.0](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5c151-177">To continue learning about the the v2.0 endpoint, head back to our [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="5c151-178">Para obter recursos adicionais, consulte:</span><span class="sxs-lookup"><span data-stu-id="5c151-178">For additional resources, check out:</span></span>

* [<span data-ttu-id="5c151-179">Exemplos do Azure no GitHub >></span><span class="sxs-lookup"><span data-stu-id="5c151-179">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="5c151-180">Azure AD no Stack Overflow >></span><span class="sxs-lookup"><span data-stu-id="5c151-180">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="5c151-181">Documentação do Azure AD no [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="5c151-181">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="5c151-182">Obter atualizações de segurança para nossos produtos</span><span class="sxs-lookup"><span data-stu-id="5c151-182">Get security updates for our products</span></span>
<span data-ttu-id="5c151-183">Recomendamos que você obtenha notificações sobre a ocorrência de incidentes de segurança visitando [esta página](https://technet.microsoft.com/security/dd252948) e assinando os alertas do Security Advisory.</span><span class="sxs-lookup"><span data-stu-id="5c151-183">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

