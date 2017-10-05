---
title: "Introdução à entrada e saída no Azure AD usando Node.js | Microsoft Docs"
description: Saiba como criar um aplicativo Web MVC Node.js Express que se integra ao Azure AD para entrar.
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
ms.openlocfilehash: 13317b016f9ff3955f376b858645c42668b0de42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="87ace-103">Entrada e saída do aplicativo Web Node.js com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="87ace-103">Node.js web app sign-in and sign-out with Azure AD</span></span>
<span data-ttu-id="87ace-104">Aqui usaremos o Passport para:</span><span class="sxs-lookup"><span data-stu-id="87ace-104">Here we use Passport to:</span></span>

* <span data-ttu-id="87ace-105">Conectar o usuário para o aplicativo com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="87ace-105">Sign the user in to the app with Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="87ace-106">Exibir informações sobre o usuário.</span><span class="sxs-lookup"><span data-stu-id="87ace-106">Display information about the user.</span></span>
* <span data-ttu-id="87ace-107">Desconectar o usuário do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="87ace-107">Sign the user out of the app.</span></span>

<span data-ttu-id="87ace-108">O Passport é um middleware de autenticação para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="87ace-108">Passport is authentication middleware for Node.js.</span></span> <span data-ttu-id="87ace-109">Flexível e modular, o Passport pode ser colocado sem impedimento em qualquer aplicativo Web baseado em Express ou Restify.</span><span class="sxs-lookup"><span data-stu-id="87ace-109">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or restify web application.</span></span> <span data-ttu-id="87ace-110">Um conjunto abrangente de estratégias dão suporte à autenticação que usa um nome de usuário e senha, Facebook, Twitter e mais.</span><span class="sxs-lookup"><span data-stu-id="87ace-110">A comprehensive set of strategies support authentication that uses a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="87ace-111">Desenvolvemos uma estratégia para o Active Directory do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="87ace-111">We have developed a strategy for Microsoft Azure Active Directory.</span></span> <span data-ttu-id="87ace-112">Instalamos esse módulo e então adicionamos o plug-in `passport-azure-ad` do Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="87ace-112">We install this module and then add the Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="87ace-113">Para fazer isso, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="87ace-113">To do this, take the following steps:</span></span>

1. <span data-ttu-id="87ace-114">Registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="87ace-114">Register an app.</span></span>
2. <span data-ttu-id="87ace-115">Configure seu aplicativo para usar a estratégia `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="87ace-115">Set up your app to use the `passport-azure-ad` strategy.</span></span>
3. <span data-ttu-id="87ace-116">Usar o Passport para emitir solicitações de entrada e saída ao AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="87ace-116">Use Passport to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="87ace-117">Imprima dados sobre o usuário.</span><span class="sxs-lookup"><span data-stu-id="87ace-117">Print data about the user.</span></span>

<span data-ttu-id="87ace-118">O código para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="87ace-118">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span></span>  <span data-ttu-id="87ace-119">Para acompanhar, você pode [baixar o esqueleto do aplicativo como um arquivo .zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) ou clonar o esqueleto:</span><span class="sxs-lookup"><span data-stu-id="87ace-119">To follow along, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="87ace-120">O aplicativo completo também é fornecido no final deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="87ace-120">The completed application is provided at the end of this tutorial as well.</span></span>

## <a name="step-1-register-an-app"></a><span data-ttu-id="87ace-121">Etapa 1: Registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="87ace-121">Step 1: Register an app</span></span>
1. <span data-ttu-id="87ace-122">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="87ace-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="87ace-123">No menu na parte superior da página, selecione sua conta.</span><span class="sxs-lookup"><span data-stu-id="87ace-123">In the menu at the top of the page, select your account.</span></span> <span data-ttu-id="87ace-124">Sob o **diretório** , escolha onde você deseja registrar seu aplicativo de locatário do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="87ace-124">Under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>

3. <span data-ttu-id="87ace-125">Selecione **Mais Serviços** no menu no lado esquerdo da tela e selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="87ace-125">Select **More Services** in the menu on the left side of the screen, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="87ace-126">Selecione **Registros do aplicativo**e, em seguida, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="87ace-126">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="87ace-127">Siga os prompts para criar um **Aplicativo Web** e/ou uma **API Web**.</span><span class="sxs-lookup"><span data-stu-id="87ace-127">Follow the prompts to create a **Web Application** and/or **WebAPI**.</span></span>
  * <span data-ttu-id="87ace-128">O **nome** do aplicativo descreve o aplicativo aos usuários.</span><span class="sxs-lookup"><span data-stu-id="87ace-128">The **name** of the application describes your application to users.</span></span>

  * <span data-ttu-id="87ace-129">A **URL de logon** é a URL base do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="87ace-129">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="87ace-130">O padrão do esqueleto é `http://localhost:3000/auth/openid/return`\`.</span><span class="sxs-lookup"><span data-stu-id="87ace-130">The skeleton's default is `http://localhost:3000/auth/openid/return`\`.</span></span>

6. <span data-ttu-id="87ace-131">Depois de registrar, AD do Azure atribui seu aplicativo uma ID de aplicativo único.</span><span class="sxs-lookup"><span data-stu-id="87ace-131">After you register, Azure AD assigns your app a unique application ID.</span></span> <span data-ttu-id="87ace-132">Você precisará desse valor nas seções a seguir, então copie-o da página do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="87ace-132">You need this value in the following sections, so copy it from the application page.</span></span>
7. <span data-ttu-id="87ace-133">Na página **Configurações** -> **Propriedades** do aplicativo, atualize o URI da ID do Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="87ace-133">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="87ace-134">O **URI da ID do aplicativo** é um identificador exclusivo para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="87ace-134">The **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="87ace-135">A convenção é usar o formato `https://<tenant-domain>/<app-name>`, por exemplo: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="87ace-135">The convention is to use the format `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

## <a name="step-2-add-prerequisites-to-your-directory"></a><span data-ttu-id="87ace-136">Etapa 2: Adicionar pré-requisitos a seu diretório</span><span class="sxs-lookup"><span data-stu-id="87ace-136">Step 2: Add prerequisites to your directory</span></span>
1. <span data-ttu-id="87ace-137">Na linha de comando, altere o diretório para a pasta raiz se você ainda não estiver lá e execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="87ace-137">From the command line, change directories to your root folder if you're not already there, and then run the following commands:</span></span>

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. <span data-ttu-id="87ace-138">Além disso, você precisa `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="87ace-138">In addition, you need `passport-azure-ad`:</span></span>
    * `npm install passport-azure-ad`

<span data-ttu-id="87ace-139">Isso instala as bibliotecas que `passport-azure-ad` depende.</span><span class="sxs-lookup"><span data-stu-id="87ace-139">This installs the libraries that `passport-azure-ad` depends on.</span></span>

## <a name="step-3-set-up-your-app-to-use-the-passport-node-js-strategy"></a><span data-ttu-id="87ace-140">Etapa 3: Configurar seu aplicativo para usar a estratégia passport-node-js</span><span class="sxs-lookup"><span data-stu-id="87ace-140">Step 3: Set up your app to use the passport-node-js strategy</span></span>
<span data-ttu-id="87ace-141">Aqui, configuramos o Express para usar o protocolo de autenticação OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="87ace-141">Here, we configure Express to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="87ace-142">O Passport é usado para fazer várias coisas, incluindo emitir solicitações de entrada e saída, gerenciar a sessão do usuário e obter informações sobre o usuário.</span><span class="sxs-lookup"><span data-stu-id="87ace-142">Passport is used to do various things, including issue sign-in and sign-out requests, manage the user's session, and get information about the user.</span></span>

1. <span data-ttu-id="87ace-143">Para começar, abra o arquivo `config.js` na raiz do projeto e insira os valores de configuração do aplicativo na seção `exports.creds`.</span><span class="sxs-lookup"><span data-stu-id="87ace-143">To begin, open the `config.js` file at the root of the project, and then enter your app's configuration values in the `exports.creds` section.</span></span>

  * <span data-ttu-id="87ace-144">`clientID` é a **ID do Aplicativo** atribuída ao seu aplicativo no portal de registro.</span><span class="sxs-lookup"><span data-stu-id="87ace-144">The `clientID` is the **Application Id** that's assigned to your app in the registration portal.</span></span>

  * <span data-ttu-id="87ace-145">`returnURL` é o **Uri de Redirecionamento** inserido no portal.</span><span class="sxs-lookup"><span data-stu-id="87ace-145">The `returnURL` is the **Redirect Uri** that you entered in the portal.</span></span>

  * <span data-ttu-id="87ace-146">O `clientSecret` é o segredo gerado no portal.</span><span class="sxs-lookup"><span data-stu-id="87ace-146">The `clientSecret` is the secret that you generated in the portal.</span></span>

2. <span data-ttu-id="87ace-147">Em seguida, abra o arquivo `app.js` na raiz do projeto.</span><span class="sxs-lookup"><span data-stu-id="87ace-147">Next, open the `app.js` file in the root of the project.</span></span> <span data-ttu-id="87ace-148">Em seguida, adicione a chamada a seguir para invocar a estratégia `OIDCStrategy` que vem com o `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="87ace-148">Then add the following call to invoke the `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. <span data-ttu-id="87ace-149">Depois disso, use a estratégia que acabamos de referenciar para manipular nossas solicitações de entrada.</span><span class="sxs-lookup"><span data-stu-id="87ace-149">After that, use the strategy we just referenced to handle our sign-in requests.</span></span>

    ```JavaScript
    // Use the OIDCStrategy within Passport. (Section 2)
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
<span data-ttu-id="87ace-150">O Passport usa um padrão semelhante para todas as estratégias (Twitter, Facebook e assim por diante) que todos os gravadores de estratégia seguem.</span><span class="sxs-lookup"><span data-stu-id="87ace-150">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="87ace-151">Observando a estratégia, você verá que passamos a ela uma função que tem um token e um done como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="87ace-151">Looking at the strategy, you see that we pass it a function that has a token and a done as the parameters.</span></span> <span data-ttu-id="87ace-152">A estratégia de volta para nós depois faz seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="87ace-152">The strategy comes back to us after it does its work.</span></span> <span data-ttu-id="87ace-153">Em seguida, queremos armazenar o usuário e acrescentar o token, para que não precisemos pedi-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="87ace-153">Then we want to store the user and stash the token so we don't need to ask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="87ace-154">O código anterior usa qualquer usuário que tente se autenticar em nosso servidor.</span><span class="sxs-lookup"><span data-stu-id="87ace-154">The previous code takes any user that happens to authenticate to our server.</span></span> <span data-ttu-id="87ace-155">Isso é conhecido como registro automático.</span><span class="sxs-lookup"><span data-stu-id="87ace-155">This is known as auto-registration.</span></span> <span data-ttu-id="87ace-156">Recomendamos que você não permita que ninguém se autentique em um servidor de produção sem primeiro se registrar por meio de um processo escolhido por você.</span><span class="sxs-lookup"><span data-stu-id="87ace-156">We    recommend that you don't let anyone authenticate to a production server without first having them register via a process that you decide on.</span></span> <span data-ttu-id="87ace-157">Geralmente, esse é o padrão visto em aplicativos de consumidor, que permitem se registrar com o Facebook, mas depois solicitam o fornecimento de informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="87ace-157">This is usually the pattern you see in consumer apps, which allow you to register with Facebook but then ask you to provide additional information.</span></span> <span data-ttu-id="87ace-158">Se esse não fosse um aplicativo de exemplo, poderíamos ter extraído o endereço de email do usuário do objeto de token retornado e, em seguida, solicitado a ele que preenchesse informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="87ace-158">If this weren't a sample application, we could have extracted the user's email address from the token object that is returned and then asked the user to fill out additional information.</span></span> <span data-ttu-id="87ace-159">Como esse é um servidor de teste, nós o adicionamos ao banco de dados em memória.</span><span class="sxs-lookup"><span data-stu-id="87ace-159">Because this is a test server, we add them to the in-memory database.</span></span>


4. <span data-ttu-id="87ace-160">Em seguida, vamos adicionar os métodos que permitem controlar os usuários autenticados conforme exigido pelo Passport.</span><span class="sxs-lookup"><span data-stu-id="87ace-160">Next, let's add the methods that enable us to track the signed-in users as required by Passport.</span></span> <span data-ttu-id="87ace-161">Esses métodos incluem a serialização e a desserialização de informações do usuário.</span><span class="sxs-lookup"><span data-stu-id="87ace-161">These methods include serializing and deserializing the user's information.</span></span>

    ```JavaScript

            // Passport session setup. (Section 2)

            //   To support persistent sign-in sessions, Passport needs to be able to
            //   serialize users into the session and deserialize them out of the session. Typically,
            //   this is done simply by storing the user ID when serializing and finding
            //   the user by ID when deserializing.
            passport.serializeUser(function(user, done) {
            done(null, user.email);
            });

            passport.deserializeUser(function(id, done) {
            findByEmail(id, function (err, user) {
                done(err, user);
            });
            });

            // array to hold signed-in users
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

5.  <span data-ttu-id="87ace-162">Em seguida, adicionaremos o código para carregar o mecanismo Express.</span><span class="sxs-lookup"><span data-stu-id="87ace-162">Next, let's add the code to load the Express engine.</span></span> <span data-ttu-id="87ace-163">Aqui você vê que usamos o padrão /views e /routes que o Express fornece.</span><span class="sxs-lookup"><span data-stu-id="87ace-163">Here we use the default /views and /routes pattern that Express provides.</span></span>

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
          // Initialize Passport!  Also use passport.session() middleware, to support
          // persistent login sessions (recommended).
          app.use(passport.initialize());
          app.use(passport.session());
          app.use(app.router);
          app.use(express.static(__dirname + '/../../public'));
        });

    ```

6. <span data-ttu-id="87ace-164">Por fim, adicionaremos as rotas que entregarão as solicitações de logon reais ao mecanismo `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="87ace-164">Finally, let's add the routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>


       ```JavaScript

        // Our Auth routes (section 3)

        // GET /auth/openid
        //   Use passport.authenticate() as route middleware to authenticate the
        //   request. The first step in OpenID authentication involves redirecting
        //   the user to their OpenID provider. After authenticating, the OpenID
        //   provider redirects the user back to this application at
        //   /auth/openid/return.
        app.get('/auth/openid',
        passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
        function(req, res) {
            log.info('Authentication was called in the Sample');
            res.redirect('/');
        });

            // GET /auth/openid/return
            //   Use passport.authenticate() as route middleware to authenticate the
            //   request. If authentication fails, the user is redirected back to the
            //   sign-in page. Otherwise, the primary route function is called,
            //   which, in this example, redirects the user to the home page.
            app.get('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });

            // POST /auth/openid/return
            //   Use passport.authenticate() as route middleware to authenticate the
            //   request. If authentication fails, the user is redirected back to the
            //   sign-in page. Otherwise, the primary route function is called,
            //   which, in this example, redirects the user to the home page.
            app.post('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });
       ```


## <a name="step-4-use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="87ace-165">Etapa 4: usar o Passport para emitir solicitações de entrada e saída ao Azure AD</span><span class="sxs-lookup"><span data-stu-id="87ace-165">Step 4: Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="87ace-166">Seu aplicativo agora está configurado corretamente para se comunicar com o ponto de extremidade usando o protocolo de autenticação OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="87ace-166">Your app is now properly configured to communicate with the endpoint by using the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="87ace-167">O `passport-azure-ad` cuidou de todos os detalhes da criação de mensagens de autenticação, validação de tokens do Azure AD e manutenção das sessões do usuário.</span><span class="sxs-lookup"><span data-stu-id="87ace-167">`passport-azure-ad` has taken care of all the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="87ace-168">Tudo o que resta é fornecer aos usuários uma maneira de entrar e sair e obter informações adicionais sobre os usuários que entraram.</span><span class="sxs-lookup"><span data-stu-id="87ace-168">All that remains is giving your users a way to sign in and sign out, and gathering additional information about the signed-in users.</span></span>

1. <span data-ttu-id="87ace-169">Primeiro, adicionaremos a conta de entrada padrão e os métodos de saída ao nosso arquivo `app.js`:</span><span class="sxs-lookup"><span data-stu-id="87ace-169">First, let's add the default, sign-in, account, and sign-out methods to our `app.js` file:</span></span>

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
            log.info('Login was called in the Sample');
            res.redirect('/');
        });

        app.get('/logout', function(req, res){
          req.logout();
          res.redirect('/');
        });

    ```

2.  <span data-ttu-id="87ace-170">Vamos examiná-los detalhadamente:</span><span class="sxs-lookup"><span data-stu-id="87ace-170">Let's review these in detail:</span></span>

  * <span data-ttu-id="87ace-171">O roteiro `/` é redirecionada para a exibição de index.ejs passando o usuário na solicitação (se houver).</span><span class="sxs-lookup"><span data-stu-id="87ace-171">The `/`route redirects to the index.ejs view, passing the user in the request (if it exists).</span></span>
  * <span data-ttu-id="87ace-172">O roteiro `/account` primeiro *garante que sejamos autenticados* (implementamos no exemplo abaixo) e passa o usuário na solicitação para que possamos obter informações adicionais sobre ele.</span><span class="sxs-lookup"><span data-stu-id="87ace-172">The `/account` route first *ensures we are authenticated* (we implement that in the following example), and then passes the user in the request so that we can get additional information about the user.</span></span>
  * <span data-ttu-id="87ace-173">O roteiro `/login` chama nosso autenticador azuread-openidconnect de `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="87ace-173">The `/login` route calls our azuread-openidconnect authenticator from `passport-azuread`.</span></span> <span data-ttu-id="87ace-174">Caso não obtenha êxito, ele redireciona o usuário para /login.</span><span class="sxs-lookup"><span data-stu-id="87ace-174">If that doesn't succeed, it redirects the user back to /login.</span></span>
  * <span data-ttu-id="87ace-175">O roteiro `/logout` simplesmente chamará logout.ejs (e o roteiro), o que limpa os cookies e, em seguida, retorna o usuário para index.ejs.</span><span class="sxs-lookup"><span data-stu-id="87ace-175">The `/logout` route simply calls the logout.ejs (and route), which clears cookies and then returns the user back to index.ejs.</span></span>

3. <span data-ttu-id="87ace-176">Para a última parte do `app.js`, vamos adicionar o método **EnsureAuthenticated** que é usado em `/account`, como mostrado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="87ace-176">For the last part of `app.js`, let's add the **EnsureAuthenticated** method that is used in `/account`, as shown earlier.</span></span>

    ```JavaScript

        // Simple route middleware to ensure user is authenticated. (section 4)

        //   Use this route middleware on any resource that needs to be protected. If
        //   the request is authenticated (typically via a persistent sign-in session),
        //   the request proceeds. Otherwise, the user is redirected to the
        //   sign-in page.
        function ensureAuthenticated(req, res, next) {
          if (req.isAuthenticated()) { return next(); }
          res.redirect('/login')
        }
    ```

4. <span data-ttu-id="87ace-177">Por fim, vamos criar o próprio servidor em `app.js`:</span><span class="sxs-lookup"><span data-stu-id="87ace-177">Finally, let's create the server itself in `app.js`:</span></span>

```JavaScript

        app.listen(3000);

```


## <a name="step-5-to-display-our-user-in-the-website-create-the-views-and-routes-in-express"></a><span data-ttu-id="87ace-178">Etapa 5: Para exibir nosso usuário no site, crie as exibições e os roteiros no Express</span><span class="sxs-lookup"><span data-stu-id="87ace-178">Step 5: To display our user in the website, create the views and routes in Express</span></span>
<span data-ttu-id="87ace-179">Agora `app.js` for concluída.</span><span class="sxs-lookup"><span data-stu-id="87ace-179">Now `app.js` is complete.</span></span> <span data-ttu-id="87ace-180">Nós simplesmente precisamos adicionar os roteiros e as exibições que mostram as informações de que precisamos para o usuário e lidar com os roteiros `/logout` e `/login` criados.</span><span class="sxs-lookup"><span data-stu-id="87ace-180">We simply need to add the routes and views that show the information we get to the user, as well as handle the `/logout` and `/login` routes that we  created.</span></span>

1. <span data-ttu-id="87ace-181">Criar a rota `/routes/index.js` no diretório raiz.</span><span class="sxs-lookup"><span data-stu-id="87ace-181">Create the `/routes/index.js` route under the root directory.</span></span>

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. <span data-ttu-id="87ace-182">Criar a rota `/routes/user.js` no diretório raiz.</span><span class="sxs-lookup"><span data-stu-id="87ace-182">Create the `/routes/user.js` route under the root directory.</span></span>

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 <span data-ttu-id="87ace-183">Eles passam a solicitação para nossos modos de exibição, incluindo o usuário se presente.</span><span class="sxs-lookup"><span data-stu-id="87ace-183">These pass along the request to our views, including the user if present.</span></span>

3. <span data-ttu-id="87ace-184">Crie o modo de exibição `/views/index.ejs` no diretório raiz.</span><span class="sxs-lookup"><span data-stu-id="87ace-184">Create the `/views/index.ejs` view under the root directory.</span></span> <span data-ttu-id="87ace-185">Essa é uma página simples que chama os nossos métodos de logon e logoff e nos permite obter dados da conta.</span><span class="sxs-lookup"><span data-stu-id="87ace-185">This is a simple page that calls our login and logout methods and enables us to grab account information.</span></span> <span data-ttu-id="87ace-186">Observe que podemos usar o `if (!user)` condicional, pois o usuário que está sendo passado na solicitação é uma prova de que temos um usuário conectado.</span><span class="sxs-lookup"><span data-stu-id="87ace-186">Notice that we can use the conditional `if (!user)` as the user being passed through in the request is evidence we have a signed-in user.</span></span>

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

4. <span data-ttu-id="87ace-187">Crie a exibição `/views/account.ejs` no diretório raiz para que possamos exibir as informações adicionais que `passport-azuread` colocou na solicitação do usuário.</span><span class="sxs-lookup"><span data-stu-id="87ace-187">Create the `/views/account.ejs` view under the root directory so that we can view additional information that `passport-azuread` has put in the user request.</span></span>

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

5. <span data-ttu-id="87ace-188">Vamos fazer essa análise boa adicionando um layout.</span><span class="sxs-lookup"><span data-stu-id="87ace-188">Let's make this look good by adding a layout.</span></span> <span data-ttu-id="87ace-189">Crie a exibição '/views/layout.ejs' sob o diretório raiz.</span><span class="sxs-lookup"><span data-stu-id="87ace-189">Create the '/views/layout.ejs' view under the root directory.</span></span>

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

##<a name="next-steps"></a><span data-ttu-id="87ace-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="87ace-190">Next steps</span></span>
<span data-ttu-id="87ace-191">Por fim, compile e execute seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="87ace-191">Finally, build and run your app.</span></span> <span data-ttu-id="87ace-192">Executar `node app.js`e, em seguida, vá para `http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="87ace-192">Run `node app.js`, and then go to `http://localhost:3000`.</span></span>

<span data-ttu-id="87ace-193">Entre com uma conta pessoal da Microsoft ou uma conta corporativa ou de estudante e observe como a identidade do usuário é exibida na lista /account.</span><span class="sxs-lookup"><span data-stu-id="87ace-193">Sign in with either a personal Microsoft account or a work or school account, and notice how the user's identity is reflected in the /account list.</span></span> <span data-ttu-id="87ace-194">Agora você tem um aplicativo Web protegido por protocolos padrão do setor, que podem autenticar usuários com as respectivas contas pessoais e corporativas ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="87ace-194">You now have a web app that's secured with industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="87ace-195">Para referência, o exemplo completo (sem seus valores de configuração) é [fornecido como um arquivo .zip](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="87ace-195">For reference, the completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="87ace-196">Como alternativa, você pode cloná-lo do GitHub:</span><span class="sxs-lookup"><span data-stu-id="87ace-196">Alternatively, you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="87ace-197">Agora você pode ir para tópicos mais avançados.</span><span class="sxs-lookup"><span data-stu-id="87ace-197">You can now move onto more advanced topics.</span></span> <span data-ttu-id="87ace-198">Você pode desejar experimentar:</span><span class="sxs-lookup"><span data-stu-id="87ace-198">You might want to try:</span></span>

[<span data-ttu-id="87ace-199">Proteger uma API Web com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="87ace-199">Secure a Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
