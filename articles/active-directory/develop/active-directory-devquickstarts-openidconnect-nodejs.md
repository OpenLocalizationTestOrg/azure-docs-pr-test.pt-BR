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
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="7f324-103">Entrada e saída do aplicativo Web Node.js com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f324-103">Node.js web app sign-in and sign-out with Azure AD</span></span>
<span data-ttu-id="7f324-104">Aqui usaremos o Passport para:</span><span class="sxs-lookup"><span data-stu-id="7f324-104">Here we use Passport to:</span></span>

* <span data-ttu-id="7f324-105">Entrada hello usuário no aplicativo toohello com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="7f324-105">Sign hello user in toohello app with Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="7f324-106">Exibir informações sobre o usuário hello.</span><span class="sxs-lookup"><span data-stu-id="7f324-106">Display information about hello user.</span></span>
* <span data-ttu-id="7f324-107">Entrada hello usuário fora do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="7f324-107">Sign hello user out of hello app.</span></span>

<span data-ttu-id="7f324-108">O Passport é um middleware de autenticação para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="7f324-108">Passport is authentication middleware for Node.js.</span></span> <span data-ttu-id="7f324-109">Flexível e modular, Passport atualizam pode ser descartado em tooany expressas ou restify o aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="7f324-109">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or restify web application.</span></span> <span data-ttu-id="7f324-110">Um conjunto abrangente de estratégias dão suporte à autenticação que usa um nome de usuário e senha, Facebook, Twitter e mais.</span><span class="sxs-lookup"><span data-stu-id="7f324-110">A comprehensive set of strategies support authentication that uses a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="7f324-111">Desenvolvemos uma estratégia para o Active Directory do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7f324-111">We have developed a strategy for Microsoft Azure Active Directory.</span></span> <span data-ttu-id="7f324-112">Podemos instalar este módulo e adicionar Olá Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="7f324-112">We install this module and then add hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="7f324-113">toodo, Olá execute as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f324-113">toodo this, take hello following steps:</span></span>

1. <span data-ttu-id="7f324-114">Registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="7f324-114">Register an app.</span></span>
2. <span data-ttu-id="7f324-115">Configurar a saudação de toouse seu aplicativo `passport-azure-ad` estratégia.</span><span class="sxs-lookup"><span data-stu-id="7f324-115">Set up your app toouse hello `passport-azure-ad` strategy.</span></span>
3. <span data-ttu-id="7f324-116">Use Passport tooissue entrar e solicitações de saída tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="7f324-116">Use Passport tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="7f324-117">Imprima dados sobre o usuário hello.</span><span class="sxs-lookup"><span data-stu-id="7f324-117">Print data about hello user.</span></span>

<span data-ttu-id="7f324-118">código de saudação para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="7f324-118">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span></span>  <span data-ttu-id="7f324-119">toofollow ao longo, você pode [baixar esqueleto de saudação do aplicativo como um arquivo. zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) ou esqueleto de saudação do clone:</span><span class="sxs-lookup"><span data-stu-id="7f324-119">toofollow along, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="7f324-120">aplicativo Hello concluída é fornecido no final da saudação deste tutorial também.</span><span class="sxs-lookup"><span data-stu-id="7f324-120">hello completed application is provided at hello end of this tutorial as well.</span></span>

## <a name="step-1-register-an-app"></a><span data-ttu-id="7f324-121">Etapa 1: Registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="7f324-121">Step 1: Register an app</span></span>
1. <span data-ttu-id="7f324-122">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7f324-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="7f324-123">No menu de saudação na parte superior de saudação da página hello, selecione sua conta.</span><span class="sxs-lookup"><span data-stu-id="7f324-123">In hello menu at hello top of hello page, select your account.</span></span> <span data-ttu-id="7f324-124">Em Olá **diretório** , escolha o locatário do Active Directory Olá onde você deseja tooregister seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7f324-124">Under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="7f324-125">Selecione **mais serviços** no hello menu Olá esquerda lado da tela hello e, em seguida, selecione **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="7f324-125">Select **More Services** in hello menu on hello left side of hello screen, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="7f324-126">Selecione **Registros do aplicativo**e, em seguida, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7f324-126">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="7f324-127">Siga Olá prompts toocreate um **aplicativo Web** e/ou **WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="7f324-127">Follow hello prompts toocreate a **Web Application** and/or **WebAPI**.</span></span>
  * <span data-ttu-id="7f324-128">Olá **nome** da saudação aplicativo descreve toousers seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7f324-128">hello **name** of hello application describes your application toousers.</span></span>

  * <span data-ttu-id="7f324-129">Olá **URL de logon** é Olá a URL base do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7f324-129">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="7f324-130">Olá padrão do esqueleto é ' http://localhost:3000/auth/openid/return '.</span><span class="sxs-lookup"><span data-stu-id="7f324-130">hello skeleton's default is `http://localhost:3000/auth/openid/return`\`.</span></span>

6. <span data-ttu-id="7f324-131">Depois de registrar, AD do Azure atribui seu aplicativo uma ID de aplicativo único.</span><span class="sxs-lookup"><span data-stu-id="7f324-131">After you register, Azure AD assigns your app a unique application ID.</span></span> <span data-ttu-id="7f324-132">É necessário que esse valor no seguinte Olá seções, portanto copie-o da página de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="7f324-132">You need this value in hello following sections, so copy it from hello application page.</span></span>
7. <span data-ttu-id="7f324-133">De saudação **configurações** -> **propriedades** página para seu aplicativo, Olá URI da ID do aplicativo de atualização.</span><span class="sxs-lookup"><span data-stu-id="7f324-133">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="7f324-134">Olá **URI da ID do aplicativo** é um identificador exclusivo para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7f324-134">hello **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="7f324-135">convenção de saudação é o formato de saudação do toouse `https://<tenant-domain>/<app-name>`, por exemplo: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="7f324-135">hello convention is toouse hello format `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

## <a name="step-2-add-prerequisites-tooyour-directory"></a><span data-ttu-id="7f324-136">Etapa 2: Adicionar o diretório de tooyour pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7f324-136">Step 2: Add prerequisites tooyour directory</span></span>
1. <span data-ttu-id="7f324-137">Na linha de comando hello, alterar pasta de raiz diretórios tooyour se você não ainda estiver lá, e, em seguida, execute Olá seguindo comandos:</span><span class="sxs-lookup"><span data-stu-id="7f324-137">From hello command line, change directories tooyour root folder if you're not already there, and then run hello following commands:</span></span>

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. <span data-ttu-id="7f324-138">Além disso, você precisa `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="7f324-138">In addition, you need `passport-azure-ad`:</span></span>
    * `npm install passport-azure-ad`

<span data-ttu-id="7f324-139">Isso instala bibliotecas Olá que `passport-azure-ad` depende.</span><span class="sxs-lookup"><span data-stu-id="7f324-139">This installs hello libraries that `passport-azure-ad` depends on.</span></span>

## <a name="step-3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a><span data-ttu-id="7f324-140">Etapa 3: Configurar a sua estratégia de passport-nó-js aplicativo toouse Olá</span><span class="sxs-lookup"><span data-stu-id="7f324-140">Step 3: Set up your app toouse hello passport-node-js strategy</span></span>
<span data-ttu-id="7f324-141">Aqui, podemos configurar protocolo de autenticação OpenID Connect do Express toouse hello.</span><span class="sxs-lookup"><span data-stu-id="7f324-141">Here, we configure Express toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="7f324-142">Passport é usado toodo várias coisas, inclusive solicitações de entrada e saída do problema, gerenciar a sessão do usuário hello e obter informações sobre o usuário hello.</span><span class="sxs-lookup"><span data-stu-id="7f324-142">Passport is used toodo various things, including issue sign-in and sign-out requests, manage hello user's session, and get information about hello user.</span></span>

1. <span data-ttu-id="7f324-143">toobegin, abra Olá `config.js` arquivo na raiz de saudação do projeto hello e, em seguida, insira os valores de configuração do aplicativo no hello `exports.creds` seção.</span><span class="sxs-lookup"><span data-stu-id="7f324-143">toobegin, open hello `config.js` file at hello root of hello project, and then enter your app's configuration values in hello `exports.creds` section.</span></span>

  * <span data-ttu-id="7f324-144">Olá `clientID` é hello **Id do aplicativo** que é atribuído tooyour aplicativo no portal de registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f324-144">hello `clientID` is hello **Application Id** that's assigned tooyour app in hello registration portal.</span></span>

  * <span data-ttu-id="7f324-145">Olá `returnURL` é hello **Uri de redirecionamento** que você inseriu no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f324-145">hello `returnURL` is hello **Redirect Uri** that you entered in hello portal.</span></span>

  * <span data-ttu-id="7f324-146">Olá `clientSecret` é segredo Olá geradas no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f324-146">hello `clientSecret` is hello secret that you generated in hello portal.</span></span>

2. <span data-ttu-id="7f324-147">Em seguida, abra Olá `app.js` arquivo na raiz de saudação do projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f324-147">Next, open hello `app.js` file in hello root of hello project.</span></span> <span data-ttu-id="7f324-148">Em seguida, adicione Olá chamada tooinvoke Olá a seguir `OIDCStrategy` estratégia que vem com `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="7f324-148">Then add hello following call tooinvoke hello `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. <span data-ttu-id="7f324-149">Depois disso, use estratégia de saudação que simplesmente referenciado toohandle nosso solicitações de entrada.</span><span class="sxs-lookup"><span data-stu-id="7f324-149">After that, use hello strategy we just referenced toohandle our sign-in requests.</span></span>

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
<span data-ttu-id="7f324-150">O Passport usa um padrão semelhante para todas as estratégias (Twitter, Facebook e assim por diante) que todos os gravadores de estratégia seguem.</span><span class="sxs-lookup"><span data-stu-id="7f324-150">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="7f324-151">Examinar a estratégia de saudação, você verá que passamos a ele uma função que tem um token e uma pronto como parâmetros de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f324-151">Looking at hello strategy, you see that we pass it a function that has a token and a done as hello parameters.</span></span> <span data-ttu-id="7f324-152">estratégia de saudação vem toous novamente depois que ele faz seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="7f324-152">hello strategy comes back toous after it does its work.</span></span> <span data-ttu-id="7f324-153">Em seguida, queremos usuário de saudação toostore e um token de saudação stash não precisamos tooask para ele novamente.</span><span class="sxs-lookup"><span data-stu-id="7f324-153">Then we want toostore hello user and stash hello token so we don't need tooask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="7f324-154">código anterior Olá usa qualquer usuário que ocorre em tooauthenticate tooour server.</span><span class="sxs-lookup"><span data-stu-id="7f324-154">hello previous code takes any user that happens tooauthenticate tooour server.</span></span> <span data-ttu-id="7f324-155">Isso é conhecido como registro automático.</span><span class="sxs-lookup"><span data-stu-id="7f324-155">This is known as auto-registration.</span></span> <span data-ttu-id="7f324-156">É recomendável que você não permita que ninguém autenticar o servidor de produção tooa sem ter que primeiro-los registrar por meio de um processo que você escolher.</span><span class="sxs-lookup"><span data-stu-id="7f324-156">We    recommend that you don't let anyone authenticate tooa production server without first having them register via a process that you decide on.</span></span> <span data-ttu-id="7f324-157">Normalmente, este é o padrão de saudação que consulte em aplicativos de consumidor, que permitem que você tooregister com o Facebook, mas, em seguida, solicitar que você tooprovide obter informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="7f324-157">This is usually hello pattern you see in consumer apps, which allow you tooregister with Facebook but then ask you tooprovide additional information.</span></span> <span data-ttu-id="7f324-158">Se isso não fosse um aplicativo de exemplo, podemos foi ter extrair endereço de email do usuário de saudação do objeto de token de saudação que é retornado e, em seguida, terá Olá usuário toofill informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="7f324-158">If this weren't a sample application, we could have extracted hello user's email address from hello token object that is returned and then asked hello user toofill out additional information.</span></span> <span data-ttu-id="7f324-159">Como esse é um servidor de teste, adicioná-los banco de dados do toohello na memória.</span><span class="sxs-lookup"><span data-stu-id="7f324-159">Because this is a test server, we add them toohello in-memory database.</span></span>


4. <span data-ttu-id="7f324-160">Em seguida, vamos adicionar métodos de saudação que nos permitem tootrack Olá conectado usuários conforme exigido pelo Passport.</span><span class="sxs-lookup"><span data-stu-id="7f324-160">Next, let's add hello methods that enable us tootrack hello signed-in users as required by Passport.</span></span> <span data-ttu-id="7f324-161">Esses métodos incluem a serialização e desserialização de informações de saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="7f324-161">These methods include serializing and deserializing hello user's information.</span></span>

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

5.  <span data-ttu-id="7f324-162">Em seguida, vamos adicionar o mecanismo do hello código tooload Olá Express.</span><span class="sxs-lookup"><span data-stu-id="7f324-162">Next, let's add hello code tooload hello Express engine.</span></span> <span data-ttu-id="7f324-163">Aqui usamos o saudação padrão /views e padrão de /routes Express fornece.</span><span class="sxs-lookup"><span data-stu-id="7f324-163">Here we use hello default /views and /routes pattern that Express provides.</span></span>

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

6. <span data-ttu-id="7f324-164">Por fim, vamos adicionar Olá roteia mão off Olá solicitações de entrada real toohello `passport-azure-ad` mecanismo:</span><span class="sxs-lookup"><span data-stu-id="7f324-164">Finally, let's add hello routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>


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


## <a name="step-4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="7f324-165">Etapa 4: Usar Passport tooissue entrar e solicitações de saída tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="7f324-165">Step 4: Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="7f324-166">Seu aplicativo agora está toocommunicate corretamente configurado com o ponto de extremidade hello usando o protocolo de autenticação OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="7f324-166">Your app is now properly configured toocommunicate with hello endpoint by using hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="7f324-167">`passport-azure-ad`tiver resolvido todos os detalhes de saudação de criação de mensagens de autenticação, validando tokens do AD do Azure e manutenção de sessões de usuário.</span><span class="sxs-lookup"><span data-stu-id="7f324-167">`passport-azure-ad` has taken care of all hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="7f324-168">Tudo o que permanece é fornecer aos usuários uma maneira toosign no e sair e coleta informações adicionais sobre usuários conectados do hello.</span><span class="sxs-lookup"><span data-stu-id="7f324-168">All that remains is giving your users a way toosign in and sign out, and gathering additional information about hello signed-in users.</span></span>

1. <span data-ttu-id="7f324-169">Primeiro, vamos adicionar saudação padrão, entrar, conta e métodos logout tooour `app.js` arquivo:</span><span class="sxs-lookup"><span data-stu-id="7f324-169">First, let's add hello default, sign-in, account, and sign-out methods tooour `app.js` file:</span></span>

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

2.  <span data-ttu-id="7f324-170">Vamos examiná-los detalhadamente:</span><span class="sxs-lookup"><span data-stu-id="7f324-170">Let's review these in detail:</span></span>

  * <span data-ttu-id="7f324-171">Olá `/`rota redireciona toohello index.ejs exibição, passando o usuário Olá na solicitação de saudação (se houver).</span><span class="sxs-lookup"><span data-stu-id="7f324-171">hello `/`route redirects toohello index.ejs view, passing hello user in hello request (if it exists).</span></span>
  * <span data-ttu-id="7f324-172">Olá `/account` rotear primeiro *garante que sejam autenticados* (implementamos que no exemplo a seguir de saudação), e, em seguida, passa Olá usuário na solicitação de saudação para que podemos obter informações adicionais sobre o usuário hello.</span><span class="sxs-lookup"><span data-stu-id="7f324-172">hello `/account` route first *ensures we are authenticated* (we implement that in hello following example), and then passes hello user in hello request so that we can get additional information about hello user.</span></span>
  * <span data-ttu-id="7f324-173">Olá `/login` rota chama nosso autenticador doWindows Azure openidconnect de `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="7f324-173">hello `/login` route calls our azuread-openidconnect authenticator from `passport-azuread`.</span></span> <span data-ttu-id="7f324-174">Se o que não for bem-sucedida, ele redireciona Olá back muito/logon de usuário.</span><span class="sxs-lookup"><span data-stu-id="7f324-174">If that doesn't succeed, it redirects hello user back too/login.</span></span>
  * <span data-ttu-id="7f324-175">Olá `/logout` rota simplesmente chama hello logout.ejs (e rota), que limpa cookies e, em seguida, retorna Olá tooindex.ejs voltar do usuário.</span><span class="sxs-lookup"><span data-stu-id="7f324-175">hello `/logout` route simply calls hello logout.ejs (and route), which clears cookies and then returns hello user back tooindex.ejs.</span></span>

3. <span data-ttu-id="7f324-176">Para a última parte saudação do `app.js`, vamos adicionar Olá **EnsureAuthenticated** que é usado no método `/account`, conforme mostrado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7f324-176">For hello last part of `app.js`, let's add hello **EnsureAuthenticated** method that is used in `/account`, as shown earlier.</span></span>

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

4. <span data-ttu-id="7f324-177">Por fim, vamos criar o próprio servidor de saudação em `app.js`:</span><span class="sxs-lookup"><span data-stu-id="7f324-177">Finally, let's create hello server itself in `app.js`:</span></span>

```JavaScript

        app.listen(3000);

```


## <a name="step-5-toodisplay-our-user-in-hello-website-create-hello-views-and-routes-in-express"></a><span data-ttu-id="7f324-178">Etapa 5: toodisplay o usuário no site de hello, criar hello exibições e rotas no Express</span><span class="sxs-lookup"><span data-stu-id="7f324-178">Step 5: toodisplay our user in hello website, create hello views and routes in Express</span></span>
<span data-ttu-id="7f324-179">Agora `app.js` for concluída.</span><span class="sxs-lookup"><span data-stu-id="7f324-179">Now `app.js` is complete.</span></span> <span data-ttu-id="7f324-180">Simplesmente precisa rotas de saudação tooadd e exibe informações de saudação que mostrar, podemos obter usuário toohello, bem como lidar com hello `/logout` e `/login` rotas que criamos.</span><span class="sxs-lookup"><span data-stu-id="7f324-180">We simply need tooadd hello routes and views that show hello information we get toohello user, as well as handle hello `/logout` and `/login` routes that we  created.</span></span>

1. <span data-ttu-id="7f324-181">Criar hello `/routes/index.js` rota no diretório raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f324-181">Create hello `/routes/index.js` route under hello root directory.</span></span>

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. <span data-ttu-id="7f324-182">Criar hello `/routes/user.js` rota no diretório raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f324-182">Create hello `/routes/user.js` route under hello root directory.</span></span>

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 <span data-ttu-id="7f324-183">Esses passam Olá solicitação tooour modos de exibição, incluindo o usuário de saudação se estiver presente.</span><span class="sxs-lookup"><span data-stu-id="7f324-183">These pass along hello request tooour views, including hello user if present.</span></span>

3. <span data-ttu-id="7f324-184">Criar hello `/views/index.ejs` no diretório raiz de saudação do modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="7f324-184">Create hello `/views/index.ejs` view under hello root directory.</span></span> <span data-ttu-id="7f324-185">Esta é uma página simple que chama os métodos de logon e logout e permite que as informações de conta de toograb.</span><span class="sxs-lookup"><span data-stu-id="7f324-185">This is a simple page that calls our login and logout methods and enables us toograb account information.</span></span> <span data-ttu-id="7f324-186">Observe que podemos usar Olá condicional `if (!user)` como usuário hello está sendo passado na solicitação de saudação é evidência temos um usuário conectado.</span><span class="sxs-lookup"><span data-stu-id="7f324-186">Notice that we can use hello conditional `if (!user)` as hello user being passed through in hello request is evidence we have a signed-in user.</span></span>

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

4. <span data-ttu-id="7f324-187">Criar hello `/views/account.ejs` exibir no diretório raiz de hello, de modo que é possível exibir informações adicionais que `passport-azuread` colocou na solicitação de saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="7f324-187">Create hello `/views/account.ejs` view under hello root directory so that we can view additional information that `passport-azuread` has put in hello user request.</span></span>

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

5. <span data-ttu-id="7f324-188">Vamos fazer essa análise boa adicionando um layout.</span><span class="sxs-lookup"><span data-stu-id="7f324-188">Let's make this look good by adding a layout.</span></span> <span data-ttu-id="7f324-189">Criar hello ' / diretório raiz de modo de exibição dos views/layout.ejs em hello.</span><span class="sxs-lookup"><span data-stu-id="7f324-189">Create hello '/views/layout.ejs' view under hello root directory.</span></span>

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

##<a name="next-steps"></a><span data-ttu-id="7f324-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7f324-190">Next steps</span></span>
<span data-ttu-id="7f324-191">Por fim, compile e execute seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7f324-191">Finally, build and run your app.</span></span> <span data-ttu-id="7f324-192">Executar `node app.js`e, em seguida, ir muito`http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="7f324-192">Run `node app.js`, and then go too`http://localhost:3000`.</span></span>

<span data-ttu-id="7f324-193">Entrar com uma conta pessoal da Microsoft ou uma conta corporativa ou de estudante e observe como a identidade do usuário Olá é refletida na lista da conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="7f324-193">Sign in with either a personal Microsoft account or a work or school account, and notice how hello user's identity is reflected in hello /account list.</span></span> <span data-ttu-id="7f324-194">Agora você tem um aplicativo Web protegido por protocolos padrão do setor, que podem autenticar usuários com as respectivas contas pessoais e corporativas ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="7f324-194">You now have a web app that's secured with industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="7f324-195">Para referência, Olá concluída exemplo (sem os valores de configuração) [é fornecido como um arquivo. zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="7f324-195">For reference, hello completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="7f324-196">Como alternativa, você pode cloná-lo do GitHub:</span><span class="sxs-lookup"><span data-stu-id="7f324-196">Alternatively, you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="7f324-197">Agora você pode ir para tópicos mais avançados.</span><span class="sxs-lookup"><span data-stu-id="7f324-197">You can now move onto more advanced topics.</span></span> <span data-ttu-id="7f324-198">Você pode desejar tootry:</span><span class="sxs-lookup"><span data-stu-id="7f324-198">You might want tootry:</span></span>

[<span data-ttu-id="7f324-199">Proteger uma API Web com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f324-199">Secure a Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
