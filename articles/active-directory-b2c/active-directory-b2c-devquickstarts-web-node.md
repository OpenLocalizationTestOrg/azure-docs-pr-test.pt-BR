---
title: Adicionar a entrada a um aplicativo Web do Node.js para o Azure B2C | Microsoft Docs
description: "Como criar um aplicativo Web do Node.js que conecta os usuários usando um locatário do B2C."
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
ms.openlocfilehash: c85b8f8434d1e837ac96ac63b9b37f990677ed6e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-add-sign-in-to-a-nodejs-web-app"></a><span data-ttu-id="452eb-103">Azure AD B2C: adicionar entrada a um aplicativo Web do Node.js</span><span class="sxs-lookup"><span data-stu-id="452eb-103">Azure AD B2C: Add sign-in to a Node.js web app</span></span>

<span data-ttu-id="452eb-104">**Passport** é middleware de autenticação para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="452eb-104">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="452eb-105">Extremamente flexível e modular, o Passport pode ser instalado sem impedimento em qualquer aplicativo Web baseado em Express ou Restify.</span><span class="sxs-lookup"><span data-stu-id="452eb-105">Extremely flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="452eb-106">Um conjunto abrangente de estratégias que dão suporte à autenticação usando um nome de usuário e uma senha, o Facebook, o Twitter e muito mais.</span><span class="sxs-lookup"><span data-stu-id="452eb-106">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="452eb-107">Desenvolvemos uma estratégia para o Azure AD (Active Directory do Azure).</span><span class="sxs-lookup"><span data-stu-id="452eb-107">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="452eb-108">Você instalará esse módulo e, em seguida, adicionará o plug-in `passport-azure-ad` do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="452eb-108">You will install this module and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="452eb-109">Para fazer isso, você precisa:</span><span class="sxs-lookup"><span data-stu-id="452eb-109">To do this, you need to:</span></span>

1. <span data-ttu-id="452eb-110">Registre um aplicativo usando o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="452eb-110">Register an application by using Azure AD.</span></span>
2. <span data-ttu-id="452eb-111">Configure seu aplicativo para usar o plug-in `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="452eb-111">Set up your app to use the `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="452eb-112">Usar o Passport para emitir solicitações de entrada e saída ao AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="452eb-112">Use Passport to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="452eb-113">Imprima dados de usuário.</span><span class="sxs-lookup"><span data-stu-id="452eb-113">Print user data.</span></span>

<span data-ttu-id="452eb-114">O código para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="452eb-114">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span></span> <span data-ttu-id="452eb-115">Para acompanhá-lo, você pode [baixar o esqueleto do aplicativo como um arquivo .zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="452eb-115">To follow along, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="452eb-116">Também é possível clonar o esqueleto:</span><span class="sxs-lookup"><span data-stu-id="452eb-116">You can also clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="452eb-117">O aplicativo completo é fornecido no fim deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="452eb-117">The completed application is provided at the end of this tutorial.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="452eb-118">Obter um diretório AD B2C do Azure</span><span class="sxs-lookup"><span data-stu-id="452eb-118">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="452eb-119">Antes de usar AD B2C do Azure, você deve criar um diretório ou locatário.</span><span class="sxs-lookup"><span data-stu-id="452eb-119">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="452eb-120">Um diretório é um contêiner para todos os seus usuários, aplicativos, grupos etc.</span><span class="sxs-lookup"><span data-stu-id="452eb-120">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="452eb-121">Se você ainda não tiver um, [crie um diretório B2C](active-directory-b2c-get-started.md) antes de prosseguir neste guia.</span><span class="sxs-lookup"><span data-stu-id="452eb-121">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="452eb-122">Criar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="452eb-122">Create an application</span></span>

<span data-ttu-id="452eb-123">Em seguida, você precisa criar um aplicativo em seu diretório B2C.</span><span class="sxs-lookup"><span data-stu-id="452eb-123">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="452eb-124">Isso fornece ao AD do Azure as informações de que ele precisa para se comunicar de forma segura com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="452eb-124">This gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="452eb-125">O aplicativo cliente e a API Web serão representados por uma única **ID do Aplicativo**, pois eles abrangem um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="452eb-125">Both the client app and web API will be represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="452eb-126">Para criar um aplicativo, [siga estas instruções](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="452eb-126">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="452eb-127">É necessário que você:</span><span class="sxs-lookup"><span data-stu-id="452eb-127">Be sure to:</span></span>

- <span data-ttu-id="452eb-128">Incluir um **aplicativo Web**/**api Web** no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="452eb-128">Include a **web app**/**web API** in the application.</span></span>
- <span data-ttu-id="452eb-129">Digite `http://localhost:3000/auth/openid/return` como uma **URL de Resposta**.</span><span class="sxs-lookup"><span data-stu-id="452eb-129">Enter `http://localhost:3000/auth/openid/return` as a **Reply URL**.</span></span> <span data-ttu-id="452eb-130">É a URL padrão deste exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="452eb-130">It is the default URL for this code sample.</span></span>
- <span data-ttu-id="452eb-131">Crie um **Segredo de aplicativo** para seu aplicativo e copie-o.</span><span class="sxs-lookup"><span data-stu-id="452eb-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="452eb-132">Você precisará dela mais tarde.</span><span class="sxs-lookup"><span data-stu-id="452eb-132">You will need it later.</span></span> <span data-ttu-id="452eb-133">Observe que esse valor precisa ser [seguido por caracteres de escape XML](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) antes de ser usado.</span><span class="sxs-lookup"><span data-stu-id="452eb-133">Note that this value needs to be [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
- <span data-ttu-id="452eb-134">Copie a **ID de aplicativo** atribuída ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="452eb-134">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="452eb-135">Você também precisará dela mais tarde.</span><span class="sxs-lookup"><span data-stu-id="452eb-135">You'll also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="452eb-136">Criar suas políticas</span><span class="sxs-lookup"><span data-stu-id="452eb-136">Create your policies</span></span>

<span data-ttu-id="452eb-137">No Azure AD B2C, toda experiência do usuário é definida por uma [política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="452eb-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="452eb-138">Esse aplicativo contém três experiências de identidade: inscrição, entrada e entrada usando o Facebook.</span><span class="sxs-lookup"><span data-stu-id="452eb-138">This app contains three identity experiences: sign up, sign in, and sign in by using Facebook.</span></span> <span data-ttu-id="452eb-139">Você precisa criar esta política de cada tipo, conforme descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="452eb-139">You need to create this policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="452eb-140">Ao criar as três políticas, não deixe de:</span><span class="sxs-lookup"><span data-stu-id="452eb-140">When you create your three policies, be sure to:</span></span>

- <span data-ttu-id="452eb-141">Escolher o **Nome de exibição** e outros atributos de inscrição em sua política de inscrição.</span><span class="sxs-lookup"><span data-stu-id="452eb-141">Choose the **Display name** and other sign-up attributes in your sign-up policy.</span></span>
- <span data-ttu-id="452eb-142">Escolha as declarações de aplicativo **Nome de exibição** e **ID do Objeto** em todas as políticas.</span><span class="sxs-lookup"><span data-stu-id="452eb-142">Choose the **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="452eb-143">Você pode escolher outras declarações também.</span><span class="sxs-lookup"><span data-stu-id="452eb-143">You can choose other claims as well.</span></span>
- <span data-ttu-id="452eb-144">Copie o **Nome** de cada política depois de criá-la.</span><span class="sxs-lookup"><span data-stu-id="452eb-144">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="452eb-145">Ele deve ter o prefixo `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="452eb-145">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="452eb-146">Você precisará esses nomes de política mais tarde.</span><span class="sxs-lookup"><span data-stu-id="452eb-146">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="452eb-147">Depois de criar as três políticas, você estará pronto para compilar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="452eb-147">After you create your three policies, you're ready to build your app.</span></span>

<span data-ttu-id="452eb-148">Observe que este artigo não aborda como usar as políticas que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="452eb-148">Note that this article does not cover how to use the policies you just created.</span></span> <span data-ttu-id="452eb-149">Para saber mais sobre o funcionamento das políticas no Azure AD B2C, comece com o [tutorial de introdução ao aplicativo Web do .NET](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="452eb-149">To learn about how policies work in Azure AD B2C, start with the [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="add-prerequisites-to-your-directory"></a><span data-ttu-id="452eb-150">Adicionar pré-requisitos a seu diretório</span><span class="sxs-lookup"><span data-stu-id="452eb-150">Add prerequisites to your directory</span></span>

<span data-ttu-id="452eb-151">Na linha de comando, altere os diretórios para a pasta raiz, se você não ainda estiver lá.</span><span class="sxs-lookup"><span data-stu-id="452eb-151">From the command line, change directories to your root folder, if you're not already there.</span></span> <span data-ttu-id="452eb-152">Execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="452eb-152">Run the following commands:</span></span>

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

<span data-ttu-id="452eb-153">Além disso, usamos `passport-azure-ad` para a visualização no esqueleto do Início Rápido.</span><span class="sxs-lookup"><span data-stu-id="452eb-153">In addition, we used `passport-azure-ad` for our preview in the skeleton of the Quickstart.</span></span>

- `npm install passport-azure-ad`

<span data-ttu-id="452eb-154">Isso instalará as bibliotecas das quais o `passport-azure-ad` depende.</span><span class="sxs-lookup"><span data-stu-id="452eb-154">This will install the libraries that `passport-azure-ad` depends on.</span></span>

## <a name="set-up-your-app-to-use-the-passport-nodejs-strategy"></a><span data-ttu-id="452eb-155">Configurar seu aplicativo para usar a estratégia do Passport-Node.js</span><span class="sxs-lookup"><span data-stu-id="452eb-155">Set up your app to use the Passport-Node.js strategy</span></span>
<span data-ttu-id="452eb-156">Configure o middleware Express para usar o protocolo de autenticação OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="452eb-156">Configure the Express middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="452eb-157">O Passport será usado para emitir solicitações de entrada e saída, gerenciar sessões de usuário e obter informações sobre usuários, entre outras ações.</span><span class="sxs-lookup"><span data-stu-id="452eb-157">Passport will be used to issue sign-in and sign-out requests, manage user sessions, and get information about users, among other actions.</span></span>

<span data-ttu-id="452eb-158">Abra o arquivo `config.js` na raiz do projeto e insira os valores de configuração do aplicativo na seção `exports.creds`.</span><span class="sxs-lookup"><span data-stu-id="452eb-158">Open the `config.js` file in the root of the project and enter your app's configuration values in the `exports.creds` section.</span></span>
- <span data-ttu-id="452eb-159">`clientID`: a **ID do Aplicativo** atribuída a seu aplicativo no portal de registro.</span><span class="sxs-lookup"><span data-stu-id="452eb-159">`clientID`: The **Application ID** assigned to your app in the registration portal.</span></span>
- <span data-ttu-id="452eb-160">`returnURL`: o **URI de Redirecionamento** que você inseriu no portal.</span><span class="sxs-lookup"><span data-stu-id="452eb-160">`returnURL`: The **Redirect URI** you entered in the portal.</span></span>
- <span data-ttu-id="452eb-161">`tenantName`: o nome do locatário de seu aplicativo; por exemplo, **contoso.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="452eb-161">`tenantName`: The tenant name of your app, for example, **contoso.onmicrosoft.com**.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="452eb-162">Abra o arquivo `app.js` na raiz do projeto.</span><span class="sxs-lookup"><span data-stu-id="452eb-162">Open the `app.js` file in the root of the project.</span></span> <span data-ttu-id="452eb-163">Adicione a chamada a seguir para invocar a estratégia `OIDCStrategy` que vem com o `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="452eb-163">Add the following call to invoke the `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

<span data-ttu-id="452eb-164">Use a estratégia referenciada para manipular solicitações de entrada.</span><span class="sxs-lookup"><span data-stu-id="452eb-164">Use the strategy you just referenced to handle sign-in requests.</span></span>

```JavaScript
// Use the OIDCStrategy in Passport (Section 2).
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
<span data-ttu-id="452eb-165">O Passport usa um padrão semelhante para todas as suas estratégias (incluindo o Twitter e o Facebook).</span><span class="sxs-lookup"><span data-stu-id="452eb-165">Passport uses a similar pattern for all of its strategies (including Twitter and Facebook).</span></span> <span data-ttu-id="452eb-166">Todos os gravadores de estratégia seguem esse padrão.</span><span class="sxs-lookup"><span data-stu-id="452eb-166">All strategy writers adhere to this pattern.</span></span> <span data-ttu-id="452eb-167">Ao examinar a estratégia, você pode ver que passa para ela um `function()` que tem um token e um `done` como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="452eb-167">When you look at the strategy, you can see that you pass it a `function()` that has a token and a `done` as the parameters.</span></span> <span data-ttu-id="452eb-168">A estratégia volta para você após fazer seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="452eb-168">The strategy comes back to you after it has done all of its work.</span></span> <span data-ttu-id="452eb-169">Armazene o usuário e guarde o token para que não precise pedi-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="452eb-169">Store the user and stash the token so that you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="452eb-170">O código anterior usa todos os usuários que o servidor autentica.</span><span class="sxs-lookup"><span data-stu-id="452eb-170">The preceding code takes all users whom the server authenticates.</span></span> <span data-ttu-id="452eb-171">Esse é o registro automático.</span><span class="sxs-lookup"><span data-stu-id="452eb-171">This is autoregistration.</span></span> <span data-ttu-id="452eb-172">Ao usar servidores de produção, não convém permitir a inclusão de usuários, a menos que eles passem por um processo de registro configurado por você.</span><span class="sxs-lookup"><span data-stu-id="452eb-172">When you use production servers, you don’t want to let in users unless they have gone through a registration process that you have set up.</span></span> <span data-ttu-id="452eb-173">Frequentemente, você pode ver esse padrão em aplicativos de consumidor.</span><span class="sxs-lookup"><span data-stu-id="452eb-173">You can often see this pattern in consumer apps.</span></span> <span data-ttu-id="452eb-174">Eles permitem que você se registre usando o Facebook, mas, em seguida, pedem que você preencha informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="452eb-174">These allow you to register by using Facebook, but then they ask you to fill out additional information.</span></span> <span data-ttu-id="452eb-175">Se o aplicativo não fosse um exemplo, poderíamos extrair um endereço de email do objeto de token que é retornado e, em seguida, pedir ao usuário que preenchesse informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="452eb-175">If our application wasn’t a sample, we could extract an email address from the token object that is returned, and then ask the user to fill out additional information.</span></span> <span data-ttu-id="452eb-176">Como esse é um servidor de teste, basta adicionar usuários ao banco de dados na memória.</span><span class="sxs-lookup"><span data-stu-id="452eb-176">Because this is a test server, we simply add users to the in-memory database.</span></span>

<span data-ttu-id="452eb-177">Adicione os métodos que lhe permitem acompanhar os usuários que se inscreveram, conforme solicitado pelo Passport.</span><span class="sxs-lookup"><span data-stu-id="452eb-177">Add the methods that allow you to keep track of users who have signed in, as required by Passport.</span></span> <span data-ttu-id="452eb-178">Isso inclui a serialização e a desserialização de informações do usuário:</span><span class="sxs-lookup"><span data-stu-id="452eb-178">This includes serializing and deserializing user information:</span></span>

```JavaScript

// Passport session setup. (Section 2)

//   To support persistent sign-in sessions, Passport needs to be able to
//   serialize users into and deserialize users out of sessions. Typically,
//   this is as simple as storing the user ID when Passport serializes a user
//   and finding the user by ID when Passport deserializes that user.
passport.serializeUser(function(user, done) {
  done(null, user.email);
});

passport.deserializeUser(function(id, done) {
  findByEmail(id, function (err, user) {
    done(err, user);
  });
});

// Array to hold users who have signed in
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

<span data-ttu-id="452eb-179">Adicione o código para carregar o mecanismo Express.</span><span class="sxs-lookup"><span data-stu-id="452eb-179">Add the code to load the Express engine.</span></span> <span data-ttu-id="452eb-180">A seguir, você pode ver que usamos o padrão `/views` e `/routes` padrão fornecidos pelo Express.</span><span class="sxs-lookup"><span data-stu-id="452eb-180">In the following, you can see that we use the default `/views` and `/routes` pattern that Express provides.</span></span>

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
  // Initialize Passport!  Also use passport.session() middleware to support
  // persistent sign-in sessions (recommended).
  app.use(passport.initialize());
  app.use(passport.session());
  app.use(app.router);
  app.use(express.static(__dirname + '/../../public'));
});

```

<span data-ttu-id="452eb-181">Adicione as rotas `POST` que entregarão as solicitações de logon reais ao mecanismo `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="452eb-181">Add the `POST` routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>

```JavaScript

// Our Auth routes (Section 3)

// GET /auth/openid
//   Use passport.authenticate() as route middleware to authenticate the
//   request. The first step in OpenID authentication involves redirecting
//   the user to an OpenID provider. After the user is authenticated,
//   the OpenID provider redirects the user back to this application at
//   /auth/openid/return

app.get('/auth/openid',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Authentication was called in the Sample');
    res.redirect('/');
  });

// GET /auth/openid/return
//   Use passport.authenticate() as route middleware to authenticate the
//   request. If authentication fails, the user will be redirected back to the
//   sign-in page. Otherwise, the primary route function will be called.
//   In this example, it redirects the user to the home page.
app.get('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });

// POST /auth/openid/return
//   Use passport.authenticate() as route middleware to authenticate the
//   request. If authentication fails, the user will be redirected back to the
//   sign-in page. Otherwise, the primary route function will be called.
//   In this example, it will redirect the user to the home page.

app.post('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });
```

## <a name="use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="452eb-182">Usar o Passport para emitir solicitações de entrada e saída ao AD do Azure</span><span class="sxs-lookup"><span data-stu-id="452eb-182">Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>

<span data-ttu-id="452eb-183">Seu aplicativo agora está configurado corretamente para se comunicar com o ponto de extremidade v2.0 usando o protocolo de autenticação OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="452eb-183">Your app is now properly configured to communicate with the v2.0 endpoint by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="452eb-184">O `passport-azure-ad` cuidou de todos os detalhes da criação de mensagens de autenticação, validação de tokens do Azure AD e manutenção da sessão do usuário.</span><span class="sxs-lookup"><span data-stu-id="452eb-184">`passport-azure-ad` has taken care of the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span> <span data-ttu-id="452eb-185">Tudo o que resta é fornecer aos usuários uma maneira de entrar e sair e obter informações adicionais sobre os usuários que entraram.</span><span class="sxs-lookup"><span data-stu-id="452eb-185">All that remains is to give your users a way to sign in and sign out, and to gather additional information on users who have signed in.</span></span>

<span data-ttu-id="452eb-186">Primeiro, adicione a conta de entrada padrão e métodos de saída ao arquivo `app.js`:</span><span class="sxs-lookup"><span data-stu-id="452eb-186">First, add the default, sign-in, account, and sign-out methods to your `app.js` file:</span></span>

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
    log.info('Login was called in the Sample');
    res.redirect('/');
});

app.get('/logout', function(req, res){
  req.logout();
  res.redirect('/');
});

```

<span data-ttu-id="452eb-187">Para examinar esses métodos em detalhes:</span><span class="sxs-lookup"><span data-stu-id="452eb-187">To review these methods in detail:</span></span>
- <span data-ttu-id="452eb-188">A rota `/` é redirecionada para o modo de exibição `index.ejs` passando o usuário na solicitação (se houver).</span><span class="sxs-lookup"><span data-stu-id="452eb-188">The `/` route redirects to the `index.ejs` view by passing the user in the request (if it exists).</span></span>
- <span data-ttu-id="452eb-189">A rota `/account` verifica primeiro se você está autenticado (a implementação para isso está abaixo).</span><span class="sxs-lookup"><span data-stu-id="452eb-189">The `/account` route first verifies that you are authenticated (the implementation for this is below).</span></span> <span data-ttu-id="452eb-190">Em seguida, ela passa o usuário na solicitação para que você possa obter informações adicionais sobre o usuário.</span><span class="sxs-lookup"><span data-stu-id="452eb-190">It then passes the user in the request so that you can get additional information about the user.</span></span>
- <span data-ttu-id="452eb-191">A rota `/login` chama o autenticador `azuread-openidconnect` de `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="452eb-191">The `/login` route calls the `azuread-openidconnect` authenticator from `passport-azure-ad`.</span></span> <span data-ttu-id="452eb-192">Se não tiver êxito, a rota redirecionará o usuário de volta para `/login`.</span><span class="sxs-lookup"><span data-stu-id="452eb-192">If it doesn't succeed, the route redirects the user back to `/login`.</span></span>
- <span data-ttu-id="452eb-193">`/logout` simplesmente chama `logout.ejs` (e sua rota).</span><span class="sxs-lookup"><span data-stu-id="452eb-193">`/logout` simply calls `logout.ejs` (and its route).</span></span> <span data-ttu-id="452eb-194">Isso limpa os cookies e, em seguida, retorna o usuário para `index.ejs`.</span><span class="sxs-lookup"><span data-stu-id="452eb-194">This clears cookies and then returns the user back to `index.ejs`.</span></span>


<span data-ttu-id="452eb-195">Para a última parte de `app.js`, adicione o método `EnsureAuthenticated` que é usado na rota `/account`.</span><span class="sxs-lookup"><span data-stu-id="452eb-195">For the last part of `app.js`, add the `EnsureAuthenticated` method that is used in the `/account` route.</span></span>

```JavaScript

// Simple route middleware to ensure that the user is authenticated. (Section 4)

//   Use this route middleware on any resource that needs to be protected. If
//   the request is authenticated (typically via a persistent sign-in session),
//   then the request will proceed. Otherwise, the user will be redirected to the
//   sign-in page.
function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) { return next(); }
  res.redirect('/login')
}

```

<span data-ttu-id="452eb-196">Por fim, crie o próprio servidor em `app.js`.</span><span class="sxs-lookup"><span data-stu-id="452eb-196">Finally, create the server itself in `app.js`.</span></span>

```JavaScript

app.listen(3000);

```


## <a name="create-the-views-and-routes-in-express-to-call-your-policies"></a><span data-ttu-id="452eb-197">Crie esses modos de exibição e rotas no Express para chamar as políticas</span><span class="sxs-lookup"><span data-stu-id="452eb-197">Create the views and routes in Express to call your policies</span></span>

<span data-ttu-id="452eb-198">O `app.js` já foi concluído.</span><span class="sxs-lookup"><span data-stu-id="452eb-198">Your `app.js` is now complete.</span></span> <span data-ttu-id="452eb-199">Basta adicionar as rotas e os modos de exibição que lhe permitem chamar as políticas de entrada e de inscrição.</span><span class="sxs-lookup"><span data-stu-id="452eb-199">You just need to add the routes and views that allow you to call the sign-in and sign-up policies.</span></span> <span data-ttu-id="452eb-200">Elas também lidam com as rotas `/logout` e `/login` que você criou.</span><span class="sxs-lookup"><span data-stu-id="452eb-200">These also handle the `/logout` and `/login` routes you created.</span></span>

<span data-ttu-id="452eb-201">Criar a rota `/routes/index.js` no diretório raiz.</span><span class="sxs-lookup"><span data-stu-id="452eb-201">Create the `/routes/index.js` route under the root directory.</span></span>

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

<span data-ttu-id="452eb-202">Criar a rota `/routes/user.js` no diretório raiz.</span><span class="sxs-lookup"><span data-stu-id="452eb-202">Create the `/routes/user.js` route under the root directory.</span></span>

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

<span data-ttu-id="452eb-203">Essas rotas simples passam solicitações para seus modos de exibição.</span><span class="sxs-lookup"><span data-stu-id="452eb-203">These simple routes pass along requests to your views.</span></span> <span data-ttu-id="452eb-204">Elas incluem o usuário, caso esteja presente.</span><span class="sxs-lookup"><span data-stu-id="452eb-204">They include the user, if one is present.</span></span>

<span data-ttu-id="452eb-205">Crie o modo de exibição `/views/index.ejs` no diretório raiz.</span><span class="sxs-lookup"><span data-stu-id="452eb-205">Create the `/views/index.ejs` view under the root directory.</span></span> <span data-ttu-id="452eb-206">Essa é uma página simples que chama as políticas de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="452eb-206">This is a simple page that calls policies for sign-in and sign-out.</span></span> <span data-ttu-id="452eb-207">Você também pode usá-la para obter informações sobre a conta.</span><span class="sxs-lookup"><span data-stu-id="452eb-207">You can also use it to grab account information.</span></span> <span data-ttu-id="452eb-208">Observe que você pode usar o `if (!user)` condicional enquanto o usuário é passado na solicitação para comprovar que o usuário está conectado.</span><span class="sxs-lookup"><span data-stu-id="452eb-208">Note that you can use the conditional `if (!user)` as the user is passed through in the request to provide evidence that the user is signed in.</span></span>

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

<span data-ttu-id="452eb-209">Crie o modo de exibição `/views/account.ejs` no diretório raiz para que você possa exibir informações adicionais que `passport-azure-ad` colocou na solicitação do usuário.</span><span class="sxs-lookup"><span data-stu-id="452eb-209">Create the `/views/account.ejs` view under the root directory so that you can view additional information that `passport-azure-ad` put in the user request.</span></span>

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

<span data-ttu-id="452eb-210">Agora você pode compilar e executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="452eb-210">You can now build and run your app.</span></span>

<span data-ttu-id="452eb-211">Execute `node app.js` e navegue até `http://localhost:3000`</span><span class="sxs-lookup"><span data-stu-id="452eb-211">Run `node app.js` and navigate to `http://localhost:3000`</span></span>


<span data-ttu-id="452eb-212">Registre-se ou entre no aplicativo usando o email ou o Facebook.</span><span class="sxs-lookup"><span data-stu-id="452eb-212">Sign up or sign in to the app by using email or Facebook.</span></span> <span data-ttu-id="452eb-213">Saia e entre novamente como outro usuário.</span><span class="sxs-lookup"><span data-stu-id="452eb-213">Sign out and sign back in as a different user.</span></span>

##<a name="next-steps"></a><span data-ttu-id="452eb-214">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="452eb-214">Next steps</span></span>

<span data-ttu-id="452eb-215">Para referência, o exemplo completo (sem seus valores de configuração) é [fornecido como um arquivo .zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="452eb-215">For reference, the completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="452eb-216">Você também pode cloná-lo do GitHub:</span><span class="sxs-lookup"><span data-stu-id="452eb-216">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="452eb-217">Agora você pode passar para tópicos mais avançados.</span><span class="sxs-lookup"><span data-stu-id="452eb-217">You can now move on to more advanced topics.</span></span> <span data-ttu-id="452eb-218">Você pode experimentar:</span><span class="sxs-lookup"><span data-stu-id="452eb-218">You might try:</span></span>

[<span data-ttu-id="452eb-219">Proteger uma API Web usando o modelo B2C no Node.js</span><span class="sxs-lookup"><span data-stu-id="452eb-219">Secure a web API by using the B2C model in Node.js</span></span>](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on to more advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing the your B2C App's UX >>]()

-->
