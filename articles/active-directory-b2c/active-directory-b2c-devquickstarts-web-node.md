---
title: aplicativo da web Node. js aaaAdd tooa entrar para B2C do Azure | Microsoft Docs
description: "Como toobuild um aplicativo da web Node. js que entra em usuários usando um locatário B2C."
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: db97f84a-1f24-447b-b6d2-0265c6896b27
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 03/10/2017
ms.author: xerners
ms.openlocfilehash: b4c334b1f7a0669df2d0864140603dc55bbb5408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-add-sign-in-tooa-nodejs-web-app"></a>B2C do Azure AD: Adicionar o aplicativo de web Node.js tooa entrar

**Passport** é middleware de autenticação para o Node.js. Extremamente flexível e modular, o Passport pode ser instalado sem impedimento em qualquer aplicativo Web baseado em Express ou Restify. Um conjunto abrangente de estratégias que dão suporte à autenticação usando um nome de usuário e uma senha, o Facebook, o Twitter e muito mais.

Desenvolvemos uma estratégia para o Azure AD (Active Directory do Azure). Você instalará esse módulo e, em seguida, adicionar Olá AD do Azure `passport-azure-ad` plug-in.

toodo isso, você precisa:

1. Registre um aplicativo usando o Azure AD.
2. Configurar a saudação de toouse seu aplicativo `passport-azure-ad` plug-in.
3. Use Passport tooissue entrar e solicitações de saída tooAzure AD.
4. Imprima dados de usuário.

Olá código para este tutorial [é mantida no GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS). toofollow ao longo, você pode [baixar esqueleto de saudação do aplicativo como um arquivo. zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip). Também é possível clonar o esqueleto do hello:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

aplicativo Hello concluída é fornecido no final da saudação deste tutorial.

## <a name="get-an-azure-ad-b2c-directory"></a>Obter um diretório AD B2C do Azure

Antes de usar AD B2C do Azure, você deve criar um diretório ou locatário.  Um diretório é um contêiner para todos os seus usuários, aplicativos, grupos etc. Se você ainda não tiver um, [crie um diretório B2C](active-directory-b2c-get-started.md) antes de prosseguir neste guia.

## <a name="create-an-application"></a>Criar um aplicativo

Em seguida, você precisa toocreate um aplicativo no seu diretório do B2C. Isso fornece informações do AD do Azure que precisa toocommunicate com segurança com seu aplicativo. Ambos Olá aplicativo cliente e a API da web será representado por um único **ID do aplicativo**, pois elas formam um aplicativo lógico. toocreate um aplicativo, siga [estas instruções](active-directory-b2c-app-registration.md). É necessário que você:

- Incluir um **aplicativo web**/**web API** no aplicativo hello.
- Digite `http://localhost:3000/auth/openid/return` como uma **URL de Resposta**. É saudação padrão URL para este exemplo de código.
- Crie um **Segredo de aplicativo** para seu aplicativo e copie-o. Você precisará dela mais tarde. Observe que esse valor precisa toobe [XML escapado](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) antes de você usá-lo.
- Saudação de cópia **ID do aplicativo** que é atribuído tooyour aplicativo. Você também precisará dela mais tarde.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Criar suas políticas

No Azure AD B2C, toda experiência do usuário é definida por uma [política](active-directory-b2c-reference-policies.md). Esse aplicativo contém três experiências de identidade: inscrição, entrada e entrada usando o Facebook. Você precisa toocreate essa política de cada tipo, conforme descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Ao criar as três políticas, não deixe de:

- Escolha Olá **nome de exibição** e outros atributos de inscrição em sua política de inscrição.
- Escolha Olá **nome de exibição** e **ID de objeto** declarações de aplicativo em cada política. Você pode escolher outras declarações também.
- Saudação de cópia **nome** de cada política depois de criá-lo. Ele deve ter o prefixo Olá `b2c_1_`.  Você precisará esses nomes de política mais tarde.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Depois de criar as três políticas, você está pronto toobuild seu aplicativo.

Observe que este artigo não aborda como as políticas de saudação toouse você acabou de criar. toolearn sobre como as diretivas funcionam no Azure AD B2C, começam com hello [.NET web aplicativo tutorial de Introdução](active-directory-b2c-devquickstarts-web-dotnet.md).

## <a name="add-prerequisites-tooyour-directory"></a>Adicionar o diretório de tooyour pré-requisitos

Na linha de comando hello, altere pasta de raiz de tooyour de diretórios, se você não ainda estiver lá. Execute Olá comandos a seguir:

- `npm install express`
- `npm install ejs`
- `npm install ejs-locals`
- `npm install restify`
- `npm install mongoose`
- `npm install bunyan`
- `npm install assert-plus`
- `npm install passport`
- `npm install webfinger`
- `npm install body-parser`
- `npm install express-session`
- `npm install cookie-parser`

Além disso, usamos `passport-azure-ad` para nossa visualização em esqueleto de saudação do hello início rápido.

- `npm install passport-azure-ad`

Isso irá instalar bibliotecas de saudação que `passport-azure-ad` depende.

## <a name="set-up-your-app-toouse-hello-passport-nodejs-strategy"></a>Configurar a saudação de toouse seu aplicativo Node. js Passport estratégia
Configure Olá Express middleware toouse Olá protocolo de autenticação OpenID Connect. Passport ser usado tooissue solicitações de entrada e saídas, gerenciar sessões de usuário e obter informações sobre usuários, entre outras ações.

Olá abrir `config.js` arquivo na raiz de saudação do projeto hello e insira os valores de configuração do aplicativo na Olá `exports.creds` seção.
- `clientID`: Olá **ID do aplicativo** atribuído tooyour aplicativo no portal de registro de saudação.
- `returnURL`: Olá **URI de redirecionamento** inserido no portal de saudação.
- `tenantName`: nome do locatário de saudação do seu aplicativo, por exemplo, **contoso.onmicrosoft.com**.

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

Olá abrir `app.js` arquivo na raiz de saudação do projeto de saudação. Adicionar Olá após a chamada tooinvoke Olá `OIDCStrategy` estratégia que vem com `passport-azure-ad`.


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

Use a estratégia de saudação apenas referenciado toohandle solicitações de entrada.

```JavaScript
// Use hello OIDCStrategy in Passport (Section 2).
//
//   Strategies in Passport require a "validate" function that accepts
//   credentials (in this case, an OpenID identifier), and invokes a callback
//   by using a user object.
passport.use(new OIDCStrategy({
    callbackURL: config.creds.returnURL,
    realm: config.creds.realm,
    clientID: config.creds.clientID,
    oidcIssuer: config.creds.issuer,
    identityMetadata: config.creds.identityMetadata,
    skipUserProfile: config.creds.skipUserProfile,
    responseType: config.creds.responseType,
    responseMode: config.creds.responseMode,
    tenantName: config.creds.tenantName
  },
  function(iss, sub, profile, accessToken, refreshToken, done) {
    log.info('Example: Email address we received was: ', profile.email);
    // asynchronous verification, for effect...
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
O Passport usa um padrão semelhante para todas as suas estratégias (incluindo o Twitter e o Facebook). Todos os gravadores de estratégia aderem toothis padrão. Quando você examinar a estratégia Olá, você pode ver que você passe uma `function()` que tem um token e um `done` como parâmetros de saudação. estratégia de saudação volta tooyou depois que ela fez todo seu trabalho. Usuário Olá de armazenar e acumular token Olá para que você não precisa tooask para ele novamente.

> [!IMPORTANT]
Olá código anterior usa todos os usuários a quem autentica o servidor de saudação. Esse é o registro automático. Quando você usa servidores de produção, você não quer toolet em usuários, a menos que eles passaram por um processo de registro que você configurou. Frequentemente, você pode ver esse padrão em aplicativos de consumidor. Essas opções permitem que você tooregister usando o Facebook, mas, em seguida, eles solicitar que você toofill informações adicionais. Se o aplicativo não foi um exemplo, podemos pode extrair um endereço de email do objeto Olá token retornado e depois peça Olá usuário toofill informações adicionais. Como esse é um servidor de teste, podemos simplesmente adicionar banco de dados do usuários toohello na memória.

Adicionar métodos Olá que permitem controlar tookeep de usuários que se conectaram, conforme solicitado pelo Passport. Isso inclui a serialização e a desserialização de informações do usuário:

```JavaScript

// Passport session setup. (Section 2)

//   toosupport persistent sign-in sessions, Passport needs toobe able to
//   serialize users into and deserialize users out of sessions. Typically,
//   this is as simple as storing hello user ID when Passport serializes a user
//   and finding hello user by ID when Passport deserializes that user.
passport.serializeUser(function(user, done) {
  done(null, user.email);
});

passport.deserializeUser(function(id, done) {
  findByEmail(id, function (err, user) {
    done(err, user);
  });
});

// Array toohold users who have signed in
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

Adicione mecanismo do hello código tooload Olá Express. No seguinte hello, você pode ver que usamos padrão Olá `/views` e `/routes` padrão Express fornece.

```JavaScript

// configure Express (Section 2)

var app = express();


app.configure(function() {
  app.set('views', __dirname + '/views');
  app.set('view engine', 'ejs');
  app.use(express.logger());
  app.use(express.methodOverride());
  app.use(cookieParser());
  app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
  app.use(bodyParser.urlencoded({ extended : true }));
  // Initialize Passport!  Also use passport.session() middleware toosupport
  // persistent sign-in sessions (recommended).
  app.use(passport.initialize());
  app.use(passport.session());
  app.use(app.router);
  app.use(express.static(__dirname + '/../../public'));
});

```

Adicionar Olá `POST` rotas entregar Olá solicitações de entrada real toohello `passport-azure-ad` mecanismo:

```JavaScript

// Our Auth routes (Section 3)

// GET /auth/openid
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. hello first step in OpenID authentication involves redirecting
//   hello user tooan OpenID provider. After hello user is authenticated,
//   hello OpenID provider redirects hello user back toothis application at
//   /auth/openid/return

app.get('/auth/openid',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Authentication was called in hello Sample');
    res.redirect('/');
  });

// GET /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it redirects hello user toohello home page.
app.get('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });

// POST /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it will redirect hello user toohello home page.

app.post('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });
```

## <a name="use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Usar o logon no Passport tooissue e solicitações de saída tooAzure AD

Seu aplicativo agora está toocommunicate corretamente configurado com o ponto de extremidade do hello v 2.0 usando o protocolo de autenticação OpenID Connect hello. `passport-azure-ad`foi resolvido detalhes de saudação de criação de mensagens de autenticação, validando tokens do AD do Azure e manter a sessão de usuário. Tudo o que permanece é toogive seus usuários uma maneira toosign em e entre out e toogather obter informações adicionais sobre os usuários que se conectaram.

Primeiro, adicione o saudação padrão, entrar, conta e métodos logout tooyour `app.js` arquivo:

```JavaScript

//Routes (Section 4)

app.get('/', function(req, res){
  res.render('index', { user: req.user });
});

app.get('/account', ensureAuthenticated, function(req, res){
  res.render('account', { user: req.user });
});

app.get('/login',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Login was called in hello Sample');
    res.redirect('/');
});

app.get('/logout', function(req, res){
  req.logout();
  res.redirect('/');
});

```

tooreview esses métodos em detalhes:
- Olá `/` rota redireciona toohello `index.ejs` exibição passando usuário Olá na solicitação de saudação (se houver).
- Olá `/account` rota primeiro verifica se você está autenticado (Olá implementação para isso é abaixo). Ele passa usuário Olá na solicitação de saudação para que você pode obter informações adicionais sobre o usuário de saudação.
- Olá `/login` rota chamadas Olá `azuread-openidconnect` autenticador de `passport-azure-ad`. Se não for bem-sucedida, rota Olá redireciona ao usuário Olá muito`/login`.
- `/logout` simplesmente chama `logout.ejs` (e sua rota). Isso limpará os cookies e, em seguida, retorna Olá ao usuário muito`index.ejs`.


Para a última parte saudação do `app.js`, adicionar Olá `EnsureAuthenticated` método que é usado em Olá `/account` rota.

```JavaScript

// Simple route middleware tooensure that hello user is authenticated. (Section 4)

//   Use this route middleware on any resource that needs toobe protected. If
//   hello request is authenticated (typically via a persistent sign-in session),
//   then hello request will proceed. Otherwise, hello user will be redirected toothe
//   sign-in page.
function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) { return next(); }
  res.redirect('/login')
}

```

Finalmente, crie o próprio servidor de saudação em `app.js`.

```JavaScript

app.listen(3000);

```


## <a name="create-hello-views-and-routes-in-express-toocall-your-policies"></a>Criar exibições hello e rotas de toocall Express suas políticas

O `app.js` já foi concluído. Você precisa apenas rotas de saudação tooadd e exibições que permitem que as políticas de entrada e inscreva-se de saudação toocall. Eles também trata Olá `/logout` e `/login` rotas que você criou.

Criar hello `/routes/index.js` rota no diretório raiz de saudação.

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

Criar hello `/routes/user.js` rota no diretório raiz de saudação.

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

Essas rotas simples passam em modos de exibição de tooyour de solicitações. Eles incluem usuário hello, se houver.

Criar hello `/views/index.ejs` no diretório raiz de saudação do modo de exibição. Essa é uma página simples que chama as políticas de entrada e saída. Você também pode usar isso toograb informações da conta. Observe que você pode usar o hello condicional `if (!user)` usuário Olá passado por meio de solicitação Olá tooprovide evidência de que o usuário hello está conectada.

```JavaScript
<% if (!user) { %>
    <h2>Welcome! Please sign in.</h2>
    <a href="/login/?p=your facebook policy">Sign in with Facebook</a>
    <a href="/login/?p=your email sign-in policy">Sign in with email</a>
    <a href="/login/?p=your email sign-up policy">Sign up with email</a>
<% } else { %>
    <h2>Hello, <%= user.displayName %>.</h2>
    <a href="/account">Account info</a></br>
    <a href="/logout">Log out</a>
<% } %>
```

Criar hello `/views/account.ejs` exibir no diretório raiz de saudação para que você possa exibir informações adicionais que `passport-azure-ad` colocar na solicitação de saudação do usuário.

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
<p>Full Claims</p>
<%- JSON.stringify(user) %>
<p></p>
<a href="/logout">Log Out</a>
<% } %>
```

Agora você pode compilar e executar o aplicativo.

Execute `node app.js` e navegue muito`http://localhost:3000`


Inscrever-se ou entrar no aplicativo toohello usando email ou do Facebook. Saia e entre novamente como outro usuário.

##<a name="next-steps"></a>Próximas etapas

Para referência, Olá concluída exemplo (sem os valores de configuração) [é fornecido como um arquivo. zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip). Você também pode cloná-lo do GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

Agora você pode mover toomore tópicos avançados. Você pode experimentar:

[Proteger uma API da web usando o modelo de saudação B2C no Node. js](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on toomore advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing hello your B2C App's UX >>]()

-->
