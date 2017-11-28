---
title: aaaSecure uma API da web do Active Directory do Azure v 2.0 usando Node. js | Microsoft Docs
description: Saiba como toobuild um Node. js web API que aceita tokens de uma conta pessoal da Microsoft e de contas corporativa ou escolar.
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 0b572fc1-2aaf-4cb6-82de-63010fb1941d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 219e324cca11e107186b7e5f995589b9260af8a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="65eed-103">Proteger uma API Web usando Node.js</span><span class="sxs-lookup"><span data-stu-id="65eed-103">Secure a web API by using Node.js</span></span>
> [!NOTE]
> <span data-ttu-id="65eed-104">Nem todos os recursos e cenários de Active Directory do Azure funcionam com o ponto de extremidade do hello v 2.0.</span><span class="sxs-lookup"><span data-stu-id="65eed-104">Not all Azure Active Directory scenarios and features work with hello v2.0 endpoint.</span></span> <span data-ttu-id="65eed-105">toodetermine se você deve usar o ponto de extremidade do hello v 2.0 ou ponto de extremidade Olá v 1.0, leia sobre [limitações v 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="65eed-105">toodetermine whether you should use hello v2.0 endpoint or hello v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="65eed-106">Quando você usa o ponto de extremidade do hello Azure Active Directory (AD do Azure) v 2.0, você pode usar [OAuth 2.0](active-directory-v2-protocols.md) tokens de acesso tooprotect sua API da web.</span><span class="sxs-lookup"><span data-stu-id="65eed-106">When you use hello Azure Active Directory (Azure AD) v2.0 endpoint, you can use [OAuth 2.0](active-directory-v2-protocols.md) access tokens tooprotect your web API.</span></span> <span data-ttu-id="65eed-107">Com os tokens de acesso OAuth 2.0, os usuários que têm uma conta da Microsoft pessoal e contas corporativas ou de estudante podem acessar sua API Web com segurança.</span><span class="sxs-lookup"><span data-stu-id="65eed-107">With OAuth 2.0 access tokens, users who have both a personal Microsoft account and work or school accounts can securely access your web API.</span></span>

<span data-ttu-id="65eed-108">*Passport* é middleware de autenticação para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="65eed-108">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="65eed-109">Flexível e modular, o Passport pode ser colocado sem impedimento em qualquer aplicativo Web baseado em Express ou Restify.</span><span class="sxs-lookup"><span data-stu-id="65eed-109">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="65eed-110">No Passport, um conjunto abrangente de estratégias dão suporte à autenticação com o uso de um nome de usuário e uma senha, Facebook, Twitter e outras opções.</span><span class="sxs-lookup"><span data-stu-id="65eed-110">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="65eed-111">Desenvolvemos uma estratégia para o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65eed-111">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="65eed-112">Neste artigo, mostramos como tooinstall Olá módulo e, em seguida, adicionar Olá AD do Azure `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="65eed-112">In this article, we show you how tooinstall hello module, and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="65eed-113">Baixar</span><span class="sxs-lookup"><span data-stu-id="65eed-113">Download</span></span>
<span data-ttu-id="65eed-114">código de saudação para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span><span class="sxs-lookup"><span data-stu-id="65eed-114">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span></span> <span data-ttu-id="65eed-115">tutorial de saudação toofollow, você pode [baixar esqueleto de saudação do aplicativo como um arquivo. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), ou esqueleto de saudação do clone:</span><span class="sxs-lookup"><span data-stu-id="65eed-115">toofollow hello tutorial, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="65eed-116">Você também pode obter aplicativo hello concluída final Olá deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="65eed-116">You also can get hello completed application at hello end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="65eed-117">1: registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="65eed-117">1: Register an app</span></span>
<span data-ttu-id="65eed-118">Criar um novo aplicativo no [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou execute [essas etapas detalhadas](active-directory-v2-app-registration.md) tooregister um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="65eed-118">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) tooregister an app.</span></span> <span data-ttu-id="65eed-119">Verifique se você:</span><span class="sxs-lookup"><span data-stu-id="65eed-119">Make sure you:</span></span>

* <span data-ttu-id="65eed-120">Saudação de cópia **Id do aplicativo** atribuído tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="65eed-120">Copy hello **Application Id** assigned tooyour app.</span></span> <span data-ttu-id="65eed-121">Ela será necessária para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="65eed-121">You'll need it for this tutorial.</span></span>
* <span data-ttu-id="65eed-122">Adicionar Olá **Mobile** plataforma para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="65eed-122">Add hello **Mobile** platform for your app.</span></span>
* <span data-ttu-id="65eed-123">Saudação de cópia **URI de redirecionamento** do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="65eed-123">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="65eed-124">Você deve usar o valor do URI de padrão de saudação `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="65eed-124">You must use hello default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-install-nodejs"></a><span data-ttu-id="65eed-125">2: instalar o Node.js</span><span class="sxs-lookup"><span data-stu-id="65eed-125">2: Install Node.js</span></span>
<span data-ttu-id="65eed-126">exemplo de hello toouse para este tutorial, você deve [instalar Node. js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="65eed-126">toouse hello sample for this tutorial, you must [install Node.js](http://nodejs.org).</span></span>

## <a name="3-install-mongodb"></a><span data-ttu-id="65eed-127">3: instalar o MongoDB</span><span class="sxs-lookup"><span data-stu-id="65eed-127">3: Install MongoDB</span></span>
<span data-ttu-id="65eed-128">toosuccessfully usar este exemplo, você deve [instalar MongoDB](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="65eed-128">toosuccessfully use this sample, you must [install MongoDB](http://www.mongodb.org).</span></span> <span data-ttu-id="65eed-129">Neste exemplo, você usar MongoDB toomake API REST persistente em instâncias de servidor.</span><span class="sxs-lookup"><span data-stu-id="65eed-129">In this sample, you use MongoDB toomake your REST API persistent across server instances.</span></span>

> [!NOTE]
> <span data-ttu-id="65eed-130">Neste artigo, vamos supor que você use Olá instalação e o servidor de pontos de extremidade padrão para o MongoDB: mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="65eed-130">In this article, we assume that you use hello default installation and server endpoints for MongoDB: mongodb://localhost.</span></span>
> 
> 

## <a name="4-install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="65eed-131">4: instalar Olá restify módulos na sua API da web</span><span class="sxs-lookup"><span data-stu-id="65eed-131">4: Install hello restify modules in your web API</span></span>
<span data-ttu-id="65eed-132">Usamos Resitfy toobuild nossa API REST.</span><span class="sxs-lookup"><span data-stu-id="65eed-132">We use Resitfy toobuild our REST API.</span></span> <span data-ttu-id="65eed-133">O Restify é uma estrutura de aplicativo do Node.js mínima e flexível, derivada do Express.</span><span class="sxs-lookup"><span data-stu-id="65eed-133">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="65eed-134">Restify tem um conjunto robusto de recursos que você pode usar toobuild APIs REST sobre conectar.</span><span class="sxs-lookup"><span data-stu-id="65eed-134">Restify has a robust set of features that you can use toobuild REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="65eed-135">Instalar o Restify</span><span class="sxs-lookup"><span data-stu-id="65eed-135">Install restify</span></span>
1.  <span data-ttu-id="65eed-136">Em um prompt de comando, altere o diretório de saudação muito**azuread**:</span><span class="sxs-lookup"><span data-stu-id="65eed-136">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

    <span data-ttu-id="65eed-137">Se hello **doWindows Azure** diretório não existe, criá-lo:</span><span class="sxs-lookup"><span data-stu-id="65eed-137">If hello **azuread** directory does not exist, create it:</span></span>

    `mkdir azuread`

2.  <span data-ttu-id="65eed-138">Instale o Restify:</span><span class="sxs-lookup"><span data-stu-id="65eed-138">Install restify:</span></span>

    `npm install restify`

    <span data-ttu-id="65eed-139">saída de Hello desse comando deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="65eed-139">hello output of this command should look like this:</span></span>

    ```
    restify@2.6.1 node_modules/restify
    ├── assert-plus@0.1.4
    ├── once@1.3.0
    ├── deep-equal@0.0.0
    ├── escape-regexp-component@1.0.2
    ├── qs@0.6.5
    ├── tunnel-agent@0.3.0
    ├── keep-alive-agent@0.0.1
    ├── lru-cache@2.3.1
    ├── node-uuid@1.4.0
    ├── negotiator@0.3.0
    ├── mime@1.2.11
    ├── semver@2.2.1
    ├── spdy@1.14.12
    ├── backoff@2.3.0
    ├── formidable@1.0.14
    ├── verror@1.3.6 (extsprintf@1.0.2)
    ├── csv@0.3.6
    ├── http-signature@0.10.0 (assert-plus@0.1.2, asn1@0.1.11, ctype@0.5.2)
    └── bunyan@0.22.0(mv@0.0.5)
    ```

#### <a name="did-you-get-an-error"></a><span data-ttu-id="65eed-140">Você obteve um erro?</span><span class="sxs-lookup"><span data-stu-id="65eed-140">Did you get an error?</span></span>
<span data-ttu-id="65eed-141">Em alguns sistemas operacionais, quando você usa Olá `npm` de comando, você verá esta mensagem: `Error: EPERM, chmod '/usr/local/bin/..'`.</span><span class="sxs-lookup"><span data-stu-id="65eed-141">On some operating systems, when you use hello `npm` command, you might see this message: `Error: EPERM, chmod '/usr/local/bin/..'`.</span></span> <span data-ttu-id="65eed-142">Erro de saudação é seguido por uma solicitação que você tente conta de saudação em execução como administrador.</span><span class="sxs-lookup"><span data-stu-id="65eed-142">hello error is followed by a request that you try running hello account as an administrator.</span></span> <span data-ttu-id="65eed-143">Se isso ocorrer, use o comando Olá `sudo` toorun `npm` em um nível de privilégio mais alto.</span><span class="sxs-lookup"><span data-stu-id="65eed-143">If this occurs, use hello command `sudo` toorun `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-related-toodtrace"></a><span data-ttu-id="65eed-144">Você obteve um erro relacionado tooDTrace?</span><span class="sxs-lookup"><span data-stu-id="65eed-144">Did you get an error related tooDTrace?</span></span>
<span data-ttu-id="65eed-145">Quando você instala o restify, pode ver esta mensagem:</span><span class="sxs-lookup"><span data-stu-id="65eed-145">When you install restify, you might see this message:</span></span>

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: two
gyp ERR! stack     at ChildProcess.onExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:267:23)
gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:789:12)
gyp ERR! System Darwin 13.1.0
gyp ERR! command "node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Volumes/Development HD/azuread/node_modules/restify/node_modules/dtrace-provider
gyp ERR! node -v v0.10.11
gyp ERR! node-gyp -v v0.10.0
gyp ERR! not ok
npm WARN optional dep failed, continuing dtrace-provider@0.2.8
```

<span data-ttu-id="65eed-146">Restify tem um tootrace poderoso mecanismo chamadas REST usando DTrace.</span><span class="sxs-lookup"><span data-stu-id="65eed-146">Restify has a powerful mechanism tootrace REST calls by using DTrace.</span></span> <span data-ttu-id="65eed-147">No entanto, o DTrace não está disponível em muitos sistemas operacionais.</span><span class="sxs-lookup"><span data-stu-id="65eed-147">However, DTrace is not available on many operating systems.</span></span> <span data-ttu-id="65eed-148">Você pode ignorar essa mensagem de erro com segurança.</span><span class="sxs-lookup"><span data-stu-id="65eed-148">You can safely ignore this error message.</span></span>


## <a name="5-install-passportjs-in-your-web-api"></a><span data-ttu-id="65eed-149">5: instalar o Passport.js na sua API Web</span><span class="sxs-lookup"><span data-stu-id="65eed-149">5: Install Passport.js in your web API</span></span>
1.  <span data-ttu-id="65eed-150">No prompt de comando hello, altere o diretório de saudação muito**azuread**.</span><span class="sxs-lookup"><span data-stu-id="65eed-150">At hello command prompt, change hello directory too**azuread**.</span></span>

2.  <span data-ttu-id="65eed-151">Instale o Passport.js:</span><span class="sxs-lookup"><span data-stu-id="65eed-151">Install Passport.js:</span></span>

    `npm install passport`

    <span data-ttu-id="65eed-152">saída de saudação do comando Olá deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="65eed-152">hello output of hello command should look like this:</span></span>

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-tooyour-web-api"></a><span data-ttu-id="65eed-153">6: Adicionar de API da web do ad de azure passport tooyour</span><span class="sxs-lookup"><span data-stu-id="65eed-153">6: Add passport-azure-ad tooyour web API</span></span>
<span data-ttu-id="65eed-154">Em seguida, adicione a estratégia de OAuth Olá, usando o passport-doWindows Azure.</span><span class="sxs-lookup"><span data-stu-id="65eed-154">Next, add hello OAuth strategy, by using passport-azuread.</span></span> <span data-ttu-id="65eed-155">`passport-azuread` é um pacote de estratégias que conectam o Azure AD ao Passport.</span><span class="sxs-lookup"><span data-stu-id="65eed-155">`passport-azuread` is a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="65eed-156">Usaremos essa estratégia para tokens de portador neste exemplo de API Rest.</span><span class="sxs-lookup"><span data-stu-id="65eed-156">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="65eed-157">Embora o OAuth 2.0 forneça uma estrutura na qual qualquer tipo de token conhecido possa ser emitido, determinados tipos de token são comumente usados.</span><span class="sxs-lookup"><span data-stu-id="65eed-157">Although OAuth 2.0 provides a framework in which any known token type can be issued, certain token types are commonly used.</span></span> <span data-ttu-id="65eed-158">Os tokens de portador são pontos de extremidade de tooprotect usadas com frequência.</span><span class="sxs-lookup"><span data-stu-id="65eed-158">Bearer tokens are commonly used tooprotect endpoints.</span></span> <span data-ttu-id="65eed-159">Tokens de portador são tipo de hello mais amplamente emitido de token do OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="65eed-159">Bearer tokens are hello most widely issued type of token in OAuth 2.0.</span></span> <span data-ttu-id="65eed-160">Muitas implementações do OAuth 2.0 supõem que os tokens de portador são Olá único tipo de token emitido.</span><span class="sxs-lookup"><span data-stu-id="65eed-160">Many OAuth 2.0 implementations assume that bearer tokens are hello only type of token issued.</span></span>
> 
> 

1.  <span data-ttu-id="65eed-161">Em um prompt de comando, altere o diretório de saudação muito**azuread**.</span><span class="sxs-lookup"><span data-stu-id="65eed-161">At a command prompt, change hello directory too**azuread**.</span></span>

    `cd azuread`

2.  <span data-ttu-id="65eed-162">Instalar Olá Passport.js `passport-azure-ad` módulo:</span><span class="sxs-lookup"><span data-stu-id="65eed-162">Install hello Passport.js `passport-azure-ad` module:</span></span>

    `npm install passport-azure-ad`

    <span data-ttu-id="65eed-163">saída de saudação do comando Olá deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="65eed-163">hello output of hello command should look like this:</span></span>

    ```
    passport-azure-ad@1.0.0 node_modules/passport-azure-ad
    ├── xtend@4.0.0
    ├── xmldom@0.1.19
    ├── passport-http-bearer@1.0.1 (passport-strategy@1.0.0)
    ├── underscore@1.8.3
    ├── async@1.3.0
    ├── jsonwebtoken@5.0.2
    ├── xml-crypto@0.5.27 (xpath.js@1.0.6)
    ├── ursa@0.8.5 (bindings@1.2.1, nan@1.8.4)
    ├── jws@3.0.0 (jwa@1.0.1, base64url@1.0.4)
    ├── request@2.58.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, tunnel-agent@0.4.1, oauth-sign@0.8.0, isstream@0.1.2, extend@2.0.1, json-stringify-safe@5.0.1, node-uuid@1.4.3, qs@3.1.0, combined-stream@1.0.5, mime-types@2.0.14, form-data@1.0.0-rc1, http-signature@0.11.0, bl@0.9.4, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    └── xml2js@0.4.9 (sax@0.6.1, xmlbuilder@2.6.4)
    ```

## <a name="7-add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="65eed-164">7: Adicionar MongoDB módulos tooyour web API</span><span class="sxs-lookup"><span data-stu-id="65eed-164">7: Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="65eed-165">Neste exemplo, usamos o MongoDB como nosso armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="65eed-165">In this sample, we use MongoDB as our data store.</span></span> 

1.  <span data-ttu-id="65eed-166">Instalar Mongoose, amplamente utilizado plug-in, toomanage modelos e esquemas:</span><span class="sxs-lookup"><span data-stu-id="65eed-166">Install Mongoose, a widely used plug-in, toomanage models and schemas:</span></span> 

    `npm install mongoose`

2.  <span data-ttu-id="65eed-167">Instale o driver de banco de dados de saudação para o MongoDB, que também é chamado MongoDB:</span><span class="sxs-lookup"><span data-stu-id="65eed-167">Install hello database driver for MongoDB, which is also called MongoDB:</span></span>

    `npm install mongodb`

## <a name="8-install-additional-modules"></a><span data-ttu-id="65eed-168">8: instalar módulos adicionais</span><span class="sxs-lookup"><span data-stu-id="65eed-168">8: Install additional modules</span></span>
<span data-ttu-id="65eed-169">Instale Olá restantes módulos necessários.</span><span class="sxs-lookup"><span data-stu-id="65eed-169">Install hello remaining required modules.</span></span>

1.  <span data-ttu-id="65eed-170">Em um prompt de comando, altere o diretório de saudação muito**azuread**:</span><span class="sxs-lookup"><span data-stu-id="65eed-170">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="65eed-171">Digite hello comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="65eed-171">Enter hello following commands.</span></span> <span data-ttu-id="65eed-172">comandos de saudação instalam Olá módulos no diretório node_modules a seguir:</span><span class="sxs-lookup"><span data-stu-id="65eed-172">hello commands install hello following modules in your node_modules directory:</span></span>

    *   `npm install crypto`
    *   `npm install assert-plus`
    *   `npm install posix-getopt`
    *   `npm install util`
    *   `npm install path`
    *   `npm install connect`
    *   `npm install xml-crypto`
    *   `npm install xml2js`
    *   `npm install xmldom`
    *   `npm install async`
    *   `npm install request`
    *   `npm install underscore`
    *   `npm install grunt-contrib-jshint@0.1.1`
    *   `npm install grunt-contrib-nodeunit@0.1.2`
    *   `npm install grunt-contrib-watch@0.2.0`
    *   `npm install grunt@0.4.1`
    *   `npm install xtend@2.0.3`
    *   `npm install bunyan`
    *   `npm update`

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a><span data-ttu-id="65eed-173">9: criar um arquivo Server.js para suas dependências</span><span class="sxs-lookup"><span data-stu-id="65eed-173">9: Create a Server.js file for your dependencies</span></span>
<span data-ttu-id="65eed-174">Um arquivo Server.js mantém maioria de saudação da funcionalidade de saudação do seu servidor de API da web.</span><span class="sxs-lookup"><span data-stu-id="65eed-174">A Server.js file holds hello majority of hello functionality for your web API server.</span></span> <span data-ttu-id="65eed-175">Adicione mais seu toothis do arquivo de código.</span><span class="sxs-lookup"><span data-stu-id="65eed-175">Add most of your code toothis file.</span></span> <span data-ttu-id="65eed-176">Para fins de produção, você pode refatorar funcionalidade Olá em arquivos menores, como para controladores e rotas separadas.</span><span class="sxs-lookup"><span data-stu-id="65eed-176">For production purposes, you can refactor hello functionality into smaller files, like for separate routes and controllers.</span></span> <span data-ttu-id="65eed-177">Neste artigo, usaremos Server.js para essa finalidade.</span><span class="sxs-lookup"><span data-stu-id="65eed-177">In this article, we use Server.js for this purpose.</span></span>

1.  <span data-ttu-id="65eed-178">Em um prompt de comando, altere o diretório de saudação muito**azuread**:</span><span class="sxs-lookup"><span data-stu-id="65eed-178">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="65eed-179">Usando um editor de sua escolha, crie um arquivo Server.js.</span><span class="sxs-lookup"><span data-stu-id="65eed-179">Using an editor of your choice, create a Server.js file.</span></span> <span data-ttu-id="65eed-180">Adicione Olá arquivo toohello de informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="65eed-180">Add hello following information toohello file:</span></span>

    ```Javascript
    'use strict';
    /**
    * Module dependencies.
    */
    var util = require('util');
    var assert = require('assert-plus');
    var mongoose = require('mongoose/');
    var bunyan = require('bunyan');
    var restify = require('restify');
    var config = require('./config');
    var passport = require('passport');
    var OIDCBearerStrategy = require('passport-azure-ad').OIDCStrategy;
    ```

3.  <span data-ttu-id="65eed-181">Salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="65eed-181">Save hello file.</span></span> <span data-ttu-id="65eed-182">Você retornará tooit em breve.</span><span class="sxs-lookup"><span data-stu-id="65eed-182">You will return tooit shortly.</span></span>

## <a name="10-create-a-config-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="65eed-183">10: criar um toostore do arquivo de configuração suas configurações do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="65eed-183">10: Create a config file toostore your Azure AD settings</span></span>
<span data-ttu-id="65eed-184">Arquivo de código passa parâmetros de configuração de saudação de seu tooPassport.js portal do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="65eed-184">This code file passes hello configuration parameters from your Azure AD portal tooPassport.js.</span></span> <span data-ttu-id="65eed-185">Você criou esses valores de configuração quando você adicionou o portal de toohello Olá web API no início de saudação do artigo hello.</span><span class="sxs-lookup"><span data-stu-id="65eed-185">You created these configuration values when you added hello web API toohello portal at hello beginning of hello article.</span></span> <span data-ttu-id="65eed-186">Depois de copiar código Olá, vamos explicar quais tooput em valores hello desses parâmetros.</span><span class="sxs-lookup"><span data-stu-id="65eed-186">After you copy hello code, we'll explain what tooput in hello values of these parameters.</span></span>

1.  <span data-ttu-id="65eed-187">Em um prompt de comando, altere o diretório de saudação muito**azuread**:</span><span class="sxs-lookup"><span data-stu-id="65eed-187">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="65eed-188">Em um editor, crie um arquivo Config.js.</span><span class="sxs-lookup"><span data-stu-id="65eed-188">In an editor, create a Config.js file.</span></span> <span data-ttu-id="65eed-189">Adicione Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="65eed-189">Add hello following information:</span></span>

    ```Javascript
    // Don't commit this file tooyour public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need toochange this.
    };

    ```



### <a name="required-values"></a><span data-ttu-id="65eed-190">Valores necessários</span><span class="sxs-lookup"><span data-stu-id="65eed-190">Required values</span></span>

*   <span data-ttu-id="65eed-191">**IdentityMetadata**: isso é onde `passport-azure-ad` procura os dados de configuração para o provedor de identidade (IDP) do hello e Olá chaves toovalidate Olá JSON Web Tokens (JWTs).</span><span class="sxs-lookup"><span data-stu-id="65eed-191">**IdentityMetadata**: This is where `passport-azure-ad` looks for your configuration data for hello identity provider (IDP) and hello keys toovalidate hello JSON Web Tokens (JWTs).</span></span> <span data-ttu-id="65eed-192">Se você estiver usando o AD do Azure, não convém toochange isso.</span><span class="sxs-lookup"><span data-stu-id="65eed-192">If you are using Azure AD, you probably don't want toochange this.</span></span>

*   <span data-ttu-id="65eed-193">**público-alvo**: O URI de redirecionamento do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="65eed-193">**audience**: Your redirect URI from hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="65eed-194">Reverta suas chaves em intervalos frequentes.</span><span class="sxs-lookup"><span data-stu-id="65eed-194">Roll your keys at frequent intervals.</span></span> <span data-ttu-id="65eed-195">Certifique-se de que você sempre efetuar pull de URL de "openid_keys" Olá, e que o aplicativo hello possa acessar Olá da Internet.</span><span class="sxs-lookup"><span data-stu-id="65eed-195">Be sure that you always pull from hello "openid_keys" URL, and that hello app can access hello Internet.</span></span>
> 
> 

## <a name="11-add-hello-configuration-tooyour-serverjs-file"></a><span data-ttu-id="65eed-196">11: Adicionar Olá configuração tooyour Server.js arquivo</span><span class="sxs-lookup"><span data-stu-id="65eed-196">11: Add hello configuration tooyour Server.js file</span></span>
<span data-ttu-id="65eed-197">Seu aplicativo precisa tooread valores de saudação do arquivo de configuração de saudação que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="65eed-197">Your application needs tooread hello values from hello config file you just created.</span></span> <span data-ttu-id="65eed-198">Adicione o arquivo. config de saudação como um recurso necessário em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="65eed-198">Add hello .config file as a required resource in your application.</span></span> <span data-ttu-id="65eed-199">Definir Olá toothose de variáveis globais que estão em Config.js.</span><span class="sxs-lookup"><span data-stu-id="65eed-199">Set hello global variables toothose that are in Config.js.</span></span>

1.  <span data-ttu-id="65eed-200">No prompt de comando hello, altere o diretório de saudação muito**azuread**:</span><span class="sxs-lookup"><span data-stu-id="65eed-200">At hello command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="65eed-201">Em um editor, abra o Server.js.</span><span class="sxs-lookup"><span data-stu-id="65eed-201">In an editor, open Server.js.</span></span> <span data-ttu-id="65eed-202">Adicione Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="65eed-202">Add hello following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```

3.  <span data-ttu-id="65eed-203">Adicione um novo tooServer.js de seção:</span><span class="sxs-lookup"><span data-stu-id="65eed-203">Add a new section tooServer.js:</span></span>

    ```Javascript
    // Pass these options in toohello ODICBearerStrategy.
    var options = {
    // hello URL of hello metadata document for your app. Put hello keys for token validation from hello URL found in hello jwks_uri tag in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array toohold signed-in users and hello current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="65eed-204">12: Adicionar Olá MongoDB modelo e informações de esquema usando Mongoose</span><span class="sxs-lookup"><span data-stu-id="65eed-204">12: Add hello MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="65eed-205">Em seguida, conecte esses três arquivos em um serviço de API REST.</span><span class="sxs-lookup"><span data-stu-id="65eed-205">Next, connect these three files in a REST API service.</span></span>

<span data-ttu-id="65eed-206">Neste artigo, usamos o MongoDB toostore nosso tarefas.</span><span class="sxs-lookup"><span data-stu-id="65eed-206">In this article, we use MongoDB toostore our tasks.</span></span> <span data-ttu-id="65eed-207">Abordaremos isso na *etapa 4*.</span><span class="sxs-lookup"><span data-stu-id="65eed-207">We discuss this in *step 4*.</span></span>

<span data-ttu-id="65eed-208">No arquivo de Config.js Olá criado na etapa 11, o banco de dados é chamado *tasklist*.</span><span class="sxs-lookup"><span data-stu-id="65eed-208">In hello Config.js file you created in step 11, your database is called *tasklist*.</span></span> <span data-ttu-id="65eed-209">Isso é o que é colocado no final da saudação da sua URL de conexão mongoose_auth_local.</span><span class="sxs-lookup"><span data-stu-id="65eed-209">That was what you put at hello end of your mongoose_auth_local connection URL.</span></span> <span data-ttu-id="65eed-210">Você não precisa toocreate banco de dados com antecedência no MongoDB.</span><span class="sxs-lookup"><span data-stu-id="65eed-210">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="65eed-211">Olá banco de dados é criado no hello primeiro execução do seu aplicativo de servidor (supondo que o banco de dados de saudação ainda não existir).</span><span class="sxs-lookup"><span data-stu-id="65eed-211">hello database is created on hello first run of your server application (assuming hello database does not already exist).</span></span>

<span data-ttu-id="65eed-212">Você informou servidor Olá que toouse de banco de dados do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="65eed-212">You've told hello server what MongoDB database toouse.</span></span> <span data-ttu-id="65eed-213">Em seguida, você precisa toowrite alguns adicionais toocreate Olá modelo e código de esquema para tarefas do servidor.</span><span class="sxs-lookup"><span data-stu-id="65eed-213">Next, you need toowrite some additional code toocreate hello model and schema for your server's tasks.</span></span>

### <a name="hello-model"></a><span data-ttu-id="65eed-214">modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="65eed-214">hello model</span></span>
<span data-ttu-id="65eed-215">modelo de esquema Olá é muito básico.</span><span class="sxs-lookup"><span data-stu-id="65eed-215">hello schema model is very basic.</span></span> <span data-ttu-id="65eed-216">Você pode expandi-lo se necessário.</span><span class="sxs-lookup"><span data-stu-id="65eed-216">You can expand it if you need to.</span></span> 

<span data-ttu-id="65eed-217">modelo de esquema Olá tem estes valores:</span><span class="sxs-lookup"><span data-stu-id="65eed-217">hello schema model has these values:</span></span>

*   <span data-ttu-id="65eed-218">**NAME**.</span><span class="sxs-lookup"><span data-stu-id="65eed-218">**NAME**.</span></span> <span data-ttu-id="65eed-219">Olá pessoa toohello atribuído a tarefa.</span><span class="sxs-lookup"><span data-stu-id="65eed-219">hello person assigned toohello task.</span></span> <span data-ttu-id="65eed-220">Esse é um valor do tipo **string**.</span><span class="sxs-lookup"><span data-stu-id="65eed-220">This is a **string** value.</span></span>
*   <span data-ttu-id="65eed-221">**TASK**.</span><span class="sxs-lookup"><span data-stu-id="65eed-221">**TASK**.</span></span> <span data-ttu-id="65eed-222">nome de saudação da tarefa de saudação.</span><span class="sxs-lookup"><span data-stu-id="65eed-222">hello name of hello task.</span></span> <span data-ttu-id="65eed-223">Esse é um valor do tipo **string**.</span><span class="sxs-lookup"><span data-stu-id="65eed-223">This is a **string** value.</span></span>
*   <span data-ttu-id="65eed-224">**DATE**.</span><span class="sxs-lookup"><span data-stu-id="65eed-224">**DATE**.</span></span> <span data-ttu-id="65eed-225">Data de saudação tarefa hello está vencida.</span><span class="sxs-lookup"><span data-stu-id="65eed-225">hello date that hello task is due.</span></span> <span data-ttu-id="65eed-226">Esse é um valor do tipo **datetime**.</span><span class="sxs-lookup"><span data-stu-id="65eed-226">This is a **datetime** value.</span></span>
*   <span data-ttu-id="65eed-227">**COMPLETED**.</span><span class="sxs-lookup"><span data-stu-id="65eed-227">**COMPLETED**.</span></span> <span data-ttu-id="65eed-228">Se a tarefa de saudação é concluída.</span><span class="sxs-lookup"><span data-stu-id="65eed-228">Whether hello task is completed.</span></span> <span data-ttu-id="65eed-229">Esse é um valor do tipo **Boolean**.</span><span class="sxs-lookup"><span data-stu-id="65eed-229">This is a **Boolean** value.</span></span>

### <a name="create-hello-schema-in-hello-code"></a><span data-ttu-id="65eed-230">Criar esquema Olá no código de saudação</span><span class="sxs-lookup"><span data-stu-id="65eed-230">Create hello schema in hello code</span></span>
1.  <span data-ttu-id="65eed-231">Em um prompt de comando, altere o diretório de saudação muito**azuread**:</span><span class="sxs-lookup"><span data-stu-id="65eed-231">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="65eed-232">No editor, abra o Server.js.</span><span class="sxs-lookup"><span data-stu-id="65eed-232">In your editor, open Server.js.</span></span> <span data-ttu-id="65eed-233">Abaixo da entrada de configuração hello, adicione Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="65eed-233">Below hello configuration entry, add hello following information:</span></span>

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

<span data-ttu-id="65eed-234">Esse código conecta toohello MongoDB server.</span><span class="sxs-lookup"><span data-stu-id="65eed-234">This code connects toohello MongoDB server.</span></span> <span data-ttu-id="65eed-235">Ele também retorna um objeto de esquema.</span><span class="sxs-lookup"><span data-stu-id="65eed-235">It also returns a schema object.</span></span>

#### <a name="using-hello-schema-create-your-model-in-hello-code"></a><span data-ttu-id="65eed-236">Usando o esquema de hello, criar seu modelo no código de saudação</span><span class="sxs-lookup"><span data-stu-id="65eed-236">Using hello schema, create your model in hello code</span></span>
<span data-ttu-id="65eed-237">Abaixo Olá precede o código, adicione Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="65eed-237">Below hello preceding code, add hello following code:</span></span>

```Javascript
// Create a basic schema toostore your tasks and users.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use hello schema tooregister a model.
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```

<span data-ttu-id="65eed-238">Como você pode ver no código hello, primeiro crie o esquema.</span><span class="sxs-lookup"><span data-stu-id="65eed-238">As you can tell from hello code, first you create your schema.</span></span> <span data-ttu-id="65eed-239">Em seguida, você cria um objeto do modelo.</span><span class="sxs-lookup"><span data-stu-id="65eed-239">Next, you create a model object.</span></span> <span data-ttu-id="65eed-240">Usar toostore de objeto de modelo Olá seus dados durante a saudação de código ao definir sua **rotas**.</span><span class="sxs-lookup"><span data-stu-id="65eed-240">You use hello model object toostore your data throughout hello code when you define your **routes**.</span></span>

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a><span data-ttu-id="65eed-241">13: adicionar as rotas ao servidor de API REST da tarefa</span><span class="sxs-lookup"><span data-stu-id="65eed-241">13: Add your routes for your task REST API server</span></span>
<span data-ttu-id="65eed-242">Agora que você tem um toowork de modelo de banco de dados com o, adicione rotas Olá que você usará para seu servidor de API REST.</span><span class="sxs-lookup"><span data-stu-id="65eed-242">Now that you have a database model toowork with, add hello routes you'll use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="65eed-243">Sobre rotas no Restify</span><span class="sxs-lookup"><span data-stu-id="65eed-243">About routes in restify</span></span>
<span data-ttu-id="65eed-244">Rotas de restify trabalho exatamente hello mesma forma, quando você usar Olá pilha Express.</span><span class="sxs-lookup"><span data-stu-id="65eed-244">Routes in restify work exactly hello same way they do when you use hello Express stack.</span></span> <span data-ttu-id="65eed-245">Definir rotas usando Olá URI que você espera Olá toocall de aplicativos de cliente.</span><span class="sxs-lookup"><span data-stu-id="65eed-245">You define routes by using hello URI that you expect hello client applications toocall.</span></span> <span data-ttu-id="65eed-246">Normalmente, você define suas rotas em um arquivo separado.</span><span class="sxs-lookup"><span data-stu-id="65eed-246">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="65eed-247">Neste tutorial, colocamos nossa rotas no Server.js.</span><span class="sxs-lookup"><span data-stu-id="65eed-247">In this tutorial, we put our routes in Server.js.</span></span> <span data-ttu-id="65eed-248">Para uso em produção, recomendamos que você coloque as rotas no próprio arquivo delas.</span><span class="sxs-lookup"><span data-stu-id="65eed-248">For production use, we recommend that you factor routes into their own file.</span></span>

<span data-ttu-id="65eed-249">Eis um padrão típico para uma rota de Restify:</span><span class="sxs-lookup"><span data-stu-id="65eed-249">A typical pattern for a restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep hello server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


<span data-ttu-id="65eed-250">Este é o padrão de saudação no nível mais básico de saudação.</span><span class="sxs-lookup"><span data-stu-id="65eed-250">This is hello pattern at hello most basic level.</span></span> <span data-ttu-id="65eed-251">Restify (e Express) fornecem muito mais funcionalidades, como tipos de aplicativo hello capacidade toodefine e roteamento complexas entre diferentes pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="65eed-251">Restify (and Express) provide much deeper functionality, like hello ability toodefine application types, and complex routing across different endpoints.</span></span>

#### <a name="add-default-routes-tooyour-server"></a><span data-ttu-id="65eed-252">Adicionar servidor de tooyour rotas padrão</span><span class="sxs-lookup"><span data-stu-id="65eed-252">Add default routes tooyour server</span></span>
<span data-ttu-id="65eed-253">Adicionar rotas CRUD básicas Olá: **criar**, **recuperar**, **atualizar**, e **excluir**.</span><span class="sxs-lookup"><span data-stu-id="65eed-253">Add hello basic CRUD routes: **create**, **retrieve**, **update**, and **delete**.</span></span>

1.  <span data-ttu-id="65eed-254">Em um prompt de comando, altere o diretório de saudação muito**azuread**:</span><span class="sxs-lookup"><span data-stu-id="65eed-254">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="65eed-255">Em um editor, abra o Server.js.</span><span class="sxs-lookup"><span data-stu-id="65eed-255">In an editor, open Server.js.</span></span> <span data-ttu-id="65eed-256">Abaixo Olá entradas do banco de dados que você fez anteriormente, adicionar Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="65eed-256">Below hello database entries you made earlier, add hello following information:</span></span>

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow you toouse MongoDB Server as your response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it tooMongoDB.
    var _task = new Task();
    if (!req.params.task) {
    req.log.warn({
    params: p
    }, 'createTodo: missing task');
    next(new MissingTaskError());
    return;
    }
    _task.owner = owner;
    _task.task = req.params.task;
    _task.date = new Date();
    _task.save(function(err) {
    if (err) {
    req.log.warn(err, 'createTask: unable toosave');
    next(err);
    } else {
    res.send(201, _task);
    }
    });
    return next();
    }
    // Delete a task by name.
    function removeTask(req, res, next) {
    Task.remove({
    task: req.params.task,
    owner: owner
    }, function(err) {
    if (err) {
    req.log.warn(err,
    'removeTask: unable toodelete %s',
    req.params.task);
    next(err);
    } else {
    log.info('Deleted task:', req.params.task);
    res.send(204);
    next();
    }
    });
    }
    // Delete all tasks.
    function removeAll(req, res, next) {
    Task.remove();
    res.send(204);
    return next();
    }
    // Get a specific task based on name.
    function getTask(req, res, next) {
    log.info('getTask was called for: ', owner);
    Task.find({
    owner: owner
    }, function(err, data) {
    if (err) {
    req.log.warn(err, 'get: unable tooread %s', owner);
    next(err);
    return;
    }
    res.json(data);
    });
    return next();
    }
    /// Returns hello list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow us toouse MongoDB Server as our response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    log.info("listTasks was called for: ", owner);
    Task.find({
    owner: owner
    }).limit(20).sort('date').exec(function(err, data) {
    if (err)
    return next(err);
    if (data.length > 0) {
    log.info(data);
    }
    if (!data.length) {
    log.warn(err, "There are no tasks in hello database. Add one!");
    }
    if (!owner) {
    log.warn(err, "You did not pass an owner when listing tasks.");
    } else {
    res.json(data);
    }
    });
    return next();
    }
    ```

### <a name="add-error-handling-for-hello-routes"></a><span data-ttu-id="65eed-257">Adicionar o tratamento de erros para rotas de saudação</span><span class="sxs-lookup"><span data-stu-id="65eed-257">Add error handling for hello routes</span></span>
<span data-ttu-id="65eed-258">Adicione alguns tratamento de erros para que possa se comunicar toohello back cliente sobre o problema de saudação encontrado.</span><span class="sxs-lookup"><span data-stu-id="65eed-258">Add some error handling so you can communicate back toohello client about hello problem you encountered.</span></span>

<span data-ttu-id="65eed-259">Adicione Olá código abaixo o código de saudação, que você já escreveu a seguir:</span><span class="sxs-lookup"><span data-stu-id="65eed-259">Add hello following code below hello code, which you've already written:</span></span>

```Javascript
///--- Errors for communicating something more information back toohello client.
function MissingTaskError() {
restify.RestError.call(this, {
statusCode: 409,
restCode: 'MissingTask',
message: '"task" is a required parameter',
constructorOpt: MissingTaskError
});
this.name = 'MissingTaskError';
}
util.inherits(MissingTaskError, restify.RestError);
function TaskExistsError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 409,
restCode: 'TaskExists',
message: owner + ' already exists',
constructorOpt: TaskExistsError
});
this.name = 'TaskExistsError';
}
util.inherits(TaskExistsError, restify.RestError);
function TaskNotFoundError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 404,
restCode: 'TaskNotFound',
message: owner + ' was not found',
constructorOpt: TaskNotFoundError
});
this.name = 'TaskNotFoundError';
}
util.inherits(TaskNotFoundError, restify.RestError);
```


## <a name="14-create-your-server"></a><span data-ttu-id="65eed-260">14: criar seu servidor</span><span class="sxs-lookup"><span data-stu-id="65eed-260">14: Create your server</span></span>
<span data-ttu-id="65eed-261">Olá toodo de última coisa é tooadd sua instância de servidor.</span><span class="sxs-lookup"><span data-stu-id="65eed-261">hello last thing toodo is tooadd your server instance.</span></span> <span data-ttu-id="65eed-262">instância do servidor de saudação gerencia suas chamadas.</span><span class="sxs-lookup"><span data-stu-id="65eed-262">hello server instance manages your calls.</span></span>

<span data-ttu-id="65eed-263">O Restify (e Express) têm personalização profunda que pode ser usada com um servidor de API REST.</span><span class="sxs-lookup"><span data-stu-id="65eed-263">Restify (and Express) have deep customization that you can use with a REST API server.</span></span> <span data-ttu-id="65eed-264">Neste tutorial, usamos a configuração mais básica do hello.</span><span class="sxs-lookup"><span data-stu-id="65eed-264">In this tutorial, we use hello most basic setup.</span></span>

```Javascript
/**
* Your server
*/
var server = restify.createServer({
name: "Microsoft Azure Active Directory TODO Server",
version: "2.0.1"
});
// Ensure that you don't drop data on uploads.
server.pre(restify.pre.pause());
// Clean up imprecise paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());
// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());
// Set a per-request Bunyan logger (with requestid filled in).
server.use(restify.requestLogger());
// Allow 5 requests/second by IP address, and burst too10.
server.use(restify.throttle({
burst: 10,
rate: 5,
ip: true,
}));
// Use common commands, such as:
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
mapParams: true
}));
```
## <a name="15-add-hello-routes-without-authentication-for-now"></a><span data-ttu-id="65eed-265">15: adicionar rotas hello (sem autenticação, por enquanto)</span><span class="sxs-lookup"><span data-stu-id="65eed-265">15: Add hello routes (without authentication, for now)</span></span>
```Javascript
/// Use CRUD tooadd hello real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in hello pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need toomaintain session state. You can experiment with removing API protection.
/* toodo this, remove hello passport.authenticate() method:
/*
/* server.get('/tasks', listTasks);
/*
**/
server.get('/tasks', listTasks);
server.get('/tasks', listTasks);
server.get('/tasks/:owner', getTask);
server.head('/tasks/:owner', getTask);
server.post('/tasks/:owner/:task', createTask);
server.post('/tasks', createTask);
server.del('/tasks/:owner/:task', removeTask);
server.del('/tasks/:owner', removeTask);
server.del('/tasks', removeTask);
server.del('/tasks', removeAll, function respond(req, res, next) {
res.send(204);
next();
});
// Register a default '/' handler
server.get('/', function root(req, res, next) {
var routes = [
'GET /',
'POST /tasks/:owner/:task',
'POST /tasks (for JSON body)',
'GET /tasks',
'PUT /tasks/:owner',
'GET /tasks/:owner',
'DELETE /tasks/:owner/:task'
];
res.send(200, routes);
next();
});
server.listen(serverPort, function() {
var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
consoleMessage += '\n %s server is listening at %s';
consoleMessage += '\n Open your browser too%s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-run-hello-server"></a><span data-ttu-id="65eed-266">16: executar o servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="65eed-266">16: Run hello server</span></span>
<span data-ttu-id="65eed-267">É uma boa ideia tootest seu servidor antes de adicionar a autenticação.</span><span class="sxs-lookup"><span data-stu-id="65eed-267">It's a good idea tootest your server before you add authentication.</span></span>

<span data-ttu-id="65eed-268">Olá tootest de maneira mais fácil o servidor está usando ondulação no prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="65eed-268">hello easiest way tootest your server is by using curl at a command prompt.</span></span> <span data-ttu-id="65eed-269">toodo isso, é necessário um utilitário simples que você pode usar a saída de tooparse como JSON.</span><span class="sxs-lookup"><span data-stu-id="65eed-269">toodo this, you need a simple utility that you can use tooparse output as JSON.</span></span> 

1.  <span data-ttu-id="65eed-270">Instale a ferramenta JSON de saudação que usamos em Olá exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="65eed-270">Install hello JSON tool that we use in hello following examples:</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="65eed-271">Isso instala a ferramenta JSON de saudação globalmente.</span><span class="sxs-lookup"><span data-stu-id="65eed-271">This installs hello JSON tool globally.</span></span>

2.  <span data-ttu-id="65eed-272">Verifique se a instância do MongoDB está em execução.</span><span class="sxs-lookup"><span data-stu-id="65eed-272">Make sure that your MongoDB instance is running:</span></span>

    `$sudo mongod`

3.  <span data-ttu-id="65eed-273">Altere o diretório de saudação muito**doWindows Azure**, e, em seguida, execute ondulação:</span><span class="sxs-lookup"><span data-stu-id="65eed-273">Change hello directory too**azuread**, and then run curl:</span></span>

    `$ cd azuread`
    `$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 2.0OK
    Connection: close
    Content-Type: application/json
    Content-Length: 171
    Date: Tue, 14 Jul 2015 05:43:38 GMT
    [
    "GET /",
    "POST /tasks/:owner/:task",
    "POST /tasks (for JSON body)",
    "GET /tasks",
    "PUT /tasks/:owner",
    "GET /tasks/:owner",
    "DELETE /tasks/:owner/:task"
    ]
    ```

4.  <span data-ttu-id="65eed-274">tooadd uma tarefa:</span><span class="sxs-lookup"><span data-stu-id="65eed-274">tooadd a task:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    <span data-ttu-id="65eed-275">Olá resposta deve ser:</span><span class="sxs-lookup"><span data-stu-id="65eed-275">hello response should be:</span></span>

    ```Shell
    HTTP/1.1 201 Created
    Connection: close
    Access-Control-Allow-Origin: *
    Access-Control-Allow-Headers: X-Requested-With
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 5
    Date: Tue, 04 Feb 2014 01:02:26 GMT
    Hello
    ```

5.  <span data-ttu-id="65eed-276">Listar tarefas para Brandon:</span><span class="sxs-lookup"><span data-stu-id="65eed-276">List tasks for Brandon:</span></span>

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="65eed-277">Se todos esses comandos são executados sem erros, você está pronto tooadd servidor de API REST de toohello de OAuth.</span><span class="sxs-lookup"><span data-stu-id="65eed-277">If all these commands run without errors, you are ready tooadd OAuth toohello REST API server.</span></span>

<span data-ttu-id="65eed-278">*Agora você tem um servidor de API REST com o MongoDB!*</span><span class="sxs-lookup"><span data-stu-id="65eed-278">*You now have a REST API server with MongoDB!*</span></span>

## <a name="17-add-authentication-tooyour-rest-api-server"></a><span data-ttu-id="65eed-279">17: Adicionar servidor de API REST de tooyour de autenticação</span><span class="sxs-lookup"><span data-stu-id="65eed-279">17: Add authentication tooyour REST API server</span></span>
<span data-ttu-id="65eed-280">Agora que você tem uma API REST em execução, configurá-lo toouse-lo com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65eed-280">Now that you have a running REST API, set it up toouse it with Azure AD.</span></span>

<span data-ttu-id="65eed-281">Em um prompt de comando, altere o diretório de saudação muito**azuread**:</span><span class="sxs-lookup"><span data-stu-id="65eed-281">At a command prompt, change hello directory too**azuread**:</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a><span data-ttu-id="65eed-282">Usar oidcbearerstrategy Olá incluído com o ad de azure passport</span><span class="sxs-lookup"><span data-stu-id="65eed-282">Use hello oidcbearerstrategy that's included with passport-azure-ad</span></span>
<span data-ttu-id="65eed-283">Até agora, você criou um servidor típico TODO do REST sem nenhum tipo de autorização.</span><span class="sxs-lookup"><span data-stu-id="65eed-283">So far, you've built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="65eed-284">Agora, adicione autenticação.</span><span class="sxs-lookup"><span data-stu-id="65eed-284">Now, add authentication.</span></span>

<span data-ttu-id="65eed-285">Primeiro, indique que você deseja toouse Passport.</span><span class="sxs-lookup"><span data-stu-id="65eed-285">First,  indicate that you want toouse Passport.</span></span> <span data-ttu-id="65eed-286">Coloque isso logo após a sua configuração anterior do servidor:</span><span class="sxs-lookup"><span data-stu-id="65eed-286">Put this right after your earlier server configuration:</span></span>

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> <span data-ttu-id="65eed-287">Quando você escreve APIs, é uma boa ideia tooalways link Olá que dados toosomething exclusivo do token Olá Olá usuário não pode falsificar.</span><span class="sxs-lookup"><span data-stu-id="65eed-287">When you write APIs, it's a good idea tooalways link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="65eed-288">Quando esse servidor armazena itens de tarefas, armazena-as com base na ID de assinatura de usuário Olá no token de saudação (chamado por meio de token.sub).</span><span class="sxs-lookup"><span data-stu-id="65eed-288">When this server stores TODO items, it stores them based on hello user subscription ID in hello token (called through token.sub).</span></span> <span data-ttu-id="65eed-289">Você pode colocar Olá token.sub no campo de "proprietário" hello.</span><span class="sxs-lookup"><span data-stu-id="65eed-289">You put hello token.sub in hello “owner” field.</span></span> <span data-ttu-id="65eed-290">Isso garante que somente este usuário pode acessar TODOs do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="65eed-290">This ensures that only that user can access hello user's TODOs.</span></span> <span data-ttu-id="65eed-291">Ninguém pode acessar TODOs Olá que foram inseridos.</span><span class="sxs-lookup"><span data-stu-id="65eed-291">No one else can access hello TODOs that were entered.</span></span> <span data-ttu-id="65eed-292">Não há nenhuma exposição em hello API para "proprietário".</span><span class="sxs-lookup"><span data-stu-id="65eed-292">There is no exposure in hello API for “owner.”</span></span> <span data-ttu-id="65eed-293">Um usuário externo pode solicitar TODOs de outros usuários, mesmo quando eles estão autenticados.</span><span class="sxs-lookup"><span data-stu-id="65eed-293">An external user can request other users' TODOs, even if they are authenticated.</span></span>
> 
> 

<span data-ttu-id="65eed-294">Em seguida, use a estratégia de portador de conectar-se do Open ID Olá que vem com `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="65eed-294">Next, use hello Open ID Connect Bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="65eed-295">Coloque isto depois do que você colou anteriormente:</span><span class="sxs-lookup"><span data-stu-id="65eed-295">Put this after what you pasted earlier:</span></span>

```Javascript
/**
/*
/* Calling hello OIDCBearerStrategy and managing users.
/*
/* Because of hello Passport pattern, you need toomanage users and info tokens
/* with a FindorCreate() method. hello method must be provided by hello implementor.
/* In hello following code, you autoregister any user and implement a FindById().
/* It's a good idea toodo something more advanced.
**/
var findById = function(id, fn) {
for (var i = 0, len = users.length; i < len; i++) {
var user = users[i];
if (user.sub === id) {
log.info('Found user: ', user);
return fn(null, user);
}
}
return fn(null, null);
};
var oidcStrategy = new OIDCBearerStrategy(options,
function(token, done) {
log.info('verifying hello user');
log.info(token, 'was hello token retrieved');
findById(token.sub, function(err, user) {
if (err) {
return done(err);
}
if (!user) {
// "Auto-registration"
log.info('User was added automatically, because they were new. Their sub is: ', token.sub);
users.push(token);
owner = token.sub;
return done(null, token);
}
owner = token.sub;
return done(null, user, token);
});
}
);
passport.use(oidcStrategy);
```

<span data-ttu-id="65eed-296">O Passport usa um padrão semelhante para todas as suas estratégias (Twitter, Facebook e assim por diante).</span><span class="sxs-lookup"><span data-stu-id="65eed-296">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="65eed-297">Todos os gravadores de estratégia aderem toohello padrão.</span><span class="sxs-lookup"><span data-stu-id="65eed-297">All strategy writers adhere toohello pattern.</span></span> <span data-ttu-id="65eed-298">Passe a estratégia de saudação um `function()` que usa um token e `done` como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="65eed-298">Pass hello strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="65eed-299">estratégia de saudação é retornada depois que ele faz seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="65eed-299">hello strategy is returned after it does all its work.</span></span> <span data-ttu-id="65eed-300">Usuário de saudação do repositório e token de saudação stash para que você não precise tooask para ele novamente.</span><span class="sxs-lookup"><span data-stu-id="65eed-300">Store hello user and stash hello token so you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65eed-301">Olá código anterior usa qualquer usuário que pode autenticar o servidor de tooyour.</span><span class="sxs-lookup"><span data-stu-id="65eed-301">hello preceding code takes any user that can authenticate tooyour server.</span></span> <span data-ttu-id="65eed-302">Isso é conhecido como registro automático.</span><span class="sxs-lookup"><span data-stu-id="65eed-302">This is known as auto-registration.</span></span> <span data-ttu-id="65eed-303">Em um servidor de produção, você não quer toolet qualquer pessoa sem ter que primeiro eles passam por um processo de registro que você escolher.</span><span class="sxs-lookup"><span data-stu-id="65eed-303">On a production server, you wouldn’t want toolet anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="65eed-304">Normalmente, este é o padrão de saudação que consulte em aplicativos de consumidor.</span><span class="sxs-lookup"><span data-stu-id="65eed-304">This is usually hello pattern you see in consumer apps.</span></span> <span data-ttu-id="65eed-305">aplicativo Hello pode permitir tooregister com o Facebook, mas, em seguida, ele solicitará que você tooenter obter informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="65eed-305">hello app might allow you tooregister with Facebook, but then it asks you tooenter additional information.</span></span> <span data-ttu-id="65eed-306">Se não houver um programa de linha de comando para este tutorial, é possível extrair o email de saudação do objeto de token de saudação que é retornado.</span><span class="sxs-lookup"><span data-stu-id="65eed-306">If you weren't using a command-line program for this tutorial, you could extract hello email from hello token object that is returned.</span></span> <span data-ttu-id="65eed-307">Em seguida, você pode solicitar informações adicionais do hello usuário tooenter.</span><span class="sxs-lookup"><span data-stu-id="65eed-307">Then, you might ask hello user tooenter additional information.</span></span> <span data-ttu-id="65eed-308">Como esse é um servidor de teste, você adicionar usuário Olá diretamente toohello memória no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="65eed-308">Because this is a test server, you add hello user directly toohello in-memory database.</span></span>
> 
> 

### <a name="protect-endpoints"></a><span data-ttu-id="65eed-309">Proteger pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="65eed-309">Protect endpoints</span></span>
<span data-ttu-id="65eed-310">Proteger os pontos de extremidade, especificando Olá **passport.authenticate()** chamada com protocolo hello que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="65eed-310">Protect endpoints by specifying hello **passport.authenticate()** call with hello protocol that you want toouse.</span></span>

<span data-ttu-id="65eed-311">Você pode editar sua rota em seu código de servidor para uma opção mais avançada:</span><span class="sxs-lookup"><span data-stu-id="65eed-311">You can edit your route in your server code for a more advanced option:</span></span>

```Javascript
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="18-run-your-server-application-again"></a><span data-ttu-id="65eed-312">18: executar o aplicativo para servidores novamente</span><span class="sxs-lookup"><span data-stu-id="65eed-312">18: Run your server application again</span></span>
<span data-ttu-id="65eed-313">Use curl novamente toosee se você tiver o OAuth 2.0 proteção contra seus pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="65eed-313">Use curl again toosee if you have OAuth 2.0 protection against your endpoints.</span></span> <span data-ttu-id="65eed-314">Faça isso antes de executar qualquer um dos seus SDKs de cliente para esse ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="65eed-314">Do this before you run any of your client SDKs against this endpoint.</span></span> <span data-ttu-id="65eed-315">cabeçalhos de saudação retornados devem informar se a autenticação está funcionando corretamente.</span><span class="sxs-lookup"><span data-stu-id="65eed-315">hello headers returned should tell you if your authentication is working correctly.</span></span>

1.  <span data-ttu-id="65eed-316">Verifique se a instância do MongoDB está em execução:</span><span class="sxs-lookup"><span data-stu-id="65eed-316">Make sure that your MongoDB isntance is running:</span></span>

    `$sudo mongod`

2.  <span data-ttu-id="65eed-317">Alterar toohello **doWindows Azure** diretório e, em seguida, use ondulação:</span><span class="sxs-lookup"><span data-stu-id="65eed-317">Change toohello **azuread** directory, and then use curl:</span></span>

    `$ cd azuread`

    `$ node server.js`

3.  <span data-ttu-id="65eed-318">Tente uma POSTAGEM básica:</span><span class="sxs-lookup"><span data-stu-id="65eed-318">Try a basic POST:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="65eed-319">Uma resposta 401 indica camada Olá Passport está tentando tooredirect toohello autorizar o ponto de extremidade, que é exatamente o que você deseja.</span><span class="sxs-lookup"><span data-stu-id="65eed-319">A 401 response indicates that hello Passport layer is trying tooredirect toohello authorize endpoint, which is exactly what you want.</span></span>

<span data-ttu-id="65eed-320">*Agora você tem um serviço de API REST que usa OAuth 2.0!*</span><span class="sxs-lookup"><span data-stu-id="65eed-320">*You now have a REST API service that uses OAuth 2.0!*</span></span>

<span data-ttu-id="65eed-321">Você já fez tudo o que podia com esse servidor sem usar um cliente compatível com o OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="65eed-321">You've gone as far as you can with this server without using an OAuth 2.0-compatible client.</span></span> <span data-ttu-id="65eed-322">Para fazer isso, você precisará tooreview um tutorial adicional.</span><span class="sxs-lookup"><span data-stu-id="65eed-322">For that, you will need tooreview an additional tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65eed-323">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="65eed-323">Next steps</span></span>
<span data-ttu-id="65eed-324">Para referência, o exemplo hello concluída (sem os valores de configuração) é fornecido como [um arquivo. zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="65eed-324">For reference, hello completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="65eed-325">Você também pode cloná-la no GitHub:</span><span class="sxs-lookup"><span data-stu-id="65eed-325">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="65eed-326">Agora, você pode mover toomore tópicos avançados.</span><span class="sxs-lookup"><span data-stu-id="65eed-326">Now, you can move on toomore advanced topics.</span></span> <span data-ttu-id="65eed-327">Talvez você queira tootry [proteger um aplicativo de web Node.js usando o ponto de extremidade do hello v 2.0](active-directory-v2-devquickstarts-node-web.md).</span><span class="sxs-lookup"><span data-stu-id="65eed-327">You might want tootry [Secure a Node.js web app using hello v2.0 endpoint](active-directory-v2-devquickstarts-node-web.md).</span></span>

<span data-ttu-id="65eed-328">Estes são alguns recursos adicionais:</span><span class="sxs-lookup"><span data-stu-id="65eed-328">Here are some additional resources:</span></span>

* [<span data-ttu-id="65eed-329">Guia do desenvolvedor do Azure AD v2.0</span><span class="sxs-lookup"><span data-stu-id="65eed-329">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="65eed-330">Marcação “azure-active-directory” do Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="65eed-330">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="65eed-331">Obter atualizações de segurança para nossos produtos</span><span class="sxs-lookup"><span data-stu-id="65eed-331">Get security updates for our products</span></span>
<span data-ttu-id="65eed-332">Recomendamos que você toosign backup toobe notificado quando ocorrerem incidentes de segurança.</span><span class="sxs-lookup"><span data-stu-id="65eed-332">We encourage you toosign up toobe notified when security incidents occur.</span></span> <span data-ttu-id="65eed-333">Em Olá [notificações de segurança técnica da Microsoft](https://technet.microsoft.com/security/dd252948) página, assinar tooSecurity comunicados de alertas.</span><span class="sxs-lookup"><span data-stu-id="65eed-333">On hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe tooSecurity Advisories Alerts.</span></span>

