---
title: "aaaGetting iniciado com a entrada no AD do Azure e saída usando Node. js | Microsoft Docs"
description: Saiba como toobuild um Node. js Express MVC web aplicativo integrado ao AD do Azure para entrar.
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 81deecec-dbe2-4e75-8bc0-cf3788645f99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 26481899c74741743b947bd891b65ff24ffc43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a>Entrada e saída do aplicativo Web Node.js com o Azure AD
Aqui usaremos o Passport para:

* Entrada hello usuário no aplicativo toohello com o Azure Active Directory (AD do Azure).
* Exibir informações sobre o usuário hello.
* Entrada hello usuário fora do aplicativo hello.

O Passport é um middleware de autenticação para o Node.js. Flexível e modular, Passport atualizam pode ser descartado em tooany expressas ou restify o aplicativo web. Um conjunto abrangente de estratégias dão suporte à autenticação que usa um nome de usuário e senha, Facebook, Twitter e mais. Desenvolvemos uma estratégia para o Active Directory do Microsoft Azure. Podemos instalar este módulo e adicionar Olá Microsoft Azure Active Directory `passport-azure-ad` plug-in.

toodo, Olá execute as etapas a seguir:

1. Registrar um aplicativo
2. Configurar a saudação de toouse seu aplicativo `passport-azure-ad` estratégia.
3. Use Passport tooissue entrar e solicitações de saída tooAzure AD.
4. Imprima dados sobre o usuário hello.

código de saudação para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).  toofollow ao longo, você pode [baixar esqueleto de saudação do aplicativo como um arquivo. zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) ou esqueleto de saudação do clone:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

aplicativo Hello concluída é fornecido no final da saudação deste tutorial também.

## <a name="step-1-register-an-app"></a>Etapa 1: Registrar um aplicativo
1. Entrar toohello [portal do Azure](https://portal.azure.com).

2. No menu de saudação na parte superior de saudação da página hello, selecione sua conta. Em Olá **diretório** , escolha o locatário do Active Directory Olá onde você deseja tooregister seu aplicativo.

3. Selecione **mais serviços** no hello menu Olá esquerda lado da tela hello e, em seguida, selecione **Active Directory do Azure**.

4. Selecione **Registros do aplicativo**e, em seguida, selecione **Adicionar**.

5. Siga Olá prompts toocreate um **aplicativo Web** e/ou **WebAPI**.
  * Olá **nome** da saudação aplicativo descreve toousers seu aplicativo.

  * Olá **URL de logon** é Olá a URL base do seu aplicativo.  Olá padrão do esqueleto é ' http://localhost:3000/auth/openid/return '.

6. Depois de registrar, AD do Azure atribui seu aplicativo uma ID de aplicativo único. É necessário que esse valor no seguinte Olá seções, portanto copie-o da página de aplicativo hello.
7. De saudação **configurações** -> **propriedades** página para seu aplicativo, Olá URI da ID do aplicativo de atualização. Olá **URI da ID do aplicativo** é um identificador exclusivo para seu aplicativo. convenção de saudação é o formato de saudação do toouse `https://<tenant-domain>/<app-name>`, por exemplo: `https://contoso.onmicrosoft.com/my-first-aad-app`.

## <a name="step-2-add-prerequisites-tooyour-directory"></a>Etapa 2: Adicionar o diretório de tooyour pré-requisitos
1. Na linha de comando hello, alterar pasta de raiz diretórios tooyour se você não ainda estiver lá, e, em seguida, execute Olá seguindo comandos:

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. Além disso, você precisa `passport-azure-ad`:
    * `npm install passport-azure-ad`

Isso instala bibliotecas Olá que `passport-azure-ad` depende.

## <a name="step-3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a>Etapa 3: Configurar a sua estratégia de passport-nó-js aplicativo toouse Olá
Aqui, podemos configurar protocolo de autenticação OpenID Connect do Express toouse hello.  Passport é usado toodo várias coisas, inclusive solicitações de entrada e saída do problema, gerenciar a sessão do usuário hello e obter informações sobre o usuário hello.

1. toobegin, abra Olá `config.js` arquivo na raiz de saudação do projeto hello e, em seguida, insira os valores de configuração do aplicativo no hello `exports.creds` seção.

  * Olá `clientID` é hello **Id do aplicativo** que é atribuído tooyour aplicativo no portal de registro de saudação.

  * Olá `returnURL` é hello **Uri de redirecionamento** que você inseriu no portal de saudação.

  * Olá `clientSecret` é segredo Olá geradas no portal de saudação.

2. Em seguida, abra Olá `app.js` arquivo na raiz de saudação do projeto de saudação. Em seguida, adicione Olá chamada tooinvoke Olá a seguir `OIDCStrategy` estratégia que vem com `passport-azure-ad`.

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. Depois disso, use estratégia de saudação que simplesmente referenciado toohandle nosso solicitações de entrada.

    ```JavaScript
    // Use hello OIDCStrategy within Passport. (Section 2)
    //
    //   Strategies in passport require a `validate` function that accepts
    //   credentials (in this case, an OpenID identifier), and invokes a callback
    //   with a user object.
    passport.use(new OIDCStrategy({
        callbackURL: config.creds.returnURL,
        realm: config.creds.realm,
        clientID: config.creds.clientID,
        clientSecret: config.creds.clientSecret,
        oidcIssuer: config.creds.issuer,
        identityMetadata: config.creds.identityMetadata,
        skipUserProfile: config.creds.skipUserProfile,
        responseType: config.creds.responseType,
        responseMode: config.creds.responseMode
    },
    function(iss, sub, profile, accessToken, refreshToken, done) {
        if (!profile.email) {
        return done(new Error("No email found"), null);
        }
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
O Passport usa um padrão semelhante para todas as estratégias (Twitter, Facebook e assim por diante) que todos os gravadores de estratégia seguem. Examinar a estratégia de saudação, você verá que passamos a ele uma função que tem um token e uma pronto como parâmetros de saudação. estratégia de saudação vem toous novamente depois que ele faz seu trabalho. Em seguida, queremos usuário de saudação toostore e um token de saudação stash não precisamos tooask para ele novamente.

> [!IMPORTANT]
código anterior Olá usa qualquer usuário que ocorre em tooauthenticate tooour server. Isso é conhecido como registro automático. É recomendável que você não permita que ninguém autenticar o servidor de produção tooa sem ter que primeiro-los registrar por meio de um processo que você escolher. Normalmente, este é o padrão de saudação que consulte em aplicativos de consumidor, que permitem que você tooregister com o Facebook, mas, em seguida, solicitar que você tooprovide obter informações adicionais. Se isso não fosse um aplicativo de exemplo, podemos foi ter extrair endereço de email do usuário de saudação do objeto de token de saudação que é retornado e, em seguida, terá Olá usuário toofill informações adicionais. Como esse é um servidor de teste, adicioná-los banco de dados do toohello na memória.


4. Em seguida, vamos adicionar métodos de saudação que nos permitem tootrack Olá conectado usuários conforme exigido pelo Passport. Esses métodos incluem a serialização e desserialização de informações de saudação do usuário.

    ```JavaScript

            // Passport session setup. (Section 2)

            //   toosupport persistent sign-in sessions, Passport needs toobe able to
            //   serialize users into hello session and deserialize them out of hello session. Typically,
            //   this is done simply by storing hello user ID when serializing and finding
            //   hello user by ID when deserializing.
            passport.serializeUser(function(user, done) {
            done(null, user.email);
            });

            passport.deserializeUser(function(id, done) {
            findByEmail(id, function (err, user) {
                done(err, user);
            });
            });

            // array toohold signed-in users
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

5.  Em seguida, vamos adicionar o mecanismo do hello código tooload Olá Express. Aqui usamos o saudação padrão /views e padrão de /routes Express fornece.

    ```JavaScript

        // configure Express (section 2)

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

6. Por fim, vamos adicionar Olá roteia mão off Olá solicitações de entrada real toohello `passport-azure-ad` mecanismo:


       ```JavaScript

        // Our Auth routes (section 3)

        // GET /auth/openid
        //   Use passport.authenticate() as route middleware tooauthenticate the
        //   request. hello first step in OpenID authentication involves redirecting
        //   hello user tootheir OpenID provider. After authenticating, hello OpenID
        //   provider redirects hello user back toothis application at
        //   /auth/openid/return.
        app.get('/auth/openid',
        passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
        function(req, res) {
            log.info('Authentication was called in hello Sample');
            res.redirect('/');
        });

            // GET /auth/openid/return
            //   Use passport.authenticate() as route middleware tooauthenticate the
            //   request. If authentication fails, hello user is redirected back toothe
            //   sign-in page. Otherwise, hello primary route function is called,
            //   which, in this example, redirects hello user toohello home page.
            app.get('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });

            // POST /auth/openid/return
            //   Use passport.authenticate() as route middleware tooauthenticate the
            //   request. If authentication fails, hello user is redirected back toothe
            //   sign-in page. Otherwise, hello primary route function is called,
            //   which, in this example, redirects hello user toohello home page.
            app.post('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });
       ```


## <a name="step-4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Etapa 4: Usar Passport tooissue entrar e solicitações de saída tooAzure AD
Seu aplicativo agora está toocommunicate corretamente configurado com o ponto de extremidade hello usando o protocolo de autenticação OpenID Connect hello.  `passport-azure-ad`tiver resolvido todos os detalhes de saudação de criação de mensagens de autenticação, validando tokens do AD do Azure e manutenção de sessões de usuário. Tudo o que permanece é fornecer aos usuários uma maneira toosign no e sair e coleta informações adicionais sobre usuários conectados do hello.

1. Primeiro, vamos adicionar saudação padrão, entrar, conta e métodos logout tooour `app.js` arquivo:

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
            log.info('Login was called in hello Sample');
            res.redirect('/');
        });

        app.get('/logout', function(req, res){
          req.logout();
          res.redirect('/');
        });

    ```

2.  Vamos examiná-los detalhadamente:

  * Olá `/`rota redireciona toohello index.ejs exibição, passando o usuário Olá na solicitação de saudação (se houver).
  * Olá `/account` rotear primeiro *garante que sejam autenticados* (implementamos que no exemplo a seguir de saudação), e, em seguida, passa Olá usuário na solicitação de saudação para que podemos obter informações adicionais sobre o usuário hello.
  * Olá `/login` rota chama nosso autenticador doWindows Azure openidconnect de `passport-azuread`. Se o que não for bem-sucedida, ele redireciona Olá back muito/logon de usuário.
  * Olá `/logout` rota simplesmente chama hello logout.ejs (e rota), que limpa cookies e, em seguida, retorna Olá tooindex.ejs voltar do usuário.

3. Para a última parte saudação do `app.js`, vamos adicionar Olá **EnsureAuthenticated** que é usado no método `/account`, conforme mostrado anteriormente.

    ```JavaScript

        // Simple route middleware tooensure user is authenticated. (section 4)

        //   Use this route middleware on any resource that needs toobe protected. If
        //   hello request is authenticated (typically via a persistent sign-in session),
        //   hello request proceeds. Otherwise, hello user is redirected toothe
        //   sign-in page.
        function ensureAuthenticated(req, res, next) {
          if (req.isAuthenticated()) { return next(); }
          res.redirect('/login')
        }
    ```

4. Por fim, vamos criar o próprio servidor de saudação em `app.js`:

```JavaScript

        app.listen(3000);

```


## <a name="step-5-toodisplay-our-user-in-hello-website-create-hello-views-and-routes-in-express"></a>Etapa 5: toodisplay o usuário no site de hello, criar hello exibições e rotas no Express
Agora `app.js` for concluída. Simplesmente precisa rotas de saudação tooadd e exibe informações de saudação que mostrar, podemos obter usuário toohello, bem como lidar com hello `/logout` e `/login` rotas que criamos.

1. Criar hello `/routes/index.js` rota no diretório raiz de saudação.

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. Criar hello `/routes/user.js` rota no diretório raiz de saudação.

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 Esses passam Olá solicitação tooour modos de exibição, incluindo o usuário de saudação se estiver presente.

3. Criar hello `/views/index.ejs` no diretório raiz de saudação do modo de exibição. Esta é uma página simple que chama os métodos de logon e logout e permite que as informações de conta de toograb. Observe que podemos usar Olá condicional `if (!user)` como usuário hello está sendo passado na solicitação de saudação é evidência temos um usuário conectado.

    ```JavaScript
    <% if (!user) { %>
        <h2>Welcome! Please log in.</h2>
        <a href="/login">Log In</a>
    <% } else { %>
        <h2>Hello, <%= user.displayName %>.</h2>
        <a href="/account">Account Info</a></br>
        <a href="/logout">Log Out</a>
    <% } %>
    ```

4. Criar hello `/views/account.ejs` exibir no diretório raiz de hello, de modo que é possível exibir informações adicionais que `passport-azuread` colocou na solicitação de saudação do usuário.

    ```Javascript
    <% if (!user) { %>
        <h2>Welcome! Please log in.</h2>
        <a href="/login">Log In</a>
    <% } else { %>
    <p>displayName: <%= user.displayName %></p>
    <p>givenName: <%= user.name.givenName %></p>
    <p>familyName: <%= user.name.familyName %></p>
    <p>UPN: <%= user._json.upn %></p>
    <p>Profile ID: <%= user.id %></p>
  ##Next steps  <p>Full Claimes</p>
    <%- JSON.stringify(user) %>
    <p></p>
    <a href="/logout">Log Out</a>
    <% } %>
    ```

5. Vamos fazer essa análise boa adicionando um layout. Criar hello ' / diretório raiz de modo de exibição dos views/layout.ejs em hello.

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
                <a href="/login">Log In</a>
                </p>
            <% } else { %>
                <p>
                <a href="/">Home</a> |
                <a href="/account">Account</a> |
                <a href="/logout">Log Out</a>
                </p>
            <% } %>
            <%- body %>
        </body>
    </html>
    ```

##<a name="next-steps"></a>Próximas etapas
Por fim, compile e execute seu aplicativo. Executar `node app.js`e, em seguida, ir muito`http://localhost:3000`.

Entrar com uma conta pessoal da Microsoft ou uma conta corporativa ou de estudante e observe como a identidade do usuário Olá é refletida na lista da conta de saudação. Agora você tem um aplicativo Web protegido por protocolos padrão do setor, que podem autenticar usuários com as respectivas contas pessoais e corporativas ou de estudante.

Para referência, Olá concluída exemplo (sem os valores de configuração) [é fornecido como um arquivo. zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip). Como alternativa, você pode cloná-lo do GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

Agora você pode ir para tópicos mais avançados. Você pode desejar tootry:

[Proteger uma API Web com o Azure AD](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
