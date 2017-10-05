---
title: "Conexão do aplicativo Web do Node.js no Azure Active Directory v2.0 | Microsoft Docs"
description: "Saiba como criar um aplicativo Web do Node.js que conecta um usuário usando uma conta pessoal da Microsoft e uma conta corporativa ou de estudante."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 1b889e72-f5c3-464a-af57-79abf5e2e147
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 6d49c742f72440e22830915c90de009d9188db2a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-a-nodejs-web-app"></a><span data-ttu-id="46d95-103">Adicionar conexão a um aplicativo Web do Node.js</span><span class="sxs-lookup"><span data-stu-id="46d95-103">Add sign-in to a Node.js web app</span></span>

> [!NOTE]
> <span data-ttu-id="46d95-104">Nem todos os cenários e recursos do Azure Active Directory funcionam com o ponto de extremidade v2.0.</span><span class="sxs-lookup"><span data-stu-id="46d95-104">Not all Azure Active Directory scenarios and features work with the v2.0 endpoint.</span></span> <span data-ttu-id="46d95-105">Para determinar se você deve usar o ponto de extremidade v2.0 ou v1.0, leia sobre as [limitações da v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="46d95-105">To determine whether you should use the v2.0 endpoint or the v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 

<span data-ttu-id="46d95-106">Neste tutorial, usamos o Passport para realizar as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="46d95-106">In this tutorial, we use Passport to do the following tasks:</span></span>

* <span data-ttu-id="46d95-107">Em um aplicativo Web, conecte o usuário usando o Azure AD (Azure Active Directory) e o ponto de extremidade v2.0.</span><span class="sxs-lookup"><span data-stu-id="46d95-107">In a web app, sign in the user by using Azure Active Directory (Azure AD) and the v2.0 endpoint.</span></span>
* <span data-ttu-id="46d95-108">Exibir informações sobre o usuário.</span><span class="sxs-lookup"><span data-stu-id="46d95-108">Display information about the user.</span></span>
* <span data-ttu-id="46d95-109">Desconectar o usuário do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46d95-109">Sign the user out of the app.</span></span>

<span data-ttu-id="46d95-110">**Passport** é middleware de autenticação para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="46d95-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="46d95-111">Flexível e modular, o Passport pode ser colocado sem impedimento em qualquer aplicativo Web baseado em Express ou Restify.</span><span class="sxs-lookup"><span data-stu-id="46d95-111">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="46d95-112">No Passport, um conjunto abrangente de estratégias dão suporte à autenticação com o uso de um nome de usuário e uma senha, Facebook, Twitter e outras opções.</span><span class="sxs-lookup"><span data-stu-id="46d95-112">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="46d95-113">Desenvolvemos uma estratégia para o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="46d95-113">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="46d95-114">Neste artigo, mostramos como instalar o módulo e, em seguida, adicione o plug-in `passport-azure-ad` do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="46d95-114">In this article, we show you how to install the module, and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="46d95-115">Baixar</span><span class="sxs-lookup"><span data-stu-id="46d95-115">Download</span></span>
<span data-ttu-id="46d95-116">O código para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span><span class="sxs-lookup"><span data-stu-id="46d95-116">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span></span> <span data-ttu-id="46d95-117">Para seguir o tutorial, [baixe o esqueleto do aplicativo como um arquivo .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) ou clone o esqueleto:</span><span class="sxs-lookup"><span data-stu-id="46d95-117">To follow the tutorial, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="46d95-118">Também obtenha o aplicativo concluído ao final deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="46d95-118">You also can get the completed application at the end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="46d95-119">1: registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="46d95-119">1: Register an app</span></span>
<span data-ttu-id="46d95-120">Crie um novo aplicativo em [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ou siga [estas etapas detalhadas](active-directory-v2-app-registration.md) para registrar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46d95-120">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) to register an app.</span></span> <span data-ttu-id="46d95-121">Verifique se você:</span><span class="sxs-lookup"><span data-stu-id="46d95-121">Make sure you:</span></span>

* <span data-ttu-id="46d95-122">Copie a **ID do Aplicativo** atribuída ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46d95-122">Copy the **Application Id** assigned to your app.</span></span> <span data-ttu-id="46d95-123">Ele é necessário para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="46d95-123">You need it for this tutorial.</span></span>
* <span data-ttu-id="46d95-124">Adicionar a plataforma **Web** para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46d95-124">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="46d95-125">Copiar o **URI de redirecionamento** do portal.</span><span class="sxs-lookup"><span data-stu-id="46d95-125">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="46d95-126">Você deve usar o valor de URI padrão `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="46d95-126">You must use the default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-add-prerequisities-to-your-directory"></a><span data-ttu-id="46d95-127">2: Adicionar pré-requisitos ao diretório</span><span class="sxs-lookup"><span data-stu-id="46d95-127">2: Add prerequisities to your directory</span></span>
<span data-ttu-id="46d95-128">No prompt de comando, altere os diretórios para acessar a pasta raiz, caso você ainda não esteja nela.</span><span class="sxs-lookup"><span data-stu-id="46d95-128">At a command prompt, change directories to go to your root folder, if you are not already there.</span></span> <span data-ttu-id="46d95-129">Execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="46d95-129">Run the following commands:</span></span>

* `npm install express`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install restify`
* `npm install mongoose`
* `npm install bunyan`
* `npm install assert-plus`
* `npm install passport`
* `npm install webfinger`
* `npm install body-parser`
* `npm install express-session`
* `npm install cookie-parser`

<span data-ttu-id="46d95-130">Além disso, usamos `passport-azure-ad` no esqueleto do início rápido:</span><span class="sxs-lookup"><span data-stu-id="46d95-130">In addition, we use `passport-azure-ad` in the skeleton of the quickstart:</span></span>

* `npm install passport-azure-ad`

<span data-ttu-id="46d95-131">Isso instala as bibliotecas utilizadas pelo `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="46d95-131">This installs the libraries that `passport-azure-ad` uses.</span></span>

## <a name="3-set-up-your-app-to-use-the-passport-node-js-strategy"></a><span data-ttu-id="46d95-132">3: Configurar o aplicativo para usar a estratégia passport-node-js</span><span class="sxs-lookup"><span data-stu-id="46d95-132">3: Set up your app to use the passport-node-js strategy</span></span>
<span data-ttu-id="46d95-133">Configure o middleware Express para usar o protocolo de autenticação OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="46d95-133">Set up the Express middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="46d95-134">O Passport é usado para emitir solicitações de entrada e saída, gerenciar a sessão do usuário e obter informações sobre o usuário, entre outras coisas.</span><span class="sxs-lookup"><span data-stu-id="46d95-134">You use Passport to issue sign-in and sign-out requests, manage the user's session, and get information about the user, among other things.</span></span>

1.  <span data-ttu-id="46d95-135">Na raiz do projeto, abra o arquivo Config.js.</span><span class="sxs-lookup"><span data-stu-id="46d95-135">In the root of the project, open the Config.js file.</span></span> <span data-ttu-id="46d95-136">Na seção `exports.creds`, insira os valores de configuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="46d95-136">In the `exports.creds` section, enter your app's configuration values.</span></span>
  
  * <span data-ttu-id="46d95-137">`clientID`: a **ID do Aplicativo** atribuída ao aplicativo no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="46d95-137">`clientID`: The **Application Id** that's assigned to your app in the Azure portal.</span></span>
  * <span data-ttu-id="46d95-138">`returnURL`: o **URI de Redirecionamento** inserido no portal.</span><span class="sxs-lookup"><span data-stu-id="46d95-138">`returnURL`: The **Redirect URI** that you entered in the portal.</span></span>
  * <span data-ttu-id="46d95-139">`clientSecret`: o segredo gerado no portal.</span><span class="sxs-lookup"><span data-stu-id="46d95-139">`clientSecret`: The secret that you generated in the portal.</span></span>

2.  <span data-ttu-id="46d95-140">Na raiz do projeto, abra o arquivo App.js.</span><span class="sxs-lookup"><span data-stu-id="46d95-140">In the root of the project, open the App.js file.</span></span> <span data-ttu-id="46d95-141">Para invocar a estratégia OIDCStrategy, que acompanha o `passport-azure-ad`, adicione a seguinte chamada:</span><span class="sxs-lookup"><span data-stu-id="46d95-141">To invoke the OIDCStrategy stratey, which comes with `passport-azure-ad`, add the following call:</span></span>

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  <span data-ttu-id="46d95-142">Para manipular solicitações de conexão, use a estratégia que você acabou de referenciar:</span><span class="sxs-lookup"><span data-stu-id="46d95-142">To handle your sign-in requests, use the strategy you just referenced:</span></span>

  ```JavaScript
  // Use the OIDCStrategy within Passport (section 2)
  //
  //   Strategies in Passport require a `validate` function. The function accepts
  //   credentials (in this case, an OpenID identifier), and invokes a callback
  //   with a user object.
  passport.use( new OIDCStrategy({
      callbackURL: config.creds.returnURL,
      realm: config.creds.realm,
      clientID: config.creds.clientID,
      clientSecret: config.creds.clientSecret,
      oidcIssuer: config.creds.issuer,
      identityMetadata: config.creds.identityMetadata,
      responseType: config.creds.responseType,
      responseMode: config.creds.responseMode,
      skipUserProfile: config.creds.skipUserProfile
      scope: config.creds.scope
    },
    function(iss, sub, profile, accessToken, refreshToken, done) {
      log.info('Example: Email address we received was: ', profile.email);
      // Asynchronous verification, for effect...
      process.nextTick(function () {
        findByEmail(profile.email, function(err, user) {
          if (err) {
            return done(err);
          }
          if (!user) {
            // "Auto-registration"
            users.push(profile);
            return done(null, profile);
          }
          return done(null, user);
        });
      });
    }
  ));
  ```

<span data-ttu-id="46d95-143">O Passport usa um padrão semelhante para todas as suas estratégias (Twitter, Facebook e assim por diante).</span><span class="sxs-lookup"><span data-stu-id="46d95-143">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="46d95-144">Todos os gravadores de estratégia seguem o padrão.</span><span class="sxs-lookup"><span data-stu-id="46d95-144">All strategy writers adhere to the pattern.</span></span> <span data-ttu-id="46d95-145">Passe uma `function()` para a estratégia que usa um token e `done` como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="46d95-145">Pass the strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="46d95-146">A estratégia é retornada depois de fazer todo o seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="46d95-146">The strategy is returned after it does all its work.</span></span> <span data-ttu-id="46d95-147">Armazene o usuário e guarde o token para que você não precise solicitá-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="46d95-147">Store the user and stash the token so you don’t need to ask for it again.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="46d95-148">O código anterior usa qualquer usuário que pode se autenticar no servidor.</span><span class="sxs-lookup"><span data-stu-id="46d95-148">The preceding code takes any user that can authenticate to your server.</span></span> <span data-ttu-id="46d95-149">Isso é conhecido como registro automático.</span><span class="sxs-lookup"><span data-stu-id="46d95-149">This is known as auto-registration.</span></span> <span data-ttu-id="46d95-150">Em um servidor de produção, você não desejará permitir que nenhuma pessoa entre sem primeiro passar por um processo de registro escolhido por você.</span><span class="sxs-lookup"><span data-stu-id="46d95-150">On a production server, you wouldn’t want to let anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="46d95-151">Geralmente, esse é o padrão visto em aplicativos de consumidor.</span><span class="sxs-lookup"><span data-stu-id="46d95-151">This is usually the pattern that you see in consumer apps.</span></span> <span data-ttu-id="46d95-152">O aplicativo pode permitir que você se registre com o Facebook, mas, em seguida, solicita que você insira informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="46d95-152">The app might allow you to register with Facebook, but then it asks you to enter additional information.</span></span> <span data-ttu-id="46d95-153">Se você não estava usando um programa de linha de comando para este tutorial, você poderá extrair o email do objeto de token que é retornado.</span><span class="sxs-lookup"><span data-stu-id="46d95-153">If you weren't using a command-line program for this tutorial, you could extract the email from the token object that is returned.</span></span> <span data-ttu-id="46d95-154">Em seguida, você poderá solicitar ao usuário que insira informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="46d95-154">Then, you might ask the user to enter additional information.</span></span> <span data-ttu-id="46d95-155">Como esse é um servidor de teste, você adiciona o usuário diretamente ao banco de dados na memória.</span><span class="sxs-lookup"><span data-stu-id="46d95-155">Because this is a test server, you add the user directly to the in-memory database.</span></span>
  > 
  > 

4.  <span data-ttu-id="46d95-156">Adicione os métodos usados para acompanhar os usuários que estão conectados, conforme solicitado pelo Passport.</span><span class="sxs-lookup"><span data-stu-id="46d95-156">Add the methods that you use to keep track of users who are signed in, as required by Passport.</span></span> <span data-ttu-id="46d95-157">Isso inclui a serialização e a desserialização de informações do usuário:</span><span class="sxs-lookup"><span data-stu-id="46d95-157">This includes serializing and deserializing the user's information:</span></span>

  ```JavaScript

  // Passport session setup (section 2)

  //   To support persistent login sessions, Passport needs to be able to
  //   serialize users into, and deserialize users out of, the session. Typically,
  //   this is as simple as storing the user ID when serializing, and finding
  //   the user by ID when deserializing.
  passport.serializeUser(function(user, done) {
    done(null, user.email);
  });

  passport.deserializeUser(function(id, done) {
    findByEmail(id, function (err, user) {
      done(err, user);
    });
  });

  // Array to hold signed-in users
  var users = [];

  var findByEmail = function(email, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
      var user = users[i];
      log.info('we are using user: ', user);
      if (user.email === email) {
        return fn(null, user);
      }
    }
    return fn(null, null);
  };
  ```

5.  <span data-ttu-id="46d95-158">Adicione o código que carrega o mecanismo Express.</span><span class="sxs-lookup"><span data-stu-id="46d95-158">Add the code that loads the Express engine.</span></span> <span data-ttu-id="46d95-159">Use o padrão /views e /routes fornecido pelo Express:</span><span class="sxs-lookup"><span data-stu-id="46d95-159">You use the default /views and /routes pattern that Express provides:</span></span>

  ```JavaScript

  // Set up Express (section 2)

  var app = express();

  app.configure(function() {
    app.set('views', __dirname + '/views');
    app.set('view engine', 'ejs');
    app.use(express.logger());
    app.use(express.methodOverride());
    app.use(cookieParser());
    app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
    app.use(bodyParser.urlencoded({ extended : true }));
    // Initialize Passport!  Also use passport.session() middleware, to support
    // persistent login sessions (recommended).
    app.use(passport.initialize());
    app.use(passport.session());
    app.use(app.router);
    app.use(express.static(__dirname + '/../../public'));
  });

  ```

6.  <span data-ttu-id="46d95-160">Adicione as rotas POST que entregam as solicitações de conexão reais ao mecanismo `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="46d95-160">Add the POST routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>

  ```JavaScript

  // Auth routes (section 3)

  // GET /auth/openid
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. The first step in OpenID authentication involves redirecting
  //   the user to the user's OpenID provider. After authenticating, the OpenID
  //   provider redirects the user back to this application at
  //   /auth/openid/return.

  app.get('/auth/openid',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Authentication was called in the sample');
      res.redirect('/');
    });

  // GET /auth/openid/return
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. If authentication fails, the user is redirected back to the
  //   sign-in page. Otherwise, the primary route function is called.
  //   In this example, it redirects the user to the home page.
  app.get('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });

  // POST /auth/openid/return
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. If authentication fails, the user is redirected back to the
  //   sign-in page. Otherwise, the primary route function is called. 
  //   In this example, it redirects the user to the home page.

  app.post('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });
  ```

## <a name="4-use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="46d95-161">4: Usar o Passport para emitir solicitações de entrada e saída ao Azure AD</span><span class="sxs-lookup"><span data-stu-id="46d95-161">4: Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="46d95-162">Seu aplicativo agora está configurado para se comunicar com o ponto de extremidade v2.0 usando o protocolo de autenticação OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="46d95-162">Your app is now set up to communicate with the v2.0 endpoint by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="46d95-163">A estratégia `passport-azure-ad` cuida de todos os detalhes da criação de mensagens de autenticação, validação de tokens do Azure AD e manutenção da sessão do usuário.</span><span class="sxs-lookup"><span data-stu-id="46d95-163">The `passport-azure-ad` strategy takes care of all the details of crafting authentication messages, validating tokens from Azure AD, and maintaining the user session.</span></span> <span data-ttu-id="46d95-164">Tudo o que resta a fazer é fornecer aos usuários uma maneira de entrar e sair do serviço e coletar mais informações sobre o usuário que está conectado.</span><span class="sxs-lookup"><span data-stu-id="46d95-164">All that is left to do is to give your users a way to sign in and sign out, and to gather more information about the user who is signed in.</span></span>

1.  <span data-ttu-id="46d95-165">Adicione os métodos **default**, **login**, **account** e **logout** ao arquivo App.js:</span><span class="sxs-lookup"><span data-stu-id="46d95-165">Add the **default**, **login**, **account**, and **logout** methods to your App.js file:</span></span>

  ```JavaScript

  //Routes (section 4)

  app.get('/', function(req, res){
    res.render('index', { user: req.user });
  });

  app.get('/account', ensureAuthenticated, function(req, res){
    res.render('account', { user: req.user });
  });

  app.get('/login',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Login was called in the sample');
      res.redirect('/');
  });

  app.get('/logout', function(req, res){
    req.logout();
    res.redirect('/');
  });

  ```

  <span data-ttu-id="46d95-166">Estes são os detalhes:</span><span class="sxs-lookup"><span data-stu-id="46d95-166">Here are the details:</span></span>
    
    * <span data-ttu-id="46d95-167">A rota `/` redireciona para a exibição index.ejs.</span><span class="sxs-lookup"><span data-stu-id="46d95-167">The `/` route redirects to the index.ejs view.</span></span> <span data-ttu-id="46d95-168">Ela passa o usuário na solicitação (se houver).</span><span class="sxs-lookup"><span data-stu-id="46d95-168">It passes the user in the request (if it exists).</span></span>
    * <span data-ttu-id="46d95-169">A rota `/account` primeiro *garante que você está autenticado* (você implementa isso no código a seguir).</span><span class="sxs-lookup"><span data-stu-id="46d95-169">The `/account` route first *ensures that you are authenticated* (you implement that in the following code).</span></span> <span data-ttu-id="46d95-170">Em seguida, ela passa o usuário na solicitação.</span><span class="sxs-lookup"><span data-stu-id="46d95-170">Then, it passes the user in the request.</span></span> <span data-ttu-id="46d95-171">Isso serve para obter mais informações sobre o usuário.</span><span class="sxs-lookup"><span data-stu-id="46d95-171">This is so you can get more information about the user.</span></span>
    * <span data-ttu-id="46d95-172">A rota `/login` chama o autenticador `azuread-openidconnect` por meio de `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="46d95-172">The `/login` route calls your `azuread-openidconnect` authenticator from `passport-azuread`.</span></span> <span data-ttu-id="46d95-173">Caso não obtenha êxito, ele redirecionará o usuário novamente para `/login`.</span><span class="sxs-lookup"><span data-stu-id="46d95-173">If that doesn't succeed, it redirects the user back to `/login`.</span></span>
    * <span data-ttu-id="46d95-174">A rota `/logout` chama a exibição logout.ejs (e a rota).</span><span class="sxs-lookup"><span data-stu-id="46d95-174">The `/logout` route calls the logout.ejs view (and route).</span></span> <span data-ttu-id="46d95-175">Isso limpa os cookies e, em seguida, retorna o usuário para index.ejs.</span><span class="sxs-lookup"><span data-stu-id="46d95-175">This clears cookies, and then returns the user back to index.ejs.</span></span>

2.  <span data-ttu-id="46d95-176">Adicione o método **EnsureAuthenticated** que você usou anteriormente em `/account`:</span><span class="sxs-lookup"><span data-stu-id="46d95-176">Add the **EnsureAuthenticated** method that you used earlier in `/account`:</span></span>

  ```JavaScript

  // Route middleware to ensure the user is authenticated (section 4)

  //   Use this route middleware on any resource that needs to be protected. If
  //   the request is authenticated (typically via a persistent login session),
  //   the request proceeds. Otherwise, the user is redirected to the
  //   sign-in page.
  function ensureAuthenticated(req, res, next) {
    if (req.isAuthenticated()) { return next(); }
    res.redirect('/login')
  }

  ```

3.  <span data-ttu-id="46d95-177">No App.js, crie o servidor:</span><span class="sxs-lookup"><span data-stu-id="46d95-177">In App.js, create the server:</span></span>

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-the-views-and-routes-in-express-that-you-show-your-user-on-the-website"></a><span data-ttu-id="46d95-178">5: Criar as exibições e rotas no Express que são mostradas ao usuário no site</span><span class="sxs-lookup"><span data-stu-id="46d95-178">5: Create the views and routes in Express that you show your user on the website</span></span>
<span data-ttu-id="46d95-179">Adicione as rotas e exibições que mostram informações ao usuário.</span><span class="sxs-lookup"><span data-stu-id="46d95-179">Add the routes and views that show information to the user.</span></span> <span data-ttu-id="46d95-180">As rotas e exibições também manipulam as rotas `/logout` e `/login` que você criou.</span><span class="sxs-lookup"><span data-stu-id="46d95-180">The routes and views also handle the `/logout` and `/login` routes that you created.</span></span>

1. <span data-ttu-id="46d95-181">No diretório raiz, crie a rota `/routes/index.js`.</span><span class="sxs-lookup"><span data-stu-id="46d95-181">In the root directory, create the `/routes/index.js` route.</span></span>

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  <span data-ttu-id="46d95-182">No diretório raiz, crie a rota `/routes/user.js`.</span><span class="sxs-lookup"><span data-stu-id="46d95-182">In the root directory, create the `/routes/user.js` route.</span></span>

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  <span data-ttu-id="46d95-183">`/routes/index.js` e `/routes/user.js` são rotas simples que passam a solicitação para as exibições, incluindo o usuário, se ele estiver presente.</span><span class="sxs-lookup"><span data-stu-id="46d95-183">`/routes/index.js` and `/routes/user.js` are simple routes that pass along the request to your views, including the user, if present.</span></span>

3.  <span data-ttu-id="46d95-184">No diretório raiz, crie a exibição `/views/index.ejs`.</span><span class="sxs-lookup"><span data-stu-id="46d95-184">In the root directory, create the `/views/index.ejs` view.</span></span> <span data-ttu-id="46d95-185">Essa página chama os métodos **login** e **logout**.</span><span class="sxs-lookup"><span data-stu-id="46d95-185">This page calls your **login** and **logout** methods.</span></span> <span data-ttu-id="46d95-186">Você também usa a exibição `/views/index.ejs` para capturar informações de conta.</span><span class="sxs-lookup"><span data-stu-id="46d95-186">You also use the `/views/index.ejs` view to capture account information.</span></span> <span data-ttu-id="46d95-187">Use o `if (!user)` condicional como o usuário que está sendo passado na solicitação.</span><span class="sxs-lookup"><span data-stu-id="46d95-187">You can use the conditional `if (!user)` as the user being passed through in the request.</span></span> <span data-ttu-id="46d95-188">Ele é uma prova de que você tem um usuário conectado.</span><span class="sxs-lookup"><span data-stu-id="46d95-188">It is evidence that you have a user signed in.</span></span>

  ```JavaScript
  <% if (!user) { %>
      <h2>Welcome! Please sign in.</h2>
      <a href="/login">Sign in</a>
  <% } else { %>
      <h2>Hello, <%= user.displayName %>.</h2>
      <a href="/account">Account info</a></br>
      <a href="/logout">Sign out</a>
  <% } %>
  ```

4.  <span data-ttu-id="46d95-189">No diretório raiz, crie a exibição `/views/account.ejs`.</span><span class="sxs-lookup"><span data-stu-id="46d95-189">In the root directory, create the `/views/account.ejs` view.</span></span> <span data-ttu-id="46d95-190">A exibição `/views/account.ejs` permite exibir informações adicionais colocadas pelo `passport-azuread` na solicitação de usuário.</span><span class="sxs-lookup"><span data-stu-id="46d95-190">The `/views/account.ejs` view allows you to view additional information that `passport-azuread` puts in the user request.</span></span>

  ```Javascript
  <% if (!user) { %>
      <h2>Welcome! Please sign in.</h2>
      <a href="/login">Sign in</a>
  <% } else { %>
  <p>displayName: <%= user.displayName %></p>
  <p>givenName: <%= user.name.givenName %></p>
  <p>familyName: <%= user.name.familyName %></p>
  <p>UPN: <%= user._json.upn %></p>
  <p>Profile ID: <%= user.id %></p>
  <p>Full Claimes</p>
  <%- JSON.stringify(user) %>
  <p></p>
  <a href="/logout">Sign out</a>
  <% } %>
  ```

5.  <span data-ttu-id="46d95-191">Adicione um layout.</span><span class="sxs-lookup"><span data-stu-id="46d95-191">Add a layout.</span></span> <span data-ttu-id="46d95-192">No diretório raiz, crie a exibição `/views/layout.ejs`.</span><span class="sxs-lookup"><span data-stu-id="46d95-192">In the root directory, create the `/views/layout.ejs` view.</span></span>

  ```HTML

  <!DOCTYPE html>
  <html>
      <head>
          <title>Passport-OpenID Example</title>
      </head>
      <body>
          <% if (!user) { %>
              <p>
              <a href="/">Home</a> |
              <a href="/login">Sign in</a>
              </p>
          <% } else { %>
              <p>
              <a href="/">Home</a> |
              <a href="/account">Account</a> |
              <a href="/logout">Sign out</a>
              </p>
          <% } %>
          <%- body %>
      </body>
  </html>
  ```

6.  <span data-ttu-id="46d95-193">Para compilar e executar seu aplicativo, execute `node app.js`.</span><span class="sxs-lookup"><span data-stu-id="46d95-193">To build and run your app, run `node app.js`.</span></span> <span data-ttu-id="46d95-194">Em seguida, acesse `http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="46d95-194">Then, go to `http://localhost:3000`.</span></span>

7.  <span data-ttu-id="46d95-195">Entre com uma conta pessoal da Microsoft ou uma conta corporativa ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="46d95-195">Sign in with either a personal Microsoft account or a work or school account.</span></span> <span data-ttu-id="46d95-196">Observe que a identidade do usuário é refletida na lista /account.</span><span class="sxs-lookup"><span data-stu-id="46d95-196">Note that the user's identity is reflected in the /account list.</span></span> 

<span data-ttu-id="46d95-197">Agora você tem um aplicativo Web que é protegido com o uso de protocolos padrão do setor.</span><span class="sxs-lookup"><span data-stu-id="46d95-197">You now have a web app that is secured by using industry standard protocols.</span></span> <span data-ttu-id="46d95-198">Você pode autenticar os usuários em seu aplicativo usando as contas pessoais e corporativas ou de estudante deles.</span><span class="sxs-lookup"><span data-stu-id="46d95-198">You can authenticate users in your app by using their personal and work or school accounts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46d95-199">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="46d95-199">Next steps</span></span>
<span data-ttu-id="46d95-200">Para referência, o exemplo completo (sem seus valores de configuração) é [fornecido como um arquivo .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="46d95-200">For reference, the completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="46d95-201">Você também pode cloná-la no GitHub:</span><span class="sxs-lookup"><span data-stu-id="46d95-201">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="46d95-202">A seguir, você pode passar para tópicos mais avançados.</span><span class="sxs-lookup"><span data-stu-id="46d95-202">Next, you can move on to more advanced topics.</span></span> <span data-ttu-id="46d95-203">Você pode desejar experimentar:</span><span class="sxs-lookup"><span data-stu-id="46d95-203">You might want to try:</span></span>

[<span data-ttu-id="46d95-204">Proteger uma API Web do Node.js usando o ponto de extremidade v2.0</span><span class="sxs-lookup"><span data-stu-id="46d95-204">Secure a Node.js web API by using the v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-node-api.md)

<span data-ttu-id="46d95-205">Estes são alguns recursos adicionais:</span><span class="sxs-lookup"><span data-stu-id="46d95-205">Here are some additional resources:</span></span>

* [<span data-ttu-id="46d95-206">Guia do desenvolvedor do Azure AD v2.0</span><span class="sxs-lookup"><span data-stu-id="46d95-206">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="46d95-207">Marcação “azure-active-directory” do Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="46d95-207">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="46d95-208">Obter atualizações de segurança para nossos produtos</span><span class="sxs-lookup"><span data-stu-id="46d95-208">Get security updates for our products</span></span>
<span data-ttu-id="46d95-209">Incentivamos você a se inscrever para receber notificações quando ocorrerem incidentes de segurança.</span><span class="sxs-lookup"><span data-stu-id="46d95-209">We encourage you to sign up to be notified when security incidents occur.</span></span> <span data-ttu-id="46d95-210">Na página [Notificações de Segurança Técnica da Microsoft](https://technet.microsoft.com/security/dd252948), assine Alertas de Avisos de Segurança.</span><span class="sxs-lookup"><span data-stu-id="46d95-210">On the [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe to Security Advisories Alerts.</span></span>

