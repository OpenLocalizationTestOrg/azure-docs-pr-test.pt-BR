---
title: v 2.0 do Active Directory de aaaAzure Node. js web aplicativo entrar | Microsoft Docs
description: "Saiba como toobuild um Node. js web aplicativo entra em um usuário usando uma conta pessoal da Microsoft e uma conta corporativa ou escolar."
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
ms.openlocfilehash: f8ce6e2b841c215cb14e82bcf444fe849634cc88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-nodejs-web-app"></a><span data-ttu-id="20554-103">Adicionar entrada tooa Node. js web app</span><span class="sxs-lookup"><span data-stu-id="20554-103">Add sign-in tooa Node.js web app</span></span>

> [!NOTE]
> <span data-ttu-id="20554-104">Nem todos os recursos e cenários de Active Directory do Azure funcionam com o ponto de extremidade do hello v 2.0.</span><span class="sxs-lookup"><span data-stu-id="20554-104">Not all Azure Active Directory scenarios and features work with hello v2.0 endpoint.</span></span> <span data-ttu-id="20554-105">toodetermine se você deve usar o ponto de extremidade do hello v 2.0 ou ponto de extremidade Olá v 1.0, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="20554-105">toodetermine whether you should use hello v2.0 endpoint or hello v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 

<span data-ttu-id="20554-106">Neste tutorial, usamos a saudação do Passport toodo tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="20554-106">In this tutorial, we use Passport toodo hello following tasks:</span></span>

* <span data-ttu-id="20554-107">Em um aplicativo web, entre no usuário hello usando o Azure Active Directory (AD do Azure) e Olá v 2.0 de ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="20554-107">In a web app, sign in hello user by using Azure Active Directory (Azure AD) and hello v2.0 endpoint.</span></span>
* <span data-ttu-id="20554-108">Exibir informações sobre o usuário hello.</span><span class="sxs-lookup"><span data-stu-id="20554-108">Display information about hello user.</span></span>
* <span data-ttu-id="20554-109">Entrada hello usuário fora do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="20554-109">Sign hello user out of hello app.</span></span>

<span data-ttu-id="20554-110">**Passport** é middleware de autenticação para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="20554-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="20554-111">Flexível e modular, o Passport pode ser colocado sem impedimento em qualquer aplicativo Web baseado em Express ou Restify.</span><span class="sxs-lookup"><span data-stu-id="20554-111">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="20554-112">No Passport, um conjunto abrangente de estratégias dão suporte à autenticação com o uso de um nome de usuário e uma senha, Facebook, Twitter e outras opções.</span><span class="sxs-lookup"><span data-stu-id="20554-112">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="20554-113">Desenvolvemos uma estratégia para o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="20554-113">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="20554-114">Neste artigo, mostramos como tooinstall Olá módulo e, em seguida, adicionar Olá AD do Azure `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="20554-114">In this article, we show you how tooinstall hello module, and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="20554-115">Baixar</span><span class="sxs-lookup"><span data-stu-id="20554-115">Download</span></span>
<span data-ttu-id="20554-116">código de saudação para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span><span class="sxs-lookup"><span data-stu-id="20554-116">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span></span> <span data-ttu-id="20554-117">tutorial de saudação toofollow, você pode [baixar esqueleto de saudação do aplicativo como um arquivo. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) ou esqueleto de saudação do clone:</span><span class="sxs-lookup"><span data-stu-id="20554-117">toofollow hello tutorial, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="20554-118">Você também pode obter aplicativo hello concluída final Olá deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="20554-118">You also can get hello completed application at hello end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="20554-119">1: registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="20554-119">1: Register an app</span></span>
<span data-ttu-id="20554-120">Criar um novo aplicativo no [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou execute [essas etapas detalhadas](active-directory-v2-app-registration.md) tooregister um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="20554-120">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) tooregister an app.</span></span> <span data-ttu-id="20554-121">Verifique se você:</span><span class="sxs-lookup"><span data-stu-id="20554-121">Make sure you:</span></span>

* <span data-ttu-id="20554-122">Saudação de cópia **Id do aplicativo** atribuído tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="20554-122">Copy hello **Application Id** assigned tooyour app.</span></span> <span data-ttu-id="20554-123">Ele é necessário para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="20554-123">You need it for this tutorial.</span></span>
* <span data-ttu-id="20554-124">Adicionar Olá **Web** plataforma para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="20554-124">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="20554-125">Saudação de cópia **URI de redirecionamento** do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="20554-125">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="20554-126">Você deve usar o valor do URI de padrão de saudação `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="20554-126">You must use hello default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-add-prerequisities-tooyour-directory"></a><span data-ttu-id="20554-127">2: Adicionar pré-requisitos tooyour diretório</span><span class="sxs-lookup"><span data-stu-id="20554-127">2: Add prerequisities tooyour directory</span></span>
<span data-ttu-id="20554-128">Em um prompt de comando, altere a pasta raiz do diretórios toogo tooyour, se você não ainda estiver lá.</span><span class="sxs-lookup"><span data-stu-id="20554-128">At a command prompt, change directories toogo tooyour root folder, if you are not already there.</span></span> <span data-ttu-id="20554-129">Execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="20554-129">Run hello following commands:</span></span>

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

<span data-ttu-id="20554-130">Além disso, podemos usar `passport-azure-ad` no esqueleto de saudação do hello quickstart:</span><span class="sxs-lookup"><span data-stu-id="20554-130">In addition, we use `passport-azure-ad` in hello skeleton of hello quickstart:</span></span>

* `npm install passport-azure-ad`

<span data-ttu-id="20554-131">Isso instala bibliotecas Olá que `passport-azure-ad` usa.</span><span class="sxs-lookup"><span data-stu-id="20554-131">This installs hello libraries that `passport-azure-ad` uses.</span></span>

## <a name="3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a><span data-ttu-id="20554-132">3: definir sua estratégia do aplicativo toouse Olá passport-nó-js</span><span class="sxs-lookup"><span data-stu-id="20554-132">3: Set up your app toouse hello passport-node-js strategy</span></span>
<span data-ttu-id="20554-133">Configure Olá Express middleware toouse Olá protocolo de autenticação OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="20554-133">Set up hello Express middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="20554-134">Usar Passport tooissue solicitações de entrada e saídas, gerenciar a sessão do usuário hello e obter informações sobre o usuário hello, entre outras coisas.</span><span class="sxs-lookup"><span data-stu-id="20554-134">You use Passport tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, among other things.</span></span>

1.  <span data-ttu-id="20554-135">Na raiz de saudação do projeto hello, abra o arquivo de Config.js de saudação.</span><span class="sxs-lookup"><span data-stu-id="20554-135">In hello root of hello project, open hello Config.js file.</span></span> <span data-ttu-id="20554-136">Em Olá `exports.creds` seção, insira os valores de configuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="20554-136">In hello `exports.creds` section, enter your app's configuration values.</span></span>
  
  * <span data-ttu-id="20554-137">`clientID`: Olá **Id do aplicativo** que é atribuído tooyour aplicativo hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="20554-137">`clientID`: hello **Application Id** that's assigned tooyour app in hello Azure portal.</span></span>
  * <span data-ttu-id="20554-138">`returnURL`: Olá **URI de redirecionamento** que você inseriu no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="20554-138">`returnURL`: hello **Redirect URI** that you entered in hello portal.</span></span>
  * <span data-ttu-id="20554-139">`clientSecret`: segredo Olá geradas no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="20554-139">`clientSecret`: hello secret that you generated in hello portal.</span></span>

2.  <span data-ttu-id="20554-140">Na raiz de saudação do projeto hello, abra o arquivo de App.js de saudação.</span><span class="sxs-lookup"><span data-stu-id="20554-140">In hello root of hello project, open hello App.js file.</span></span> <span data-ttu-id="20554-141">tooinvoke Olá OIDCStrategy stratey, que vem com `passport-azure-ad`, adicionar Olá chamada a seguir:</span><span class="sxs-lookup"><span data-stu-id="20554-141">tooinvoke hello OIDCStrategy stratey, which comes with `passport-azure-ad`, add hello following call:</span></span>

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  <span data-ttu-id="20554-142">toohandle suas solicitações de entrada, use a estratégia Olá apenas referenciado:</span><span class="sxs-lookup"><span data-stu-id="20554-142">toohandle your sign-in requests, use hello strategy you just referenced:</span></span>

  ```JavaScript
  // Use hello OIDCStrategy within Passport (section 2)
  //
  //   Strategies in Passport require a `validate` function. hello function accepts
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

<span data-ttu-id="20554-143">O Passport usa um padrão semelhante para todas as suas estratégias (Twitter, Facebook e assim por diante).</span><span class="sxs-lookup"><span data-stu-id="20554-143">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="20554-144">Todos os gravadores de estratégia aderem toohello padrão.</span><span class="sxs-lookup"><span data-stu-id="20554-144">All strategy writers adhere toohello pattern.</span></span> <span data-ttu-id="20554-145">Passe a estratégia de saudação um `function()` que usa um token e `done` como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="20554-145">Pass hello strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="20554-146">estratégia de saudação é retornada depois que ele faz seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="20554-146">hello strategy is returned after it does all its work.</span></span> <span data-ttu-id="20554-147">Usuário de saudação do repositório e token de saudação stash para que você não precise tooask para ele novamente.</span><span class="sxs-lookup"><span data-stu-id="20554-147">Store hello user and stash hello token so you don’t need tooask for it again.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="20554-148">Olá código anterior usa qualquer usuário que pode autenticar o servidor de tooyour.</span><span class="sxs-lookup"><span data-stu-id="20554-148">hello preceding code takes any user that can authenticate tooyour server.</span></span> <span data-ttu-id="20554-149">Isso é conhecido como registro automático.</span><span class="sxs-lookup"><span data-stu-id="20554-149">This is known as auto-registration.</span></span> <span data-ttu-id="20554-150">Em um servidor de produção, você não quer toolet qualquer pessoa sem ter que primeiro eles passam por um processo de registro que você escolher.</span><span class="sxs-lookup"><span data-stu-id="20554-150">On a production server, you wouldn’t want toolet anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="20554-151">Normalmente, este é o padrão de saudação que você vê em aplicativos de consumidor.</span><span class="sxs-lookup"><span data-stu-id="20554-151">This is usually hello pattern that you see in consumer apps.</span></span> <span data-ttu-id="20554-152">aplicativo Hello pode permitir tooregister com o Facebook, mas, em seguida, ele solicitará que você tooenter obter informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="20554-152">hello app might allow you tooregister with Facebook, but then it asks you tooenter additional information.</span></span> <span data-ttu-id="20554-153">Se não houver um programa de linha de comando para este tutorial, é possível extrair o email de saudação do objeto de token de saudação que é retornado.</span><span class="sxs-lookup"><span data-stu-id="20554-153">If you weren't using a command-line program for this tutorial, you could extract hello email from hello token object that is returned.</span></span> <span data-ttu-id="20554-154">Em seguida, você pode solicitar informações adicionais do hello usuário tooenter.</span><span class="sxs-lookup"><span data-stu-id="20554-154">Then, you might ask hello user tooenter additional information.</span></span> <span data-ttu-id="20554-155">Como esse é um servidor de teste, você adicionar usuário Olá diretamente toohello memória no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="20554-155">Because this is a test server, you add hello user directly toohello in-memory database.</span></span>
  > 
  > 

4.  <span data-ttu-id="20554-156">Adicionar métodos de saudação que você use o controle tookeep de usuários que estão conectados, conforme solicitado pelo Passport.</span><span class="sxs-lookup"><span data-stu-id="20554-156">Add hello methods that you use tookeep track of users who are signed in, as required by Passport.</span></span> <span data-ttu-id="20554-157">Isso inclui a serialização e desserialização de informações de saudação do usuário:</span><span class="sxs-lookup"><span data-stu-id="20554-157">This includes serializing and deserializing hello user's information:</span></span>

  ```JavaScript

  // Passport session setup (section 2)

  //   toosupport persistent login sessions, Passport needs toobe able to
  //   serialize users into, and deserialize users out of, hello session. Typically,
  //   this is as simple as storing hello user ID when serializing, and finding
  //   hello user by ID when deserializing.
  passport.serializeUser(function(user, done) {
    done(null, user.email);
  });

  passport.deserializeUser(function(id, done) {
    findByEmail(id, function (err, user) {
      done(err, user);
    });
  });

  // Array toohold signed-in users
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

5.  <span data-ttu-id="20554-158">Adicione código de saudação que carrega o mecanismo do hello Express.</span><span class="sxs-lookup"><span data-stu-id="20554-158">Add hello code that loads hello Express engine.</span></span> <span data-ttu-id="20554-159">Usar saudação padrão /views e padrão de /routes Express fornece:</span><span class="sxs-lookup"><span data-stu-id="20554-159">You use hello default /views and /routes pattern that Express provides:</span></span>

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
    // Initialize Passport!  Also use passport.session() middleware, toosupport
    // persistent login sessions (recommended).
    app.use(passport.initialize());
    app.use(passport.session());
    app.use(app.router);
    app.use(express.static(__dirname + '/../../public'));
  });

  ```

6.  <span data-ttu-id="20554-160">Adicionar Olá POST roteia mão off Olá solicitações de entrada real toohello `passport-azure-ad` mecanismo:</span><span class="sxs-lookup"><span data-stu-id="20554-160">Add hello POST routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>

  ```JavaScript

  // Auth routes (section 3)

  // GET /auth/openid
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. hello first step in OpenID authentication involves redirecting
  //   hello user toohello user's OpenID provider. After authenticating, hello OpenID
  //   provider redirects hello user back toothis application at
  //   /auth/openid/return.

  app.get('/auth/openid',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Authentication was called in hello sample');
      res.redirect('/');
    });

  // GET /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called.
  //   In this example, it redirects hello user toohello home page.
  app.get('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });

  // POST /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called. 
  //   In this example, it redirects hello user toohello home page.

  app.post('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });
  ```

## <a name="4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="20554-161">4: usar Passport tooissue entrada e saída solicitações tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="20554-161">4: Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="20554-162">Seu aplicativo agora está configurado para toocommunicate com o ponto de extremidade do hello v 2.0 usando o protocolo de autenticação OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="20554-162">Your app is now set up toocommunicate with hello v2.0 endpoint by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="20554-163">Olá `passport-azure-ad` estratégia cuida de todos os detalhes de saudação de criação de mensagens de autenticação, validando tokens do AD do Azure e manter a sessão de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="20554-163">hello `passport-azure-ad` strategy takes care of all hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining hello user session.</span></span> <span data-ttu-id="20554-164">Tudo que resta toodo é toogive seus usuários uma maneira toosign em e entre out e toogather para obter mais informações sobre o usuário Olá conectado.</span><span class="sxs-lookup"><span data-stu-id="20554-164">All that is left toodo is toogive your users a way toosign in and sign out, and toogather more information about hello user who is signed in.</span></span>

1.  <span data-ttu-id="20554-165">Adicionar Olá **padrão**, **login**, **conta**, e **logout** métodos tooyour App.js arquivo:</span><span class="sxs-lookup"><span data-stu-id="20554-165">Add hello **default**, **login**, **account**, and **logout** methods tooyour App.js file:</span></span>

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
      log.info('Login was called in hello sample');
      res.redirect('/');
  });

  app.get('/logout', function(req, res){
    req.logout();
    res.redirect('/');
  });

  ```

  <span data-ttu-id="20554-166">Aqui estão os detalhes de saudação:</span><span class="sxs-lookup"><span data-stu-id="20554-166">Here are hello details:</span></span>
    
    * <span data-ttu-id="20554-167">Olá `/` toohello index.ejs exibição redireciona a rota.</span><span class="sxs-lookup"><span data-stu-id="20554-167">hello `/` route redirects toohello index.ejs view.</span></span> <span data-ttu-id="20554-168">Ele passa usuário Olá na solicitação de saudação (se houver).</span><span class="sxs-lookup"><span data-stu-id="20554-168">It passes hello user in hello request (if it exists).</span></span>
    * <span data-ttu-id="20554-169">Olá `/account` rotear primeiro *garante que sejam autenticados* (para implementar que em Olá código a seguir).</span><span class="sxs-lookup"><span data-stu-id="20554-169">hello `/account` route first *ensures that you are authenticated* (you implement that in hello following code).</span></span> <span data-ttu-id="20554-170">Em seguida, ele passa usuário Olá na solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="20554-170">Then, it passes hello user in hello request.</span></span> <span data-ttu-id="20554-171">Isso é para obter mais informações sobre o usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="20554-171">This is so you can get more information about hello user.</span></span>
    * <span data-ttu-id="20554-172">Olá `/login` rotear chamadas seu `azuread-openidconnect` autenticador de `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="20554-172">hello `/login` route calls your `azuread-openidconnect` authenticator from `passport-azuread`.</span></span> <span data-ttu-id="20554-173">Se que não for bem-sucedida, ele redireciona ao usuário Olá muito`/login`.</span><span class="sxs-lookup"><span data-stu-id="20554-173">If that doesn't succeed, it redirects hello user back too`/login`.</span></span>
    * <span data-ttu-id="20554-174">Olá `/logout` rota chama logout.ejs exibição hello (e rota).</span><span class="sxs-lookup"><span data-stu-id="20554-174">hello `/logout` route calls hello logout.ejs view (and route).</span></span> <span data-ttu-id="20554-175">Isso limpará os cookies e, em seguida, retorna Olá tooindex.ejs voltar do usuário.</span><span class="sxs-lookup"><span data-stu-id="20554-175">This clears cookies, and then returns hello user back tooindex.ejs.</span></span>

2.  <span data-ttu-id="20554-176">Adicionar Olá **EnsureAuthenticated** método que você usou anteriormente na `/account`:</span><span class="sxs-lookup"><span data-stu-id="20554-176">Add hello **EnsureAuthenticated** method that you used earlier in `/account`:</span></span>

  ```JavaScript

  // Route middleware tooensure hello user is authenticated (section 4)

  //   Use this route middleware on any resource that needs toobe protected. If
  //   hello request is authenticated (typically via a persistent login session),
  //   hello request proceeds. Otherwise, hello user is redirected toothe
  //   sign-in page.
  function ensureAuthenticated(req, res, next) {
    if (req.isAuthenticated()) { return next(); }
    res.redirect('/login')
  }

  ```

3.  <span data-ttu-id="20554-177">Em App.js, crie servidor de saudação:</span><span class="sxs-lookup"><span data-stu-id="20554-177">In App.js, create hello server:</span></span>

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-hello-views-and-routes-in-express-that-you-show-your-user-on-hello-website"></a><span data-ttu-id="20554-178">5: criar exibições de saudação e rotas em que mostra o usuário no site de saudação do Express</span><span class="sxs-lookup"><span data-stu-id="20554-178">5: Create hello views and routes in Express that you show your user on hello website</span></span>
<span data-ttu-id="20554-179">Adicione rotas hello e modos de exibição que mostram informações toohello usuário.</span><span class="sxs-lookup"><span data-stu-id="20554-179">Add hello routes and views that show information toohello user.</span></span> <span data-ttu-id="20554-180">rotas Hello e modos de exibição também trata Olá `/logout` e `/login` rotas que você criou.</span><span class="sxs-lookup"><span data-stu-id="20554-180">hello routes and views also handle hello `/logout` and `/login` routes that you created.</span></span>

1. <span data-ttu-id="20554-181">No diretório raiz de hello, criar hello `/routes/index.js` rota.</span><span class="sxs-lookup"><span data-stu-id="20554-181">In hello root directory, create hello `/routes/index.js` route.</span></span>

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  <span data-ttu-id="20554-182">No diretório raiz de hello, criar hello `/routes/user.js` rota.</span><span class="sxs-lookup"><span data-stu-id="20554-182">In hello root directory, create hello `/routes/user.js` route.</span></span>

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  <span data-ttu-id="20554-183">`/routes/index.js`e `/routes/user.js` rotas simples que passa Olá solicitação tooyour modos de exibição, incluindo o usuário hello, se presente.</span><span class="sxs-lookup"><span data-stu-id="20554-183">`/routes/index.js` and `/routes/user.js` are simple routes that pass along hello request tooyour views, including hello user, if present.</span></span>

3.  <span data-ttu-id="20554-184">No diretório raiz de hello, criar hello `/views/index.ejs` exibição.</span><span class="sxs-lookup"><span data-stu-id="20554-184">In hello root directory, create hello `/views/index.ejs` view.</span></span> <span data-ttu-id="20554-185">Essa página chama os métodos **login** e **logout**.</span><span class="sxs-lookup"><span data-stu-id="20554-185">This page calls your **login** and **logout** methods.</span></span> <span data-ttu-id="20554-186">Você também usar Olá `/views/index.ejs` exibir toocapture informações da conta.</span><span class="sxs-lookup"><span data-stu-id="20554-186">You also use hello `/views/index.ejs` view toocapture account information.</span></span> <span data-ttu-id="20554-187">Você pode usar o hello condicional `if (!user)` como usuário hello está sendo passado na solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="20554-187">You can use hello conditional `if (!user)` as hello user being passed through in hello request.</span></span> <span data-ttu-id="20554-188">Ele é uma prova de que você tem um usuário conectado.</span><span class="sxs-lookup"><span data-stu-id="20554-188">It is evidence that you have a user signed in.</span></span>

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

4.  <span data-ttu-id="20554-189">No diretório raiz de hello, criar hello `/views/account.ejs` exibição.</span><span class="sxs-lookup"><span data-stu-id="20554-189">In hello root directory, create hello `/views/account.ejs` view.</span></span> <span data-ttu-id="20554-190">Olá `/views/account.ejs` exibição permite a você informações adicionais de tooview que `passport-azuread` coloca na solicitação de saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="20554-190">hello `/views/account.ejs` view allows you tooview additional information that `passport-azuread` puts in hello user request.</span></span>

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

5.  <span data-ttu-id="20554-191">Adicione um layout.</span><span class="sxs-lookup"><span data-stu-id="20554-191">Add a layout.</span></span> <span data-ttu-id="20554-192">No diretório raiz de hello, criar hello `/views/layout.ejs` exibição.</span><span class="sxs-lookup"><span data-stu-id="20554-192">In hello root directory, create hello `/views/layout.ejs` view.</span></span>

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

6.  <span data-ttu-id="20554-193">toobuild e executar seu aplicativo, executar `node app.js`.</span><span class="sxs-lookup"><span data-stu-id="20554-193">toobuild and run your app, run `node app.js`.</span></span> <span data-ttu-id="20554-194">Em seguida, ir muito`http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="20554-194">Then, go too`http://localhost:3000`.</span></span>

7.  <span data-ttu-id="20554-195">Entre com uma conta pessoal da Microsoft ou uma conta corporativa ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="20554-195">Sign in with either a personal Microsoft account or a work or school account.</span></span> <span data-ttu-id="20554-196">Observe que Olá a identidade de usuário é refletida na lista de conta hello.</span><span class="sxs-lookup"><span data-stu-id="20554-196">Note that hello user's identity is reflected in hello /account list.</span></span> 

<span data-ttu-id="20554-197">Agora você tem um aplicativo Web que é protegido com o uso de protocolos padrão do setor.</span><span class="sxs-lookup"><span data-stu-id="20554-197">You now have a web app that is secured by using industry standard protocols.</span></span> <span data-ttu-id="20554-198">Você pode autenticar os usuários em seu aplicativo usando as contas pessoais e corporativas ou de estudante deles.</span><span class="sxs-lookup"><span data-stu-id="20554-198">You can authenticate users in your app by using their personal and work or school accounts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20554-199">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="20554-199">Next steps</span></span>
<span data-ttu-id="20554-200">Para referência, o exemplo hello concluída (sem os valores de configuração) é fornecido como [um arquivo. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="20554-200">For reference, hello completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="20554-201">Você também pode cloná-la no GitHub:</span><span class="sxs-lookup"><span data-stu-id="20554-201">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="20554-202">Em seguida, você pode mover toomore tópicos avançados.</span><span class="sxs-lookup"><span data-stu-id="20554-202">Next, you can move on toomore advanced topics.</span></span> <span data-ttu-id="20554-203">Você pode desejar tootry:</span><span class="sxs-lookup"><span data-stu-id="20554-203">You might want tootry:</span></span>

[<span data-ttu-id="20554-204">Proteger uma API da web Node. js usando o ponto de extremidade do hello v 2.0</span><span class="sxs-lookup"><span data-stu-id="20554-204">Secure a Node.js web API by using hello v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-node-api.md)

<span data-ttu-id="20554-205">Estes são alguns recursos adicionais:</span><span class="sxs-lookup"><span data-stu-id="20554-205">Here are some additional resources:</span></span>

* [<span data-ttu-id="20554-206">Guia do desenvolvedor do Azure AD v2.0</span><span class="sxs-lookup"><span data-stu-id="20554-206">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="20554-207">Marcação “azure-active-directory” do Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="20554-207">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="20554-208">Obter atualizações de segurança para nossos produtos</span><span class="sxs-lookup"><span data-stu-id="20554-208">Get security updates for our products</span></span>
<span data-ttu-id="20554-209">Recomendamos que você toosign backup toobe notificado quando ocorrerem incidentes de segurança.</span><span class="sxs-lookup"><span data-stu-id="20554-209">We encourage you toosign up toobe notified when security incidents occur.</span></span> <span data-ttu-id="20554-210">Em Olá [notificações de segurança técnica da Microsoft](https://technet.microsoft.com/security/dd252948) página, assinar tooSecurity comunicados de alertas.</span><span class="sxs-lookup"><span data-stu-id="20554-210">On hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe tooSecurity Advisories Alerts.</span></span>

