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
# <a name="add-sign-in-tooa-nodejs-web-app"></a>Adicionar entrada tooa Node. js web app

> [!NOTE]
> Nem todos os recursos e cenários de Active Directory do Azure funcionam com o ponto de extremidade do hello v 2.0. toodetermine se você deve usar o ponto de extremidade do hello v 2.0 ou ponto de extremidade Olá v 1.0, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).
> 

Neste tutorial, usamos a saudação do Passport toodo tarefas a seguir:

* Em um aplicativo web, entre no usuário hello usando o Azure Active Directory (AD do Azure) e Olá v 2.0 de ponto de extremidade.
* Exibir informações sobre o usuário hello.
* Entrada hello usuário fora do aplicativo hello.

**Passport** é middleware de autenticação para o Node.js. Flexível e modular, o Passport pode ser colocado sem impedimento em qualquer aplicativo Web baseado em Express ou Restify. No Passport, um conjunto abrangente de estratégias dão suporte à autenticação com o uso de um nome de usuário e uma senha, Facebook, Twitter e outras opções. Desenvolvemos uma estratégia para o Azure AD. Neste artigo, mostramos como tooinstall Olá módulo e, em seguida, adicionar Olá AD do Azure `passport-azure-ad` plug-in.

## <a name="download"></a>Baixar
código de saudação para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs). tutorial de saudação toofollow, você pode [baixar esqueleto de saudação do aplicativo como um arquivo. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) ou esqueleto de saudação do clone:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

Você também pode obter aplicativo hello concluída final Olá deste tutorial.

## <a name="1-register-an-app"></a>1: registrar um aplicativo
Criar um novo aplicativo no [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou execute [essas etapas detalhadas](active-directory-v2-app-registration.md) tooregister um aplicativo. Verifique se você:

* Saudação de cópia **Id do aplicativo** atribuído tooyour aplicativo. Ele é necessário para este tutorial.
* Adicionar Olá **Web** plataforma para seu aplicativo.
* Saudação de cópia **URI de redirecionamento** do portal de saudação. Você deve usar o valor do URI de padrão de saudação `urn:ietf:wg:oauth:2.0:oob`.

## <a name="2-add-prerequisities-tooyour-directory"></a>2: Adicionar pré-requisitos tooyour diretório
Em um prompt de comando, altere a pasta raiz do diretórios toogo tooyour, se você não ainda estiver lá. Execute Olá comandos a seguir:

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

Além disso, podemos usar `passport-azure-ad` no esqueleto de saudação do hello quickstart:

* `npm install passport-azure-ad`

Isso instala bibliotecas Olá que `passport-azure-ad` usa.

## <a name="3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a>3: definir sua estratégia do aplicativo toouse Olá passport-nó-js
Configure Olá Express middleware toouse Olá protocolo de autenticação OpenID Connect. Usar Passport tooissue solicitações de entrada e saídas, gerenciar a sessão do usuário hello e obter informações sobre o usuário hello, entre outras coisas.

1.  Na raiz de saudação do projeto hello, abra o arquivo de Config.js de saudação. Em Olá `exports.creds` seção, insira os valores de configuração do aplicativo.
  
  * `clientID`: Olá **Id do aplicativo** que é atribuído tooyour aplicativo hello portal do Azure.
  * `returnURL`: Olá **URI de redirecionamento** que você inseriu no portal de saudação.
  * `clientSecret`: segredo Olá geradas no portal de saudação.

2.  Na raiz de saudação do projeto hello, abra o arquivo de App.js de saudação. tooinvoke Olá OIDCStrategy stratey, que vem com `passport-azure-ad`, adicionar Olá chamada a seguir:

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  toohandle suas solicitações de entrada, use a estratégia Olá apenas referenciado:

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

O Passport usa um padrão semelhante para todas as suas estratégias (Twitter, Facebook e assim por diante). Todos os gravadores de estratégia aderem toohello padrão. Passe a estratégia de saudação um `function()` que usa um token e `done` como parâmetros. estratégia de saudação é retornada depois que ele faz seu trabalho. Usuário de saudação do repositório e token de saudação stash para que você não precise tooask para ele novamente.

  > [!IMPORTANT]
  > Olá código anterior usa qualquer usuário que pode autenticar o servidor de tooyour. Isso é conhecido como registro automático. Em um servidor de produção, você não quer toolet qualquer pessoa sem ter que primeiro eles passam por um processo de registro que você escolher. Normalmente, este é o padrão de saudação que você vê em aplicativos de consumidor. aplicativo Hello pode permitir tooregister com o Facebook, mas, em seguida, ele solicitará que você tooenter obter informações adicionais. Se não houver um programa de linha de comando para este tutorial, é possível extrair o email de saudação do objeto de token de saudação que é retornado. Em seguida, você pode solicitar informações adicionais do hello usuário tooenter. Como esse é um servidor de teste, você adicionar usuário Olá diretamente toohello memória no banco de dados.
  > 
  > 

4.  Adicionar métodos de saudação que você use o controle tookeep de usuários que estão conectados, conforme solicitado pelo Passport. Isso inclui a serialização e desserialização de informações de saudação do usuário:

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

5.  Adicione código de saudação que carrega o mecanismo do hello Express. Usar saudação padrão /views e padrão de /routes Express fornece:

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

6.  Adicionar Olá POST roteia mão off Olá solicitações de entrada real toohello `passport-azure-ad` mecanismo:

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

## <a name="4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>4: usar Passport tooissue entrada e saída solicitações tooAzure AD
Seu aplicativo agora está configurado para toocommunicate com o ponto de extremidade do hello v 2.0 usando o protocolo de autenticação OpenID Connect hello. Olá `passport-azure-ad` estratégia cuida de todos os detalhes de saudação de criação de mensagens de autenticação, validando tokens do AD do Azure e manter a sessão de usuário de saudação. Tudo que resta toodo é toogive seus usuários uma maneira toosign em e entre out e toogather para obter mais informações sobre o usuário Olá conectado.

1.  Adicionar Olá **padrão**, **login**, **conta**, e **logout** métodos tooyour App.js arquivo:

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

  Aqui estão os detalhes de saudação:
    
    * Olá `/` toohello index.ejs exibição redireciona a rota. Ele passa usuário Olá na solicitação de saudação (se houver).
    * Olá `/account` rotear primeiro *garante que sejam autenticados* (para implementar que em Olá código a seguir). Em seguida, ele passa usuário Olá na solicitação de saudação. Isso é para obter mais informações sobre o usuário de saudação.
    * Olá `/login` rotear chamadas seu `azuread-openidconnect` autenticador de `passport-azuread`. Se que não for bem-sucedida, ele redireciona ao usuário Olá muito`/login`.
    * Olá `/logout` rota chama logout.ejs exibição hello (e rota). Isso limpará os cookies e, em seguida, retorna Olá tooindex.ejs voltar do usuário.

2.  Adicionar Olá **EnsureAuthenticated** método que você usou anteriormente na `/account`:

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

3.  Em App.js, crie servidor de saudação:

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-hello-views-and-routes-in-express-that-you-show-your-user-on-hello-website"></a>5: criar exibições de saudação e rotas em que mostra o usuário no site de saudação do Express
Adicione rotas hello e modos de exibição que mostram informações toohello usuário. rotas Hello e modos de exibição também trata Olá `/logout` e `/login` rotas que você criou.

1. No diretório raiz de hello, criar hello `/routes/index.js` rota.

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  No diretório raiz de hello, criar hello `/routes/user.js` rota.

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  `/routes/index.js`e `/routes/user.js` rotas simples que passa Olá solicitação tooyour modos de exibição, incluindo o usuário hello, se presente.

3.  No diretório raiz de hello, criar hello `/views/index.ejs` exibição. Essa página chama os métodos **login** e **logout**. Você também usar Olá `/views/index.ejs` exibir toocapture informações da conta. Você pode usar o hello condicional `if (!user)` como usuário hello está sendo passado na solicitação de saudação. Ele é uma prova de que você tem um usuário conectado.

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

4.  No diretório raiz de hello, criar hello `/views/account.ejs` exibição. Olá `/views/account.ejs` exibição permite a você informações adicionais de tooview que `passport-azuread` coloca na solicitação de saudação do usuário.

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

5.  Adicione um layout. No diretório raiz de hello, criar hello `/views/layout.ejs` exibição.

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

6.  toobuild e executar seu aplicativo, executar `node app.js`. Em seguida, ir muito`http://localhost:3000`.

7.  Entre com uma conta pessoal da Microsoft ou uma conta corporativa ou de estudante. Observe que Olá a identidade de usuário é refletida na lista de conta hello. 

Agora você tem um aplicativo Web que é protegido com o uso de protocolos padrão do setor. Você pode autenticar os usuários em seu aplicativo usando as contas pessoais e corporativas ou de estudante deles.

## <a name="next-steps"></a>Próximas etapas
Para referência, o exemplo hello concluída (sem os valores de configuração) é fornecido como [um arquivo. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip). Você também pode cloná-la no GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

Em seguida, você pode mover toomore tópicos avançados. Você pode desejar tootry:

[Proteger uma API da web Node. js usando o ponto de extremidade do hello v 2.0](active-directory-v2-devquickstarts-node-api.md)

Estes são alguns recursos adicionais:

* [Guia do desenvolvedor do Azure AD v2.0](active-directory-appmodel-v2-overview.md)
* [Marcação “azure-active-directory” do Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a>Obter atualizações de segurança para nossos produtos
Recomendamos que você toosign backup toobe notificado quando ocorrerem incidentes de segurança. Em Olá [notificações de segurança técnica da Microsoft](https://technet.microsoft.com/security/dd252948) página, assinar tooSecurity comunicados de alertas.

