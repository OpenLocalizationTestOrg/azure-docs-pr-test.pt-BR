---
title: 'Azure AD B2C: proteger uma API Web usando o Node.js | Microsoft Docs'
description: "Como a API da web do toobuild um Node. js que aceita tokens de um locatário B2C"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: fc2b9af8-fbda-44e0-962a-8b963449106a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: 47f5bae025a9ba2f486e36acef36aa37cfb43543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="740a3-103">Azure AD B2C: proteger uma API Web usando o Node .js</span><span class="sxs-lookup"><span data-stu-id="740a3-103">Azure AD B2C: Secure a web API by using Node.js</span></span>
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

<span data-ttu-id="740a3-104">Com o Active Directory B2C do Azure (AD do Azure), você pode proteger uma API Web usando tokens de acesso do OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="740a3-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="740a3-105">Esses tokens permitem que seus aplicativos cliente que usam a API do Azure AD B2C tooauthenticate toohello.</span><span class="sxs-lookup"><span data-stu-id="740a3-105">These tokens allow your client apps that use Azure AD B2C tooauthenticate toohello API.</span></span> <span data-ttu-id="740a3-106">Este artigo mostra como toocreate uma "lista de tarefas" API que permite aos usuários tooadd e lista de tarefas.</span><span class="sxs-lookup"><span data-stu-id="740a3-106">This article shows you how toocreate a "to-do list" API that allows users tooadd and list tasks.</span></span> <span data-ttu-id="740a3-107">Olá web API é protegida usando o Azure AD B2C e só permite que os usuários autenticados toomanage sua lista de tarefas pendentes.</span><span class="sxs-lookup"><span data-stu-id="740a3-107">hello web API is secured using Azure AD B2C and only allows authenticated users toomanage their to-do list.</span></span>

> [!NOTE]
> <span data-ttu-id="740a3-108">Este exemplo foi escrito toobe conectado tooby usando nosso [aplicativo de exemplo do iOS B2C](active-directory-b2c-devquickstarts-ios.md).</span><span class="sxs-lookup"><span data-stu-id="740a3-108">This sample was written toobe connected tooby using our [iOS B2C sample application](active-directory-b2c-devquickstarts-ios.md).</span></span> <span data-ttu-id="740a3-109">Olá passo a passo atual primeiro e depois junto com o exemplo.</span><span class="sxs-lookup"><span data-stu-id="740a3-109">Do hello current walk-through first, and then follow along with that sample.</span></span>
>
>

<span data-ttu-id="740a3-110">**Passport** é middleware de autenticação para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="740a3-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="740a3-111">Flexível e modular, o Passport pode ser instalado sem impedimento em qualquer aplicativo Web baseado em Express ou Restify.</span><span class="sxs-lookup"><span data-stu-id="740a3-111">Flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="740a3-112">Um conjunto abrangente de estratégias que dão suporte à autenticação usando um nome de usuário e uma senha, o Facebook, o Twitter e muito mais.</span><span class="sxs-lookup"><span data-stu-id="740a3-112">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="740a3-113">Desenvolvemos uma estratégia para o Azure AD (Active Directory do Azure).</span><span class="sxs-lookup"><span data-stu-id="740a3-113">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="740a3-114">Instalar este módulo e, em seguida, adicionar Olá AD do Azure `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="740a3-114">You install this module and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="740a3-115">toodo neste exemplo, você precisa:</span><span class="sxs-lookup"><span data-stu-id="740a3-115">toodo this sample, you need to:</span></span>

1. <span data-ttu-id="740a3-116">Registrar um aplicativo com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="740a3-116">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="740a3-117">Configurar seu aplicativo toouse Passport `azure-ad-passport` plug-in.</span><span class="sxs-lookup"><span data-stu-id="740a3-117">Set up your application toouse Passport's `azure-ad-passport` plug-in.</span></span>
3. <span data-ttu-id="740a3-118">Configure um cliente aplicativo toocall hello "lista de tarefas" API da web.</span><span class="sxs-lookup"><span data-stu-id="740a3-118">Configure a client application toocall hello "to-do list" web API.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="740a3-119">Obter um diretório AD B2C do Azure</span><span class="sxs-lookup"><span data-stu-id="740a3-119">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="740a3-120">Antes de usar AD B2C do Azure, você deve criar um diretório ou locatário.</span><span class="sxs-lookup"><span data-stu-id="740a3-120">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="740a3-121">Um diretório é um contêiner para todos os usuários, aplicativos, grupos e muito mais.</span><span class="sxs-lookup"><span data-stu-id="740a3-121">A directory is a container for all users, apps, groups, and more.</span></span>  <span data-ttu-id="740a3-122">Se você ainda não tiver um, [crie um diretório B2C](active-directory-b2c-get-started.md) antes de prosseguir.</span><span class="sxs-lookup"><span data-stu-id="740a3-122">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="740a3-123">Criar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="740a3-123">Create an application</span></span>
<span data-ttu-id="740a3-124">Em seguida, você precisa toocreate um aplicativo em seu diretório do B2C que fornece algumas informações que precisa toosecurely de AD do Azure se comunicar com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="740a3-124">Next, you need toocreate an app in your B2C directory that gives Azure AD some information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="740a3-125">Nesse caso, a saudação aplicativo de cliente e a API da web são representados por um único **ID do aplicativo**, pois elas formam um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="740a3-125">In this case, both hello client app and web API are represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="740a3-126">toocreate um aplicativo, siga [estas instruções](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="740a3-126">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="740a3-127">É necessário que você:</span><span class="sxs-lookup"><span data-stu-id="740a3-127">Be sure to:</span></span>

* <span data-ttu-id="740a3-128">Incluir um **web do aplicativo de web api** no aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="740a3-128">Include a **web app/web api** in hello application</span></span>
* <span data-ttu-id="740a3-129">Digite `http://localhost/TodoListService` como uma **URL de Resposta**.</span><span class="sxs-lookup"><span data-stu-id="740a3-129">Enter `http://localhost/TodoListService` as a **Reply URL**.</span></span> <span data-ttu-id="740a3-130">É saudação padrão URL para este exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="740a3-130">It is hello default URL for this code sample.</span></span>
* <span data-ttu-id="740a3-131">Crie um **Segredo de aplicativo** para seu aplicativo e copie-o.</span><span class="sxs-lookup"><span data-stu-id="740a3-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="740a3-132">Você precisa destes dados mais tarde.</span><span class="sxs-lookup"><span data-stu-id="740a3-132">You need this data later.</span></span> <span data-ttu-id="740a3-133">Observe que esse valor precisa toobe [XML escapado](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) antes de você usá-lo.</span><span class="sxs-lookup"><span data-stu-id="740a3-133">Note that this value needs toobe [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
* <span data-ttu-id="740a3-134">Saudação de cópia **ID do aplicativo** que é atribuído tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="740a3-134">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="740a3-135">Você precisa destes dados mais tarde.</span><span class="sxs-lookup"><span data-stu-id="740a3-135">You need this data later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="740a3-136">Criar suas políticas</span><span class="sxs-lookup"><span data-stu-id="740a3-136">Create your policies</span></span>
<span data-ttu-id="740a3-137">No AD B2C do Azure, cada experiência do usuário é definida por uma [política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="740a3-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="740a3-138">O aplicativo contém duas experiências de identidade: inscrever-se e entrar.</span><span class="sxs-lookup"><span data-stu-id="740a3-138">This app contains two identity experiences: sign up and sign in.</span></span> <span data-ttu-id="740a3-139">Você precisa de uma política de toocreate de cada tipo, conforme descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="740a3-139">You need toocreate one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span>  <span data-ttu-id="740a3-140">Ao criar as três políticas, não deixe de:</span><span class="sxs-lookup"><span data-stu-id="740a3-140">When you create your three policies, be sure to:</span></span>

* <span data-ttu-id="740a3-141">Escolha Olá **nome de exibição** e outros atributos de inscrição em sua política de inscrição.</span><span class="sxs-lookup"><span data-stu-id="740a3-141">Choose hello **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="740a3-142">Escolha Olá **nome de exibição** e **ID de objeto** declarações de aplicativo em cada política.</span><span class="sxs-lookup"><span data-stu-id="740a3-142">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span>  <span data-ttu-id="740a3-143">Você pode escolher outras declarações também.</span><span class="sxs-lookup"><span data-stu-id="740a3-143">You can choose other claims as well.</span></span>
* <span data-ttu-id="740a3-144">Cópia para baixo Olá **nome** de cada política depois de criá-lo.</span><span class="sxs-lookup"><span data-stu-id="740a3-144">Copy down hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="740a3-145">Ele deve ter o prefixo Olá `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="740a3-145">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="740a3-146">Mais tarde, você precisará desses nomes de política.</span><span class="sxs-lookup"><span data-stu-id="740a3-146">You need those policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="740a3-147">Depois de ter criado as três políticas, você está pronto toobuild seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="740a3-147">After you have created your three policies, you're ready toobuild your app.</span></span>

<span data-ttu-id="740a3-148">toolearn sobre como as diretivas funcionam no Azure AD B2C, começam com hello [.NET web aplicativo tutorial de Introdução](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="740a3-148">toolearn about how policies work in Azure AD B2C, start with hello [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="740a3-149">Baixar o código de saudação</span><span class="sxs-lookup"><span data-stu-id="740a3-149">Download hello code</span></span>
<span data-ttu-id="740a3-150">Olá código para este tutorial [é mantida no GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="740a3-150">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span></span> <span data-ttu-id="740a3-151">exemplo de hello toobuild que você vá, você pode [baixar um projeto de esqueleto como um arquivo. zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="740a3-151">toobuild hello sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="740a3-152">Também é possível clonar o esqueleto do hello:</span><span class="sxs-lookup"><span data-stu-id="740a3-152">You can also clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

<span data-ttu-id="740a3-153">aplicativo Hello concluída também é [disponível como um arquivo. zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) ou em Olá `complete` ramificação da saudação mesmo repositório.</span><span class="sxs-lookup"><span data-stu-id="740a3-153">hello completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) or on hello `complete` branch of hello same repository.</span></span>

## <a name="download-nodejs-for-your-platform"></a><span data-ttu-id="740a3-154">Baixar o Node.js para sua plataforma</span><span class="sxs-lookup"><span data-stu-id="740a3-154">Download Node.js for your platform</span></span>
<span data-ttu-id="740a3-155">toosuccessfully usar este exemplo, você precisa de uma instalação de trabalho do Node. js.</span><span class="sxs-lookup"><span data-stu-id="740a3-155">toosuccessfully use this sample, you need a working installation of Node.js.</span></span>

<span data-ttu-id="740a3-156">Instale o Node.js de [nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="740a3-156">Install Node.js from [nodejs.org](http://nodejs.org).</span></span>

## <a name="install-mongodb-for-your-platform"></a><span data-ttu-id="740a3-157">Instalar o MongoDB para sua plataforma</span><span class="sxs-lookup"><span data-stu-id="740a3-157">Install MongoDB for your platform</span></span>
<span data-ttu-id="740a3-158">toosuccessfully usar este exemplo, você precisa de uma instalação de trabalho do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="740a3-158">toosuccessfully use this sample, you need a working installation of MongoDB.</span></span> <span data-ttu-id="740a3-159">Podemos usar o MongoDB toomake API REST persistente em instâncias de servidor.</span><span class="sxs-lookup"><span data-stu-id="740a3-159">We use MongoDB toomake your REST API persistent across server instances.</span></span>

<span data-ttu-id="740a3-160">Instale o MongoDB de [mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="740a3-160">Install MongoDB from [mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="740a3-161">Este passo a passo pressupõe que você use Olá instalação e o servidor de pontos de extremidade padrão para o MongoDB, que em tempo de saudação da redação deste artigo é `mongodb://localhost`.</span><span class="sxs-lookup"><span data-stu-id="740a3-161">This walk-through assumes that you use hello default installation and server endpoints for MongoDB, which at hello time of this writing is `mongodb://localhost`.</span></span>
>
>

## <a name="install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="740a3-162">Instalar módulos de Restify Olá em sua API da web</span><span class="sxs-lookup"><span data-stu-id="740a3-162">Install hello Restify modules in your web API</span></span>
<span data-ttu-id="740a3-163">Usamos Restify toobuild a API REST.</span><span class="sxs-lookup"><span data-stu-id="740a3-163">We use Restify toobuild your REST API.</span></span> <span data-ttu-id="740a3-164">O Restify é uma estrutura de aplicativo do Node.js mínima e flexível, derivada do Express.</span><span class="sxs-lookup"><span data-stu-id="740a3-164">Restify is a minimal and flexible Node.js application framework derived from Express.</span></span> <span data-ttu-id="740a3-165">Tem um conjunto robusto de recursos para a criação de APIs REST sobre o Connect.</span><span class="sxs-lookup"><span data-stu-id="740a3-165">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="740a3-166">Instalar Restify</span><span class="sxs-lookup"><span data-stu-id="740a3-166">Install Restify</span></span>
<span data-ttu-id="740a3-167">Olá linha de comando, altere seu diretório muito`azuread`.</span><span class="sxs-lookup"><span data-stu-id="740a3-167">From hello command line, change your directory too`azuread`.</span></span> <span data-ttu-id="740a3-168">Se hello `azuread` diretório não existe, criá-lo.</span><span class="sxs-lookup"><span data-stu-id="740a3-168">If hello `azuread` directory doesn't exist, create it.</span></span>

<span data-ttu-id="740a3-169">`cd azuread` ou `mkdir azuread;`</span><span class="sxs-lookup"><span data-stu-id="740a3-169">`cd azuread` or `mkdir azuread;`</span></span>

<span data-ttu-id="740a3-170">Digite hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="740a3-170">Enter hello following command:</span></span>

`npm install restify`

<span data-ttu-id="740a3-171">Este comando instala o Restify.</span><span class="sxs-lookup"><span data-stu-id="740a3-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="740a3-172">Você obteve um erro?</span><span class="sxs-lookup"><span data-stu-id="740a3-172">Did you get an error?</span></span>
<span data-ttu-id="740a3-173">Em alguns sistemas operacionais, quando você usa `npm`, você pode receber o erro Olá `Error: EPERM, chmod '/usr/local/bin/..'` e uma solicitação que você execute conta hello como um administrador.</span><span class="sxs-lookup"><span data-stu-id="740a3-173">In some operating systems, when you use `npm`, you may receive hello error `Error: EPERM, chmod '/usr/local/bin/..'` and a request that you run hello account as an administrator.</span></span> <span data-ttu-id="740a3-174">Se ocorrer esse problema, use Olá `sudo` toorun comando `npm` em um nível de privilégio mais alto.</span><span class="sxs-lookup"><span data-stu-id="740a3-174">If this problem occurs, use hello `sudo` command toorun `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-a-dtrace-error"></a><span data-ttu-id="740a3-175">Você recebeu um erro DTrace?</span><span class="sxs-lookup"><span data-stu-id="740a3-175">Did you get a DTrace error?</span></span>
<span data-ttu-id="740a3-176">Você pode ver algo como este texto ao instalar o Restify:</span><span class="sxs-lookup"><span data-stu-id="740a3-176">You may see something like this text when you install Restify:</span></span>

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
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

<span data-ttu-id="740a3-177">O Restify fornece um mecanismo poderoso para rastreamento de chamadas REST usando o DTrace.</span><span class="sxs-lookup"><span data-stu-id="740a3-177">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="740a3-178">No entanto, muitos sistemas operacionais não têm o DTrace disponível.</span><span class="sxs-lookup"><span data-stu-id="740a3-178">However, many operating systems do not have DTrace available.</span></span> <span data-ttu-id="740a3-179">Você pode ignorar com segurança esses erros.</span><span class="sxs-lookup"><span data-stu-id="740a3-179">You can safely ignore these errors.</span></span>

<span data-ttu-id="740a3-180">saída de saudação do comando de saudação deve aparecer texto toothis semelhante:</span><span class="sxs-lookup"><span data-stu-id="740a3-180">hello output of hello command should appear similar toothis text:</span></span>

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
    └── bunyan@0.22.0 (mv@0.0.5)

## <a name="install-passport-in-your-web-api"></a><span data-ttu-id="740a3-181">Instalar o Passport.js na API Web</span><span class="sxs-lookup"><span data-stu-id="740a3-181">Install Passport in your web API</span></span>
<span data-ttu-id="740a3-182">Olá linha de comando, altere seu diretório muito`azuread`, se ainda não estiver lá.</span><span class="sxs-lookup"><span data-stu-id="740a3-182">From hello command line, change your directory too`azuread`, if it's not already there.</span></span>

<span data-ttu-id="740a3-183">Instale o Passport usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="740a3-183">Install Passport using hello following command:</span></span>

`npm install passport`

<span data-ttu-id="740a3-184">saída de saudação do comando Olá deve ser texto toothis semelhante:</span><span class="sxs-lookup"><span data-stu-id="740a3-184">hello output of hello command should be similar toothis text:</span></span>

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-tooyour-web-api"></a><span data-ttu-id="740a3-185">Adicionar passport azuread tooyour web API</span><span class="sxs-lookup"><span data-stu-id="740a3-185">Add passport-azuread tooyour web API</span></span>
<span data-ttu-id="740a3-186">Em seguida, adicione a estratégia de OAuth hello usando `passport-azuread`, um conjunto de estratégias que se conectam do AD do Azure com o Passport.</span><span class="sxs-lookup"><span data-stu-id="740a3-186">Next, add hello OAuth strategy by using `passport-azuread`, a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="740a3-187">Use essa estratégia para tokens de portador no exemplo de API REST hello.</span><span class="sxs-lookup"><span data-stu-id="740a3-187">Use this strategy for bearer tokens in hello REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="740a3-188">Embora o OAuth2 forneça uma estrutura na qual qualquer tipo de token conhecido pode ser emitido, somente determinados tipos de token passaram a ser amplamente usados.</span><span class="sxs-lookup"><span data-stu-id="740a3-188">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types have gained widespread use.</span></span> <span data-ttu-id="740a3-189">tokens de saudação para proteger pontos de extremidade são tokens de portador.</span><span class="sxs-lookup"><span data-stu-id="740a3-189">hello tokens for protecting endpoints are bearer tokens.</span></span> <span data-ttu-id="740a3-190">Esses tipos de tokens são hello mais amplamente emitido em OAuth2.</span><span class="sxs-lookup"><span data-stu-id="740a3-190">These types of tokens are hello most widely issued in OAuth2.</span></span> <span data-ttu-id="740a3-191">Muitas implementações supõem que os tokens de portador são Olá único tipo de token emitido.</span><span class="sxs-lookup"><span data-stu-id="740a3-191">Many implementations assume that bearer tokens are hello only type of token issued.</span></span>
>
>

<span data-ttu-id="740a3-192">Olá linha de comando, altere seu diretório muito`azuread`, se ainda não estiver lá.</span><span class="sxs-lookup"><span data-stu-id="740a3-192">From hello command line, change your directory too`azuread`, if it's not already there.</span></span>

<span data-ttu-id="740a3-193">Instalar Olá Passport `passport-azure-ad` módulo usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="740a3-193">Install hello Passport `passport-azure-ad` module using hello following command:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="740a3-194">saída de saudação do comando Olá deve ser texto toothis semelhante:</span><span class="sxs-lookup"><span data-stu-id="740a3-194">hello output of hello command should be similar toothis text:</span></span>

``
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
``

## <a name="add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="740a3-195">Adicionar de API da web do MongoDB módulos tooyour</span><span class="sxs-lookup"><span data-stu-id="740a3-195">Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="740a3-196">Este exemplo usa o MongoDB como repositório de dados.</span><span class="sxs-lookup"><span data-stu-id="740a3-196">This sample uses MongoDB as your data store.</span></span> <span data-ttu-id="740a3-197">Para isso, instale o Mongoose, um plug-in amplamente utilizado para gerenciar modelos e esquemas.</span><span class="sxs-lookup"><span data-stu-id="740a3-197">For that install Mongoose, a widely used plug-in for managing models and schemas.</span></span>

* `npm install mongoose`

## <a name="install-additional-modules"></a><span data-ttu-id="740a3-198">Instalar módulos adicionais</span><span class="sxs-lookup"><span data-stu-id="740a3-198">Install additional modules</span></span>
<span data-ttu-id="740a3-199">Em seguida, instale Olá restantes módulos necessários.</span><span class="sxs-lookup"><span data-stu-id="740a3-199">Next, install hello remaining required modules.</span></span>

<span data-ttu-id="740a3-200">Olá linha de comando, altere seu diretório muito`azuread`, se ainda não estiver lá:</span><span class="sxs-lookup"><span data-stu-id="740a3-200">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="740a3-201">Instalar módulos Olá no seu `node_modules` diretório:</span><span class="sxs-lookup"><span data-stu-id="740a3-201">Install hello modules in your `node_modules` directory:</span></span>

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a><span data-ttu-id="740a3-202">Criar um arquivo server.js com suas dependências</span><span class="sxs-lookup"><span data-stu-id="740a3-202">Create a server.js file with your dependencies</span></span>
<span data-ttu-id="740a3-203">Olá `server.js` arquivo fornece a maioria de saudação da funcionalidade de saudação para seu servidor de API da Web.</span><span class="sxs-lookup"><span data-stu-id="740a3-203">hello `server.js` file provides hello majority of hello functionality for your Web API server.</span></span>

<span data-ttu-id="740a3-204">Olá linha de comando, altere seu diretório muito`azuread`, se ainda não estiver lá:</span><span class="sxs-lookup"><span data-stu-id="740a3-204">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="740a3-205">Crie um arquivo `server.js` em um editor.</span><span class="sxs-lookup"><span data-stu-id="740a3-205">Create a `server.js` file in an editor.</span></span> <span data-ttu-id="740a3-206">Adicione Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="740a3-206">Add hello following information:</span></span>

```Javascript
'use strict';
/**
* Module dependencies.
*/
var fs = require('fs');
var path = require('path');
var util = require('util');
var assert = require('assert-plus');
var mongoose = require('mongoose/');
var bunyan = require('bunyan');
var restify = require('restify');
var config = require('./config');
var passport = require('passport');
var OIDCBearerStrategy = require('passport-azure-ad').BearerStrategy;
```

<span data-ttu-id="740a3-207">Salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="740a3-207">Save hello file.</span></span> <span data-ttu-id="740a3-208">Você pode retornar tooit mais tarde.</span><span class="sxs-lookup"><span data-stu-id="740a3-208">You return tooit later.</span></span>

## <a name="create-a-configjs-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="740a3-209">Criar um toostore de arquivo config.js suas configurações do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="740a3-209">Create a config.js file toostore your Azure AD settings</span></span>
<span data-ttu-id="740a3-210">Esse arquivo de código passa parâmetros de configuração de saudação do seu Portal do AD do Azure toohello `Passport.js` arquivo.</span><span class="sxs-lookup"><span data-stu-id="740a3-210">This code file passes hello configuration parameters from your Azure AD Portal toohello `Passport.js` file.</span></span> <span data-ttu-id="740a3-211">Você criou esses valores de configuração quando você adicionou o portal de toohello Olá web API a primeira parte Olá passo a passo hello.</span><span class="sxs-lookup"><span data-stu-id="740a3-211">You created these configuration values when you added hello web API toohello portal in hello first part of hello walk-through.</span></span> <span data-ttu-id="740a3-212">Explicamos que tooput em valores desses parâmetros Olá depois de copiar o código de saudação.</span><span class="sxs-lookup"><span data-stu-id="740a3-212">We explain what tooput in hello values of these parameters after you copy hello code.</span></span>

<span data-ttu-id="740a3-213">Olá linha de comando, altere seu diretório muito`azuread`, se ainda não estiver lá:</span><span class="sxs-lookup"><span data-stu-id="740a3-213">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="740a3-214">Crie um arquivo `config.js` em um editor.</span><span class="sxs-lookup"><span data-stu-id="740a3-214">Create a `config.js` file in an editor.</span></span> <span data-ttu-id="740a3-215">Adicione Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="740a3-215">Add hello following information:</span></span>

```Javascript
// Don't commit this file tooyour public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in hello portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // hello Client ID of hello application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add hello B2C tenant name in hello <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is hello policy you'll want toovalidate against in B2C. Usually this is your Sign-in policy (as users sign in toothis API)
passReqToCallback: false // This is a node.js construct that lets you pass hello req all hello way back tooany upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a><span data-ttu-id="740a3-216">Valores necessários</span><span class="sxs-lookup"><span data-stu-id="740a3-216">Required values</span></span>
<span data-ttu-id="740a3-217">`clientID`: Olá ID do cliente do seu aplicativo de API da Web.</span><span class="sxs-lookup"><span data-stu-id="740a3-217">`clientID`: hello client ID of your Web API application.</span></span>

<span data-ttu-id="740a3-218">`IdentityMetadata`: Esse é o local onde `passport-azure-ad` procura os dados de configuração para o provedor de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="740a3-218">`IdentityMetadata`: This is where `passport-azure-ad` looks for your configuration data for hello identity provider.</span></span> <span data-ttu-id="740a3-219">Ele também procura tokens da web JSON de saudação do hello chaves toovalidate.</span><span class="sxs-lookup"><span data-stu-id="740a3-219">It also looks for hello keys toovalidate hello JSON web tokens.</span></span>

<span data-ttu-id="740a3-220">`audience`: Olá identificador de recurso uniforme (URI) do portal de saudação que identifica seu aplicativo de chamada.</span><span class="sxs-lookup"><span data-stu-id="740a3-220">`audience`: hello uniform resource identifier (URI) from hello portal that identifies your calling application.</span></span>

<span data-ttu-id="740a3-221">`tenantName`: o nome do locatário (por exemplo, **contoso.onmicrosoft.com**).</span><span class="sxs-lookup"><span data-stu-id="740a3-221">`tenantName`: Your tenant name (for example, **contoso.onmicrosoft.com**).</span></span>

<span data-ttu-id="740a3-222">`policyName`: Olá política que deseja que os tokens de saudação toovalidate as novidades no servidor tooyour.</span><span class="sxs-lookup"><span data-stu-id="740a3-222">`policyName`: hello policy that you want toovalidate hello tokens coming in tooyour server.</span></span> <span data-ttu-id="740a3-223">Esta política deve ser Olá política mesmo que você usa no aplicativo de cliente hello para entrar.</span><span class="sxs-lookup"><span data-stu-id="740a3-223">This policy should be hello same policy that you use on hello client application for sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="740a3-224">Por enquanto, use Olá mesmo políticas pela instalação de cliente e servidor.</span><span class="sxs-lookup"><span data-stu-id="740a3-224">For now, use hello same policies across both client and server setup.</span></span> <span data-ttu-id="740a3-225">Se você já tiver concluído uma apresentação e criar essas políticas, você não precisa toodo novamente.</span><span class="sxs-lookup"><span data-stu-id="740a3-225">If you have already completed a walk-through and created these policies, you don't need toodo so again.</span></span> <span data-ttu-id="740a3-226">Como concluir o passo a passo Olá, você não deve necessário tooset novas políticas para orientações de cliente no site de saudação.</span><span class="sxs-lookup"><span data-stu-id="740a3-226">Because you completed hello walk-through, you shouldn't need tooset up new policies for client walk-throughs on hello site.</span></span>
>
>

## <a name="add-configuration-tooyour-serverjs-file"></a><span data-ttu-id="740a3-227">Adicionar o arquivo de configuração de server.js tooyour</span><span class="sxs-lookup"><span data-stu-id="740a3-227">Add configuration tooyour server.js file</span></span>
<span data-ttu-id="740a3-228">tooread valores Olá Olá `config.js` arquivo criado, adicione Olá `.config` arquivo como um recurso necessário em seu aplicativo e depois defina Olá variáveis globais toothose no hello `config.js` documento.</span><span class="sxs-lookup"><span data-stu-id="740a3-228">tooread hello values from hello `config.js` file you created, add hello `.config` file as a required resource in your application, and then set hello global variables toothose in hello `config.js` document.</span></span>

<span data-ttu-id="740a3-229">Olá linha de comando, altere seu diretório muito`azuread`, se ainda não estiver lá:</span><span class="sxs-lookup"><span data-stu-id="740a3-229">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="740a3-230">Olá abrir `server.js` arquivo em um editor.</span><span class="sxs-lookup"><span data-stu-id="740a3-230">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="740a3-231">Adicione Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="740a3-231">Add hello following information:</span></span>

```Javascript
var config = require('./config');
```
<span data-ttu-id="740a3-232">Adicionar uma nova seção muito`server.js` que inclui a saudação de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="740a3-232">Add a new section too`server.js` that includes hello following code:</span></span>

```Javascript
// We pass these options in toohello ODICBearerStrategy.

var options = {
    // hello URL of hello metadata document for your app. We put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

<span data-ttu-id="740a3-233">Em seguida, vamos adicionar alguns espaços reservados para os usuários de saudação que recebemos de nossos aplicativos de chamada.</span><span class="sxs-lookup"><span data-stu-id="740a3-233">Next, let's add some placeholders for hello users we receive from our calling applications.</span></span>

```Javascript
// array toohold logged in users and hello current logged in user (owner)
var users = [];
var owner = null;
```

<span data-ttu-id="740a3-234">Vamos prosseguir e criar nosso logger também.</span><span class="sxs-lookup"><span data-stu-id="740a3-234">Let's go ahead and create our logger too.</span></span>

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="740a3-235">Adicionar informações de modelo e o esquema do MongoDB hello usando Mongoose</span><span class="sxs-lookup"><span data-stu-id="740a3-235">Add hello MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="740a3-236">Olá preparação anterior paga como trazer esses três arquivos juntos em um serviço de API REST.</span><span class="sxs-lookup"><span data-stu-id="740a3-236">hello earlier preparation pays off as you bring these three files together in a REST API service.</span></span>

<span data-ttu-id="740a3-237">Para este passo a passo, use MongoDB toostore suas tarefas, conforme discutido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="740a3-237">For this walk-through, use MongoDB toostore your tasks, as discussed earlier.</span></span>

<span data-ttu-id="740a3-238">Em Olá `config.js` arquivo, você chamou o seu banco de dados **tasklist**.</span><span class="sxs-lookup"><span data-stu-id="740a3-238">In hello `config.js` file, you called your database **tasklist**.</span></span> <span data-ttu-id="740a3-239">Esse nome também é o que é colocado no final de saudação do hello `mongoose_auth_local` URL de conexão.</span><span class="sxs-lookup"><span data-stu-id="740a3-239">That name was also what you put at hello end of hello `mongoose_auth_local` connection URL.</span></span> <span data-ttu-id="740a3-240">Você não precisa toocreate banco de dados com antecedência no MongoDB.</span><span class="sxs-lookup"><span data-stu-id="740a3-240">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="740a3-241">Ele cria o banco de dados de saudação para você na primeira execução de saudação do seu aplicativo de servidor.</span><span class="sxs-lookup"><span data-stu-id="740a3-241">It creates hello database for you on hello first run of your server application.</span></span>

<span data-ttu-id="740a3-242">Depois que você informa o servidor de saudação que toouse de banco de dados do MongoDB, você precisa toowrite alguns adicionais toocreate Olá modelo e código de esquema para suas tarefas de servidor.</span><span class="sxs-lookup"><span data-stu-id="740a3-242">After you tell hello server which MongoDB database toouse, you need toowrite some additional code toocreate hello model and schema for your server tasks.</span></span>

### <a name="expand-hello-model"></a><span data-ttu-id="740a3-243">Expanda o modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="740a3-243">Expand hello model</span></span>
<span data-ttu-id="740a3-244">Esse modelo de esquema é simples.</span><span class="sxs-lookup"><span data-stu-id="740a3-244">This schema model is simple.</span></span> <span data-ttu-id="740a3-245">Você pode expandi-lo conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="740a3-245">You can expand it as required.</span></span>

<span data-ttu-id="740a3-246">`owner`: Que é atribuído a tarefa toohello.</span><span class="sxs-lookup"><span data-stu-id="740a3-246">`owner`: Who is assigned toohello task.</span></span> <span data-ttu-id="740a3-247">Este objeto é uma **cadeia de caracteres**.</span><span class="sxs-lookup"><span data-stu-id="740a3-247">This object is a **string**.</span></span>  

<span data-ttu-id="740a3-248">`Text`: tarefa Olá em si.</span><span class="sxs-lookup"><span data-stu-id="740a3-248">`Text`: hello task itself.</span></span> <span data-ttu-id="740a3-249">Este objeto é uma **cadeia de caracteres**.</span><span class="sxs-lookup"><span data-stu-id="740a3-249">This object is a **string**.</span></span>

<span data-ttu-id="740a3-250">`date`: date de hello tarefa hello está vencida.</span><span class="sxs-lookup"><span data-stu-id="740a3-250">`date`: hello date that hello task is due.</span></span> <span data-ttu-id="740a3-251">Este objeto é um **datetime**.</span><span class="sxs-lookup"><span data-stu-id="740a3-251">This object is a **datetime**.</span></span>

<span data-ttu-id="740a3-252">`completed`: Se Olá tarefa foi concluída.</span><span class="sxs-lookup"><span data-stu-id="740a3-252">`completed`: If hello task is complete.</span></span> <span data-ttu-id="740a3-253">Este objeto é um **Booliano**.</span><span class="sxs-lookup"><span data-stu-id="740a3-253">This object is a **Boolean**.</span></span>

### <a name="create-hello-schema-in-hello-code"></a><span data-ttu-id="740a3-254">Criar esquema Olá no código de saudação</span><span class="sxs-lookup"><span data-stu-id="740a3-254">Create hello schema in hello code</span></span>
<span data-ttu-id="740a3-255">Olá linha de comando, altere seu diretório muito`azuread`, se ainda não estiver lá:</span><span class="sxs-lookup"><span data-stu-id="740a3-255">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="740a3-256">Olá abrir `server.js` arquivo em um editor.</span><span class="sxs-lookup"><span data-stu-id="740a3-256">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="740a3-257">Adicione Olá informações abaixo da entrada de configuração de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="740a3-257">Add hello following information below hello configuration entry:</span></span>

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect tooMongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema toostore our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use hello schema tooregister a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
<span data-ttu-id="740a3-258">Criar esquema Olá primeiro e, em seguida, você cria um objeto de modelo que você usar toostore seus dados durante a saudação de código ao definir sua **rotas**.</span><span class="sxs-lookup"><span data-stu-id="740a3-258">You first create hello schema, and then you create a model object that you use toostore your data throughout hello code when you define your **routes**.</span></span>

## <a name="add-routes-for-your-rest-api-task-server"></a><span data-ttu-id="740a3-259">Adicionar rotas para o servidor de tarefa da API REST</span><span class="sxs-lookup"><span data-stu-id="740a3-259">Add routes for your REST API task server</span></span>
<span data-ttu-id="740a3-260">Agora que você tem um toowork de modelo de banco de dados com, adicione rotas Olá usado para o seu servidor de API REST.</span><span class="sxs-lookup"><span data-stu-id="740a3-260">Now that you have a database model toowork with, add hello routes you use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="740a3-261">Sobre rotas no Restify</span><span class="sxs-lookup"><span data-stu-id="740a3-261">About routes in Restify</span></span>
<span data-ttu-id="740a3-262">Rotas funcionam em Restify em Olá mesma forma como funcionam quando eles usam a pilha do hello Express.</span><span class="sxs-lookup"><span data-stu-id="740a3-262">Routes work in Restify in hello same way that they work when they use hello Express stack.</span></span> <span data-ttu-id="740a3-263">Definir rotas usando Olá URI que você espera Olá toocall de aplicativos de cliente.</span><span class="sxs-lookup"><span data-stu-id="740a3-263">You define routes by using hello URI that you expect hello client applications toocall.</span></span>

<span data-ttu-id="740a3-264">Um padrão típico para uma rota do Restify é:</span><span class="sxs-lookup"><span data-stu-id="740a3-264">A typical pattern for a Restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep hello server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

<span data-ttu-id="740a3-265">O Restify e o Express fornecem funcionalidade muito mais aprofundada, como a definição de tipos de aplicativos e o roteamento complexo entre diferentes pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="740a3-265">Restify and Express can provide much deeper functionality, such as defining application types and doing complex routing across different endpoints.</span></span> <span data-ttu-id="740a3-266">Para fins de saudação deste tutorial, podemos manter essas rotas simples.</span><span class="sxs-lookup"><span data-stu-id="740a3-266">For hello purposes of this tutorial, we keep these routes simple.</span></span>

#### <a name="add-default-routes-tooyour-server"></a><span data-ttu-id="740a3-267">Adicionar servidor de tooyour rotas padrão</span><span class="sxs-lookup"><span data-stu-id="740a3-267">Add default routes tooyour server</span></span>
<span data-ttu-id="740a3-268">Agora que você adicionar Olá básica CRUD rotas **criar** e **lista** para nossa API REST.</span><span class="sxs-lookup"><span data-stu-id="740a3-268">You now add hello basic CRUD routes of **create** and **list** for our REST API.</span></span> <span data-ttu-id="740a3-269">Outras rotas podem ser encontradas no hello `complete` ramificação do exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="740a3-269">Other routes can be found in hello `complete` branch of hello sample.</span></span>

<span data-ttu-id="740a3-270">Olá linha de comando, altere seu diretório muito`azuread`, se ainda não estiver lá:</span><span class="sxs-lookup"><span data-stu-id="740a3-270">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="740a3-271">Olá abrir `server.js` arquivo em um editor.</span><span class="sxs-lookup"><span data-stu-id="740a3-271">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="740a3-272">Abaixo de entradas de banco de dados de saudação feitas acima adicionar Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="740a3-272">Below hello database entries you made above add hello following information:</span></span>

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it tooMongodb
    var _task = new Task();

    if (!req.params.Text) {
        req.log.warn({
            params: req.params
        }, 'createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.Text = req.params.Text;
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
```

```Javascript
/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

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
            log.warn(err, "There is no tasks in hello database. Add one!");
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


#### <a name="add-error-handling-for-hello-routes"></a><span data-ttu-id="740a3-273">Adicionar o tratamento de erros para rotas de saudação</span><span class="sxs-lookup"><span data-stu-id="740a3-273">Add error handling for hello routes</span></span>
<span data-ttu-id="740a3-274">Adicione alguns tratamentos de erro para que você possa comunicar os problemas encontrados back toohello cliente de forma que ele possa entender.</span><span class="sxs-lookup"><span data-stu-id="740a3-274">Add some error handling so that you can communicate any problems you encounter back toohello client in a way that it can understand.</span></span>

<span data-ttu-id="740a3-275">Adicione Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="740a3-275">Add hello following code:</span></span>

```Javascript
///--- Errors for communicating something interesting back toohello client
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


## <a name="create-your-server"></a><span data-ttu-id="740a3-276">Criar seu servidor</span><span class="sxs-lookup"><span data-stu-id="740a3-276">Create your server</span></span>
<span data-ttu-id="740a3-277">Agora você definiu o banco de dados e incluiu as rotas.</span><span class="sxs-lookup"><span data-stu-id="740a3-277">You have now defined your database and put your routes in place.</span></span> <span data-ttu-id="740a3-278">Olá última coisa para você toodo é instância de servidor de saudação tooadd que gerencia suas chamadas.</span><span class="sxs-lookup"><span data-stu-id="740a3-278">hello last thing for you toodo is tooadd hello server instance that manages your calls.</span></span>

<span data-ttu-id="740a3-279">Restify e Express fornecem personalização profunda para um servidor de API REST, mas podemos usar a configuração mais básica do hello aqui.</span><span class="sxs-lookup"><span data-stu-id="740a3-279">Restify and Express provide deep customization for a REST API server, but we use hello most basic setup here.</span></span>

```Javascript

/**
 * Our Server
 */


var server = restify.createServer({
    name: "Microsoft Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//
server.pre(restify.pre.sanitizePath());

// Handles annoying user agents (curl)
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in)
server.use(restify.requestLogger());

// Allow 5 requests/second by IP, and burst too10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping tooREST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-hello-routes-toohello-server-without-authentication"></a><span data-ttu-id="740a3-280">Adicionar servidor de toohello rotas hello (sem autenticação)</span><span class="sxs-lookup"><span data-stu-id="740a3-280">Add hello routes toohello server (without authentication)</span></span>
```Javascript
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.head('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.post('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.post('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.del('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeAll, function respond(req, res, next) {
    res.send(204);
    next();
});


// Register a default '/' handler

server.get('/', function root(req, res, next) {
    var routes = [
        'GET     /',
        'POST    /api/tasks/:owner/:task',
        'POST    /api/tasks (for JSON body)',
        'GET     /api/tasks',
        'PUT     /api/tasks/:owner',
        'GET     /api/tasks/:owner',
        'DELETE  /api/tasks/:owner/:task'
    ];
    res.send(200, routes);
    next();
});
```

```Javascript

server.listen(serverPort, function() {

    var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
    consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
    consoleMessage += '\n %s server is listening at %s';
    consoleMessage += '\n Open your browser too%s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-tooyour-rest-api-server"></a><span data-ttu-id="740a3-281">Adicionar servidor de API REST de tooyour de autenticação</span><span class="sxs-lookup"><span data-stu-id="740a3-281">Add authentication tooyour REST API server</span></span>
<span data-ttu-id="740a3-282">Agora que tem um servidor de API REST em execução, você pode torná-lo útil no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="740a3-282">Now that you have a running REST API server, you can make it useful against Azure AD.</span></span>

<span data-ttu-id="740a3-283">Olá linha de comando, altere seu diretório muito`azuread`, se ainda não estiver lá:</span><span class="sxs-lookup"><span data-stu-id="740a3-283">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="740a3-284">Use Olá OIDCBearerStrategy que está incluído no ad de azure passport</span><span class="sxs-lookup"><span data-stu-id="740a3-284">Use hello OIDCBearerStrategy that is included with passport-azure-ad</span></span>
> [!TIP]
> <span data-ttu-id="740a3-285">Quando você escreve APIs, você deve sempre vincular Olá dados toosomething exclusivo do token Olá Olá usuário não pode falsificar.</span><span class="sxs-lookup"><span data-stu-id="740a3-285">When you write APIs, you should always link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="740a3-286">Quando o servidor de saudação armazena itens de tarefas, ele faz então com base em Olá **oid** do usuário Olá no token de saudação (chamado por meio de token.oid), que vai no campo proprietário"Olá".</span><span class="sxs-lookup"><span data-stu-id="740a3-286">When hello server stores ToDo items, it does so based on hello **oid** of hello user in hello token (called through token.oid), which goes in hello “owner” field.</span></span> <span data-ttu-id="740a3-287">Esse valor garante que somente o usuário possa acessar seus próprios itens de Tarefas Pendentes.</span><span class="sxs-lookup"><span data-stu-id="740a3-287">This value ensures that only that user can access their own ToDo items.</span></span> <span data-ttu-id="740a3-288">Não há nenhuma exposição no Olá API de "proprietário", para que um usuário externo pode solicitar outros itens de tarefas, mesmo quando eles são autenticados.</span><span class="sxs-lookup"><span data-stu-id="740a3-288">There is no exposure in hello API of “owner,” so an external user can request others’ ToDo items even if they are authenticated.</span></span>
>
>

<span data-ttu-id="740a3-289">Em seguida, usar a estratégia de portador de saudação que vem com `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="740a3-289">Next, use hello bearer strategy that comes with `passport-azure-ad`.</span></span>

```Javascript
var findById = function(id, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
        var user = users[i];
        if (user.oid === id) {
            log.info('Found user: ', user);
            return fn(null, user);
        }
    }
    return fn(null, null);
};


var oidcStrategy = new OIDCBearerStrategy(options,
    function(token, done) {
        log.info('verifying hello user');
        log.info(token, 'was hello token retreived');
        findById(token.sub, function(err, user) {
            if (err) {
                return done(err);
            }
            if (!user) {
                // "Auto-registration"
                log.info('User was added automatically as they were new. Their sub is: ', token.oid);
                users.push(token);
                owner = token.oid;
                return done(null, token);
            }
            owner = token.sub;
            return done(null, user, token);
        });
    }
);

passport.use(oidcStrategy);
```

<span data-ttu-id="740a3-290">Passport usa Olá mesmo padrão para todas as suas estratégias.</span><span class="sxs-lookup"><span data-stu-id="740a3-290">Passport uses hello same pattern for all its strategies.</span></span> <span data-ttu-id="740a3-291">Você o passa como um `function()` que tem `token` e `done` como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="740a3-291">You pass it a `function()` that has `token` and `done` as parameters.</span></span> <span data-ttu-id="740a3-292">estratégia de saudação volta tooyou depois que ela fez todo seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="740a3-292">hello strategy comes back tooyou after it has done all of its work.</span></span> <span data-ttu-id="740a3-293">Você deve armazenar usuário hello e salvar o token Olá para que você não precisa tooask para ele novamente.</span><span class="sxs-lookup"><span data-stu-id="740a3-293">You should then store hello user and save hello token so that you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="740a3-294">código de saudação acima usa qualquer usuário que acontece tooauthenticate tooyour server.</span><span class="sxs-lookup"><span data-stu-id="740a3-294">hello code above takes any user who happens tooauthenticate tooyour server.</span></span> <span data-ttu-id="740a3-295">Este processo é conhecido como registro automático.</span><span class="sxs-lookup"><span data-stu-id="740a3-295">This process is known as autoregistration.</span></span> <span data-ttu-id="740a3-296">Em servidores de produção, não deixe em qualquer API de saudação de acesso de usuários, sem ter que primeiro-los passar por um processo de registro.</span><span class="sxs-lookup"><span data-stu-id="740a3-296">In production servers, don't let in any users access hello API without first having them go through a registration process.</span></span> <span data-ttu-id="740a3-297">Esse processo é geralmente padrão Olá que consulte em aplicativos cliente que permitem que você tooregister usando o Facebook, mas, em seguida, solicitar que você toofill informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="740a3-297">This process is usually hello pattern you see in consumer apps that allow you tooregister by using Facebook but then ask you toofill out additional information.</span></span> <span data-ttu-id="740a3-298">Se este programa não um programa de linha de comando, podemos foi ter extrair email saudação do objeto de token de saudação que é retornado e, em seguida, terá os usuários toofill informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="740a3-298">If this program wasn’t a command-line program, we could have extracted hello email from hello token object that is returned and then asked users toofill out additional information.</span></span> <span data-ttu-id="740a3-299">Como esse é um exemplo, adicioná-los banco de dados do tooan na memória.</span><span class="sxs-lookup"><span data-stu-id="740a3-299">Because this is a sample, we add them tooan in-memory database.</span></span>
>
>

## <a name="run-your-server-application-tooverify-that-it-rejects-you"></a><span data-ttu-id="740a3-300">Execute o tooverify do aplicativo de servidor que ele rejeita você</span><span class="sxs-lookup"><span data-stu-id="740a3-300">Run your server application tooverify that it rejects you</span></span>
<span data-ttu-id="740a3-301">Você pode usar `curl` toosee se você já OAuth2 proteção contra seus pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="740a3-301">You can use `curl` toosee if you now have OAuth2 protection against your endpoints.</span></span> <span data-ttu-id="740a3-302">Olá cabeçalhos retornados devem ser suficientes tootell que estão no caminho de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="740a3-302">hello headers returned should be enough tootell you that you are on hello right path.</span></span>

<span data-ttu-id="740a3-303">Verifique se a instância do MongoDB está em execução.</span><span class="sxs-lookup"><span data-stu-id="740a3-303">Make sure that your MongoDB instance is running:</span></span>

    $sudo mongodb

<span data-ttu-id="740a3-304">Alterar diretório toohello e servidor de saudação de execução:</span><span class="sxs-lookup"><span data-stu-id="740a3-304">Change toohello directory and run hello server:</span></span>

    $ cd azuread
    $ node server.js

<span data-ttu-id="740a3-305">Em uma nova janela de terminal, execute `curl`</span><span class="sxs-lookup"><span data-stu-id="740a3-305">In a new terminal window, run `curl`</span></span>

<span data-ttu-id="740a3-306">Tente uma POSTAGEM básica:</span><span class="sxs-lookup"><span data-stu-id="740a3-306">Try a basic POST:</span></span>

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

<span data-ttu-id="740a3-307">Um erro 401 é resposta Olá desejado.</span><span class="sxs-lookup"><span data-stu-id="740a3-307">A 401 error is hello response you want.</span></span> <span data-ttu-id="740a3-308">Ele indica a camada Olá Passport está tentando tooredirect toohello autorizar o ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="740a3-308">It indicates that hello Passport layer is trying tooredirect toohello authorize endpoint.</span></span>

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a><span data-ttu-id="740a3-309">Agora você tem um serviço de API REST que usa OAuth2</span><span class="sxs-lookup"><span data-stu-id="740a3-309">You now have a REST API service that uses OAuth2</span></span>
<span data-ttu-id="740a3-310">Você implementou uma API REST usando Restify e OAuth!</span><span class="sxs-lookup"><span data-stu-id="740a3-310">You have implemented a REST API by using Restify and OAuth!</span></span> <span data-ttu-id="740a3-311">Agora você tem código suficiente para que você possa continuar toodevelop seu serviço e compilar este exemplo.</span><span class="sxs-lookup"><span data-stu-id="740a3-311">You now have sufficient code so that you can continue toodevelop your service and build on this example.</span></span> <span data-ttu-id="740a3-312">Você  fez tudo o que podia com esse servidor sem usar um cliente compatível com OAuth2.</span><span class="sxs-lookup"><span data-stu-id="740a3-312">You have gone as far as you can with this server without using an OAuth2-compatible client.</span></span> <span data-ttu-id="740a3-313">Para a próxima etapa, use uma passo a passo adicional como nosso [conectar-se a API da web do tooa usando iOS com B2C](active-directory-b2c-devquickstarts-ios.md) passo a passo.</span><span class="sxs-lookup"><span data-stu-id="740a3-313">For that next step use an additional walk-through like our [Connect tooa web API by using iOS with B2C](active-directory-b2c-devquickstarts-ios.md) walkthrough.</span></span>

## <a name="next-steps"></a><span data-ttu-id="740a3-314">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="740a3-314">Next steps</span></span>
<span data-ttu-id="740a3-315">Agora você pode mover tópicos toomore avançada, como:</span><span class="sxs-lookup"><span data-stu-id="740a3-315">You can now move toomore advanced topics, such as:</span></span>

[<span data-ttu-id="740a3-316">Conecte-se a API da web do tooa usando iOS com B2C</span><span class="sxs-lookup"><span data-stu-id="740a3-316">Connect tooa web API by using iOS with B2C</span></span>](active-directory-b2c-devquickstarts-ios.md)
