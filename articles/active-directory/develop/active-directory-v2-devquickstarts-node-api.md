---
title: Proteger uma API Web do Azure Active Directory v2.0 usando o Node.js | Microsoft Docs
description: Aprenda a compilar uma API Web Node.js que aceita tokens de contas da Microsoft pessoais e de contas corporativas ou de estudante.
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
ms.openlocfilehash: 94e945a52b9df7c495de1611baa08083357670c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="cfa89-103">Proteger uma API Web usando Node.js</span><span class="sxs-lookup"><span data-stu-id="cfa89-103">Secure a web API by using Node.js</span></span>
> [!NOTE]
> <span data-ttu-id="cfa89-104">Nem todos os cenários e recursos do Azure Active Directory funcionam com o ponto de extremidade v2.0.</span><span class="sxs-lookup"><span data-stu-id="cfa89-104">Not all Azure Active Directory scenarios and features work with the v2.0 endpoint.</span></span> <span data-ttu-id="cfa89-105">Para determinar se você deve usar o ponto de extremidade v2.0 ou v1.0, leia sobre as [limitações da v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="cfa89-105">To determine whether you should use the v2.0 endpoint or the v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="cfa89-106">Quando você usa o ponto de extremidade do Azure AD (Azure Active Directory) v2.0, você pode usar os tokens de acesso [OAuth 2.0](active-directory-v2-protocols.md) para proteger sua API Web.</span><span class="sxs-lookup"><span data-stu-id="cfa89-106">When you use the Azure Active Directory (Azure AD) v2.0 endpoint, you can use [OAuth 2.0](active-directory-v2-protocols.md) access tokens to protect your web API.</span></span> <span data-ttu-id="cfa89-107">Com os tokens de acesso OAuth 2.0, os usuários que têm uma conta da Microsoft pessoal e contas corporativas ou de estudante podem acessar sua API Web com segurança.</span><span class="sxs-lookup"><span data-stu-id="cfa89-107">With OAuth 2.0 access tokens, users who have both a personal Microsoft account and work or school accounts can securely access your web API.</span></span>

<span data-ttu-id="cfa89-108">*Passport* é middleware de autenticação para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="cfa89-108">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="cfa89-109">Flexível e modular, o Passport pode ser colocado sem impedimento em qualquer aplicativo Web baseado em Express ou Restify.</span><span class="sxs-lookup"><span data-stu-id="cfa89-109">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="cfa89-110">No Passport, um conjunto abrangente de estratégias dão suporte à autenticação com o uso de um nome de usuário e uma senha, Facebook, Twitter e outras opções.</span><span class="sxs-lookup"><span data-stu-id="cfa89-110">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="cfa89-111">Desenvolvemos uma estratégia para o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfa89-111">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="cfa89-112">Neste artigo, mostramos como instalar o módulo e, em seguida, adicione o plug-in `passport-azure-ad` do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfa89-112">In this article, we show you how to install the module, and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="cfa89-113">Baixar</span><span class="sxs-lookup"><span data-stu-id="cfa89-113">Download</span></span>
<span data-ttu-id="cfa89-114">O código para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span><span class="sxs-lookup"><span data-stu-id="cfa89-114">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span></span> <span data-ttu-id="cfa89-115">Para seguir o tutorial, [baixe o esqueleto do aplicativo como um arquivo .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip) ou clone o esqueleto:</span><span class="sxs-lookup"><span data-stu-id="cfa89-115">To follow the tutorial, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="cfa89-116">Também obtenha o aplicativo concluído ao final deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="cfa89-116">You also can get the completed application at the end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="cfa89-117">1: registrar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="cfa89-117">1: Register an app</span></span>
<span data-ttu-id="cfa89-118">Crie um novo aplicativo em [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ou siga [estas etapas detalhadas](active-directory-v2-app-registration.md) para registrar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cfa89-118">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) to register an app.</span></span> <span data-ttu-id="cfa89-119">Verifique se você:</span><span class="sxs-lookup"><span data-stu-id="cfa89-119">Make sure you:</span></span>

* <span data-ttu-id="cfa89-120">Copiou a **ID do Aplicativo** atribuída ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cfa89-120">Copy the **Application Id** assigned to your app.</span></span> <span data-ttu-id="cfa89-121">Ela será necessária para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="cfa89-121">You'll need it for this tutorial.</span></span>
* <span data-ttu-id="cfa89-122">Adicione a plataforma **Móvel** de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cfa89-122">Add the **Mobile** platform for your app.</span></span>
* <span data-ttu-id="cfa89-123">Copiar o **URI de redirecionamento** do portal.</span><span class="sxs-lookup"><span data-stu-id="cfa89-123">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="cfa89-124">Você deve usar o valor de URI padrão `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="cfa89-124">You must use the default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-install-nodejs"></a><span data-ttu-id="cfa89-125">2: instalar o Node.js</span><span class="sxs-lookup"><span data-stu-id="cfa89-125">2: Install Node.js</span></span>
<span data-ttu-id="cfa89-126">Para usar o exemplo neste tutorial, você deve [instalar o Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="cfa89-126">To use the sample for this tutorial, you must [install Node.js](http://nodejs.org).</span></span>

## <a name="3-install-mongodb"></a><span data-ttu-id="cfa89-127">3: instalar o MongoDB</span><span class="sxs-lookup"><span data-stu-id="cfa89-127">3: Install MongoDB</span></span>
<span data-ttu-id="cfa89-128">Para poder usar esse exemplo com êxito, você deve [instalar o MongoDB](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="cfa89-128">To successfully use this sample, you must [install MongoDB](http://www.mongodb.org).</span></span> <span data-ttu-id="cfa89-129">Nesse exemplo, você usa o MongoDB para tornar a API REST persistente entre instâncias de servidor.</span><span class="sxs-lookup"><span data-stu-id="cfa89-129">In this sample, you use MongoDB to make your REST API persistent across server instances.</span></span>

> [!NOTE]
> <span data-ttu-id="cfa89-130">Neste artigo, supomos que você usa a instalação e os pontos de extremidade de servidor padrão para o MongoDB: mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="cfa89-130">In this article, we assume that you use the default installation and server endpoints for MongoDB: mongodb://localhost.</span></span>
> 
> 

## <a name="4-install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="cfa89-131">4: instalar os módulos Restify na API Web</span><span class="sxs-lookup"><span data-stu-id="cfa89-131">4: Install the restify modules in your web API</span></span>
<span data-ttu-id="cfa89-132">Usaremos Resitfy para criar nossa API REST.</span><span class="sxs-lookup"><span data-stu-id="cfa89-132">We use Resitfy to build our REST API.</span></span> <span data-ttu-id="cfa89-133">O Restify é uma estrutura de aplicativo do Node.js mínima e flexível, derivada do Express.</span><span class="sxs-lookup"><span data-stu-id="cfa89-133">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="cfa89-134">O Restify tem um conjunto robusto de recursos que você pode usar para criar APIs REST no Connect.</span><span class="sxs-lookup"><span data-stu-id="cfa89-134">Restify has a robust set of features that you can use to build REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="cfa89-135">Instalar o Restify</span><span class="sxs-lookup"><span data-stu-id="cfa89-135">Install restify</span></span>
1.  <span data-ttu-id="cfa89-136">Em um prompt de comando, altere o diretório para **azuread**:</span><span class="sxs-lookup"><span data-stu-id="cfa89-136">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

    <span data-ttu-id="cfa89-137">Se o diretório **azuread** não existir, crie-o:</span><span class="sxs-lookup"><span data-stu-id="cfa89-137">If the **azuread** directory does not exist, create it:</span></span>

    `mkdir azuread`

2.  <span data-ttu-id="cfa89-138">Instale o Restify:</span><span class="sxs-lookup"><span data-stu-id="cfa89-138">Install restify:</span></span>

    `npm install restify`

    <span data-ttu-id="cfa89-139">A saída desse comando deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="cfa89-139">The output of this command should look like this:</span></span>

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

#### <a name="did-you-get-an-error"></a><span data-ttu-id="cfa89-140">Você obteve um erro?</span><span class="sxs-lookup"><span data-stu-id="cfa89-140">Did you get an error?</span></span>
<span data-ttu-id="cfa89-141">Em alguns sistemas operacionais, quando você usar o comando `npm`, você verá esta mensagem: `Error: EPERM, chmod '/usr/local/bin/..'`.</span><span class="sxs-lookup"><span data-stu-id="cfa89-141">On some operating systems, when you use the `npm` command, you might see this message: `Error: EPERM, chmod '/usr/local/bin/..'`.</span></span> <span data-ttu-id="cfa89-142">O erro é seguido de uma solicitação para tentar executar a conta como administrador.</span><span class="sxs-lookup"><span data-stu-id="cfa89-142">The error is followed by a request that you try running the account as an administrator.</span></span> <span data-ttu-id="cfa89-143">Se isso ocorrer, use o comando `sudo` para executar `npm` com um nível de privilégio mais elevado.</span><span class="sxs-lookup"><span data-stu-id="cfa89-143">If this occurs, use the command `sudo` to run `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-related-to-dtrace"></a><span data-ttu-id="cfa89-144">Você obteve um erro com relação ao DTrace?</span><span class="sxs-lookup"><span data-stu-id="cfa89-144">Did you get an error related to DTrace?</span></span>
<span data-ttu-id="cfa89-145">Quando você instala o restify, pode ver esta mensagem:</span><span class="sxs-lookup"><span data-stu-id="cfa89-145">When you install restify, you might see this message:</span></span>

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

<span data-ttu-id="cfa89-146">O Restify tem um mecanismo eficiente para rastrear chamadas REST usando o DTrace.</span><span class="sxs-lookup"><span data-stu-id="cfa89-146">Restify has a powerful mechanism to trace REST calls by using DTrace.</span></span> <span data-ttu-id="cfa89-147">No entanto, o DTrace não está disponível em muitos sistemas operacionais.</span><span class="sxs-lookup"><span data-stu-id="cfa89-147">However, DTrace is not available on many operating systems.</span></span> <span data-ttu-id="cfa89-148">Você pode ignorar essa mensagem de erro com segurança.</span><span class="sxs-lookup"><span data-stu-id="cfa89-148">You can safely ignore this error message.</span></span>


## <a name="5-install-passportjs-in-your-web-api"></a><span data-ttu-id="cfa89-149">5: instalar o Passport.js na sua API Web</span><span class="sxs-lookup"><span data-stu-id="cfa89-149">5: Install Passport.js in your web API</span></span>
1.  <span data-ttu-id="cfa89-150">Em um prompt de comando, altere o diretório para **azuread**.</span><span class="sxs-lookup"><span data-stu-id="cfa89-150">At the command prompt, change the directory to **azuread**.</span></span>

2.  <span data-ttu-id="cfa89-151">Instale o Passport.js:</span><span class="sxs-lookup"><span data-stu-id="cfa89-151">Install Passport.js:</span></span>

    `npm install passport`

    <span data-ttu-id="cfa89-152">A saída do comando deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="cfa89-152">The output of the command should look like this:</span></span>

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-to-your-web-api"></a><span data-ttu-id="cfa89-153">6: adicionar o passport-azure-ad à sua API Web</span><span class="sxs-lookup"><span data-stu-id="cfa89-153">6: Add passport-azure-ad to your web API</span></span>
<span data-ttu-id="cfa89-154">Em seguida, adicione a estratégia de OAuth, usando passport-azure-ad.</span><span class="sxs-lookup"><span data-stu-id="cfa89-154">Next, add the OAuth strategy, by using passport-azuread.</span></span> <span data-ttu-id="cfa89-155">`passport-azuread` é um pacote de estratégias que conectam o Azure AD ao Passport.</span><span class="sxs-lookup"><span data-stu-id="cfa89-155">`passport-azuread` is a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="cfa89-156">Usaremos essa estratégia para tokens de portador neste exemplo de API Rest.</span><span class="sxs-lookup"><span data-stu-id="cfa89-156">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="cfa89-157">Embora o OAuth 2.0 forneça uma estrutura na qual qualquer tipo de token conhecido possa ser emitido, determinados tipos de token são comumente usados.</span><span class="sxs-lookup"><span data-stu-id="cfa89-157">Although OAuth 2.0 provides a framework in which any known token type can be issued, certain token types are commonly used.</span></span> <span data-ttu-id="cfa89-158">Os tokens de portador são usados para proteger os pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="cfa89-158">Bearer tokens are commonly used to protect endpoints.</span></span> <span data-ttu-id="cfa89-159">Esses são o tipo mais amplamente emitido de token no OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="cfa89-159">Bearer tokens are the most widely issued type of token in OAuth 2.0.</span></span> <span data-ttu-id="cfa89-160">Muitas implementações do OAuth 2.0 presumem que os tokens de portador sejam o único tipo de token emitido.</span><span class="sxs-lookup"><span data-stu-id="cfa89-160">Many OAuth 2.0 implementations assume that bearer tokens are the only type of token issued.</span></span>
> 
> 

1.  <span data-ttu-id="cfa89-161">Em um prompt de comando, altere o diretório para **azuread**.</span><span class="sxs-lookup"><span data-stu-id="cfa89-161">At a command prompt, change the directory to **azuread**.</span></span>

    `cd azuread`

2.  <span data-ttu-id="cfa89-162">Instale o módulo `passport-azure-ad` do Passport.js:</span><span class="sxs-lookup"><span data-stu-id="cfa89-162">Install the Passport.js `passport-azure-ad` module:</span></span>

    `npm install passport-azure-ad`

    <span data-ttu-id="cfa89-163">A saída do comando deve ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="cfa89-163">The output of the command should look like this:</span></span>

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

## <a name="7-add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="cfa89-164">7: adicionar módulos do MongoDB à sua API Web</span><span class="sxs-lookup"><span data-stu-id="cfa89-164">7: Add MongoDB modules to your web API</span></span>
<span data-ttu-id="cfa89-165">Neste exemplo, usamos o MongoDB como nosso armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="cfa89-165">In this sample, we use MongoDB as our data store.</span></span> 

1.  <span data-ttu-id="cfa89-166">Instale o Mongoose, um plug-in amplamente utilizado para gerenciar modelos e esquemas:</span><span class="sxs-lookup"><span data-stu-id="cfa89-166">Install Mongoose, a widely used plug-in, to manage models and schemas:</span></span> 

    `npm install mongoose`

2.  <span data-ttu-id="cfa89-167">Instale o driver do banco de dados para o MongoDB, que também é chamado de MongoDB:</span><span class="sxs-lookup"><span data-stu-id="cfa89-167">Install the database driver for MongoDB, which is also called MongoDB:</span></span>

    `npm install mongodb`

## <a name="8-install-additional-modules"></a><span data-ttu-id="cfa89-168">8: instalar módulos adicionais</span><span class="sxs-lookup"><span data-stu-id="cfa89-168">8: Install additional modules</span></span>
<span data-ttu-id="cfa89-169">Instale os módulos necessários restantes.</span><span class="sxs-lookup"><span data-stu-id="cfa89-169">Install the remaining required modules.</span></span>

1.  <span data-ttu-id="cfa89-170">Em um prompt de comando, altere o diretório para **azuread**:</span><span class="sxs-lookup"><span data-stu-id="cfa89-170">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="cfa89-171">Digite os comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="cfa89-171">Enter the following commands.</span></span> <span data-ttu-id="cfa89-172">Os comandos instalam os módulos a seguir em seu diretório node_modules:</span><span class="sxs-lookup"><span data-stu-id="cfa89-172">The commands install the following modules in your node_modules directory:</span></span>

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

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a><span data-ttu-id="cfa89-173">9: criar um arquivo Server.js para suas dependências</span><span class="sxs-lookup"><span data-stu-id="cfa89-173">9: Create a Server.js file for your dependencies</span></span>
<span data-ttu-id="cfa89-174">Um arquivo Server.js retém a maior parte da funcionalidade para o servidor de API Web.</span><span class="sxs-lookup"><span data-stu-id="cfa89-174">A Server.js file holds the majority of the functionality for your web API server.</span></span> <span data-ttu-id="cfa89-175">Adicione a maior parte do nosso código a esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="cfa89-175">Add most of your code to this file.</span></span> <span data-ttu-id="cfa89-176">Para fins de produção, você pode refatorar a funcionalidade em arquivos menores, assim como para controladores e rotas separadas.</span><span class="sxs-lookup"><span data-stu-id="cfa89-176">For production purposes, you can refactor the functionality into smaller files, like for separate routes and controllers.</span></span> <span data-ttu-id="cfa89-177">Neste artigo, usaremos Server.js para essa finalidade.</span><span class="sxs-lookup"><span data-stu-id="cfa89-177">In this article, we use Server.js for this purpose.</span></span>

1.  <span data-ttu-id="cfa89-178">Em um prompt de comando, altere o diretório para **azuread**:</span><span class="sxs-lookup"><span data-stu-id="cfa89-178">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="cfa89-179">Usando um editor de sua escolha, crie um arquivo Server.js.</span><span class="sxs-lookup"><span data-stu-id="cfa89-179">Using an editor of your choice, create a Server.js file.</span></span> <span data-ttu-id="cfa89-180">Adicione as seguintes informações ao arquivo:</span><span class="sxs-lookup"><span data-stu-id="cfa89-180">Add the following information to the file:</span></span>

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

3.  <span data-ttu-id="cfa89-181">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="cfa89-181">Save the file.</span></span> <span data-ttu-id="cfa89-182">Voltaremos a ele em breve.</span><span class="sxs-lookup"><span data-stu-id="cfa89-182">You will return to it shortly.</span></span>

## <a name="10-create-a-config-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="cfa89-183">10: criar um arquivo de configuração para armazenar as configurações do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cfa89-183">10: Create a config file to store your Azure AD settings</span></span>
<span data-ttu-id="cfa89-184">Esse arquivo de código passa os parâmetros de configuração do Portal do Azure AD para o arquivo Passport.js.</span><span class="sxs-lookup"><span data-stu-id="cfa89-184">This code file passes the configuration parameters from your Azure AD portal to Passport.js.</span></span> <span data-ttu-id="cfa89-185">Você criou esses valores de configuração quando adicionou a API Web ao portal no início do artigo.</span><span class="sxs-lookup"><span data-stu-id="cfa89-185">You created these configuration values when you added the web API to the portal at the beginning of the article.</span></span> <span data-ttu-id="cfa89-186">Após você copiar o código, explicaremos o que deve ser inserido nos valores desses parâmetros.</span><span class="sxs-lookup"><span data-stu-id="cfa89-186">After you copy the code, we'll explain what to put in the values of these parameters.</span></span>

1.  <span data-ttu-id="cfa89-187">Em um prompt de comando, altere o diretório para **azuread**:</span><span class="sxs-lookup"><span data-stu-id="cfa89-187">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="cfa89-188">Em um editor, crie um arquivo Config.js.</span><span class="sxs-lookup"><span data-stu-id="cfa89-188">In an editor, create a Config.js file.</span></span> <span data-ttu-id="cfa89-189">Adicione as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="cfa89-189">Add the following information:</span></span>

    ```Javascript
    // Don't commit this file to your public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need to change this.
    };

    ```



### <a name="required-values"></a><span data-ttu-id="cfa89-190">Valores necessários</span><span class="sxs-lookup"><span data-stu-id="cfa89-190">Required values</span></span>

*   <span data-ttu-id="cfa89-191">**IdentityMetadata**: é onde `passport-azure-ad` procura os dados de configuração para o IdP (provedor de identidade), bem como as chaves para validar os tokens JWT (Token Web JSON).</span><span class="sxs-lookup"><span data-stu-id="cfa89-191">**IdentityMetadata**: This is where `passport-azure-ad` looks for your configuration data for the identity provider (IDP) and the keys to validate the JSON Web Tokens (JWTs).</span></span> <span data-ttu-id="cfa89-192">Se você estiver usando o Azure AD, você provavelmente não desejará alterar isso.</span><span class="sxs-lookup"><span data-stu-id="cfa89-192">If you are using Azure AD, you probably don't want to change this.</span></span>

*   <span data-ttu-id="cfa89-193">**audience**: o URI de redirecionamento do portal.</span><span class="sxs-lookup"><span data-stu-id="cfa89-193">**audience**: Your redirect URI from the portal.</span></span>

> [!NOTE]
> <span data-ttu-id="cfa89-194">Reverta suas chaves em intervalos frequentes.</span><span class="sxs-lookup"><span data-stu-id="cfa89-194">Roll your keys at frequent intervals.</span></span> <span data-ttu-id="cfa89-195">Verifique se você está extraindo sempre da URL "openid_keys" e de que o aplicativo pode acessar a Internet.</span><span class="sxs-lookup"><span data-stu-id="cfa89-195">Be sure that you always pull from the "openid_keys" URL, and that the app can access the Internet.</span></span>
> 
> 

## <a name="11-add-the-configuration-to-your-serverjs-file"></a><span data-ttu-id="cfa89-196">11: adicionar configuração ao arquivo Server.js</span><span class="sxs-lookup"><span data-stu-id="cfa89-196">11: Add the configuration to your Server.js file</span></span>
<span data-ttu-id="cfa89-197">O aplicativo precisa ler esses valores do arquivo de configuração que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="cfa89-197">Your application needs to read the values from the config file you just created.</span></span> <span data-ttu-id="cfa89-198">Adicione o arquivo .config como um recurso necessário no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cfa89-198">Add the .config file as a required resource in your application.</span></span> <span data-ttu-id="cfa89-199">Defina as variáveis globais para aqueles que estão em Config.js.</span><span class="sxs-lookup"><span data-stu-id="cfa89-199">Set the global variables to those that are in Config.js.</span></span>

1.  <span data-ttu-id="cfa89-200">No prompt de comando, altere o diretório para **azuread**:</span><span class="sxs-lookup"><span data-stu-id="cfa89-200">At the command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="cfa89-201">Em um editor, abra o Server.js.</span><span class="sxs-lookup"><span data-stu-id="cfa89-201">In an editor, open Server.js.</span></span> <span data-ttu-id="cfa89-202">Adicione as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="cfa89-202">Add the following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```

3.  <span data-ttu-id="cfa89-203">Adicione uma nova seção ao Server.js:</span><span class="sxs-lookup"><span data-stu-id="cfa89-203">Add a new section to Server.js:</span></span>

    ```Javascript
    // Pass these options in to the ODICBearerStrategy.
    var options = {
    // The URL of the metadata document for your app. Put the keys for token validation from the URL found in the jwks_uri tag in the metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array to hold signed-in users and the current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="cfa89-204">12: Adicionar as informações de esquema e modelo do MongoDB usando Mongoose</span><span class="sxs-lookup"><span data-stu-id="cfa89-204">12: Add the MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="cfa89-205">Em seguida, conecte esses três arquivos em um serviço de API REST.</span><span class="sxs-lookup"><span data-stu-id="cfa89-205">Next, connect these three files in a REST API service.</span></span>

<span data-ttu-id="cfa89-206">Neste artigo, usaremos o MongoDB para armazenar nossas tarefas.</span><span class="sxs-lookup"><span data-stu-id="cfa89-206">In this article, we use MongoDB to store our tasks.</span></span> <span data-ttu-id="cfa89-207">Abordaremos isso na *etapa 4*.</span><span class="sxs-lookup"><span data-stu-id="cfa89-207">We discuss this in *step 4*.</span></span>

<span data-ttu-id="cfa89-208">No arquivo Config.js criado na etapa 11, o banco de dados é chamado de *tasklist*.</span><span class="sxs-lookup"><span data-stu-id="cfa89-208">In the Config.js file you created in step 11, your database is called *tasklist*.</span></span> <span data-ttu-id="cfa89-209">É isso que você colocou no final da URL de conexão mongoose_auth_local.</span><span class="sxs-lookup"><span data-stu-id="cfa89-209">That was what you put at the end of your mongoose_auth_local connection URL.</span></span> <span data-ttu-id="cfa89-210">Você não precisa criar esse banco de dados com antecedência no MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cfa89-210">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="cfa89-211">O banco de dados é criado na primeira execução do seu aplicativo para servidores (supondo que o banco de dados ainda não existe).</span><span class="sxs-lookup"><span data-stu-id="cfa89-211">The database is created on the first run of your server application (assuming the database does not already exist).</span></span>

<span data-ttu-id="cfa89-212">Você informou ao servidor qual banco de dados MongoDB usar.</span><span class="sxs-lookup"><span data-stu-id="cfa89-212">You've told the server what MongoDB database to use.</span></span> <span data-ttu-id="cfa89-213">Em seguida, você precisa escrever algum código adicional para criar o modelo e o esquema para tarefas do servidor.</span><span class="sxs-lookup"><span data-stu-id="cfa89-213">Next, you need to write some additional code to create the model and schema for your server's tasks.</span></span>

### <a name="the-model"></a><span data-ttu-id="cfa89-214">O modelo</span><span class="sxs-lookup"><span data-stu-id="cfa89-214">The model</span></span>
<span data-ttu-id="cfa89-215">O modelo de esquema é muito básico.</span><span class="sxs-lookup"><span data-stu-id="cfa89-215">The schema model is very basic.</span></span> <span data-ttu-id="cfa89-216">Você pode expandi-lo se necessário.</span><span class="sxs-lookup"><span data-stu-id="cfa89-216">You can expand it if you need to.</span></span> 

<span data-ttu-id="cfa89-217">O modelo de esquema tem estes valores:</span><span class="sxs-lookup"><span data-stu-id="cfa89-217">The schema model has these values:</span></span>

*   <span data-ttu-id="cfa89-218">**NAME**.</span><span class="sxs-lookup"><span data-stu-id="cfa89-218">**NAME**.</span></span> <span data-ttu-id="cfa89-219">A pessoa atribuída à tarefa.</span><span class="sxs-lookup"><span data-stu-id="cfa89-219">The person assigned to the task.</span></span> <span data-ttu-id="cfa89-220">Esse é um valor do tipo **string**.</span><span class="sxs-lookup"><span data-stu-id="cfa89-220">This is a **string** value.</span></span>
*   <span data-ttu-id="cfa89-221">**TASK**.</span><span class="sxs-lookup"><span data-stu-id="cfa89-221">**TASK**.</span></span> <span data-ttu-id="cfa89-222">O nome da tarefa.</span><span class="sxs-lookup"><span data-stu-id="cfa89-222">The name of the task.</span></span> <span data-ttu-id="cfa89-223">Esse é um valor do tipo **string**.</span><span class="sxs-lookup"><span data-stu-id="cfa89-223">This is a **string** value.</span></span>
*   <span data-ttu-id="cfa89-224">**DATE**.</span><span class="sxs-lookup"><span data-stu-id="cfa89-224">**DATE**.</span></span> <span data-ttu-id="cfa89-225">A data na qual a tarefa expira.</span><span class="sxs-lookup"><span data-stu-id="cfa89-225">The date that the task is due.</span></span> <span data-ttu-id="cfa89-226">Esse é um valor do tipo **datetime**.</span><span class="sxs-lookup"><span data-stu-id="cfa89-226">This is a **datetime** value.</span></span>
*   <span data-ttu-id="cfa89-227">**COMPLETED**.</span><span class="sxs-lookup"><span data-stu-id="cfa89-227">**COMPLETED**.</span></span> <span data-ttu-id="cfa89-228">Se a tarefa está ou não concluída.</span><span class="sxs-lookup"><span data-stu-id="cfa89-228">Whether the task is completed.</span></span> <span data-ttu-id="cfa89-229">Esse é um valor do tipo **Boolean**.</span><span class="sxs-lookup"><span data-stu-id="cfa89-229">This is a **Boolean** value.</span></span>

### <a name="create-the-schema-in-the-code"></a><span data-ttu-id="cfa89-230">Criar o esquema no código</span><span class="sxs-lookup"><span data-stu-id="cfa89-230">Create the schema in the code</span></span>
1.  <span data-ttu-id="cfa89-231">Em um prompt de comando, altere o diretório para **azuread**:</span><span class="sxs-lookup"><span data-stu-id="cfa89-231">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="cfa89-232">No editor, abra o Server.js.</span><span class="sxs-lookup"><span data-stu-id="cfa89-232">In your editor, open Server.js.</span></span> <span data-ttu-id="cfa89-233">Adicione as seguintes informações abaixo da entrada de configuração:</span><span class="sxs-lookup"><span data-stu-id="cfa89-233">Below the configuration entry, add the following information:</span></span>

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect to MongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

<span data-ttu-id="cfa89-234">Esse código se conecta ao servidor MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cfa89-234">This code connects to the MongoDB server.</span></span> <span data-ttu-id="cfa89-235">Ele também retorna um objeto de esquema.</span><span class="sxs-lookup"><span data-stu-id="cfa89-235">It also returns a schema object.</span></span>

#### <a name="using-the-schema-create-your-model-in-the-code"></a><span data-ttu-id="cfa89-236">Usando o esquema, crie o modelo no código</span><span class="sxs-lookup"><span data-stu-id="cfa89-236">Using the schema, create your model in the code</span></span>
<span data-ttu-id="cfa89-237">Abaixo do código anterior, adicione o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="cfa89-237">Below the preceding code, add the following code:</span></span>

```Javascript
// Create a basic schema to store your tasks and users.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use the schema to register a model.
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```

<span data-ttu-id="cfa89-238">Como você pode ver no código, você cria o esquema primeiro.</span><span class="sxs-lookup"><span data-stu-id="cfa89-238">As you can tell from the code, first you create your schema.</span></span> <span data-ttu-id="cfa89-239">Em seguida, você cria um objeto do modelo.</span><span class="sxs-lookup"><span data-stu-id="cfa89-239">Next, you create a model object.</span></span> <span data-ttu-id="cfa89-240">Você usa o objeto do modelo para armazenar os dados em todo o código ao definir suas **rotas**.</span><span class="sxs-lookup"><span data-stu-id="cfa89-240">You use the model object to store your data throughout the code when you define your **routes**.</span></span>

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a><span data-ttu-id="cfa89-241">13: adicionar as rotas ao servidor de API REST da tarefa</span><span class="sxs-lookup"><span data-stu-id="cfa89-241">13: Add your routes for your task REST API server</span></span>
<span data-ttu-id="cfa89-242">Agora que você tem um modelo de banco de dados com o qual trabalhar, adicione as rotas que você usará para o servidor de API REST.</span><span class="sxs-lookup"><span data-stu-id="cfa89-242">Now that you have a database model to work with, add the routes you'll use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="cfa89-243">Sobre rotas no Restify</span><span class="sxs-lookup"><span data-stu-id="cfa89-243">About routes in restify</span></span>
<span data-ttu-id="cfa89-244">As rotas no Restify funcionam exatamente da mesma forma que quando você usar a pilha do Express.</span><span class="sxs-lookup"><span data-stu-id="cfa89-244">Routes in restify work exactly the same way they do when you use the Express stack.</span></span> <span data-ttu-id="cfa89-245">Você define rotas usando o URI que espera que os aplicativos de cliente chamem.</span><span class="sxs-lookup"><span data-stu-id="cfa89-245">You define routes by using the URI that you expect the client applications to call.</span></span> <span data-ttu-id="cfa89-246">Normalmente, você define suas rotas em um arquivo separado.</span><span class="sxs-lookup"><span data-stu-id="cfa89-246">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="cfa89-247">Neste tutorial, colocamos nossa rotas no Server.js.</span><span class="sxs-lookup"><span data-stu-id="cfa89-247">In this tutorial, we put our routes in Server.js.</span></span> <span data-ttu-id="cfa89-248">Para uso em produção, recomendamos que você coloque as rotas no próprio arquivo delas.</span><span class="sxs-lookup"><span data-stu-id="cfa89-248">For production use, we recommend that you factor routes into their own file.</span></span>

<span data-ttu-id="cfa89-249">Eis um padrão típico para uma rota de Restify:</span><span class="sxs-lookup"><span data-stu-id="cfa89-249">A typical pattern for a restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep the server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


<span data-ttu-id="cfa89-250">Este é o padrão no nível mais básico.</span><span class="sxs-lookup"><span data-stu-id="cfa89-250">This is the pattern at the most basic level.</span></span> <span data-ttu-id="cfa89-251">O Restify (e o Express) fornecem uma funcionalidade muito mais aprofundada, como a definição de tipos de aplicativos e o roteamento complexo entre diferentes pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="cfa89-251">Restify (and Express) provide much deeper functionality, like the ability to define application types, and complex routing across different endpoints.</span></span>

#### <a name="add-default-routes-to-your-server"></a><span data-ttu-id="cfa89-252">Adicionar rotas padrão a seu servidor</span><span class="sxs-lookup"><span data-stu-id="cfa89-252">Add default routes to your server</span></span>
<span data-ttu-id="cfa89-253">Adicione as rotas CRUD básicas: **create** (criar), **retrieve** (extrair), **update** (atualizar) e **delete** (excluir).</span><span class="sxs-lookup"><span data-stu-id="cfa89-253">Add the basic CRUD routes: **create**, **retrieve**, **update**, and **delete**.</span></span>

1.  <span data-ttu-id="cfa89-254">Em um prompt de comando, altere o diretório para **azuread**:</span><span class="sxs-lookup"><span data-stu-id="cfa89-254">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="cfa89-255">Em um editor, abra o Server.js.</span><span class="sxs-lookup"><span data-stu-id="cfa89-255">In an editor, open Server.js.</span></span> <span data-ttu-id="cfa89-256">Abaixo das entradas de banco de dados que você criou anteriormente, adicione as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="cfa89-256">Below the database entries you made earlier, add the following information:</span></span>

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you to set default headers.
    // These headers comply with CORS, and allow you to use MongoDB Server as your response to any origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it to MongoDB.
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
    req.log.warn(err, 'createTask: unable to save');
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
    'removeTask: unable to delete %s',
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
    req.log.warn(err, 'get: unable to read %s', owner);
    next(err);
    return;
    }
    res.json(data);
    });
    return next();
    }
    /// Returns the list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you to set default headers.
    // These headers comply with CORS, and allow us to use MongoDB Server as our response to any origin.
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
    log.warn(err, "There are no tasks in the database. Add one!");
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

### <a name="add-error-handling-for-the-routes"></a><span data-ttu-id="cfa89-257">Adicionar tratamento de erro para as rotas</span><span class="sxs-lookup"><span data-stu-id="cfa89-257">Add error handling for the routes</span></span>
<span data-ttu-id="cfa89-258">Adicione algum tratamento de erro para que você possa se comunicar de volta com o cliente sobre o problema encontrado.</span><span class="sxs-lookup"><span data-stu-id="cfa89-258">Add some error handling so you can communicate back to the client about the problem you encountered.</span></span>

<span data-ttu-id="cfa89-259">Adicione o código a seguir abaixo do código que você já escreveu:</span><span class="sxs-lookup"><span data-stu-id="cfa89-259">Add the following code below the code, which you've already written:</span></span>

```Javascript
///--- Errors for communicating something more information back to the client.
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


## <a name="14-create-your-server"></a><span data-ttu-id="cfa89-260">14: criar seu servidor</span><span class="sxs-lookup"><span data-stu-id="cfa89-260">14: Create your server</span></span>
<span data-ttu-id="cfa89-261">A última coisa a fazer é adicionar a instância do servidor.</span><span class="sxs-lookup"><span data-stu-id="cfa89-261">The last thing to do is to add your server instance.</span></span> <span data-ttu-id="cfa89-262">A instância do servidor gerencia suas chamadas.</span><span class="sxs-lookup"><span data-stu-id="cfa89-262">The server instance manages your calls.</span></span>

<span data-ttu-id="cfa89-263">O Restify (e Express) têm personalização profunda que pode ser usada com um servidor de API REST.</span><span class="sxs-lookup"><span data-stu-id="cfa89-263">Restify (and Express) have deep customization that you can use with a REST API server.</span></span> <span data-ttu-id="cfa89-264">Neste tutorial, usamos a configuração mais básica.</span><span class="sxs-lookup"><span data-stu-id="cfa89-264">In this tutorial, we use the most basic setup.</span></span>

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
// Allow 5 requests/second by IP address, and burst to 10.
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
## <a name="15-add-the-routes-without-authentication-for-now"></a><span data-ttu-id="cfa89-265">15: adicionar as rotas (sem autenticação por enquanto)</span><span class="sxs-lookup"><span data-stu-id="cfa89-265">15: Add the routes (without authentication, for now)</span></span>
```Javascript
/// Use CRUD to add the real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in the pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need to maintain session state. You can experiment with removing API protection.
/* To do this, remove the passport.authenticate() method:
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
consoleMessage += '\n Open your browser to %s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-run-the-server"></a><span data-ttu-id="cfa89-266">16: executar o servidor</span><span class="sxs-lookup"><span data-stu-id="cfa89-266">16: Run the server</span></span>
<span data-ttu-id="cfa89-267">É uma boa ideia testar o servidor antes de adicionar a autenticação.</span><span class="sxs-lookup"><span data-stu-id="cfa89-267">It's a good idea to test your server before you add authentication.</span></span>

<span data-ttu-id="cfa89-268">A maneira mais fácil de testar o servidor é usando curl em um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="cfa89-268">The easiest way to test your server is by using curl at a command prompt.</span></span> <span data-ttu-id="cfa89-269">Para fazer isso, você precisa de um utilitário simples que você pode usar para analisar a saída como JSON.</span><span class="sxs-lookup"><span data-stu-id="cfa89-269">To do this, you need a simple utility that you can use to parse output as JSON.</span></span> 

1.  <span data-ttu-id="cfa89-270">Instale a ferramenta JSON que usamos nos exemplos a seguir:</span><span class="sxs-lookup"><span data-stu-id="cfa89-270">Install the JSON tool that we use in the following examples:</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="cfa89-271">Isso instala a ferramenta JSON globalmente.</span><span class="sxs-lookup"><span data-stu-id="cfa89-271">This installs the JSON tool globally.</span></span>

2.  <span data-ttu-id="cfa89-272">Verifique se a instância do MongoDB está em execução.</span><span class="sxs-lookup"><span data-stu-id="cfa89-272">Make sure that your MongoDB instance is running:</span></span>

    `$sudo mongod`

3.  <span data-ttu-id="cfa89-273">Altere o diretório para **azuread** e execute o curl:</span><span class="sxs-lookup"><span data-stu-id="cfa89-273">Change the directory to **azuread**, and then run curl:</span></span>

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

4.  <span data-ttu-id="cfa89-274">Para adicionar uma tarefa:</span><span class="sxs-lookup"><span data-stu-id="cfa89-274">To add a task:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    <span data-ttu-id="cfa89-275">A resposta deve ser:</span><span class="sxs-lookup"><span data-stu-id="cfa89-275">The response should be:</span></span>

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

5.  <span data-ttu-id="cfa89-276">Listar tarefas para Brandon:</span><span class="sxs-lookup"><span data-stu-id="cfa89-276">List tasks for Brandon:</span></span>

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="cfa89-277">Se todos esses comandos são executados sem erros, você está pronto para adicionar OAuth ao servidor de API REST.</span><span class="sxs-lookup"><span data-stu-id="cfa89-277">If all these commands run without errors, you are ready to add OAuth to the REST API server.</span></span>

<span data-ttu-id="cfa89-278">*Agora você tem um servidor de API REST com o MongoDB!*</span><span class="sxs-lookup"><span data-stu-id="cfa89-278">*You now have a REST API server with MongoDB!*</span></span>

## <a name="17-add-authentication-to-your-rest-api-server"></a><span data-ttu-id="cfa89-279">17: adicionar autenticação a seu servidor de API REST</span><span class="sxs-lookup"><span data-stu-id="cfa89-279">17: Add authentication to your REST API server</span></span>
<span data-ttu-id="cfa89-280">Agora que você tem uma API REST em execução, configure-a para usá-la com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfa89-280">Now that you have a running REST API, set it up to use it with Azure AD.</span></span>

<span data-ttu-id="cfa89-281">Em um prompt de comando, altere o diretório para **azuread**:</span><span class="sxs-lookup"><span data-stu-id="cfa89-281">At a command prompt, change the directory to **azuread**:</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a><span data-ttu-id="cfa89-282">Usar o oidcbearerstrategy que está incluído no passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="cfa89-282">Use the oidcbearerstrategy that's included with passport-azure-ad</span></span>
<span data-ttu-id="cfa89-283">Até agora, você criou um servidor típico TODO do REST sem nenhum tipo de autorização.</span><span class="sxs-lookup"><span data-stu-id="cfa89-283">So far, you've built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="cfa89-284">Agora, adicione autenticação.</span><span class="sxs-lookup"><span data-stu-id="cfa89-284">Now, add authentication.</span></span>

<span data-ttu-id="cfa89-285">Primeiro, indique que você deseja usar o Passport.</span><span class="sxs-lookup"><span data-stu-id="cfa89-285">First,  indicate that you want to use Passport.</span></span> <span data-ttu-id="cfa89-286">Coloque isso logo após a sua configuração anterior do servidor:</span><span class="sxs-lookup"><span data-stu-id="cfa89-286">Put this right after your earlier server configuration:</span></span>

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> <span data-ttu-id="cfa89-287">Ao escrever APIs, convém sempre vincular os dados a algo exclusivo do token que o usuário não possa falsificar.</span><span class="sxs-lookup"><span data-stu-id="cfa89-287">When you write APIs, it's a good idea to always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="cfa89-288">Quando esse servidor armazena itens TODO, armazena-os com base na ID da assinatura do usuário no token (chamado por meio de token.sub).</span><span class="sxs-lookup"><span data-stu-id="cfa89-288">When this server stores TODO items, it stores them based on the user subscription ID in the token (called through token.sub).</span></span> <span data-ttu-id="cfa89-289">Você pode colocar o token.sub no campo "proprietário".</span><span class="sxs-lookup"><span data-stu-id="cfa89-289">You put the token.sub in the “owner” field.</span></span> <span data-ttu-id="cfa89-290">Isso garante que somente esse usuário possa acessar os TODOs do usuário.</span><span class="sxs-lookup"><span data-stu-id="cfa89-290">This ensures that only that user can access the user's TODOs.</span></span> <span data-ttu-id="cfa89-291">Ninguém pode acessar as TODOs que foram inseridas.</span><span class="sxs-lookup"><span data-stu-id="cfa89-291">No one else can access the TODOs that were entered.</span></span> <span data-ttu-id="cfa89-292">Não há nenhuma exposição na API para o "proprietário".</span><span class="sxs-lookup"><span data-stu-id="cfa89-292">There is no exposure in the API for “owner.”</span></span> <span data-ttu-id="cfa89-293">Um usuário externo pode solicitar TODOs de outros usuários, mesmo quando eles estão autenticados.</span><span class="sxs-lookup"><span data-stu-id="cfa89-293">An external user can request other users' TODOs, even if they are authenticated.</span></span>
> 
> 

<span data-ttu-id="cfa89-294">Em seguida, usaremos a estratégia de Open ID Connect Bearer que vem com `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="cfa89-294">Next, use the Open ID Connect Bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="cfa89-295">Coloque isto depois do que você colou anteriormente:</span><span class="sxs-lookup"><span data-stu-id="cfa89-295">Put this after what you pasted earlier:</span></span>

```Javascript
/**
/*
/* Calling the OIDCBearerStrategy and managing users.
/*
/* Because of the Passport pattern, you need to manage users and info tokens
/* with a FindorCreate() method. The method must be provided by the implementor.
/* In the following code, you autoregister any user and implement a FindById().
/* It's a good idea to do something more advanced.
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
log.info('verifying the user');
log.info(token, 'was the token retrieved');
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

<span data-ttu-id="cfa89-296">O Passport usa um padrão semelhante para todas as suas estratégias (Twitter, Facebook e assim por diante).</span><span class="sxs-lookup"><span data-stu-id="cfa89-296">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="cfa89-297">Todos os gravadores de estratégia seguem o padrão.</span><span class="sxs-lookup"><span data-stu-id="cfa89-297">All strategy writers adhere to the pattern.</span></span> <span data-ttu-id="cfa89-298">Passe uma `function()` para a estratégia que usa um token e `done` como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="cfa89-298">Pass the strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="cfa89-299">A estratégia é retornada depois de fazer todo o seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="cfa89-299">The strategy is returned after it does all its work.</span></span> <span data-ttu-id="cfa89-300">Armazene o usuário e guarde o token para que você não precise solicitá-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="cfa89-300">Store the user and stash the token so you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cfa89-301">O código anterior usa qualquer usuário que pode se autenticar no servidor.</span><span class="sxs-lookup"><span data-stu-id="cfa89-301">The preceding code takes any user that can authenticate to your server.</span></span> <span data-ttu-id="cfa89-302">Isso é conhecido como registro automático.</span><span class="sxs-lookup"><span data-stu-id="cfa89-302">This is known as auto-registration.</span></span> <span data-ttu-id="cfa89-303">Em um servidor de produção, você não desejará permitir que nenhuma pessoa entre sem primeiro passar por um processo de registro escolhido por você.</span><span class="sxs-lookup"><span data-stu-id="cfa89-303">On a production server, you wouldn’t want to let anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="cfa89-304">Geralmente, esse é o padrão visto em aplicativos de consumidor.</span><span class="sxs-lookup"><span data-stu-id="cfa89-304">This is usually the pattern you see in consumer apps.</span></span> <span data-ttu-id="cfa89-305">O aplicativo pode permitir que você se registre com o Facebook, mas, em seguida, solicita que você insira informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="cfa89-305">The app might allow you to register with Facebook, but then it asks you to enter additional information.</span></span> <span data-ttu-id="cfa89-306">Se você não estava usando um programa de linha de comando para este tutorial, você poderá extrair o email do objeto de token que é retornado.</span><span class="sxs-lookup"><span data-stu-id="cfa89-306">If you weren't using a command-line program for this tutorial, you could extract the email from the token object that is returned.</span></span> <span data-ttu-id="cfa89-307">Em seguida, você poderá solicitar ao usuário que insira informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="cfa89-307">Then, you might ask the user to enter additional information.</span></span> <span data-ttu-id="cfa89-308">Como esse é um servidor de teste, você adiciona o usuário diretamente ao banco de dados na memória.</span><span class="sxs-lookup"><span data-stu-id="cfa89-308">Because this is a test server, you add the user directly to the in-memory database.</span></span>
> 
> 

### <a name="protect-endpoints"></a><span data-ttu-id="cfa89-309">Proteger pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="cfa89-309">Protect endpoints</span></span>
<span data-ttu-id="cfa89-310">Você pode proteger pontos de extremidade, especificando a chamada **passport.authenticate()** com o protocolo que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="cfa89-310">Protect endpoints by specifying the **passport.authenticate()** call with the protocol that you want to use.</span></span>

<span data-ttu-id="cfa89-311">Você pode editar sua rota em seu código de servidor para uma opção mais avançada:</span><span class="sxs-lookup"><span data-stu-id="cfa89-311">You can edit your route in your server code for a more advanced option:</span></span>

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

## <a name="18-run-your-server-application-again"></a><span data-ttu-id="cfa89-312">18: executar o aplicativo para servidores novamente</span><span class="sxs-lookup"><span data-stu-id="cfa89-312">18: Run your server application again</span></span>
<span data-ttu-id="cfa89-313">Use o curl novamente para ver se você tem a proteção OAuth 2.0 para os pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="cfa89-313">Use curl again to see if you have OAuth 2.0 protection against your endpoints.</span></span> <span data-ttu-id="cfa89-314">Faça isso antes de executar qualquer um dos seus SDKs de cliente para esse ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="cfa89-314">Do this before you run any of your client SDKs against this endpoint.</span></span> <span data-ttu-id="cfa89-315">Os cabeçalhos retornados devem lhe informar se a autenticação está funcionando corretamente.</span><span class="sxs-lookup"><span data-stu-id="cfa89-315">The headers returned should tell you if your authentication is working correctly.</span></span>

1.  <span data-ttu-id="cfa89-316">Verifique se a instância do MongoDB está em execução:</span><span class="sxs-lookup"><span data-stu-id="cfa89-316">Make sure that your MongoDB isntance is running:</span></span>

    `$sudo mongod`

2.  <span data-ttu-id="cfa89-317">Altere para o diretório **azuread** e, em seguida, use o curl:</span><span class="sxs-lookup"><span data-stu-id="cfa89-317">Change to the **azuread** directory, and then use curl:</span></span>

    `$ cd azuread`

    `$ node server.js`

3.  <span data-ttu-id="cfa89-318">Tente uma POSTAGEM básica:</span><span class="sxs-lookup"><span data-stu-id="cfa89-318">Try a basic POST:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="cfa89-319">Uma resposta 401 indica que a camada do Passport está tentando redirecionar-se para o ponto de extremidade autorizado, que é exatamente o que você deseja.</span><span class="sxs-lookup"><span data-stu-id="cfa89-319">A 401 response indicates that the Passport layer is trying to redirect to the authorize endpoint, which is exactly what you want.</span></span>

<span data-ttu-id="cfa89-320">*Agora você tem um serviço de API REST que usa OAuth 2.0!*</span><span class="sxs-lookup"><span data-stu-id="cfa89-320">*You now have a REST API service that uses OAuth 2.0!*</span></span>

<span data-ttu-id="cfa89-321">Você já fez tudo o que podia com esse servidor sem usar um cliente compatível com o OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="cfa89-321">You've gone as far as you can with this server without using an OAuth 2.0-compatible client.</span></span> <span data-ttu-id="cfa89-322">Para fazer isso, você precisará examinar um tutorial adicional.</span><span class="sxs-lookup"><span data-stu-id="cfa89-322">For that, you will need to review an additional tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfa89-323">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cfa89-323">Next steps</span></span>
<span data-ttu-id="cfa89-324">Para referência, o exemplo completo (sem seus valores de configuração) é [fornecido como um arquivo .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="cfa89-324">For reference, the completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="cfa89-325">Você também pode cloná-la do GitHub:</span><span class="sxs-lookup"><span data-stu-id="cfa89-325">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="cfa89-326">Agora, você pode passar para tópicos mais avançados.</span><span class="sxs-lookup"><span data-stu-id="cfa89-326">Now, you can move on to more advanced topics.</span></span> <span data-ttu-id="cfa89-327">Talvez você queira experimentar [Proteger um aplicativo Web do Node.js usando o ponto de extremidade v2.0](active-directory-v2-devquickstarts-node-web.md).</span><span class="sxs-lookup"><span data-stu-id="cfa89-327">You might want to try [Secure a Node.js web app using the v2.0 endpoint](active-directory-v2-devquickstarts-node-web.md).</span></span>

<span data-ttu-id="cfa89-328">Estes são alguns recursos adicionais:</span><span class="sxs-lookup"><span data-stu-id="cfa89-328">Here are some additional resources:</span></span>

* [<span data-ttu-id="cfa89-329">Guia do desenvolvedor do Azure AD v2.0</span><span class="sxs-lookup"><span data-stu-id="cfa89-329">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="cfa89-330">Marcação “azure-active-directory” do Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="cfa89-330">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="cfa89-331">Obter atualizações de segurança para nossos produtos</span><span class="sxs-lookup"><span data-stu-id="cfa89-331">Get security updates for our products</span></span>
<span data-ttu-id="cfa89-332">Incentivamos você a se inscrever para receber notificações quando ocorrerem incidentes de segurança.</span><span class="sxs-lookup"><span data-stu-id="cfa89-332">We encourage you to sign up to be notified when security incidents occur.</span></span> <span data-ttu-id="cfa89-333">Na página [Notificações de Segurança Técnica da Microsoft](https://technet.microsoft.com/security/dd252948), assine Alertas de Avisos de Segurança.</span><span class="sxs-lookup"><span data-stu-id="cfa89-333">On the [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe to Security Advisories Alerts.</span></span>

