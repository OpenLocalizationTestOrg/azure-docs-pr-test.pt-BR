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
# <a name="azure-ad-b2c-add-sign-in-tooa-nodejs-web-app"></a><span data-ttu-id="97b18-103">B2C do Azure AD: Adicionar o aplicativo de web Node.js tooa entrar</span><span class="sxs-lookup"><span data-stu-id="97b18-103">Azure AD B2C: Add sign-in tooa Node.js web app</span></span>

<span data-ttu-id="97b18-104">**Passport** é middleware de autenticação para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="97b18-104">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="97b18-105">Extremamente flexível e modular, o Passport pode ser instalado sem impedimento em qualquer aplicativo Web baseado em Express ou Restify.</span><span class="sxs-lookup"><span data-stu-id="97b18-105">Extremely flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="97b18-106">Um conjunto abrangente de estratégias que dão suporte à autenticação usando um nome de usuário e uma senha, o Facebook, o Twitter e muito mais.</span><span class="sxs-lookup"><span data-stu-id="97b18-106">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="97b18-107">Desenvolvemos uma estratégia para o Azure AD (Active Directory do Azure).</span><span class="sxs-lookup"><span data-stu-id="97b18-107">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="97b18-108">Você instalará esse módulo e, em seguida, adicionar Olá AD do Azure `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="97b18-108">You will install this module and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="97b18-109">toodo isso, você precisa:</span><span class="sxs-lookup"><span data-stu-id="97b18-109">toodo this, you need to:</span></span>

1. <span data-ttu-id="97b18-110">Registre um aplicativo usando o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97b18-110">Register an application by using Azure AD.</span></span>
2. <span data-ttu-id="97b18-111">Configurar a saudação de toouse seu aplicativo `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="97b18-111">Set up your app toouse hello `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="97b18-112">Use Passport tooissue entrar e solicitações de saída tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="97b18-112">Use Passport tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="97b18-113">Imprima dados de usuário.</span><span class="sxs-lookup"><span data-stu-id="97b18-113">Print user data.</span></span>

<span data-ttu-id="97b18-114">Olá código para este tutorial [é mantida no GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="97b18-114">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span></span> <span data-ttu-id="97b18-115">toofollow ao longo, você pode [baixar esqueleto de saudação do aplicativo como um arquivo. zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="97b18-115">toofollow along, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="97b18-116">Também é possível clonar o esqueleto do hello:</span><span class="sxs-lookup"><span data-stu-id="97b18-116">You can also clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="97b18-117">aplicativo Hello concluída é fornecido no final da saudação deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="97b18-117">hello completed application is provided at hello end of this tutorial.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="97b18-118">Obter um diretório AD B2C do Azure</span><span class="sxs-lookup"><span data-stu-id="97b18-118">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="97b18-119">Antes de usar AD B2C do Azure, você deve criar um diretório ou locatário.</span><span class="sxs-lookup"><span data-stu-id="97b18-119">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="97b18-120">Um diretório é um contêiner para todos os seus usuários, aplicativos, grupos etc.</span><span class="sxs-lookup"><span data-stu-id="97b18-120">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="97b18-121">Se você ainda não tiver um, [crie um diretório B2C](active-directory-b2c-get-started.md) antes de prosseguir neste guia.</span><span class="sxs-lookup"><span data-stu-id="97b18-121">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="97b18-122">Criar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="97b18-122">Create an application</span></span>

<span data-ttu-id="97b18-123">Em seguida, você precisa toocreate um aplicativo no seu diretório do B2C.</span><span class="sxs-lookup"><span data-stu-id="97b18-123">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="97b18-124">Isso fornece informações do AD do Azure que precisa toocommunicate com segurança com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="97b18-124">This gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="97b18-125">Ambos Olá aplicativo cliente e a API da web será representado por um único **ID do aplicativo**, pois elas formam um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="97b18-125">Both hello client app and web API will be represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="97b18-126">toocreate um aplicativo, siga [estas instruções](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="97b18-126">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="97b18-127">É necessário que você:</span><span class="sxs-lookup"><span data-stu-id="97b18-127">Be sure to:</span></span>

- <span data-ttu-id="97b18-128">Incluir um **aplicativo web**/**web API** no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="97b18-128">Include a **web app**/**web API** in hello application.</span></span>
- <span data-ttu-id="97b18-129">Digite `http://localhost:3000/auth/openid/return` como uma **URL de Resposta**.</span><span class="sxs-lookup"><span data-stu-id="97b18-129">Enter `http://localhost:3000/auth/openid/return` as a **Reply URL**.</span></span> <span data-ttu-id="97b18-130">É saudação padrão URL para este exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="97b18-130">It is hello default URL for this code sample.</span></span>
- <span data-ttu-id="97b18-131">Crie um **Segredo de aplicativo** para seu aplicativo e copie-o.</span><span class="sxs-lookup"><span data-stu-id="97b18-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="97b18-132">Você precisará dela mais tarde.</span><span class="sxs-lookup"><span data-stu-id="97b18-132">You will need it later.</span></span> <span data-ttu-id="97b18-133">Observe que esse valor precisa toobe [XML escapado](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) antes de você usá-lo.</span><span class="sxs-lookup"><span data-stu-id="97b18-133">Note that this value needs toobe [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
- <span data-ttu-id="97b18-134">Saudação de cópia **ID do aplicativo** que é atribuído tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="97b18-134">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="97b18-135">Você também precisará dela mais tarde.</span><span class="sxs-lookup"><span data-stu-id="97b18-135">You'll also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="97b18-136">Criar suas políticas</span><span class="sxs-lookup"><span data-stu-id="97b18-136">Create your policies</span></span>

<span data-ttu-id="97b18-137">No Azure AD B2C, toda experiência do usuário é definida por uma [política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="97b18-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="97b18-138">Esse aplicativo contém três experiências de identidade: inscrição, entrada e entrada usando o Facebook.</span><span class="sxs-lookup"><span data-stu-id="97b18-138">This app contains three identity experiences: sign up, sign in, and sign in by using Facebook.</span></span> <span data-ttu-id="97b18-139">Você precisa toocreate essa política de cada tipo, conforme descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="97b18-139">You need toocreate this policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="97b18-140">Ao criar as três políticas, não deixe de:</span><span class="sxs-lookup"><span data-stu-id="97b18-140">When you create your three policies, be sure to:</span></span>

- <span data-ttu-id="97b18-141">Escolha Olá **nome de exibição** e outros atributos de inscrição em sua política de inscrição.</span><span class="sxs-lookup"><span data-stu-id="97b18-141">Choose hello **Display name** and other sign-up attributes in your sign-up policy.</span></span>
- <span data-ttu-id="97b18-142">Escolha Olá **nome de exibição** e **ID de objeto** declarações de aplicativo em cada política.</span><span class="sxs-lookup"><span data-stu-id="97b18-142">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="97b18-143">Você pode escolher outras declarações também.</span><span class="sxs-lookup"><span data-stu-id="97b18-143">You can choose other claims as well.</span></span>
- <span data-ttu-id="97b18-144">Saudação de cópia **nome** de cada política depois de criá-lo.</span><span class="sxs-lookup"><span data-stu-id="97b18-144">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="97b18-145">Ele deve ter o prefixo Olá `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="97b18-145">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="97b18-146">Você precisará esses nomes de política mais tarde.</span><span class="sxs-lookup"><span data-stu-id="97b18-146">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="97b18-147">Depois de criar as três políticas, você está pronto toobuild seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="97b18-147">After you create your three policies, you're ready toobuild your app.</span></span>

<span data-ttu-id="97b18-148">Observe que este artigo não aborda como as políticas de saudação toouse você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="97b18-148">Note that this article does not cover how toouse hello policies you just created.</span></span> <span data-ttu-id="97b18-149">toolearn sobre como as diretivas funcionam no Azure AD B2C, começam com hello [.NET web aplicativo tutorial de Introdução](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="97b18-149">toolearn about how policies work in Azure AD B2C, start with hello [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="add-prerequisites-tooyour-directory"></a><span data-ttu-id="97b18-150">Adicionar o diretório de tooyour pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="97b18-150">Add prerequisites tooyour directory</span></span>

<span data-ttu-id="97b18-151">Na linha de comando hello, altere pasta de raiz de tooyour de diretórios, se você não ainda estiver lá.</span><span class="sxs-lookup"><span data-stu-id="97b18-151">From hello command line, change directories tooyour root folder, if you're not already there.</span></span> <span data-ttu-id="97b18-152">Execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="97b18-152">Run hello following commands:</span></span>

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

<span data-ttu-id="97b18-153">Além disso, usamos `passport-azure-ad` para nossa visualização em esqueleto de saudação do hello início rápido.</span><span class="sxs-lookup"><span data-stu-id="97b18-153">In addition, we used `passport-azure-ad` for our preview in hello skeleton of hello Quickstart.</span></span>

- `npm install passport-azure-ad`

<span data-ttu-id="97b18-154">Isso irá instalar bibliotecas de saudação que `passport-azure-ad` depende.</span><span class="sxs-lookup"><span data-stu-id="97b18-154">This will install hello libraries that `passport-azure-ad` depends on.</span></span>

## <a name="set-up-your-app-toouse-hello-passport-nodejs-strategy"></a><span data-ttu-id="97b18-155">Configurar a saudação de toouse seu aplicativo Node. js Passport estratégia</span><span class="sxs-lookup"><span data-stu-id="97b18-155">Set up your app toouse hello Passport-Node.js strategy</span></span>
<span data-ttu-id="97b18-156">Configure Olá Express middleware toouse Olá protocolo de autenticação OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="97b18-156">Configure hello Express middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="97b18-157">Passport ser usado tooissue solicitações de entrada e saídas, gerenciar sessões de usuário e obter informações sobre usuários, entre outras ações.</span><span class="sxs-lookup"><span data-stu-id="97b18-157">Passport will be used tooissue sign-in and sign-out requests, manage user sessions, and get information about users, among other actions.</span></span>

<span data-ttu-id="97b18-158">Olá abrir `config.js` arquivo na raiz de saudação do projeto hello e insira os valores de configuração do aplicativo na Olá `exports.creds` seção.</span><span class="sxs-lookup"><span data-stu-id="97b18-158">Open hello `config.js` file in hello root of hello project and enter your app's configuration values in hello `exports.creds` section.</span></span>
- <span data-ttu-id="97b18-159">`clientID`: Olá **ID do aplicativo** atribuído tooyour aplicativo no portal de registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="97b18-159">`clientID`: hello **Application ID** assigned tooyour app in hello registration portal.</span></span>
- <span data-ttu-id="97b18-160">`returnURL`: Olá **URI de redirecionamento** inserido no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="97b18-160">`returnURL`: hello **Redirect URI** you entered in hello portal.</span></span>
- <span data-ttu-id="97b18-161">`tenantName`: nome do locatário de saudação do seu aplicativo, por exemplo, **contoso.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="97b18-161">`tenantName`: hello tenant name of your app, for example, **contoso.onmicrosoft.com**.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="97b18-162">Olá abrir `app.js` arquivo na raiz de saudação do projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="97b18-162">Open hello `app.js` file in hello root of hello project.</span></span> <span data-ttu-id="97b18-163">Adicionar Olá após a chamada tooinvoke Olá `OIDCStrategy` estratégia que vem com `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="97b18-163">Add hello following call tooinvoke hello `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

<span data-ttu-id="97b18-164">Use a estratégia de saudação apenas referenciado toohandle solicitações de entrada.</span><span class="sxs-lookup"><span data-stu-id="97b18-164">Use hello strategy you just referenced toohandle sign-in requests.</span></span>

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
<span data-ttu-id="97b18-165">O Passport usa um padrão semelhante para todas as suas estratégias (incluindo o Twitter e o Facebook).</span><span class="sxs-lookup"><span data-stu-id="97b18-165">Passport uses a similar pattern for all of its strategies (including Twitter and Facebook).</span></span> <span data-ttu-id="97b18-166">Todos os gravadores de estratégia aderem toothis padrão.</span><span class="sxs-lookup"><span data-stu-id="97b18-166">All strategy writers adhere toothis pattern.</span></span> <span data-ttu-id="97b18-167">Quando você examinar a estratégia Olá, você pode ver que você passe uma `function()` que tem um token e um `done` como parâmetros de saudação.</span><span class="sxs-lookup"><span data-stu-id="97b18-167">When you look at hello strategy, you can see that you pass it a `function()` that has a token and a `done` as hello parameters.</span></span> <span data-ttu-id="97b18-168">estratégia de saudação volta tooyou depois que ela fez todo seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="97b18-168">hello strategy comes back tooyou after it has done all of its work.</span></span> <span data-ttu-id="97b18-169">Usuário Olá de armazenar e acumular token Olá para que você não precisa tooask para ele novamente.</span><span class="sxs-lookup"><span data-stu-id="97b18-169">Store hello user and stash hello token so that you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="97b18-170">Olá código anterior usa todos os usuários a quem autentica o servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="97b18-170">hello preceding code takes all users whom hello server authenticates.</span></span> <span data-ttu-id="97b18-171">Esse é o registro automático.</span><span class="sxs-lookup"><span data-stu-id="97b18-171">This is autoregistration.</span></span> <span data-ttu-id="97b18-172">Quando você usa servidores de produção, você não quer toolet em usuários, a menos que eles passaram por um processo de registro que você configurou.</span><span class="sxs-lookup"><span data-stu-id="97b18-172">When you use production servers, you don’t want toolet in users unless they have gone through a registration process that you have set up.</span></span> <span data-ttu-id="97b18-173">Frequentemente, você pode ver esse padrão em aplicativos de consumidor.</span><span class="sxs-lookup"><span data-stu-id="97b18-173">You can often see this pattern in consumer apps.</span></span> <span data-ttu-id="97b18-174">Essas opções permitem que você tooregister usando o Facebook, mas, em seguida, eles solicitar que você toofill informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="97b18-174">These allow you tooregister by using Facebook, but then they ask you toofill out additional information.</span></span> <span data-ttu-id="97b18-175">Se o aplicativo não foi um exemplo, podemos pode extrair um endereço de email do objeto Olá token retornado e depois peça Olá usuário toofill informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="97b18-175">If our application wasn’t a sample, we could extract an email address from hello token object that is returned, and then ask hello user toofill out additional information.</span></span> <span data-ttu-id="97b18-176">Como esse é um servidor de teste, podemos simplesmente adicionar banco de dados do usuários toohello na memória.</span><span class="sxs-lookup"><span data-stu-id="97b18-176">Because this is a test server, we simply add users toohello in-memory database.</span></span>

<span data-ttu-id="97b18-177">Adicionar métodos Olá que permitem controlar tookeep de usuários que se conectaram, conforme solicitado pelo Passport.</span><span class="sxs-lookup"><span data-stu-id="97b18-177">Add hello methods that allow you tookeep track of users who have signed in, as required by Passport.</span></span> <span data-ttu-id="97b18-178">Isso inclui a serialização e a desserialização de informações do usuário:</span><span class="sxs-lookup"><span data-stu-id="97b18-178">This includes serializing and deserializing user information:</span></span>

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

<span data-ttu-id="97b18-179">Adicione mecanismo do hello código tooload Olá Express.</span><span class="sxs-lookup"><span data-stu-id="97b18-179">Add hello code tooload hello Express engine.</span></span> <span data-ttu-id="97b18-180">No seguinte hello, você pode ver que usamos padrão Olá `/views` e `/routes` padrão Express fornece.</span><span class="sxs-lookup"><span data-stu-id="97b18-180">In hello following, you can see that we use hello default `/views` and `/routes` pattern that Express provides.</span></span>

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

<span data-ttu-id="97b18-181">Adicionar Olá `POST` rotas entregar Olá solicitações de entrada real toohello `passport-azure-ad` mecanismo:</span><span class="sxs-lookup"><span data-stu-id="97b18-181">Add hello `POST` routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>

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

## <a name="use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="97b18-182">Usar o logon no Passport tooissue e solicitações de saída tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="97b18-182">Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>

<span data-ttu-id="97b18-183">Seu aplicativo agora está toocommunicate corretamente configurado com o ponto de extremidade do hello v 2.0 usando o protocolo de autenticação OpenID Connect hello.</span><span class="sxs-lookup"><span data-stu-id="97b18-183">Your app is now properly configured toocommunicate with hello v2.0 endpoint by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="97b18-184">`passport-azure-ad`foi resolvido detalhes de saudação de criação de mensagens de autenticação, validando tokens do AD do Azure e manter a sessão de usuário.</span><span class="sxs-lookup"><span data-stu-id="97b18-184">`passport-azure-ad` has taken care of hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span> <span data-ttu-id="97b18-185">Tudo o que permanece é toogive seus usuários uma maneira toosign em e entre out e toogather obter informações adicionais sobre os usuários que se conectaram.</span><span class="sxs-lookup"><span data-stu-id="97b18-185">All that remains is toogive your users a way toosign in and sign out, and toogather additional information on users who have signed in.</span></span>

<span data-ttu-id="97b18-186">Primeiro, adicione o saudação padrão, entrar, conta e métodos logout tooyour `app.js` arquivo:</span><span class="sxs-lookup"><span data-stu-id="97b18-186">First, add hello default, sign-in, account, and sign-out methods tooyour `app.js` file:</span></span>

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

<span data-ttu-id="97b18-187">tooreview esses métodos em detalhes:</span><span class="sxs-lookup"><span data-stu-id="97b18-187">tooreview these methods in detail:</span></span>
- <span data-ttu-id="97b18-188">Olá `/` rota redireciona toohello `index.ejs` exibição passando usuário Olá na solicitação de saudação (se houver).</span><span class="sxs-lookup"><span data-stu-id="97b18-188">hello `/` route redirects toohello `index.ejs` view by passing hello user in hello request (if it exists).</span></span>
- <span data-ttu-id="97b18-189">Olá `/account` rota primeiro verifica se você está autenticado (Olá implementação para isso é abaixo).</span><span class="sxs-lookup"><span data-stu-id="97b18-189">hello `/account` route first verifies that you are authenticated (hello implementation for this is below).</span></span> <span data-ttu-id="97b18-190">Ele passa usuário Olá na solicitação de saudação para que você pode obter informações adicionais sobre o usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="97b18-190">It then passes hello user in hello request so that you can get additional information about hello user.</span></span>
- <span data-ttu-id="97b18-191">Olá `/login` rota chamadas Olá `azuread-openidconnect` autenticador de `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="97b18-191">hello `/login` route calls hello `azuread-openidconnect` authenticator from `passport-azure-ad`.</span></span> <span data-ttu-id="97b18-192">Se não for bem-sucedida, rota Olá redireciona ao usuário Olá muito`/login`.</span><span class="sxs-lookup"><span data-stu-id="97b18-192">If it doesn't succeed, hello route redirects hello user back too`/login`.</span></span>
- <span data-ttu-id="97b18-193">`/logout` simplesmente chama `logout.ejs` (e sua rota).</span><span class="sxs-lookup"><span data-stu-id="97b18-193">`/logout` simply calls `logout.ejs` (and its route).</span></span> <span data-ttu-id="97b18-194">Isso limpará os cookies e, em seguida, retorna Olá ao usuário muito`index.ejs`.</span><span class="sxs-lookup"><span data-stu-id="97b18-194">This clears cookies and then returns hello user back too`index.ejs`.</span></span>


<span data-ttu-id="97b18-195">Para a última parte saudação do `app.js`, adicionar Olá `EnsureAuthenticated` método que é usado em Olá `/account` rota.</span><span class="sxs-lookup"><span data-stu-id="97b18-195">For hello last part of `app.js`, add hello `EnsureAuthenticated` method that is used in hello `/account` route.</span></span>

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

<span data-ttu-id="97b18-196">Finalmente, crie o próprio servidor de saudação em `app.js`.</span><span class="sxs-lookup"><span data-stu-id="97b18-196">Finally, create hello server itself in `app.js`.</span></span>

```JavaScript

app.listen(3000);

```


## <a name="create-hello-views-and-routes-in-express-toocall-your-policies"></a><span data-ttu-id="97b18-197">Criar exibições hello e rotas de toocall Express suas políticas</span><span class="sxs-lookup"><span data-stu-id="97b18-197">Create hello views and routes in Express toocall your policies</span></span>

<span data-ttu-id="97b18-198">O `app.js` já foi concluído.</span><span class="sxs-lookup"><span data-stu-id="97b18-198">Your `app.js` is now complete.</span></span> <span data-ttu-id="97b18-199">Você precisa apenas rotas de saudação tooadd e exibições que permitem que as políticas de entrada e inscreva-se de saudação toocall.</span><span class="sxs-lookup"><span data-stu-id="97b18-199">You just need tooadd hello routes and views that allow you toocall hello sign-in and sign-up policies.</span></span> <span data-ttu-id="97b18-200">Eles também trata Olá `/logout` e `/login` rotas que você criou.</span><span class="sxs-lookup"><span data-stu-id="97b18-200">These also handle hello `/logout` and `/login` routes you created.</span></span>

<span data-ttu-id="97b18-201">Criar hello `/routes/index.js` rota no diretório raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="97b18-201">Create hello `/routes/index.js` route under hello root directory.</span></span>

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

<span data-ttu-id="97b18-202">Criar hello `/routes/user.js` rota no diretório raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="97b18-202">Create hello `/routes/user.js` route under hello root directory.</span></span>

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

<span data-ttu-id="97b18-203">Essas rotas simples passam em modos de exibição de tooyour de solicitações.</span><span class="sxs-lookup"><span data-stu-id="97b18-203">These simple routes pass along requests tooyour views.</span></span> <span data-ttu-id="97b18-204">Eles incluem usuário hello, se houver.</span><span class="sxs-lookup"><span data-stu-id="97b18-204">They include hello user, if one is present.</span></span>

<span data-ttu-id="97b18-205">Criar hello `/views/index.ejs` no diretório raiz de saudação do modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="97b18-205">Create hello `/views/index.ejs` view under hello root directory.</span></span> <span data-ttu-id="97b18-206">Essa é uma página simples que chama as políticas de entrada e saída. Você também pode usar isso toograb informações da conta.</span><span class="sxs-lookup"><span data-stu-id="97b18-206">This is a simple page that calls policies for sign-in and sign-out. You can also use it toograb account information.</span></span> <span data-ttu-id="97b18-207">Observe que você pode usar o hello condicional `if (!user)` usuário Olá passado por meio de solicitação Olá tooprovide evidência de que o usuário hello está conectada.</span><span class="sxs-lookup"><span data-stu-id="97b18-207">Note that you can use hello conditional `if (!user)` as hello user is passed through in hello request tooprovide evidence that hello user is signed in.</span></span>

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

<span data-ttu-id="97b18-208">Criar hello `/views/account.ejs` exibir no diretório raiz de saudação para que você possa exibir informações adicionais que `passport-azure-ad` colocar na solicitação de saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="97b18-208">Create hello `/views/account.ejs` view under hello root directory so that you can view additional information that `passport-azure-ad` put in hello user request.</span></span>

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

<span data-ttu-id="97b18-209">Agora você pode compilar e executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="97b18-209">You can now build and run your app.</span></span>

<span data-ttu-id="97b18-210">Execute `node app.js` e navegue muito`http://localhost:3000`</span><span class="sxs-lookup"><span data-stu-id="97b18-210">Run `node app.js` and navigate too`http://localhost:3000`</span></span>


<span data-ttu-id="97b18-211">Inscrever-se ou entrar no aplicativo toohello usando email ou do Facebook.</span><span class="sxs-lookup"><span data-stu-id="97b18-211">Sign up or sign in toohello app by using email or Facebook.</span></span> <span data-ttu-id="97b18-212">Saia e entre novamente como outro usuário.</span><span class="sxs-lookup"><span data-stu-id="97b18-212">Sign out and sign back in as a different user.</span></span>

##<a name="next-steps"></a><span data-ttu-id="97b18-213">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="97b18-213">Next steps</span></span>

<span data-ttu-id="97b18-214">Para referência, Olá concluída exemplo (sem os valores de configuração) [é fornecido como um arquivo. zip](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="97b18-214">For reference, hello completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="97b18-215">Você também pode cloná-lo do GitHub:</span><span class="sxs-lookup"><span data-stu-id="97b18-215">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="97b18-216">Agora você pode mover toomore tópicos avançados.</span><span class="sxs-lookup"><span data-stu-id="97b18-216">You can now move on toomore advanced topics.</span></span> <span data-ttu-id="97b18-217">Você pode experimentar:</span><span class="sxs-lookup"><span data-stu-id="97b18-217">You might try:</span></span>

[<span data-ttu-id="97b18-218">Proteger uma API da web usando o modelo de saudação B2C no Node. js</span><span class="sxs-lookup"><span data-stu-id="97b18-218">Secure a web API by using hello B2C model in Node.js</span></span>](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on toomore advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing hello your B2C App's UX >>]()

-->
