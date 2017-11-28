---
title: "aaaAzure AD Node. js Introdução | Microsoft Docs"
description: "Como toobuild uma API da web REST Node. js que se integra com o Azure AD para autenticação."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 7654ab4c-4489-4ea5-aba9-d7cdc256e42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 512ae6de9acfde8b58c0447ab4a6b573fb6407c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a><span data-ttu-id="36591-103">Introdução às APIs Web para o Node.js</span><span class="sxs-lookup"><span data-stu-id="36591-103">Get started with web APIs for Node.js</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="36591-104">*Passport* é middleware de autenticação para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="36591-104">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="36591-105">Flexível e modular, Passport atualizam pode ser descartado em tooany expressas ou Restify o aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="36591-105">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or Restify web application.</span></span> <span data-ttu-id="36591-106">Um conjunto abrangente de estratégias dão suporte à autenticação usando um nome de usuário e senha, Facebook, Twitter e mais.</span><span class="sxs-lookup"><span data-stu-id="36591-106">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="36591-107">Desenvolvemos uma estratégia para o Microsoft Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="36591-107">We have developed a strategy for Microsoft Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="36591-108">Podemos instalar este módulo e adicionar Olá Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="36591-108">We install this module and then add hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="36591-109">toodo isso, você precisa:</span><span class="sxs-lookup"><span data-stu-id="36591-109">toodo this, you need to:</span></span>

1. <span data-ttu-id="36591-110">Registrar um aplicativo com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36591-110">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="36591-111">Configurar seu aplicativo toouse Passport `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="36591-111">Set up your app toouse Passport's `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="36591-112">Configure um cliente aplicativo toocall Olá tooDo lista API da web.</span><span class="sxs-lookup"><span data-stu-id="36591-112">Configure a client application toocall hello tooDo List web API.</span></span>

<span data-ttu-id="36591-113">código de saudação para este tutorial é mantido [no GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span><span class="sxs-lookup"><span data-stu-id="36591-113">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span></span>

> [!NOTE]
> <span data-ttu-id="36591-114">Este artigo não aborda como tooimplement entrar, inscrição, ou criar o perfil de gerenciamento com o Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="36591-114">This article doesn't cover how tooimplement sign-in, sign-up, or profile management with Azure AD B2C.</span></span> <span data-ttu-id="36591-115">Ele se concentra em APIs da web chamado depois que o usuário Olá já está autenticado.</span><span class="sxs-lookup"><span data-stu-id="36591-115">It focuses on calling web APIs after hello user is already authenticated.</span></span>  <span data-ttu-id="36591-116">É recomendável que você inicie com [como toointegrate com documentos do Active Directory do Azure](active-directory-how-to-integrate.md) toolearn sobre noções básicas de saudação do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="36591-116">We recommend that you start with [How toointegrate with Azure Active Directory document](active-directory-how-to-integrate.md) toolearn about hello basics of Azure Active Directory.</span></span>
>
>

<span data-ttu-id="36591-117">Assim, já lançamos o código-fonte para este exemplo em execução no GitHub sob uma licença do MIT, Olá todos os se sentir tooclone livre (ou melhor ainda, bifurcação) e fornecer comentários e efetuar pull das solicitações.</span><span class="sxs-lookup"><span data-stu-id="36591-117">We've released all hello source code for this running example in GitHub under an MIT license, so feel free tooclone (or even better, fork), and provide feedback and pull requests.</span></span>

## <a name="about-nodejs-modules"></a><span data-ttu-id="36591-118">Sobre os módulos do Node.js</span><span class="sxs-lookup"><span data-stu-id="36591-118">About Node.js modules</span></span>
<span data-ttu-id="36591-119">Usaremos módulos do Node.js neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="36591-119">We use Node.js modules in this walkthrough.</span></span> <span data-ttu-id="36591-120">Os módulos são pacotes carregáveis do JavaScript que fornecem funcionalidade específica para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="36591-120">Modules are loadable JavaScript packages that provide specific functionality for your application.</span></span> <span data-ttu-id="36591-121">Geralmente instalar módulos, usando a saudação Node. js, uma ferramenta de linha de comando NPM no diretório de instalação de NPM hello.</span><span class="sxs-lookup"><span data-stu-id="36591-121">You usually install modules by using hello Node.js an NPM command-line tool in hello NPM installation directory.</span></span> <span data-ttu-id="36591-122">No entanto, alguns módulos, como o módulo HTTP do hello, estão incluídos no pacote de Node. js de núcleo de saudação.</span><span class="sxs-lookup"><span data-stu-id="36591-122">However, some modules, such as hello HTTP module, are included in hello core Node.js package.</span></span>

<span data-ttu-id="36591-123">Módulos instalados são salvos em Olá **node_modules** diretório raiz de saudação do seu diretório de instalação do Node. js.</span><span class="sxs-lookup"><span data-stu-id="36591-123">Installed modules are saved in hello **node_modules** directory at hello root of your Node.js installation directory.</span></span> <span data-ttu-id="36591-124">Cada módulo no hello **node_modules** directory mantém seu próprio **node_modules** diretório que contém todos os módulos que ele depende.</span><span class="sxs-lookup"><span data-stu-id="36591-124">Each module in hello **node_modules** directory maintains its own **node_modules** directory that contains any modules that it depends on.</span></span> <span data-ttu-id="36591-125">Além disso, cada módulo requerido tem um diretório **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="36591-125">Also, each required module has a **node_modules** directory.</span></span> <span data-ttu-id="36591-126">Esta estrutura de diretório recursiva representa a cadeia de dependência de saudação.</span><span class="sxs-lookup"><span data-stu-id="36591-126">This recursive directory structure represents hello dependency chain.</span></span>

<span data-ttu-id="36591-127">Essa estrutura de cadeia de dependência resulta em um espaço de aplicativo maior.</span><span class="sxs-lookup"><span data-stu-id="36591-127">This dependency chain structure results in a larger application footprint.</span></span> <span data-ttu-id="36591-128">Mas ela também garante que todas as dependências são atendidas e versão do módulos Olá Olá é usado no desenvolvimento também é usado na produção.</span><span class="sxs-lookup"><span data-stu-id="36591-128">But it also guarantees that all dependencies are met and that hello version of hello modules that's used in development is also used in production.</span></span> <span data-ttu-id="36591-129">Isso torna o comportamento do aplicativo de produção de hello mais previsível e evita os problemas de controle de versão que podem afetar os usuários.</span><span class="sxs-lookup"><span data-stu-id="36591-129">This makes hello production app behavior more predictable and prevents versioning problems that might affect users.</span></span>

## <a name="step-1-register-an-azure-ad-tenant"></a><span data-ttu-id="36591-130">Etapa 1: registrar um locatário do Azure AD</span><span class="sxs-lookup"><span data-stu-id="36591-130">Step 1: Register an Azure AD tenant</span></span>
<span data-ttu-id="36591-131">toouse exemplo, é necessário um locatário do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="36591-131">toouse this sample, you need an Azure Active Directory tenant.</span></span> <span data-ttu-id="36591-132">Se você não tiver certeza de que um locatário é ou como tooget, consulte [como tooget um AD do Azure locatário](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="36591-132">If you're not sure what a tenant is or how tooget one, see [How tooget an Azure AD tenant](active-directory-howto-tenant.md).</span></span>

## <a name="step-2-create-an-application"></a><span data-ttu-id="36591-133">Etapa 2: criar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="36591-133">Step 2: Create an application</span></span>
<span data-ttu-id="36591-134">Em seguida, você cria um aplicativo em seu diretório que dá o AD do Azure informações que precisa toosecurely se comunicar com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="36591-134">Next you create an app in your directory that gives Azure AD information that it needs toosecurely communicate with your app.</span></span>  <span data-ttu-id="36591-135">Aplicativo de cliente hello e a API da web são representados por um único **ID do aplicativo** nesse caso, porque eles compõem um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="36591-135">Both hello client app and web API are represented by a single **Application ID** in this case, because they comprise one logical app.</span></span>  <span data-ttu-id="36591-136">toocreate um aplicativo, siga [estas instruções](active-directory-how-applications-are-added.md).</span><span class="sxs-lookup"><span data-stu-id="36591-136">toocreate an app, follow [these instructions](active-directory-how-applications-are-added.md).</span></span> <span data-ttu-id="36591-137">Se você estiver criando um aplicativo de linha de negócios, [estas instruções adicionais podem ser úteis](../active-directory-applications-guiding-developers-for-lob-applications.md).</span><span class="sxs-lookup"><span data-stu-id="36591-137">If you are building a line-of-business app, [these additional instructions might be useful](../active-directory-applications-guiding-developers-for-lob-applications.md).</span></span>

<span data-ttu-id="36591-138">toocreate um aplicativo:</span><span class="sxs-lookup"><span data-stu-id="36591-138">toocreate an application:</span></span>

1. <span data-ttu-id="36591-139">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="36591-139">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="36591-140">No menu superior do hello, selecione sua conta.</span><span class="sxs-lookup"><span data-stu-id="36591-140">On hello top menu, select your account.</span></span> <span data-ttu-id="36591-141">Em seguida, em Olá **diretório** , escolha o locatário do Active Directory Olá onde você deseja tooregister seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="36591-141">Then, under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="36591-142">No menu Olá Olá esquerda, selecione **mais serviços**e, em seguida, selecione **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="36591-142">In hello menu on hello left, select **More Services**, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="36591-143">Selecione **Registros do aplicativo**e, em seguida, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="36591-143">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="36591-144">Siga Olá prompts toocreate um **aplicativo Web e/ou WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="36591-144">Follow hello prompts toocreate a **Web Application and/or WebAPI**.</span></span>

      * <span data-ttu-id="36591-145">Olá **nome** da saudação aplicativo descreve os usuários de tooend do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="36591-145">hello **name** of hello application describes your application tooend users.</span></span>

      * <span data-ttu-id="36591-146">Olá **URL de logon** é Olá a URL base do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="36591-146">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="36591-147">Olá URL do código de exemplo hello padrão é `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="36591-147">hello default URL of hello sample code is `https://localhost:8080`.</span></span>

6. <span data-ttu-id="36591-148">Depois de se registrar, o Azure AD atribui uma ID de aplicativo única ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="36591-148">After you register, Azure AD assigns your app a unique Application ID.</span></span> <span data-ttu-id="36591-149">Você precisa desse valor nas seções de Avançar Olá, portanto copie-o da página de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="36591-149">You need this value in hello next sections, so copy it from hello application page.</span></span>

7. <span data-ttu-id="36591-150">De saudação **configurações** -> **propriedades** página para seu aplicativo, Olá URI da ID do aplicativo de atualização.</span><span class="sxs-lookup"><span data-stu-id="36591-150">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="36591-151">Olá **URI da ID do aplicativo** é um identificador exclusivo para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="36591-151">hello **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="36591-152">convenção de saudação é toouse `https://<tenant-domain>/<app-name>`, por exemplo: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="36591-152">hello convention is toouse `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

8. <span data-ttu-id="36591-153">Criar um **chave** para seu aplicativo de saudação **configurações** página e, em seguida, copie-o em algum lugar.</span><span class="sxs-lookup"><span data-stu-id="36591-153">Create a **Key** for your application from hello **Settings** page, and then copy it somewhere.</span></span> <span data-ttu-id="36591-154">Você precisará dela em breve.</span><span class="sxs-lookup"><span data-stu-id="36591-154">You'll need it shortly.</span></span>

## <a name="step-3-download-nodejs-for-your-platform"></a><span data-ttu-id="36591-155">Etapa 3: baixar o Node.js para a sua plataforma</span><span class="sxs-lookup"><span data-stu-id="36591-155">Step 3: Download Node.js for your platform</span></span>
<span data-ttu-id="36591-156">toosuccessfully usar este exemplo, você deve ter uma instalação em funcionamento do Node. js.</span><span class="sxs-lookup"><span data-stu-id="36591-156">toosuccessfully use this sample, you must have a working installation of Node.js.</span></span>

<span data-ttu-id="36591-157">Instale o Node.js a partir de [http://nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="36591-157">Install Node.js from [http://nodejs.org](http://nodejs.org).</span></span>

## <a name="step-4-install-mongodb-on-your-platform"></a><span data-ttu-id="36591-158">Etapa 4: instalar o MongoDB na sua plataforma</span><span class="sxs-lookup"><span data-stu-id="36591-158">Step 4: Install MongoDB on your platform</span></span>
<span data-ttu-id="36591-159">toosuccessfully usar este exemplo, você deve ter uma instalação em funcionamento do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="36591-159">toosuccessfully use this sample, you must have a working installation of MongoDB.</span></span> <span data-ttu-id="36591-160">Use o MongoDB toomake Olá REST API persistente em instâncias de servidor.</span><span class="sxs-lookup"><span data-stu-id="36591-160">You use MongoDB toomake hello REST API persistent across server instances.</span></span>

<span data-ttu-id="36591-161">Instalar o MongoDB a partir de [http://mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="36591-161">Install MongoDB from [http://mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="36591-162">Este passo a passo pressupõe que você use Olá instalação e o servidor de pontos de extremidade padrão para o MongoDB, que em tempo de saudação da redação deste artigo é mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="36591-162">This walkthrough assumes that you use hello default installation and server endpoints for MongoDB, which at hello time of this writing is mongodb://localhost.</span></span>
>
>

## <a name="step-5-install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="36591-163">Etapa 5: Instalar os módulos de Restify de saudação em sua API da web</span><span class="sxs-lookup"><span data-stu-id="36591-163">Step 5: Install hello Restify modules in your web API</span></span>
<span data-ttu-id="36591-164">Estamos usando Restify toobuild nossa API REST.</span><span class="sxs-lookup"><span data-stu-id="36591-164">We are using Restify toobuild our REST API.</span></span> <span data-ttu-id="36591-165">O Restify é uma estrutura de aplicativo do Node.js mínima e flexível, derivada do Express.</span><span class="sxs-lookup"><span data-stu-id="36591-165">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="36591-166">Tem um conjunto robusto de recursos para a criação de APIs REST sobre o Connect.</span><span class="sxs-lookup"><span data-stu-id="36591-166">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="36591-167">Instalar Restify</span><span class="sxs-lookup"><span data-stu-id="36591-167">Install Restify</span></span>
1. <span data-ttu-id="36591-168">Olá linha de comando, altere diretórios toohello **doWindows Azure** directory.</span><span class="sxs-lookup"><span data-stu-id="36591-168">From hello command line, change directories toohello **azuread** directory.</span></span> <span data-ttu-id="36591-169">Se hello **doWindows Azure** diretório não existe, criá-lo.</span><span class="sxs-lookup"><span data-stu-id="36591-169">If hello **azuread** directory does not exist, create it.</span></span>

        `cd azuread - or- mkdir azuread; cd azuread`

2. <span data-ttu-id="36591-170">Digite hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="36591-170">Type hello following command:</span></span>

    `npm install restify`

    <span data-ttu-id="36591-171">Este comando instala o Restify.</span><span class="sxs-lookup"><span data-stu-id="36591-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="36591-172">Você obteve um erro?</span><span class="sxs-lookup"><span data-stu-id="36591-172">Did you get an error?</span></span>
<span data-ttu-id="36591-173">Ao usar o NPM em alguns sistemas operacionais, você poderá receber uma mensagem de erro que diz: **Erro: EPERM, chmod '/usr/local/bin/..'**</span><span class="sxs-lookup"><span data-stu-id="36591-173">When you use NPM on some operating systems, you might receive an error that says **Error: EPERM, chmod '/usr/local/bin/..'**</span></span> <span data-ttu-id="36591-174">e uma sugestão que você tente conta de saudação em execução como administrador.</span><span class="sxs-lookup"><span data-stu-id="36591-174">and a suggestion that you try running hello account as an administrator.</span></span> <span data-ttu-id="36591-175">Se isso ocorrer, use Olá sudo comando toorun NPM em um nível de privilégio mais alto.</span><span class="sxs-lookup"><span data-stu-id="36591-175">If this occurs, use hello sudo command toorun NPM at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-regarding-dtrace"></a><span data-ttu-id="36591-176">Ocorreu um erro com relação ao DTRACE?</span><span class="sxs-lookup"><span data-stu-id="36591-176">Did you get an error regarding DTRACE?</span></span>
<span data-ttu-id="36591-177">Você poderá ver um erro assim ao instalar o Restify:</span><span class="sxs-lookup"><span data-stu-id="36591-177">You might see an error like this when installing Restify:</span></span>

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
<span data-ttu-id="36591-178">O Restify fornece um mecanismo poderoso para rastreamento de chamadas REST usando o DTrace.</span><span class="sxs-lookup"><span data-stu-id="36591-178">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="36591-179">No entanto, muitos sistemas operacionais não possuem o DTrace.</span><span class="sxs-lookup"><span data-stu-id="36591-179">However, many operating systems do not have DTrace.</span></span> <span data-ttu-id="36591-180">Você pode ignorar com segurança esses erros.</span><span class="sxs-lookup"><span data-stu-id="36591-180">You can safely ignore these errors.</span></span>

<span data-ttu-id="36591-181">saída de Hello desse comando deve ser semelhante toohello saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="36591-181">hello output of this command should look similar toohello following output:</span></span>

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


## <a name="step-6-install-passportjs-in-your-web-api"></a><span data-ttu-id="36591-182">Etapa 6: instalar o Passport.js na sua API da Web</span><span class="sxs-lookup"><span data-stu-id="36591-182">Step 6: Install Passport.js in your web API</span></span>
<span data-ttu-id="36591-183">[Passport](http://passportjs.org/) é middleware de autenticação para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="36591-183">[Passport](http://passportjs.org/) is authentication middleware for Node.js.</span></span> <span data-ttu-id="36591-184">Flexível e modular, Passport atualizam pode ser descartado em tooany expressas ou Restify o aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="36591-184">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or Restify web application.</span></span> <span data-ttu-id="36591-185">Um conjunto abrangente de estratégias dão suporte à autenticação usando um nome de usuário e senha, Facebook, Twitter e mais.</span><span class="sxs-lookup"><span data-stu-id="36591-185">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="36591-186">Desenvolvemos uma estratégia para o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="36591-186">We have developed a strategy for Azure Active Directory.</span></span> <span data-ttu-id="36591-187">Podemos instalar este módulo e adicionar plug-in da estratégia de Active Directory do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="36591-187">We install this module and then add hello Azure Active Directory strategy plug-in.</span></span>

1. <span data-ttu-id="36591-188">Olá linha de comando, altere diretórios toohello **doWindows Azure** directory.</span><span class="sxs-lookup"><span data-stu-id="36591-188">From hello command line, change directories toohello **azuread** directory.</span></span>

2. <span data-ttu-id="36591-189">tooinstall passport.js, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="36591-189">tooinstall passport.js, enter hello following command :</span></span>

    `npm install passport`

    <span data-ttu-id="36591-190">saída de saudação do comando Olá deve ser a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="36591-190">hello output of hello command should look similar toohello following:</span></span>

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-tooyour-web-api"></a><span data-ttu-id="36591-191">Etapa 7: Adicionar API da web do AD de Azure Passport tooyour</span><span class="sxs-lookup"><span data-stu-id="36591-191">Step 7: Add Passport-Azure-AD tooyour web API</span></span>
<span data-ttu-id="36591-192">Em seguida, adicionamos estratégia de OAuth hello usando `passport-azure-ad`, um conjunto de estratégias que se conectam tooPassport do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="36591-192">Next we add hello OAuth strategy by using `passport-azure-ad`, a suite of strategies that connect Azure Active Directory tooPassport.</span></span> <span data-ttu-id="36591-193">Usaremos essa estratégia para tokens de portador neste exemplo de API Rest.</span><span class="sxs-lookup"><span data-stu-id="36591-193">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="36591-194">Embora o OAuth2 forneça uma estrutura na qual qualquer tipo de token conhecido possa ser emitido, somente determinados tipos de token são comumente usados.</span><span class="sxs-lookup"><span data-stu-id="36591-194">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types are commonly used.</span></span> <span data-ttu-id="36591-195">Tokens de portador são tokens de hello mais comumente usada para proteger os pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="36591-195">Bearer tokens are hello most commonly used tokens for protecting endpoints.</span></span> <span data-ttu-id="36591-196">Eles são o tipo de hello mais amplamente emitido de token em OAuth2.</span><span class="sxs-lookup"><span data-stu-id="36591-196">They are hello most widely issued type of token in OAuth2.</span></span> <span data-ttu-id="36591-197">Muitas implementações supõem que os tokens de portador são Olá únicos tipos de tokens emitidos.</span><span class="sxs-lookup"><span data-stu-id="36591-197">Many implementations assume that bearer tokens are hello only type of tokens that are issued.</span></span>
>
>

<span data-ttu-id="36591-198">Olá linha de comando, altere diretórios toohello **doWindows Azure** directory.</span><span class="sxs-lookup"><span data-stu-id="36591-198">From hello command line, change directories toohello **azuread** directory.</span></span>

<span data-ttu-id="36591-199">Digite o seguinte Olá comando Olá tooinstall Passport.js `passport-azure-ad module`:</span><span class="sxs-lookup"><span data-stu-id="36591-199">Type hello following command tooinstall hello Passport.js `passport-azure-ad module`:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="36591-200">saída de saudação do comando Olá deve ser semelhante toohello saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="36591-200">hello output of hello command should look similar toohello following output:</span></span>


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



## <a name="step-8-add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="36591-201">Etapa 8: Adicionar MongoDB módulos tooyour web API</span><span class="sxs-lookup"><span data-stu-id="36591-201">Step 8: Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="36591-202">Usamos o MongoDB como nosso repositório de dados.</span><span class="sxs-lookup"><span data-stu-id="36591-202">We use MongoDB as our datastore.</span></span> <span data-ttu-id="36591-203">Por esse motivo, é preciso tooinstall Olá amplamente usada plug-in Modelos de toomanage Mongoose chamados e esquemas.</span><span class="sxs-lookup"><span data-stu-id="36591-203">For that reason, we need tooinstall hello widely used plug-in called Mongoose toomanage models and schemas.</span></span> <span data-ttu-id="36591-204">Também precisamos de driver de banco de dados tooinstall Olá para o MongoDB (que também é chamado MongoDB).</span><span class="sxs-lookup"><span data-stu-id="36591-204">We also need tooinstall hello database driver for MongoDB (which is also called MongoDB).</span></span>

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a><span data-ttu-id="36591-205">Etapa 9: instalar módulos adicionais</span><span class="sxs-lookup"><span data-stu-id="36591-205">Step 9: Install additional modules</span></span>
<span data-ttu-id="36591-206">Em seguida, podemos instalar Olá restantes módulos necessários.</span><span class="sxs-lookup"><span data-stu-id="36591-206">Next we install hello remaining required modules.</span></span>

1. <span data-ttu-id="36591-207">Olá linha de comando, altere diretórios toohello **doWindows Azure** pasta se você não ainda estiver lá.</span><span class="sxs-lookup"><span data-stu-id="36591-207">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="36591-208">Digite hello tooinstall comandos a seguir esses módulos em seu **node_modules** diretório:</span><span class="sxs-lookup"><span data-stu-id="36591-208">Enter hello following commands tooinstall these modules in your **node_modules** directory:</span></span>

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a><span data-ttu-id="36591-209">Etapa 10: criar um server.js com as suas dependências</span><span class="sxs-lookup"><span data-stu-id="36591-209">Step 10: Create a server.js with your dependencies</span></span>
<span data-ttu-id="36591-210">arquivo de server.js de saudação fornece a maioria da funcionalidade de saudação para nosso servidor de API da web.</span><span class="sxs-lookup"><span data-stu-id="36591-210">hello server.js file provides most of hello functionality for our web API server.</span></span> <span data-ttu-id="36591-211">Vamos adicionar mais nosso toothis do arquivo de código.</span><span class="sxs-lookup"><span data-stu-id="36591-211">We add most of our code toothis file.</span></span> <span data-ttu-id="36591-212">Para fins de produção, recomendamos que você refatorar funcionalidade Olá em arquivos menores, como controladores e rotas separadas.</span><span class="sxs-lookup"><span data-stu-id="36591-212">For production purposes, we recommend that you refactor hello functionality into smaller files, such as separate routes and controllers.</span></span> <span data-ttu-id="36591-213">Nesta demonstração, usaremos o server.js para essa funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="36591-213">In this demo, we use server.js for this functionality.</span></span>

1. <span data-ttu-id="36591-214">Olá linha de comando, altere diretórios toohello **doWindows Azure** pasta se você não ainda estiver lá.</span><span class="sxs-lookup"><span data-stu-id="36591-214">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="36591-215">Criar um `server.js` de arquivo em seu editor favorito e adicione Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="36591-215">Create a `server.js` file in your favorite editor, and then add hello following information:</span></span>

    ```Javascript
        'use strict';

        /**
         * Module dependencies.
         */

        var fs = require('fs');
        var path = require('path');
        var util = require('util');
        var assert = require('assert-plus');
        var bunyan = require('bunyan');
        var getopt = require('posix-getopt');
        var mongoose = require('mongoose/');
        var restify = require('restify');
        var passport = require('passport');
      var BearerStrategy = require('passport-azure-ad').BearerStrategy;
    ```

3. <span data-ttu-id="36591-216">Salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="36591-216">Save hello file.</span></span> <span data-ttu-id="36591-217">Retornaremos tooit em breve.</span><span class="sxs-lookup"><span data-stu-id="36591-217">We'll return tooit shortly.</span></span>

## <a name="step-11-create-a-config-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="36591-218">Etapa 11: Criar um toostore do arquivo de configuração de suas configurações do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="36591-218">Step 11: Create a config file toostore your Azure AD settings</span></span>
<span data-ttu-id="36591-219">Arquivo de código passa parâmetros de configuração de saudação de seu tooPassport.js portal do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="36591-219">This code file passes hello configuration parameters from your Azure Active Directory portal tooPassport.js.</span></span> <span data-ttu-id="36591-220">Quando você adicionou o portal de toohello Olá web API na primeira parte Olá Olá passo a passo, você criou esses valores de configuração.</span><span class="sxs-lookup"><span data-stu-id="36591-220">You created these configuration values when you added hello web API toohello portal in hello first part of hello walkthrough.</span></span> <span data-ttu-id="36591-221">Explicamos que tooput em valores desses parâmetros Olá depois de copiar o código de saudação.</span><span class="sxs-lookup"><span data-stu-id="36591-221">We explain what tooput in hello values of these parameters after you copy hello code.</span></span>

1. <span data-ttu-id="36591-222">Olá linha de comando, altere diretórios toohello **doWindows Azure** pasta se você não ainda estiver lá.</span><span class="sxs-lookup"><span data-stu-id="36591-222">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="36591-223">Criar um `config.js` de arquivo em seu editor favorito e adicione Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="36591-223">Create a `config.js` file in your favorite editor, and then add hello following information:</span></span>

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in tooyour server unless you use hello common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in tooyour server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes toostderr in Unix.

         };
    ```
3. <span data-ttu-id="36591-224">Salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="36591-224">Save hello file.</span></span>

## <a name="step-12-add-configuration-values-tooyour-serverjs-file"></a><span data-ttu-id="36591-225">Etapa 12: Adicionar o arquivo de configuração de valores tooyour Server. js</span><span class="sxs-lookup"><span data-stu-id="36591-225">Step 12: Add configuration values tooyour server.js file</span></span>
<span data-ttu-id="36591-226">É preciso tooread esses valores no arquivo. config Olá que você criou em nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="36591-226">We need tooread these values from hello .config file that you created across our application.</span></span> <span data-ttu-id="36591-227">toodo isso, adicionamos arquivo. config de saudação como um recurso necessário em nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="36591-227">toodo this, we add hello .config file as a required resource in our application.</span></span> <span data-ttu-id="36591-228">Em seguida, vamos definir variáveis de Olá Olá variáveis globais toomatch no documento de config.js hello.</span><span class="sxs-lookup"><span data-stu-id="36591-228">Then we set hello global variables toomatch hello variables in hello config.js document.</span></span>

1. <span data-ttu-id="36591-229">Olá linha de comando, altere diretórios toohello **doWindows Azure** pasta se você não ainda estiver lá.</span><span class="sxs-lookup"><span data-stu-id="36591-229">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="36591-230">Abra o `server.js` do arquivo em seu editor favorito e adicione Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="36591-230">Open your `server.js` file in your favorite editor, and then add hello following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```
3. <span data-ttu-id="36591-231">Em seguida, adicione uma nova seção muito`server.js` com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="36591-231">Then add a new section too`server.js` with hello following code:</span></span>

    ```Javascript
    var options = {
        // hello URL of hello metadata document for your app. We will put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array toohold logged in users and hello current logged in user (owner).
    var users = [];
    var owner = null;

    // Our logger.
    var log = bunyan.createLogger({
        name: 'Azure Active Directory Bearer Sample',
             streams: [
            {
                stream: process.stderr,
                level: "error",
                name: "error"
            },
            {
                stream: process.stdout,
                level: "warn",
                name: "console"
            }, ]
    });

      // If hello logging level is specified, switch tooit.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. <span data-ttu-id="36591-232">Salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="36591-232">Save hello file.</span></span>

## <a name="step-13-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="36591-233">Etapa 13: Adicionar Olá MongoDB modelo e informações de esquema usando Mongoose</span><span class="sxs-lookup"><span data-stu-id="36591-233">Step 13: Add hello MongoDB Model and schema information by using Mongoose</span></span>
<span data-ttu-id="36591-234">Agora todos os essa preparação vai toostart pagar como podemos combinar esses três arquivos em um serviço de API REST.</span><span class="sxs-lookup"><span data-stu-id="36591-234">Now all this preparation is going toostart paying off as we combine these three files into a REST API service.</span></span>

<span data-ttu-id="36591-235">Para este passo a passo, usamos MongoDB toostore nosso tarefas, conforme descrito na etapa 4.</span><span class="sxs-lookup"><span data-stu-id="36591-235">For this walkthrough, we use MongoDB toostore our tasks as discussed in Step 4.</span></span>

<span data-ttu-id="36591-236">Em Olá `config.js` que criamos na etapa 11, chamamos nosso banco de dados de arquivo `tasklist`, pois esse era o que colocar no final de saudação do nosso **mogoose_auth_local** URL de conexão.</span><span class="sxs-lookup"><span data-stu-id="36591-236">In hello `config.js` file that we created in Step 11, we called our database `tasklist`, because that was what we put at hello end of our **mogoose_auth_local** connection URL.</span></span> <span data-ttu-id="36591-237">Você não precisa toocreate banco de dados com antecedência no MongoDB.</span><span class="sxs-lookup"><span data-stu-id="36591-237">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="36591-238">Em vez disso, MongoDB cria isso para que possamos em Olá primeiro execução de nosso aplicativo de servidor (supondo que o banco de dados Olá ainda não existe).</span><span class="sxs-lookup"><span data-stu-id="36591-238">Instead, MongoDB creates this for us on hello first run of our server application (assuming that hello database doesn't already exist).</span></span>

<span data-ttu-id="36591-239">Agora que dissemos servidor Olá qual banco de dados do MongoDB gostaríamos toouse, precisamos toowrite alguns adicionais toocreate Olá modelo e código de esquema para tarefas do servidor.</span><span class="sxs-lookup"><span data-stu-id="36591-239">Now that we've told hello server which MongoDB database we'd like toouse, we need toowrite some additional code toocreate hello model and schema for our server's tasks.</span></span>

### <a name="discussion-of-hello-model"></a><span data-ttu-id="36591-240">Descrição do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="36591-240">Discussion of hello model</span></span>
<span data-ttu-id="36591-241">Nosso modelo de esquema é simples.</span><span class="sxs-lookup"><span data-stu-id="36591-241">Our schema model is simple.</span></span> <span data-ttu-id="36591-242">Você pode expandi-lo conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="36591-242">You expand it as required.</span></span>

<span data-ttu-id="36591-243">NOME: o nome de saudação da saudação pessoa designada toohello tarefa.</span><span class="sxs-lookup"><span data-stu-id="36591-243">NAME: hello name of hello person who is assigned toohello task.</span></span> <span data-ttu-id="36591-244">Uma **cadeia de caracteres**.</span><span class="sxs-lookup"><span data-stu-id="36591-244">A **String**.</span></span>

<span data-ttu-id="36591-245">TAREFA: Olá própria tarefa.</span><span class="sxs-lookup"><span data-stu-id="36591-245">TASK: hello task itself.</span></span> <span data-ttu-id="36591-246">Uma **cadeia de caracteres**.</span><span class="sxs-lookup"><span data-stu-id="36591-246">A **String**.</span></span>

<span data-ttu-id="36591-247">Data de saudação de data: tarefa Olá é devida.</span><span class="sxs-lookup"><span data-stu-id="36591-247">DATE: hello date that hello task is due.</span></span> <span data-ttu-id="36591-248">UM VALOR **DATETIME**.</span><span class="sxs-lookup"><span data-stu-id="36591-248">A **DATETIME**.</span></span>

<span data-ttu-id="36591-249">CONCLUÍDA: Se Olá tarefa tiver sido concluída ou não.</span><span class="sxs-lookup"><span data-stu-id="36591-249">COMPLETED: If hello task has been completed or not.</span></span> <span data-ttu-id="36591-250">UM VALOR **BOOLEANO**.</span><span class="sxs-lookup"><span data-stu-id="36591-250">A **BOOLEAN**.</span></span>

### <a name="creating-hello-schema-in-hello-code"></a><span data-ttu-id="36591-251">Criando esquema Olá em código de saudação</span><span class="sxs-lookup"><span data-stu-id="36591-251">Creating hello schema in hello code</span></span>
1. <span data-ttu-id="36591-252">Olá linha de comando, altere diretórios toohello **doWindows Azure** pasta se você não ainda estiver lá.</span><span class="sxs-lookup"><span data-stu-id="36591-252">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="36591-253">Abra seu `server.js` arquivo em seu editor favorito e adicione Olá informações abaixo da entrada de configuração de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="36591-253">Open your `server.js` file in your favorite editor, and then add hello following information below hello configuration entry:</span></span>

    ```Javascript
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema toostore our tasks and users. It's a fairly simple schema for now.
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
<span data-ttu-id="36591-254">Como você pode ver no código hello, criamos nossa esquema primeiro.</span><span class="sxs-lookup"><span data-stu-id="36591-254">As you can tell from hello code, we create our schema first.</span></span> <span data-ttu-id="36591-255">Em seguida, podemos criar um objeto de modelo que usamos toostore nossos dados durante a saudação código quando definimos nosso **rotas**.</span><span class="sxs-lookup"><span data-stu-id="36591-255">Then we create a model object that we use toostore our data throughout hello code when we define our **Routes**.</span></span>

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a><span data-ttu-id="36591-256">Etapa 14: adicionar nossas rotas a nosso servidor de API REST da tarefa</span><span class="sxs-lookup"><span data-stu-id="36591-256">Step 14: Add our routes for our task REST API server</span></span>
<span data-ttu-id="36591-257">Agora que temos uma toowork de modelo de banco de dados com, vamos adicionar rotas Olá estamos use contínuo para nosso servidor de API REST.</span><span class="sxs-lookup"><span data-stu-id="36591-257">Now that we have a database model toowork with, let's add hello routes we are going use for our REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="36591-258">Sobre rotas no Restify</span><span class="sxs-lookup"><span data-stu-id="36591-258">About routes in Restify</span></span>
<span data-ttu-id="36591-259">Rotas funcionam em Restify Olá mesma maneira como eles em Olá Express de pilha.</span><span class="sxs-lookup"><span data-stu-id="36591-259">Routes work in Restify hello same way they do in hello Express stack.</span></span> <span data-ttu-id="36591-260">Definir rotas usando Olá URI que você espera Olá toocall de aplicativos de cliente.</span><span class="sxs-lookup"><span data-stu-id="36591-260">You define routes by using hello URI that you expect hello client applications toocall.</span></span> <span data-ttu-id="36591-261">Normalmente, você define suas rotas em um arquivo separado.</span><span class="sxs-lookup"><span data-stu-id="36591-261">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="36591-262">Para nossos objetivos, colocamos nossas rotas no arquivo de server.js hello.</span><span class="sxs-lookup"><span data-stu-id="36591-262">For our purposes, we put our routes in hello server.js file.</span></span> <span data-ttu-id="36591-263">Recomendamos que você as coloque no seu próprio arquivo para uso em produção.</span><span class="sxs-lookup"><span data-stu-id="36591-263">We recommend that you factor these routes into their own file for production use.</span></span>

<span data-ttu-id="36591-264">Um padrão típico para uma rota do Restify é:</span><span class="sxs-lookup"><span data-stu-id="36591-264">A typical pattern for a Restify route is as follows:</span></span>

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep hello server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


<span data-ttu-id="36591-265">Este é o padrão de saudação em seu nível mais básico.</span><span class="sxs-lookup"><span data-stu-id="36591-265">This is hello pattern at its most basic level.</span></span> <span data-ttu-id="36591-266">O Restify (e o Express) fornece uma funcionalidade muito mais aprofundada, como a definição de tipos de aplicativos e o roteamento complexo entre diferentes pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="36591-266">Restify (and Express) provide much deeper functionality, such as defining application types and providing complex routing across different endpoints.</span></span> <span data-ttu-id="36591-267">Para nossos propósitos, estamos mantendo essas rotas simples.</span><span class="sxs-lookup"><span data-stu-id="36591-267">For our purposes, we are keeping these routes simple.</span></span>

### <a name="add-default-routes-tooour-server"></a><span data-ttu-id="36591-268">Adicionar servidor de tooour rotas padrão</span><span class="sxs-lookup"><span data-stu-id="36591-268">Add default routes tooour server</span></span>
<span data-ttu-id="36591-269">Agora adicionar Olá básica CRUD rotas de criar, recuperar, atualizar e excluir.</span><span class="sxs-lookup"><span data-stu-id="36591-269">We now add hello basic CRUD routes of Create, Retrieve, Update, and Delete.</span></span>

1. <span data-ttu-id="36591-270">Olá linha de comando, altere diretórios toohello **doWindows Azure** pasta se você não ainda estiver lá:</span><span class="sxs-lookup"><span data-stu-id="36591-270">From hello command line, change directories toohello **azuread** folder if you're not already there:</span></span>

    `cd azuread`

2. <span data-ttu-id="36591-271">Olá abrir `server.js` arquivo em seu editor favorito e adicione Olá informações abaixo Olá banco de dados as entradas anteriores feitas a seguir:</span><span class="sxs-lookup"><span data-stu-id="36591-271">Open hello `server.js` file in your favorite editor, and then add hello following information below hello previous database entries that you made:</span></span>

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it tooMongodb.
    var _task = new Task();

    if (!req.params.task) {
        req.log.warn('createTodo: missing task');
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

/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err) {
            return next(err);
        }

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Did you initialize hello database as stated in hello README?");
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

### <a name="add-error-handling-in-our-apis"></a><span data-ttu-id="36591-272">Adicionar tratamento de erros em nossas APIs</span><span class="sxs-lookup"><span data-stu-id="36591-272">Add error handling in our APIs</span></span>
```

///--- Errors for communicating something interesting back toohello client.

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


## <a name="step-15-create-your-server"></a><span data-ttu-id="36591-273">Etapa 15: criar seu servidor</span><span class="sxs-lookup"><span data-stu-id="36591-273">Step 15: Create your server</span></span>
<span data-ttu-id="36591-274">Definimos nosso banco de dados e nossas rotas estão em vigor.</span><span class="sxs-lookup"><span data-stu-id="36591-274">We have defined our database and our routes are in place.</span></span> <span data-ttu-id="36591-275">Olá última coisa toodo é adicionar a instância do servidor de saudação que gerencia nossas chamadas.</span><span class="sxs-lookup"><span data-stu-id="36591-275">hello last thing toodo is add hello server instance that manages our calls.</span></span>

<span data-ttu-id="36591-276">Restify (e Express), você pode fazer muita de personalização para um servidor de API REST, mas, novamente, vamos configuração mais básica do toouse Olá para nossas finalidades.</span><span class="sxs-lookup"><span data-stu-id="36591-276">In Restify (and Express) you can do a lot of customization for a REST API server, but again we are going toouse hello most basic setup for our purposes.</span></span>

```Javascript
/**
 * Our server.
 */


var server = restify.createServer({
    name: "Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads.
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());

// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in).
server.use(restify.requestLogger());

// Allow five requests per second by IP, and burst too10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping tooREST.
```

## <a name="step-16-add-hello-routes-toohello-server-without-authentication-for-now"></a><span data-ttu-id="36591-277">Etapa 16: Adicionar o servidor de toohello de rotas de saudação (sem autenticação agora)</span><span class="sxs-lookup"><span data-stu-id="36591-277">Step 16: Add hello routes toohello server (without authentication for now)</span></span>
```Javascript
/// Now hello real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In hello pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need toomaintain session state. You can experiment with removing API protection
/* by removing hello passport.authenticate() method as follows:
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
// Register a default '/' handler.
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

## <a name="step-17-run-hello-server-before-adding-oauth-support"></a><span data-ttu-id="36591-278">Etapa 17: Executar o servidor de saudação (antes de adicionar suporte OAuth)</span><span class="sxs-lookup"><span data-stu-id="36591-278">Step 17: Run hello server (before adding OAuth support)</span></span>
<span data-ttu-id="36591-279">Teste o seu servidor antes de adicionarmos a autenticação.</span><span class="sxs-lookup"><span data-stu-id="36591-279">Test out your server before we add authentication.</span></span>

<span data-ttu-id="36591-280">Olá tootest de maneira mais fácil o servidor está usando ondulação em uma linha de comando.</span><span class="sxs-lookup"><span data-stu-id="36591-280">hello easiest way tootest your server is by using curl in a command line.</span></span> <span data-ttu-id="36591-281">Antes de fazermos isso, precisamos de um utilitário que nos permite saída tooparse como JSON.</span><span class="sxs-lookup"><span data-stu-id="36591-281">Before we do that, we need a utility that allows us tooparse output as JSON.</span></span>

1. <span data-ttu-id="36591-282">Instale Olá, ferramenta JSON (Olá todos os exemplos a seguir usam esta ferramenta) a seguir:</span><span class="sxs-lookup"><span data-stu-id="36591-282">Install hello following JSON tool (all hello following examples use this tool):</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="36591-283">Isso instala a ferramenta JSON de saudação globalmente.</span><span class="sxs-lookup"><span data-stu-id="36591-283">This installs hello JSON tool globally.</span></span> <span data-ttu-id="36591-284">Agora que nós já realizado que, vamos executar com o servidor de saudação:</span><span class="sxs-lookup"><span data-stu-id="36591-284">Now that we’ve accomplished that, let’s play with hello server:</span></span>

2. <span data-ttu-id="36591-285">Primeiro, verifique se a instância do MongoDB está em execução:</span><span class="sxs-lookup"><span data-stu-id="36591-285">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

3. <span data-ttu-id="36591-286">Em seguida, altere o diretório toohello e iniciar curling:</span><span class="sxs-lookup"><span data-stu-id="36591-286">Then, change toohello directory and start curling:</span></span>

    <span data-ttu-id="36591-287">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="36591-287">`$ cd azuread` `$ node server.js`</span></span>

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 200 OK
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

4. <span data-ttu-id="36591-288">Então, podemos adicionar uma tarefa deste modo:</span><span class="sxs-lookup"><span data-stu-id="36591-288">Then, we can add a task this way:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    <span data-ttu-id="36591-289">Olá resposta deve ser:</span><span class="sxs-lookup"><span data-stu-id="36591-289">hello response should be:</span></span>

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
    <span data-ttu-id="36591-290">E podemos pode listar tarefas para Brandon deste modo:</span><span class="sxs-lookup"><span data-stu-id="36591-290">And we can list tasks for Brandon this way:</span></span>

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="36591-291">Se tudo isso funciona, estamos servidor de API REST de toohello tooadd pronto OAuth.</span><span class="sxs-lookup"><span data-stu-id="36591-291">If all this works, we're ready tooadd OAuth toohello REST API server.</span></span>

<span data-ttu-id="36591-292">Você tem um servidor de API REST com o MongoDB!</span><span class="sxs-lookup"><span data-stu-id="36591-292">You have a REST API server with MongoDB!</span></span>

## <a name="step-18-add-authentication-tooour-rest-api-server"></a><span data-ttu-id="36591-293">Etapa 18: Adicionar o servidor de API REST de tooour de autenticação</span><span class="sxs-lookup"><span data-stu-id="36591-293">Step 18: Add authentication tooour REST API server</span></span>
<span data-ttu-id="36591-294">Agora que temos uma API REST em execução, vamos começar ativando-a com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36591-294">Now that we have a running REST API, let's start making it useful with Azure AD.</span></span>

<span data-ttu-id="36591-295">Olá linha de comando, altere diretórios toohello **doWindows Azure** pasta se você não ainda estiver lá.</span><span class="sxs-lookup"><span data-stu-id="36591-295">From hello command line, change directories toohello **azuread** folder if you're not already there.</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="36591-296">Use Olá OIDCBearerStrategy que está incluído no ad de azure passport</span><span class="sxs-lookup"><span data-stu-id="36591-296">Use hello OIDCBearerStrategy that is included with passport-azure-ad</span></span>
<span data-ttu-id="36591-297">Até agora, criamos um servidor típico TODO do REST sem nenhum tipo de autorização.</span><span class="sxs-lookup"><span data-stu-id="36591-297">So far we have built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="36591-298">Aqui é onde começamos a juntar as peças.</span><span class="sxs-lookup"><span data-stu-id="36591-298">This is where we start putting that together.</span></span>

1. <span data-ttu-id="36591-299">Primeiro, precisamos tooindicate que desejamos toouse Passport.</span><span class="sxs-lookup"><span data-stu-id="36591-299">First, we need tooindicate that we want toouse Passport.</span></span> <span data-ttu-id="36591-300">Coloque isso logo após a configuração do servidor:</span><span class="sxs-lookup"><span data-stu-id="36591-300">Put this right after your other server configuration:</span></span>

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > <span data-ttu-id="36591-301">Quando você escreve APIs, recomendamos que você sempre vincular Olá dados toosomething exclusivo do token Olá Olá usuário não pode falsificar.</span><span class="sxs-lookup"><span data-stu-id="36591-301">When you write APIs, we recommend that you always link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="36591-302">Quando esse servidor armazena itens de tarefas, armazena-as com base na ID de objeto de saudação do usuário Olá no token de saudação (chamado por meio de token.oid), que são colocados no campo de "proprietário" hello.</span><span class="sxs-lookup"><span data-stu-id="36591-302">When this server stores TODO items, it stores them based on hello object ID of hello user in hello token (called through token.oid), which we put in hello “owner” field.</span></span> <span data-ttu-id="36591-303">Isso garante que somente o usuário possa acessar seus TODOs.</span><span class="sxs-lookup"><span data-stu-id="36591-303">This ensures that only that user can access their TODOs.</span></span> <span data-ttu-id="36591-304">Não há nenhuma exposição no Olá API de "proprietário", para que um usuário externo pode solicitar Olá TODOs outros mesmo quando eles são autenticados.</span><span class="sxs-lookup"><span data-stu-id="36591-304">There is no exposure in hello API of “owner,” so an external user can request hello TODOs of others even if they are authenticated.</span></span>                    

2. <span data-ttu-id="36591-305">Avançar vamos usar a estratégia de portador de saudação que vem com `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="36591-305">Next let’s use hello bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="36591-306">Examine o código de saudação por enquanto e explicaremos rest Olá em breve.</span><span class="sxs-lookup"><span data-stu-id="36591-306">Look at hello code for now and we'll explain hello rest shortly.</span></span> <span data-ttu-id="36591-307">Coloque isto depois do que você colou acima:</span><span class="sxs-lookup"><span data-stu-id="36591-307">Put this after what you pasted above:</span></span>

```Javascript
    /**
    /*
    /* Calling hello OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides hello need toomanage users and info tokens
    /* with a FindorCreate() method that must be provided by hello implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want toodo something smarter.
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


    var bearerStrategy = new BearerStrategy(options,
        function(token, done) {
            log.info('verifying hello user');
            log.info(token, 'was hello token retreived');
            findById(token.sub, function(err, user) {
                if (err) {
                    return done(err);
                }
                if (!user) {
                    // "Auto-registration"
                    log.info('User was added automatically as they were new. Their sub is: ', token.sub);
                    users.push(token);
                    owner = token.sub;
                    return done(null, token);
                }
                owner = token.sub;
                return done(null, user, token);
            });
        }
    );

    passport.use(bearerStrategy);
```

<span data-ttu-id="36591-308">O Passport usa um padrão semelhante para todas as estratégias (Twitter, Facebook e assim por diante) que todos os gravadores de estratégia seguem.</span><span class="sxs-lookup"><span data-stu-id="36591-308">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="36591-309">Passamos a ele uma função que tem um token e uma pronto como parâmetros de saudação observando estratégia hello, consulte.</span><span class="sxs-lookup"><span data-stu-id="36591-309">Looking at hello strategy, you see we pass it a function that has a token and a done as hello parameters.</span></span> <span data-ttu-id="36591-310">estratégia de saudação vem toous novamente depois que ele faz seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="36591-310">hello strategy comes back toous after it does its work.</span></span> <span data-ttu-id="36591-311">Depois que ele faz, armazenamos Olá usuário e token de saudação stash para que não seja necessário tooask para ele novamente.</span><span class="sxs-lookup"><span data-stu-id="36591-311">After it does, we store hello user and stash hello token so we won’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36591-312">código anterior Olá usa qualquer usuário que ocorre em tooauthenticate tooour server.</span><span class="sxs-lookup"><span data-stu-id="36591-312">hello previous code takes any user that happens tooauthenticate tooour server.</span></span> <span data-ttu-id="36591-313">Isso é conhecido como registro automático.</span><span class="sxs-lookup"><span data-stu-id="36591-313">This is known as auto-registration.</span></span> <span data-ttu-id="36591-314">Em servidores de produção, não convém permitir que qualquer pessoa entre sem primeiro passar por um processo de registro em que você decida.</span><span class="sxs-lookup"><span data-stu-id="36591-314">In production servers, you we recommend that you don't let anyone in without first having them go through a registration process that you decide on.</span></span> <span data-ttu-id="36591-315">Normalmente, este é o padrão de saudação que consulte em aplicativos de consumidor, que permitem que você tooregister com o Facebook, mas, em seguida, solicitar que você toofill informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="36591-315">This is usually hello pattern you see in consumer apps, which allow you tooregister with Facebook but then ask you toofill out additional information.</span></span> <span data-ttu-id="36591-316">Se isso não era um programa de linha de comando, podemos foi ter extrair email saudação do objeto de token de saudação que é retornado e, em seguida, terá Olá usuário toofill informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="36591-316">If this wasn’t a command-line program, we could have extracted hello email from hello token object that is returned and then asked hello user toofill out additional information.</span></span> <span data-ttu-id="36591-317">Como esse é um servidor de teste, basta adicioná-los banco de dados do toohello na memória.</span><span class="sxs-lookup"><span data-stu-id="36591-317">Because this is a test server, we simply add them toohello in-memory database.</span></span>
>
>

### <a name="protect-some-endpoints"></a><span data-ttu-id="36591-318">Proteger alguns pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="36591-318">Protect some endpoints</span></span>
<span data-ttu-id="36591-319">Proteger os pontos de extremidade, especificando Olá `passport.authenticate()` chamada com protocolo hello que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="36591-319">You protect endpoints by specifying hello `passport.authenticate()` call with hello protocol that you want toouse.</span></span>

<span data-ttu-id="36591-320">toomake nosso código do servidor fazer algo mais interessante, vamos Editar rota de saudação.</span><span class="sxs-lookup"><span data-stu-id="36591-320">toomake our server code do something more interesting, let’s edit hello route.</span></span>

```Javascript
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a><span data-ttu-id="36591-321">Etapa 19: executar o aplicativo de servidor novamente e certificar-se de que rejeitará você</span><span class="sxs-lookup"><span data-stu-id="36591-321">Step 19: Run your server application again and ensure it rejects you</span></span>
<span data-ttu-id="36591-322">Vamos usar `curl` novamente toosee se agora temos OAuth2 proteção contra os pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="36591-322">Let's use `curl` again toosee if we now have OAuth2 protection against our endpoints.</span></span> <span data-ttu-id="36591-323">Fazemos isso antes de executar qualquer um dos nossos SDKs de cliente para esse ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="36591-323">We do this test before running any of our client SDKs against this endpoint.</span></span> <span data-ttu-id="36591-324">Hello cabeçalhos que são retornados devem ser suficientes tootell conosco se vamos caminho certo hello.</span><span class="sxs-lookup"><span data-stu-id="36591-324">hello headers that are returned should be enough tootell us if we're going down hello right path.</span></span>

1. <span data-ttu-id="36591-325">Primeiro, verifique se a instância do MongoDB está em execução:</span><span class="sxs-lookup"><span data-stu-id="36591-325">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

2. <span data-ttu-id="36591-326">Em seguida, altere o diretório toohello e iniciar curling.</span><span class="sxs-lookup"><span data-stu-id="36591-326">Then, change toohello directory and start curling.</span></span>

      <span data-ttu-id="36591-327">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="36591-327">`$ cd azuread` `$ node server.js`</span></span>

3. <span data-ttu-id="36591-328">Tente uma POSTAGEM básica.</span><span class="sxs-lookup"><span data-stu-id="36591-328">Try a basic POST.</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="36591-329">Um 401 é resposta Olá que você está procurando aqui.</span><span class="sxs-lookup"><span data-stu-id="36591-329">A 401 is hello response you are looking for here.</span></span> <span data-ttu-id="36591-330">Essa resposta indica que camada Olá Passport está tentando tooredirect toohello autorizado ponto de extremidade que é exatamente o que você deseja.</span><span class="sxs-lookup"><span data-stu-id="36591-330">This response indicates that hello Passport layer is trying tooredirect toohello authorized endpoint, which is exactly what you want.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36591-331">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="36591-331">Next steps</span></span>
<span data-ttu-id="36591-332">Você já fez tudo o que podia com esse servidor sem usar um cliente compatível com o OAuth2.</span><span class="sxs-lookup"><span data-stu-id="36591-332">You've gone as far as you can with this server without using an OAuth2 compatible client.</span></span> <span data-ttu-id="36591-333">Você precisará toogo por meio de uma passo a passo adicional.</span><span class="sxs-lookup"><span data-stu-id="36591-333">You will need toogo through an additional walkthrough.</span></span>

<span data-ttu-id="36591-334">Você aprendeu como tooimplement uma API REST usando Restify e OAuth2.</span><span class="sxs-lookup"><span data-stu-id="36591-334">You've now learned how tooimplement a REST API by using Restify and OAuth2.</span></span> <span data-ttu-id="36591-335">Você também tem mais do que suficiente tookeep código desenvolver seu serviço e aprender como toobuild neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="36591-335">You also have more than enough code tookeep developing your service and learning how toobuild on this example.</span></span>

<span data-ttu-id="36591-336">Se você estiver interessado em próximas etapas de saudação em sua jornada ADAL, aqui estão alguns clientes ADAL com suporte, é recomendável que você continuar trabalhando com.</span><span class="sxs-lookup"><span data-stu-id="36591-336">If you are interested in hello next steps in your ADAL journey, here are some supported ADAL clients we recommend that you  keep working with.</span></span>

<span data-ttu-id="36591-337">Clonar a máquina do desenvolvedor tooyour e configure conforme descrito no passo a passo de saudação.</span><span class="sxs-lookup"><span data-stu-id="36591-337">Clone down tooyour developer machine and configure as described in hello walkthrough.</span></span>

[<span data-ttu-id="36591-338">ADAL para iOS</span><span class="sxs-lookup"><span data-stu-id="36591-338">ADAL for iOS</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[<span data-ttu-id="36591-339">ADAL para Android</span><span class="sxs-lookup"><span data-stu-id="36591-339">ADAL for Android</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
