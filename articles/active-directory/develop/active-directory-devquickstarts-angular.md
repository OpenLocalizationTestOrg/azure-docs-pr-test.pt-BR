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
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a><span data-ttu-id="5a71b-103">Ajudar a proteger aplicativos de página única AngularJS usando o AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5a71b-103">Help secure AngularJS single-page apps by using Azure AD</span></span>

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="5a71b-104">Azure Active Directory (AD do Azure) torna simples e direta para você tooadd entrada, saída e chamadas de API de OAuth seguro tooyour aplicativos de única página.</span><span class="sxs-lookup"><span data-stu-id="5a71b-104">Azure Active Directory (Azure AD) makes it simple and straightforward for you tooadd sign-in, sign-out, and secure OAuth API calls tooyour single-page apps.</span></span>  <span data-ttu-id="5a71b-105">Ele permite que os usuários de tooauthenticate aplicativos com suas contas do Active Directory do Windows Server e consumir qualquer API do AD do Azure ajuda a proteger, como Olá APIs do Office 365 ou hello Azure API da web.</span><span class="sxs-lookup"><span data-stu-id="5a71b-105">It enables your apps tooauthenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="5a71b-106">Para aplicativos de JavaScript em execução em um navegador, o AD do Azure fornece Olá biblioteca de autenticação do Active Directory (ADAL) ou adal.js.</span><span class="sxs-lookup"><span data-stu-id="5a71b-106">For JavaScript applications running in a browser, Azure AD provides hello Active Directory Authentication Library (ADAL), or adal.js.</span></span> <span data-ttu-id="5a71b-107">Olá única finalidade adal.js é toomake fácil para seus tokens de acesso do aplicativo tooget.</span><span class="sxs-lookup"><span data-stu-id="5a71b-107">hello sole purpose of adal.js is toomake it easy for your app tooget access tokens.</span></span> <span data-ttu-id="5a71b-108">toodemonstrate facilidade é, aqui é possível compilar um aplicativo de lista de tooDo do AngularJS:</span><span class="sxs-lookup"><span data-stu-id="5a71b-108">toodemonstrate just how easy it is, here we'll build an AngularJS tooDo List application that:</span></span>

* <span data-ttu-id="5a71b-109">Sinais Olá usuário no aplicativo toohello usando o AD do Azure como provedor de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="5a71b-109">Signs hello user in toohello app by using Azure AD as hello identity provider.</span></span>

* <span data-ttu-id="5a71b-110">Exibe algumas informações sobre o usuário hello.</span><span class="sxs-lookup"><span data-stu-id="5a71b-110">Displays some information about hello user.</span></span>
* <span data-ttu-id="5a71b-111">Com segurança chamadas Olá tooDo do aplicativo lista API usando tokens de portador do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a71b-111">Securely calls hello app's tooDo List API by using bearer tokens from Azure AD.</span></span>
* <span data-ttu-id="5a71b-112">Sinais Olá usuário fora do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="5a71b-112">Signs hello user out of hello app.</span></span>

<span data-ttu-id="5a71b-113">aplicativo toobuild hello de concluído, trabalho, você precisa:</span><span class="sxs-lookup"><span data-stu-id="5a71b-113">toobuild hello complete, working application, you need to:</span></span>

1. <span data-ttu-id="5a71b-114">Registrar um aplicativo no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a71b-114">Register your app with Azure AD.</span></span>
2. <span data-ttu-id="5a71b-115">Instalar o ADAL e configurar o aplicativo de página única hello.</span><span class="sxs-lookup"><span data-stu-id="5a71b-115">Install ADAL and configure hello single-page app.</span></span>
3. <span data-ttu-id="5a71b-116">Use páginas seguras toohelp ADAL no aplicativo de página única hello.</span><span class="sxs-lookup"><span data-stu-id="5a71b-116">Use ADAL toohelp secure pages in hello single-page app.</span></span>

<span data-ttu-id="5a71b-117">tooget iniciado, [baixar o esqueleto do aplicativo hello](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) ou [baixar exemplo hello concluída](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="5a71b-117">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="5a71b-118">Você também precisará de um locatário do Azure AD no qual possa criar usuários e registrar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5a71b-118">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="5a71b-119">Se você ainda não tiver um locatário, [Saiba como tooget uma](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="5a71b-119">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-hello-directorysearcher-application"></a><span data-ttu-id="5a71b-120">Etapa 1: Registrar o aplicativo de DirectorySearcher hello</span><span class="sxs-lookup"><span data-stu-id="5a71b-120">Step 1: Register hello DirectorySearcher application</span></span>
<span data-ttu-id="5a71b-121">tooenable aplicativo tooauthenticate usuários e tokens de get, primeiro é necessário tooregistê-lo no AD do Azure locatário:</span><span class="sxs-lookup"><span data-stu-id="5a71b-121">tooenable your app tooauthenticate users and get tokens, you first need tooregister it in your Azure AD tenant:</span></span>

1. <span data-ttu-id="5a71b-122">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5a71b-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5a71b-123">Se você tiver entrado em diretórios toomultiple, talvez seja necessário tooensure que você está exibindo o diretório correto hello.</span><span class="sxs-lookup"><span data-stu-id="5a71b-123">If you are signed in toomultiple directories, you may need tooensure you are viewing hello correct directory.</span></span> <span data-ttu-id="5a71b-124">toodo assim, na barra superior do hello, clique em sua conta.</span><span class="sxs-lookup"><span data-stu-id="5a71b-124">toodo so, on hello top bar, click your account.</span></span> <span data-ttu-id="5a71b-125">Em Olá **diretório** , escolha o locatário de saudação do AD do Azure onde deseja tooregister seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5a71b-125">Under hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="5a71b-126">Clique em **mais serviços** Olá painel esquerdo e, em seguida, selecione **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="5a71b-126">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="5a71b-127">Clique em **Registros do aplicativo** e, em seguida, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5a71b-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="5a71b-128">Siga os prompts de saudação e criar um novo aplicativo web e/ou API da web:</span><span class="sxs-lookup"><span data-stu-id="5a71b-128">Follow hello prompts and create a new web application and/or web API:</span></span>
  * <span data-ttu-id="5a71b-129">**Nome** descreve toousers seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5a71b-129">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="5a71b-130">**Uri de redirecionamento** é Olá local toowhich AD do Azure retornará tokens.</span><span class="sxs-lookup"><span data-stu-id="5a71b-130">**Redirect Uri** is hello location toowhich Azure AD will return tokens.</span></span> <span data-ttu-id="5a71b-131">saudação padrão local para este exemplo é `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="5a71b-131">hello default location for this sample is `https://localhost:44326/`.</span></span>
6. <span data-ttu-id="5a71b-132">Depois de concluir o registro, o Azure AD atribui a um aplicativo de tooyour de ID de aplicativo único.</span><span class="sxs-lookup"><span data-stu-id="5a71b-132">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span>  <span data-ttu-id="5a71b-133">Você precisará desse valor nas seções de Avançar hello, portanto copiá-lo do guia do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="5a71b-133">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="5a71b-134">O Adal.js usa toocommunicate de fluxo implícitos OAuth Olá com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a71b-134">Adal.js uses hello OAuth implicit flow toocommunicate with Azure AD.</span></span> <span data-ttu-id="5a71b-135">Você deve habilitar o fluxo implícito Olá para seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="5a71b-135">You must enable hello implicit flow for your application:</span></span>
  1. <span data-ttu-id="5a71b-136">Clique em aplicativo hello e selecione **manifesto** editor de manifesto tooopen Olá embutido.</span><span class="sxs-lookup"><span data-stu-id="5a71b-136">Click hello application and select **Manifest** tooopen hello inline manifest editor.</span></span>
  2. <span data-ttu-id="5a71b-137">Localizar Olá `oauth2AllowImplicitFlow` propriedade.</span><span class="sxs-lookup"><span data-stu-id="5a71b-137">Locate hello `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="5a71b-138">Defina seu valor muito`true`.</span><span class="sxs-lookup"><span data-stu-id="5a71b-138">Set its value too`true`.</span></span>
  3. <span data-ttu-id="5a71b-139">Clique em **salvar** toosave manifesto de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a71b-139">Click **Save** toosave hello manifest.</span></span>
8. <span data-ttu-id="5a71b-140">Conceda permissões em seu locatário para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5a71b-140">Grant permissions across your tenant for your application.</span></span> <span data-ttu-id="5a71b-141">Vá muito**configurações** > **propriedades** > **permissões necessárias**e clique em Olá **conceder permissões**botão na barra superior hello.</span><span class="sxs-lookup"><span data-stu-id="5a71b-141">Go too**Settings** > **Properties** > **Required Permissions**, and click hello **Grant Permissions** button on hello top bar.</span></span> <span data-ttu-id="5a71b-142">Clique em **Sim** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="5a71b-142">Click **Yes** tooconfirm.</span></span>

## <a name="step-2-install-adal-and-configure-hello-single-page-app"></a><span data-ttu-id="5a71b-143">Etapa 2: Instalar ADAL e configurar o aplicativo de página única Olá</span><span class="sxs-lookup"><span data-stu-id="5a71b-143">Step 2: Install ADAL and configure hello single-page app</span></span>
<span data-ttu-id="5a71b-144">Agora que você tem um aplicativo no AD do Azure, você pode instalar a adal.js e escrever seu código relacionado à identidade.</span><span class="sxs-lookup"><span data-stu-id="5a71b-144">Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.</span></span>

### <a name="configure-hello-javascript-client"></a><span data-ttu-id="5a71b-145">Configurar o cliente de JavaScript Olá</span><span class="sxs-lookup"><span data-stu-id="5a71b-145">Configure hello JavaScript client</span></span>
<span data-ttu-id="5a71b-146">Começar adicionando adal.js toohello TodoSPA projeto usando Olá Package Manager Console:</span><span class="sxs-lookup"><span data-stu-id="5a71b-146">Begin by adding adal.js toohello TodoSPA project by using hello Package Manager Console:</span></span>
  1. <span data-ttu-id="5a71b-147">Baixar [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) e adicioná-lo toohello `App/Scripts/` diretório do projeto.</span><span class="sxs-lookup"><span data-stu-id="5a71b-147">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it toohello `App/Scripts/` project directory.</span></span>
  2. <span data-ttu-id="5a71b-148">Baixar [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) e adicioná-lo toohello `App/Scripts/` diretório do projeto.</span><span class="sxs-lookup"><span data-stu-id="5a71b-148">Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it toohello `App/Scripts/` project directory.</span></span>
  3. <span data-ttu-id="5a71b-149">Carregar cada script antes final Olá Olá `</body>` em `index.html`:</span><span class="sxs-lookup"><span data-stu-id="5a71b-149">Load each script before hello end of hello `</body>` in `index.html`:</span></span>

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-hello-back-end-server"></a><span data-ttu-id="5a71b-150">Configurar o servidor de back-end Olá</span><span class="sxs-lookup"><span data-stu-id="5a71b-150">Configure hello back end server</span></span>
<span data-ttu-id="5a71b-151">Para tokens de tooaccept do aplicativo de página única Olá tooDo de back-end API da lista de navegador hello, back-end Olá precisa de informações de configuração sobre o registro do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="5a71b-151">For hello single-page app's back-end tooDo List API tooaccept tokens from hello browser, hello back end needs configuration information about hello app registration.</span></span> <span data-ttu-id="5a71b-152">No projeto de TodoSPA hello, abra `web.config`.</span><span class="sxs-lookup"><span data-stu-id="5a71b-152">In hello TodoSPA project, open `web.config`.</span></span> <span data-ttu-id="5a71b-153">Substituir valores de saudação de elementos Olá Olá `<appSettings>` Olá a seção tooreflect Olá os valores que você usou no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a71b-153">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values that you used in hello Azure portal.</span></span> <span data-ttu-id="5a71b-154">Seu código fará referência a esses valores sempre que ele usar a ADAL.</span><span class="sxs-lookup"><span data-stu-id="5a71b-154">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="5a71b-155">`ida:Tenant`é o domínio de saudação do seu locatário do AD do Azure – por exemplo, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="5a71b-155">`ida:Tenant` is hello domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="5a71b-156">`ida:Audience`é Olá ID do cliente do aplicativo que você copiou do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a71b-156">`ida:Audience` is hello client ID of your application that you copied from hello portal.</span></span>

## <a name="step-3-use-adal-toohelp-secure-pages-in-hello-single-page-app"></a><span data-ttu-id="5a71b-157">Etapa 3: Use ADAL toohelp seguras páginas Olá aplicativo de página única</span><span class="sxs-lookup"><span data-stu-id="5a71b-157">Step 3: Use ADAL toohelp secure pages in hello single-page app</span></span>
<span data-ttu-id="5a71b-158">O Adal.js integra-se ao roteiro AngularJS e aos provedores HTTP e, portanto, você pode ajudar a proteger exibições individuais em seu aplicativo de página única.</span><span class="sxs-lookup"><span data-stu-id="5a71b-158">Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.</span></span>

1. <span data-ttu-id="5a71b-159">Em `App/Scripts/app.js`, Avançar no módulo de adal.js hello:</span><span class="sxs-lookup"><span data-stu-id="5a71b-159">In `App/Scripts/app.js`, bring in hello adal.js module:</span></span>

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. <span data-ttu-id="5a71b-160">Inicializar `adalProvider` usando valores de configuração de saudação de seu registro de aplicativo, também no `App/Scripts/app.js`:</span><span class="sxs-lookup"><span data-stu-id="5a71b-160">Initialize `adalProvider` by using hello configuration values of your application registration, also in `App/Scripts/app.js`:</span></span>

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
3. <span data-ttu-id="5a71b-161">Ajudar a proteger Olá `TodoList` exibição no aplicativo hello usando apenas uma linha de código: `requireADLogin`.</span><span class="sxs-lookup"><span data-stu-id="5a71b-161">Help secure hello `TodoList` view in hello app by using only one line of code: `requireADLogin`.</span></span>

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a><span data-ttu-id="5a71b-162">Resumo</span><span class="sxs-lookup"><span data-stu-id="5a71b-162">Summary</span></span>
<span data-ttu-id="5a71b-163">Agora você tem um aplicativo de única página seguro que pode entrar em usuários e emitir solicitações protegidas de token de portador tooits back-end API.</span><span class="sxs-lookup"><span data-stu-id="5a71b-163">You now have a secure single-page app that can sign in users and issue bearer-token-protected requests tooits back-end API.</span></span> <span data-ttu-id="5a71b-164">Quando um usuário clica Olá **TodoList** link, o adal.js será automaticamente redirecionada tooAzure AD para entrar se necessário.</span><span class="sxs-lookup"><span data-stu-id="5a71b-164">When a user clicks hello **TodoList** link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span> <span data-ttu-id="5a71b-165">Além disso, o adal.js anexa automaticamente um acesso token tooany Ajax solicitações que são enviadas de back-end do aplicativo toohello.</span><span class="sxs-lookup"><span data-stu-id="5a71b-165">In addition, adal.js will automatically attach an access token tooany Ajax requests that are sent toohello app's back end.</span></span>  

<span data-ttu-id="5a71b-166">Olá etapas anteriores são Olá bare mínimo necessário toobuild um aplicativo de página única usando o adal.js.</span><span class="sxs-lookup"><span data-stu-id="5a71b-166">hello preceding steps are hello bare minimum necessary toobuild a single-page app by using adal.js.</span></span> <span data-ttu-id="5a71b-167">Mas alguns outros recursos são úteis no aplicativo de página única:</span><span class="sxs-lookup"><span data-stu-id="5a71b-167">But a few other features are useful in single-page app:</span></span>

* <span data-ttu-id="5a71b-168">tooexplicitly emitir solicitações de entrada e saídas, você pode definir funções em seus controladores que invocam adal.js.</span><span class="sxs-lookup"><span data-stu-id="5a71b-168">tooexplicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.</span></span>  <span data-ttu-id="5a71b-169">Em `App/Scripts/homeCtrl.js`:</span><span class="sxs-lookup"><span data-stu-id="5a71b-169">In `App/Scripts/homeCtrl.js`:</span></span>

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
* <span data-ttu-id="5a71b-170">Talvez você queira toopresent informações do usuário na interface de usuário do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="5a71b-170">You might want toopresent user information in hello app's UI.</span></span> <span data-ttu-id="5a71b-171">Olá ADAL serviço já foi adicionado toohello `userDataCtrl` controlador, para que você possa acessar Olá `userInfo` exibição, associada ao objeto no hello `App/Views/UserData.html`:</span><span class="sxs-lookup"><span data-stu-id="5a71b-171">hello ADAL service has already been added toohello `userDataCtrl` controller, so you can access hello `userInfo` object in hello associated view, `App/Views/UserData.html`:</span></span>

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* <span data-ttu-id="5a71b-172">Há muitos cenários em que você desejará tooknow se Olá usuário está conectado ou não.</span><span class="sxs-lookup"><span data-stu-id="5a71b-172">There are many scenarios in which you'll want tooknow if hello user is signed in or not.</span></span> <span data-ttu-id="5a71b-173">Você também pode usar o hello `userInfo` objeto toogather essas informações.</span><span class="sxs-lookup"><span data-stu-id="5a71b-173">You can also use hello `userInfo` object toogather this information.</span></span>  <span data-ttu-id="5a71b-174">Por exemplo, em `index.html`, você pode mostrar o hello **Login** ou **Logout** botão com base no status de autenticação:</span><span class="sxs-lookup"><span data-stu-id="5a71b-174">For instance, in `index.html`, you can show either hello **Login** or **Logout** button based on authentication status:</span></span>

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

<span data-ttu-id="5a71b-175">O aplicativo de página única integrado ao AD do Azure pode autenticar os usuários, com segurança chamar seu back-end usando OAuth 2.0 e obter informações básicas sobre o usuário hello.</span><span class="sxs-lookup"><span data-stu-id="5a71b-175">Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about hello user.</span></span> <span data-ttu-id="5a71b-176">Se você ainda não fez isso, agora é Olá tempo toopopulate seu locatário com alguns usuários.</span><span class="sxs-lookup"><span data-stu-id="5a71b-176">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span> <span data-ttu-id="5a71b-177">Executar seu aplicativo de página única lista tooDo e entrar com um desses usuários.</span><span class="sxs-lookup"><span data-stu-id="5a71b-177">Run your tooDo List single-page app, and sign in with one of those users.</span></span> <span data-ttu-id="5a71b-178">Adicionar lista de tarefas do usuário do tarefas toohello, sair e entrar novamente.</span><span class="sxs-lookup"><span data-stu-id="5a71b-178">Add tasks toohello user's to-do list, sign out, and sign back in.</span></span>

<span data-ttu-id="5a71b-179">Adal.js torna fácil tooincorporate recursos comuns de identidade em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5a71b-179">Adal.js makes it easy tooincorporate common identity features into your application.</span></span> <span data-ttu-id="5a71b-180">Cuida de todo o trabalho sujo Olá para você: gerenciamento de cache, suporte ao protocolo OAuth, apresentando usuário Olá com uma entrada da interface do usuário, atualizando tokens expirados e muito mais.</span><span class="sxs-lookup"><span data-stu-id="5a71b-180">It takes care of all hello dirty work for you: cache management, OAuth protocol support, presenting hello user with a sign-in UI, refreshing expired tokens, and more.</span></span>

<span data-ttu-id="5a71b-181">Para referência, o exemplo hello concluída (sem os valores de configuração) está disponível em [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="5a71b-181">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a71b-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5a71b-182">Next steps</span></span>
<span data-ttu-id="5a71b-183">Agora você pode mover tooadditional cenários.</span><span class="sxs-lookup"><span data-stu-id="5a71b-183">You can now move on tooadditional scenarios.</span></span> <span data-ttu-id="5a71b-184">Talvez você queira tootry: [chamar uma API da web CORS de um aplicativo de página única](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span><span class="sxs-lookup"><span data-stu-id="5a71b-184">You might want tootry: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
