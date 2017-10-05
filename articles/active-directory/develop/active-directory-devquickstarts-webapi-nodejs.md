---
title: "Introdução ao Node.js do Azure AD | Microsoft Docs"
description: "Como compilar uma API Web REST do Node.js que se integre ao Azure AD para autenticação."
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
ms.openlocfilehash: 4f58177f540c14172d7ece8b4bc8c8a2b9787f8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a><span data-ttu-id="7ab6c-103">Introdução às APIs Web para o Node.js</span><span class="sxs-lookup"><span data-stu-id="7ab6c-103">Get started with web APIs for Node.js</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="7ab6c-104">*Passport* é middleware de autenticação para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-104">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="7ab6c-105">Flexível e modular, o Passport pode ser colocado sem impedimento em qualquer aplicativo Web baseado em Express ou Restify.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-105">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Restify web application.</span></span> <span data-ttu-id="7ab6c-106">Um conjunto abrangente de estratégias dão suporte à autenticação usando um nome de usuário e senha, Facebook, Twitter e mais.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-106">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="7ab6c-107">Desenvolvemos uma estratégia para o Microsoft Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7ab6c-107">We have developed a strategy for Microsoft Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="7ab6c-108">Instalamos esse módulo e então adicionamos o plug-in `passport-azure-ad` do Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-108">We install this module and then add the Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="7ab6c-109">Para fazer isso, você precisa:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-109">To do this, you need to:</span></span>

1. <span data-ttu-id="7ab6c-110">Registrar um aplicativo com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-110">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="7ab6c-111">Configurar seu aplicativo para usar o plug-in `passport-azure-ad` do Passport.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-111">Set up your app to use Passport's `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="7ab6c-112">Configurar um aplicativo cliente para chamar a API da Web da "lista de tarefas pendentes".</span><span class="sxs-lookup"><span data-stu-id="7ab6c-112">Configure a client application to call the To Do List web API.</span></span>

<span data-ttu-id="7ab6c-113">O código para este tutorial é mantido [no GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span><span class="sxs-lookup"><span data-stu-id="7ab6c-113">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span></span>

> [!NOTE]
> <span data-ttu-id="7ab6c-114">Este artigo não aborda como implementar conexão, registro e gerenciamento de perfil com o Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-114">This article doesn't cover how to implement sign-in, sign-up, or profile management with Azure AD B2C.</span></span> <span data-ttu-id="7ab6c-115">Ele se concentra na chamada a APIs Web depois que o usuário já está autenticado.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-115">It focuses on calling web APIs after the user is already authenticated.</span></span>  <span data-ttu-id="7ab6c-116">Recomendamos que você comece lendo o [documento Como integrar com o Azure Active Directory](active-directory-how-to-integrate.md) para saber mais sobre os conceitos básicos do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-116">We recommend that you start with [How to integrate with Azure Active Directory document](active-directory-how-to-integrate.md) to learn about the basics of Azure Active Directory.</span></span>
>
>

<span data-ttu-id="7ab6c-117">Já lançamos todo o código-fonte para este exemplo em execução no GitHub sob uma licença do MIT, então fique à vontade para copiar (ou melhor ainda, divulgar), fazer comentários e solicitações pull.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-117">We've released all the source code for this running example in GitHub under an MIT license, so feel free to clone (or even better, fork), and provide feedback and pull requests.</span></span>

## <a name="about-nodejs-modules"></a><span data-ttu-id="7ab6c-118">Sobre os módulos do Node.js</span><span class="sxs-lookup"><span data-stu-id="7ab6c-118">About Node.js modules</span></span>
<span data-ttu-id="7ab6c-119">Usaremos módulos do Node.js neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-119">We use Node.js modules in this walkthrough.</span></span> <span data-ttu-id="7ab6c-120">Os módulos são pacotes carregáveis do JavaScript que fornecem funcionalidade específica para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-120">Modules are loadable JavaScript packages that provide specific functionality for your application.</span></span> <span data-ttu-id="7ab6c-121">Você geralmente instala módulos usando uma ferramenta de linha de comando NPM do Node.js no diretório de instalação do NPM.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-121">You usually install modules by using the Node.js an NPM command-line tool in the NPM installation directory.</span></span> <span data-ttu-id="7ab6c-122">No entanto, alguns módulos, como o módulo HTTP, estão inclusos no pacote do Node.js do núcleo.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-122">However, some modules, such as the HTTP module, are included in the core Node.js package.</span></span>

<span data-ttu-id="7ab6c-123">Os módulos instalados são salvos no diretório **node_modules**, na raiz do diretório de instalação do seu Node.js.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-123">Installed modules are saved in the **node_modules** directory at the root of your Node.js installation directory.</span></span> <span data-ttu-id="7ab6c-124">Cada módulo dentro do diretório **node_modules** mantém seu próprio diretório **node_modules** que contém todos os módulos dos quais ele depende.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-124">Each module in the **node_modules** directory maintains its own **node_modules** directory that contains any modules that it depends on.</span></span> <span data-ttu-id="7ab6c-125">Além disso, cada módulo requerido tem um diretório **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-125">Also, each required module has a **node_modules** directory.</span></span> <span data-ttu-id="7ab6c-126">Essa estrutura de diretório recursiva representa a cadeia de dependências.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-126">This recursive directory structure represents the dependency chain.</span></span>

<span data-ttu-id="7ab6c-127">Essa estrutura de cadeia de dependência resulta em um espaço de aplicativo maior.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-127">This dependency chain structure results in a larger application footprint.</span></span> <span data-ttu-id="7ab6c-128">Mas ela também garante que todas as dependências sejam atendidas e que a versão dos módulos usada no desenvolvimento também seja usada na produção.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-128">But it also guarantees that all dependencies are met and that the version of the modules that's used in development is also used in production.</span></span> <span data-ttu-id="7ab6c-129">Isso torna o comportamento do aplicativo de produção mais previsível e evita os problemas de controle de versão que podem afetar os usuários.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-129">This makes the production app behavior more predictable and prevents versioning problems that might affect users.</span></span>

## <a name="step-1-register-an-azure-ad-tenant"></a><span data-ttu-id="7ab6c-130">Etapa 1: registrar um locatário do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ab6c-130">Step 1: Register an Azure AD tenant</span></span>
<span data-ttu-id="7ab6c-131">Para usar esse exemplo, você precisará de um locatário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-131">To use this sample, you need an Azure Active Directory tenant.</span></span> <span data-ttu-id="7ab6c-132">Se você não tem certeza do que é um locatário ou como obter um, consulte [Como obter um locatário do Azure AD](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="7ab6c-132">If you're not sure what a tenant is or how to get one, see [How to get an Azure AD tenant](active-directory-howto-tenant.md).</span></span>

## <a name="step-2-create-an-application"></a><span data-ttu-id="7ab6c-133">Etapa 2: criar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="7ab6c-133">Step 2: Create an application</span></span>
<span data-ttu-id="7ab6c-134">Em seguida, crie um aplicativo no seu diretório que dê ao Azure AD algumas informações de que ele precisa para se comunicar de forma segura com o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-134">Next you create an app in your directory that gives Azure AD information that it needs to securely communicate with your app.</span></span>  <span data-ttu-id="7ab6c-135">O aplicativo cliente e a API da Web são representados por uma única **ID de aplicativo** nesse caso, pois eles abrangem um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-135">Both the client app and web API are represented by a single **Application ID** in this case, because they comprise one logical app.</span></span>  <span data-ttu-id="7ab6c-136">Para criar um aplicativo, [siga estas instruções](active-directory-how-applications-are-added.md).</span><span class="sxs-lookup"><span data-stu-id="7ab6c-136">To create an app, follow [these instructions](active-directory-how-applications-are-added.md).</span></span> <span data-ttu-id="7ab6c-137">Se você estiver criando um aplicativo de linha de negócios, [estas instruções adicionais podem ser úteis](../active-directory-applications-guiding-developers-for-lob-applications.md).</span><span class="sxs-lookup"><span data-stu-id="7ab6c-137">If you are building a line-of-business app, [these additional instructions might be useful](../active-directory-applications-guiding-developers-for-lob-applications.md).</span></span>

<span data-ttu-id="7ab6c-138">Para criar um aplicativo:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-138">To create an application:</span></span>

1. <span data-ttu-id="7ab6c-139">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7ab6c-139">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="7ab6c-140">No menu superior, selecione a sua conta.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-140">On the top menu, select your account.</span></span> <span data-ttu-id="7ab6c-141">Na lista **Diretório**, escolha o locatário do Active Directory onde você deseja registrar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-141">Then, under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>

3. <span data-ttu-id="7ab6c-142">No menu do lado esquerdo da tela, selecione **Mais Serviços**, depois selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-142">In the menu on the left, select **More Services**, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="7ab6c-143">Selecione **Registros do aplicativo**e, em seguida, selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-143">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="7ab6c-144">Siga os prompts para criar um **Aplicativo Web e/ou uma WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-144">Follow the prompts to create a **Web Application and/or WebAPI**.</span></span>

      * <span data-ttu-id="7ab6c-145">O **nome** do aplicativo descreve o seu aplicativo aos usuários finais.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-145">The **name** of the application describes your application to end users.</span></span>

      * <span data-ttu-id="7ab6c-146">A **URL de logon** é a URL base do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-146">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="7ab6c-147">A URL padrão do código de exemplo é `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-147">The default URL of the sample code is `https://localhost:8080`.</span></span>

6. <span data-ttu-id="7ab6c-148">Depois de se registrar, o Azure AD atribui uma ID de aplicativo única ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-148">After you register, Azure AD assigns your app a unique Application ID.</span></span> <span data-ttu-id="7ab6c-149">Você precisará desse valor nas próximas seções, então copie-o da página do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-149">You need this value in the next sections, so copy it from the application page.</span></span>

7. <span data-ttu-id="7ab6c-150">Na página **Configurações** -> **Propriedades** do aplicativo, atualize o URI da ID do Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-150">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="7ab6c-151">O **URI da ID do aplicativo** é um identificador exclusivo para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-151">The **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="7ab6c-152">A convenção é usar `https://<tenant-domain>/<app-name>`, por exemplo: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-152">The convention is to use `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

8. <span data-ttu-id="7ab6c-153">Crie uma **Chave** para o seu aplicativo na página **Configurações** e copie-a em algum lugar.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-153">Create a **Key** for your application from the **Settings** page, and then copy it somewhere.</span></span> <span data-ttu-id="7ab6c-154">Você precisará dela em breve.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-154">You'll need it shortly.</span></span>

## <a name="step-3-download-nodejs-for-your-platform"></a><span data-ttu-id="7ab6c-155">Etapa 3: baixar o Node.js para a sua plataforma</span><span class="sxs-lookup"><span data-stu-id="7ab6c-155">Step 3: Download Node.js for your platform</span></span>
<span data-ttu-id="7ab6c-156">Para usar este exemplo com êxito, você deve ter uma instalação do Node.js em funcionamento.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-156">To successfully use this sample, you must have a working installation of Node.js.</span></span>

<span data-ttu-id="7ab6c-157">Instale o Node.js a partir de [http://nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="7ab6c-157">Install Node.js from [http://nodejs.org](http://nodejs.org).</span></span>

## <a name="step-4-install-mongodb-on-your-platform"></a><span data-ttu-id="7ab6c-158">Etapa 4: instalar o MongoDB na sua plataforma</span><span class="sxs-lookup"><span data-stu-id="7ab6c-158">Step 4: Install MongoDB on your platform</span></span>
<span data-ttu-id="7ab6c-159">Para usar este exemplo com êxito, você deve ter uma instalação do MongoDB funcionando corretamente.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-159">To successfully use this sample, you must have a working installation of MongoDB.</span></span> <span data-ttu-id="7ab6c-160">Use o MongoDB para tornar a API REST persistente entre as instâncias do servidor.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-160">You use MongoDB to make the REST API persistent across server instances.</span></span>

<span data-ttu-id="7ab6c-161">Instalar o MongoDB a partir de [http://mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="7ab6c-161">Install MongoDB from [http://mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="7ab6c-162">Este passo a passo presume que você usa os pontos de extremidade de servidor e de instalação padrão para o MongoDB, que, no momento da redação deste artigo, é: mongodb://localhost.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-162">This walkthrough assumes that you use the default installation and server endpoints for MongoDB, which at the time of this writing is mongodb://localhost.</span></span>
>
>

## <a name="step-5-install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="7ab6c-163">Etapa 5: instalar os módulos Restify na sua API da Web</span><span class="sxs-lookup"><span data-stu-id="7ab6c-163">Step 5: Install the Restify modules in your web API</span></span>
<span data-ttu-id="7ab6c-164">Usaremos o Resitfy para criar nossa API REST.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-164">We are using Restify to build our REST API.</span></span> <span data-ttu-id="7ab6c-165">O Restify é uma estrutura de aplicativo do Node.js mínima e flexível, derivada do Express.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-165">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="7ab6c-166">Tem um conjunto robusto de recursos para a criação de APIs REST sobre o Connect.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-166">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="7ab6c-167">Instalar Restify</span><span class="sxs-lookup"><span data-stu-id="7ab6c-167">Install Restify</span></span>
1. <span data-ttu-id="7ab6c-168">Na linha de comando, altere os diretórios para o diretório **azuread**.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-168">From the command line, change directories to the **azuread** directory.</span></span> <span data-ttu-id="7ab6c-169">Se o diretório **azuread** não existir, crie-o.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-169">If the **azuread** directory does not exist, create it.</span></span>

        `cd azuread - or- mkdir azuread; cd azuread`

2. <span data-ttu-id="7ab6c-170">Digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-170">Type the following command:</span></span>

    `npm install restify`

    <span data-ttu-id="7ab6c-171">Este comando instala o Restify.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="7ab6c-172">Você obteve um erro?</span><span class="sxs-lookup"><span data-stu-id="7ab6c-172">Did you get an error?</span></span>
<span data-ttu-id="7ab6c-173">Ao usar o NPM em alguns sistemas operacionais, você poderá receber uma mensagem de erro que diz: **Erro: EPERM, chmod '/usr/local/bin/..'**</span><span class="sxs-lookup"><span data-stu-id="7ab6c-173">When you use NPM on some operating systems, you might receive an error that says **Error: EPERM, chmod '/usr/local/bin/..'**</span></span> <span data-ttu-id="7ab6c-174">e uma solicitação para tentar executar a conta como administrador.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-174">and a suggestion that you try running the account as an administrator.</span></span> <span data-ttu-id="7ab6c-175">Se isso ocorrer, use o comando sudo para executar o NPM com um nível de privilégio mais elevado.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-175">If this occurs, use the sudo command to run NPM at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-regarding-dtrace"></a><span data-ttu-id="7ab6c-176">Ocorreu um erro com relação ao DTRACE?</span><span class="sxs-lookup"><span data-stu-id="7ab6c-176">Did you get an error regarding DTRACE?</span></span>
<span data-ttu-id="7ab6c-177">Você poderá ver um erro assim ao instalar o Restify:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-177">You might see an error like this when installing Restify:</span></span>

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
<span data-ttu-id="7ab6c-178">O Restify fornece um mecanismo poderoso para rastreamento de chamadas REST usando o DTrace.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-178">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="7ab6c-179">No entanto, muitos sistemas operacionais não possuem o DTrace.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-179">However, many operating systems do not have DTrace.</span></span> <span data-ttu-id="7ab6c-180">Você pode ignorar com segurança esses erros.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-180">You can safely ignore these errors.</span></span>

<span data-ttu-id="7ab6c-181">A saída desse comando deve ser semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-181">The output of this command should look similar to the following output:</span></span>

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


## <a name="step-6-install-passportjs-in-your-web-api"></a><span data-ttu-id="7ab6c-182">Etapa 6: instalar o Passport.js na sua API da Web</span><span class="sxs-lookup"><span data-stu-id="7ab6c-182">Step 6: Install Passport.js in your web API</span></span>
<span data-ttu-id="7ab6c-183">[Passport](http://passportjs.org/) é middleware de autenticação para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-183">[Passport](http://passportjs.org/) is authentication middleware for Node.js.</span></span> <span data-ttu-id="7ab6c-184">Flexível e modular, o Passport pode ser colocado sem impedimento em qualquer aplicativo Web baseado em Express ou Restify.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-184">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Restify web application.</span></span> <span data-ttu-id="7ab6c-185">Um conjunto abrangente de estratégias dão suporte à autenticação usando um nome de usuário e senha, Facebook, Twitter e mais.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-185">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="7ab6c-186">Desenvolvemos uma estratégia para o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-186">We have developed a strategy for Azure Active Directory.</span></span> <span data-ttu-id="7ab6c-187">Instalaremos esse módulo e, em seguida, adicionaremos o plug-in de estratégia do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-187">We install this module and then add the Azure Active Directory strategy plug-in.</span></span>

1. <span data-ttu-id="7ab6c-188">Na linha de comando, altere os diretórios para o diretório **azuread**.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-188">From the command line, change directories to the **azuread** directory.</span></span>

2. <span data-ttu-id="7ab6c-189">Insira o comando a seguir para instalar o passport.js:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-189">To install passport.js, enter the following command :</span></span>

    `npm install passport`

    <span data-ttu-id="7ab6c-190">A saída do comando deve ser semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-190">The output of the command should look similar to the following:</span></span>

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-to-your-web-api"></a><span data-ttu-id="7ab6c-191">Etapa 7: adicionar o Passport-Azure-AD à sua API da Web</span><span class="sxs-lookup"><span data-stu-id="7ab6c-191">Step 7: Add Passport-Azure-AD to your web API</span></span>
<span data-ttu-id="7ab6c-192">Em seguida, adicionamos a estratégia OAuth usando `passport-azure-ad`, um pacote de estratégias que conectam o Azure Active Directory ao Passport.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-192">Next we add the OAuth strategy by using `passport-azure-ad`, a suite of strategies that connect Azure Active Directory to Passport.</span></span> <span data-ttu-id="7ab6c-193">Usaremos essa estratégia para tokens de portador neste exemplo de API Rest.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-193">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="7ab6c-194">Embora o OAuth2 forneça uma estrutura na qual qualquer tipo de token conhecido possa ser emitido, somente determinados tipos de token são comumente usados.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-194">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types are commonly used.</span></span> <span data-ttu-id="7ab6c-195">Os tokens de portador são os tokens mais usados para proteger os pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-195">Bearer tokens are the most commonly used tokens for protecting endpoints.</span></span> <span data-ttu-id="7ab6c-196">Esses são o tipo mais amplamente emitido de token no OAuth2.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-196">They are the most widely issued type of token in OAuth2.</span></span> <span data-ttu-id="7ab6c-197">Muitas implementações presumem que os tokens de portador sejam o único tipo de token emitido.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-197">Many implementations assume that bearer tokens are the only type of tokens that are issued.</span></span>
>
>

<span data-ttu-id="7ab6c-198">Na linha de comando, altere os diretórios para o diretório **azuread**.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-198">From the command line, change directories to the **azuread** directory.</span></span>

<span data-ttu-id="7ab6c-199">Insira o comando a seguir para instalar o Passport.js`passport-azure-ad module`:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-199">Type the following command to install the Passport.js `passport-azure-ad module`:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="7ab6c-200">A saída do comando deve ser semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-200">The output of the command should look similar to the following output:</span></span>


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



## <a name="step-8-add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="7ab6c-201">Etapa 8: adicionar módulos do MongoDB à sua API da Web</span><span class="sxs-lookup"><span data-stu-id="7ab6c-201">Step 8: Add MongoDB modules to your web API</span></span>
<span data-ttu-id="7ab6c-202">Usamos o MongoDB como nosso repositório de dados.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-202">We use MongoDB as our datastore.</span></span> <span data-ttu-id="7ab6c-203">Por esse motivo, é preciso instalar o plug-in amplamente utilizado chamado Mongoose para gerenciar modelos e esquemas.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-203">For that reason, we need to install the widely used plug-in called Mongoose to manage models and schemas.</span></span> <span data-ttu-id="7ab6c-204">Também é necessário instalar o driver do banco de dados para o MongoDB (que também é chamado de MongoDB).</span><span class="sxs-lookup"><span data-stu-id="7ab6c-204">We also need to install the database driver for MongoDB (which is also called MongoDB).</span></span>

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a><span data-ttu-id="7ab6c-205">Etapa 9: instalar módulos adicionais</span><span class="sxs-lookup"><span data-stu-id="7ab6c-205">Step 9: Install additional modules</span></span>
<span data-ttu-id="7ab6c-206">Em seguida, instalaremos os módulos necessários restantes.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-206">Next we install the remaining required modules.</span></span>

1. <span data-ttu-id="7ab6c-207">Na linha de comando, altere os diretórios para a pasta **azuread**, se você ainda não estiver nela.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-207">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="7ab6c-208">Digite os comandos a seguir para instalar esses módulos no seu diretório **node_modules**:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-208">Enter the following commands to install these modules in your **node_modules** directory:</span></span>

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a><span data-ttu-id="7ab6c-209">Etapa 10: criar um server.js com as suas dependências</span><span class="sxs-lookup"><span data-stu-id="7ab6c-209">Step 10: Create a server.js with your dependencies</span></span>
<span data-ttu-id="7ab6c-210">O arquivo server.js fornece a maior parte da funcionalidade para o nosso servidor de API da Web.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-210">The server.js file provides most of the functionality for our web API server.</span></span> <span data-ttu-id="7ab6c-211">Adicionamos a maior parte do nosso código a esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-211">We add most of our code to this file.</span></span> <span data-ttu-id="7ab6c-212">Para fins de produção, recomendamos que você refatore a funcionalidade em arquivos menores, como rotas separadas e controladores.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-212">For production purposes, we recommend that you refactor the functionality into smaller files, such as separate routes and controllers.</span></span> <span data-ttu-id="7ab6c-213">Nesta demonstração, usaremos o server.js para essa funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-213">In this demo, we use server.js for this functionality.</span></span>

1. <span data-ttu-id="7ab6c-214">Na linha de comando, altere os diretórios para a pasta **azuread**, se você ainda não estiver nela.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-214">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="7ab6c-215">Crie um arquivo `server.js` no seu editor favorito e adicione as informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-215">Create a `server.js` file in your favorite editor, and then add the following information:</span></span>

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

3. <span data-ttu-id="7ab6c-216">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-216">Save the file.</span></span> <span data-ttu-id="7ab6c-217">Voltaremos a ele em breve.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-217">We'll return to it shortly.</span></span>

## <a name="step-11-create-a-config-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="7ab6c-218">Etapa 11: criar um arquivo de configuração para armazenar as configurações do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="7ab6c-218">Step 11: Create a config file to store your Azure AD settings</span></span>
<span data-ttu-id="7ab6c-219">Esse arquivo de código passa os parâmetros de configuração do seu Portal do Azure Active Directory ao Passport.js.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-219">This code file passes the configuration parameters from your Azure Active Directory portal to Passport.js.</span></span> <span data-ttu-id="7ab6c-220">Você criou esses valores de configuração quando adicionou a API da Web ao portal na primeira parte do passo a passo.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-220">You created these configuration values when you added the web API to the portal in the first part of the walkthrough.</span></span> <span data-ttu-id="7ab6c-221">Explicaremos o que deve ser inserido nos valores desses parâmetros depois que você copiar o código.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-221">We explain what to put in the values of these parameters after you copy the code.</span></span>

1. <span data-ttu-id="7ab6c-222">Na linha de comando, altere os diretórios para a pasta **azuread**, se você ainda não estiver nela.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-222">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="7ab6c-223">Crie um arquivo `config.js` no seu editor favorito e adicione as informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-223">Create a `config.js` file in your favorite editor, and then add the following information:</span></span>

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in to your server unless you use the common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in to your server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes to stderr in Unix.

         };
    ```
3. <span data-ttu-id="7ab6c-224">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-224">Save the file.</span></span>

## <a name="step-12-add-configuration-values-to-your-serverjs-file"></a><span data-ttu-id="7ab6c-225">Etapa 12: adicione valores de configuração ao seu arquivo server.js</span><span class="sxs-lookup"><span data-stu-id="7ab6c-225">Step 12: Add configuration values to your server.js file</span></span>
<span data-ttu-id="7ab6c-226">Precisamos ler esses valores do arquivo .config que você acabou de criar no nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-226">We need to read these values from the .config file that you created across our application.</span></span> <span data-ttu-id="7ab6c-227">Para fazer isso, adicionamos o arquivo .config como um recurso necessário em nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-227">To do this, we add the .config file as a required resource in our application.</span></span> <span data-ttu-id="7ab6c-228">Em seguida, definimos as variáveis globais para corresponder às variáveis no documento config. js.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-228">Then we set the global variables to match the variables in the config.js document.</span></span>

1. <span data-ttu-id="7ab6c-229">Na linha de comando, altere os diretórios para a pasta **azuread**, se você ainda não estiver nela.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-229">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="7ab6c-230">Abra o arquivo `server.js` no seu editor favorito e adicione as informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-230">Open your `server.js` file in your favorite editor, and then add the following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```
3. <span data-ttu-id="7ab6c-231">Em seguida, adicione uma nova seção a `server.js` com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-231">Then add a new section to `server.js` with the following code:</span></span>

    ```Javascript
    var options = {
        // The URL of the metadata document for your app. We will put the keys for token validation from the URL found in the jwks_uri tag of the in the metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array to hold logged in users and the current logged in user (owner).
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

      // If the logging level is specified, switch to it.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. <span data-ttu-id="7ab6c-232">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-232">Save the file.</span></span>

## <a name="step-13-add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="7ab6c-233">Etapa 13: adicionar as informações de esquema e modelo do MongoDB usando o Mongoose</span><span class="sxs-lookup"><span data-stu-id="7ab6c-233">Step 13: Add The MongoDB Model and schema information by using Mongoose</span></span>
<span data-ttu-id="7ab6c-234">Agora toda essa preparação passará a compensar, enquanto combinamos esses três arquivos em um serviço de API REST.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-234">Now all this preparation is going to start paying off as we combine these three files into a REST API service.</span></span>

<span data-ttu-id="7ab6c-235">Para este passo a passo, usaremos o MongoDB para armazenar nossas tarefas, conforme discutido na Etapa 4.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-235">For this walkthrough, we use MongoDB to store our tasks as discussed in Step 4.</span></span>

<span data-ttu-id="7ab6c-236">No arquivo `config.js` criado na Etapa 11, chamamos nosso banco de dados de `tasklist`, já que foi isso que colocamos no final da nossa URL de conexão **mogoose_auth_local**.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-236">In the `config.js` file that we created in Step 11, we called our database `tasklist`, because that was what we put at the end of our **mogoose_auth_local** connection URL.</span></span> <span data-ttu-id="7ab6c-237">Você não precisa criar esse banco de dados com antecedência no MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-237">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="7ab6c-238">Em vez disso, o MongoDB o criará para nós na primeira execução do nosso aplicativo de servidor (supondo que o banco de dados ainda não existe).</span><span class="sxs-lookup"><span data-stu-id="7ab6c-238">Instead, MongoDB creates this for us on the first run of our server application (assuming that the database doesn't already exist).</span></span>

<span data-ttu-id="7ab6c-239">Agora que dissemos ao servidor qual banco de dados MongoDB gostaríamos de usar, precisamos escrever algum código adicional para criar o modelo e o esquema para as tarefas do nosso servidor.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-239">Now that we've told the server which MongoDB database we'd like to use, we need to write some additional code to create the model and schema for our server's tasks.</span></span>

### <a name="discussion-of-the-model"></a><span data-ttu-id="7ab6c-240">Discussão do modelo</span><span class="sxs-lookup"><span data-stu-id="7ab6c-240">Discussion of the model</span></span>
<span data-ttu-id="7ab6c-241">Nosso modelo de esquema é simples.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-241">Our schema model is simple.</span></span> <span data-ttu-id="7ab6c-242">Você pode expandi-lo conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-242">You expand it as required.</span></span>

<span data-ttu-id="7ab6c-243">NAME: o nome da pessoa a quem é atribuída a tarefa.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-243">NAME: The name of the person who is assigned to the task.</span></span> <span data-ttu-id="7ab6c-244">Uma **cadeia de caracteres**.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-244">A **String**.</span></span>

<span data-ttu-id="7ab6c-245">TASK: a própria tarefa.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-245">TASK: The task itself.</span></span> <span data-ttu-id="7ab6c-246">Uma **cadeia de caracteres**.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-246">A **String**.</span></span>

<span data-ttu-id="7ab6c-247">DATE: a data em que a tarefa deverá ser concluída.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-247">DATE: The date that the task is due.</span></span> <span data-ttu-id="7ab6c-248">UM VALOR **DATETIME**.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-248">A **DATETIME**.</span></span>

<span data-ttu-id="7ab6c-249">COMPLETED: se a tarefa foi concluída ou não.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-249">COMPLETED: If the task has been completed or not.</span></span> <span data-ttu-id="7ab6c-250">UM VALOR **BOOLEANO**.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-250">A **BOOLEAN**.</span></span>

### <a name="creating-the-schema-in-the-code"></a><span data-ttu-id="7ab6c-251">Criando o esquema no código</span><span class="sxs-lookup"><span data-stu-id="7ab6c-251">Creating the schema in the code</span></span>
1. <span data-ttu-id="7ab6c-252">Na linha de comando, altere os diretórios para a pasta **azuread**, se você ainda não estiver nela.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-252">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="7ab6c-253">Abra o arquivo `server.js` no seu editor favorito e adicione as seguintes informações abaixo da entrada de configuração:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-253">Open your `server.js` file in your favorite editor, and then add the following information below the configuration entry:</span></span>

    ```Javascript
    // Connect to MongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema to store our tasks and users. It's a fairly simple schema for now.
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
<span data-ttu-id="7ab6c-254">Como você pode ver no código, criamos nosso esquema primeiro.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-254">As you can tell from the code, we create our schema first.</span></span> <span data-ttu-id="7ab6c-255">Em seguida, criamos um objeto de modelo que usamos para armazenar nossos dados por todo o código quando definimos nossas **Rotas**.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-255">Then we create a model object that we use to store our data throughout the code when we define our **Routes**.</span></span>

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a><span data-ttu-id="7ab6c-256">Etapa 14: adicionar nossas rotas a nosso servidor de API REST da tarefa</span><span class="sxs-lookup"><span data-stu-id="7ab6c-256">Step 14: Add our routes for our task REST API server</span></span>
<span data-ttu-id="7ab6c-257">Agora que temos um modelo de banco de dados com o qual trabalhar, vamos adicionar as rotas que usaremos para o nosso servidor de API REST.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-257">Now that we have a database model to work with, let's add the routes we are going use for our REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="7ab6c-258">Sobre rotas no Restify</span><span class="sxs-lookup"><span data-stu-id="7ab6c-258">About routes in Restify</span></span>
<span data-ttu-id="7ab6c-259">As rotas funcionam no Restify exatamente da mesma maneira que funcionam usando a pilha Express.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-259">Routes work in Restify the same way they do in the Express stack.</span></span> <span data-ttu-id="7ab6c-260">Você define rotas usando o URI que espera que os aplicativos de cliente chamem.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-260">You define routes by using the URI that you expect the client applications to call.</span></span> <span data-ttu-id="7ab6c-261">Normalmente, você define suas rotas em um arquivo separado.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-261">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="7ab6c-262">Para nossos propósitos, colocaremos as nossas rotas no arquivo server.js.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-262">For our purposes, we put our routes in the server.js file.</span></span> <span data-ttu-id="7ab6c-263">Recomendamos que você as coloque no seu próprio arquivo para uso em produção.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-263">We recommend that you factor these routes into their own file for production use.</span></span>

<span data-ttu-id="7ab6c-264">Um padrão típico para uma rota do Restify é:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-264">A typical pattern for a Restify route is as follows:</span></span>

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep the server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


<span data-ttu-id="7ab6c-265">Esse é o padrão no nível mais básico.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-265">This is the pattern at its most basic level.</span></span> <span data-ttu-id="7ab6c-266">O Restify (e o Express) fornece uma funcionalidade muito mais aprofundada, como a definição de tipos de aplicativos e o roteamento complexo entre diferentes pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-266">Restify (and Express) provide much deeper functionality, such as defining application types and providing complex routing across different endpoints.</span></span> <span data-ttu-id="7ab6c-267">Para nossos propósitos, estamos mantendo essas rotas simples.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-267">For our purposes, we are keeping these routes simple.</span></span>

### <a name="add-default-routes-to-our-server"></a><span data-ttu-id="7ab6c-268">Adicionar rotas padrão ao nosso servidor</span><span class="sxs-lookup"><span data-stu-id="7ab6c-268">Add default routes to our server</span></span>
<span data-ttu-id="7ab6c-269">Agora adicionamos as rotas CRUD básicas de Create (criar), Retrieve (extrair), Update (atualizar) e Delete (excluir).</span><span class="sxs-lookup"><span data-stu-id="7ab6c-269">We now add the basic CRUD routes of Create, Retrieve, Update, and Delete.</span></span>

1. <span data-ttu-id="7ab6c-270">Na linha de comando, altere os diretórios para a pasta **azuread**, se você ainda não estiver nela:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-270">From the command line, change directories to the **azuread** folder if you're not already there:</span></span>

    `cd azuread`

2. <span data-ttu-id="7ab6c-271">Abra o arquivo `server.js` no nosso editor favorito e adicione as seguintes informações abaixo das entradas anteriores do banco de dados que você criou:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-271">Open the `server.js` file in your favorite editor, and then add the following information below the previous database entries that you made:</span></span>

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you to set default headers.
    // These headers comply with CORS and allow us to mongodbServer our response to any origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it to Mongodb.
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

/// Simple returns the list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you to set default headers.
    // These headers comply with CORS and allow us to mongodbServer our response to any origin.

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
            log.warn(err, "There is no tasks in the database. Did you initialize the database as stated in the README?");
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

### <a name="add-error-handling-in-our-apis"></a><span data-ttu-id="7ab6c-272">Adicionar tratamento de erros em nossas APIs</span><span class="sxs-lookup"><span data-stu-id="7ab6c-272">Add error handling in our APIs</span></span>
```

///--- Errors for communicating something interesting back to the client.

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


## <a name="step-15-create-your-server"></a><span data-ttu-id="7ab6c-273">Etapa 15: criar seu servidor</span><span class="sxs-lookup"><span data-stu-id="7ab6c-273">Step 15: Create your server</span></span>
<span data-ttu-id="7ab6c-274">Definimos nosso banco de dados e nossas rotas estão em vigor.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-274">We have defined our database and our routes are in place.</span></span> <span data-ttu-id="7ab6c-275">A última coisa a fazer é adicionar a instância do servidor que gerencia nossas chamadas.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-275">The last thing to do is add the server instance that manages our calls.</span></span>

<span data-ttu-id="7ab6c-276">No Restify (e no Express) é possível fazer várias personalizações em um servidor de API REST, mas, novamente, usaremos a configuração mais básica para atender aos nossos objetivos.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-276">In Restify (and Express) you can do a lot of customization for a REST API server, but again we are going to use the most basic setup for our purposes.</span></span>

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

// Allow five requests per second by IP, and burst to 10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use the common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping to REST.
```

## <a name="step-16-add-the-routes-to-the-server-without-authentication-for-now"></a><span data-ttu-id="7ab6c-277">Etapa 16: adicionar as rotas ao servidor (sem autenticação, por enquanto)</span><span class="sxs-lookup"><span data-stu-id="7ab6c-277">Step 16: Add the routes to the server (without authentication for now)</span></span>
```Javascript
/// Now the real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In the pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need to maintain session state. You can experiment with removing API protection
/* by removing the passport.authenticate() method as follows:
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
consoleMessage += '\n Open your browser to %s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```

## <a name="step-17-run-the-server-before-adding-oauth-support"></a><span data-ttu-id="7ab6c-278">Etapa 17: executar o servidor (antes de adicionar o suporte ao OAuth)</span><span class="sxs-lookup"><span data-stu-id="7ab6c-278">Step 17: Run the server (before adding OAuth support)</span></span>
<span data-ttu-id="7ab6c-279">Teste o seu servidor antes de adicionarmos a autenticação.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-279">Test out your server before we add authentication.</span></span>

<span data-ttu-id="7ab6c-280">A maneira mais fácil de testar o seu servidor é usando ondulação em uma linha de comando.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-280">The easiest way to test your server is by using curl in a command line.</span></span> <span data-ttu-id="7ab6c-281">Antes de fazermos isso, precisamos de um utilitário que nos permita analisar a saída como JSON.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-281">Before we do that, we need a utility that allows us to parse output as JSON.</span></span>

1. <span data-ttu-id="7ab6c-282">Instale a seguinte ferramenta JSON (todos os exemplos a seguir usam essa ferramenta):</span><span class="sxs-lookup"><span data-stu-id="7ab6c-282">Install the following JSON tool (all the following examples use this tool):</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="7ab6c-283">Isso instala a ferramenta JSON globalmente.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-283">This installs the JSON tool globally.</span></span> <span data-ttu-id="7ab6c-284">Agora que você conseguiu fazer isso, vamos mexer com o servidor:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-284">Now that we’ve accomplished that, let’s play with the server:</span></span>

2. <span data-ttu-id="7ab6c-285">Primeiro, verifique se a instância do MongoDB está em execução:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-285">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

3. <span data-ttu-id="7ab6c-286">Em seguida, vá até o diretório e inicie a ondulação:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-286">Then, change to the directory and start curling:</span></span>

    <span data-ttu-id="7ab6c-287">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="7ab6c-287">`$ cd azuread` `$ node server.js`</span></span>

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

4. <span data-ttu-id="7ab6c-288">Então, podemos adicionar uma tarefa deste modo:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-288">Then, we can add a task this way:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    <span data-ttu-id="7ab6c-289">A resposta deve ser:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-289">The response should be:</span></span>

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
    <span data-ttu-id="7ab6c-290">E podemos pode listar tarefas para Brandon deste modo:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-290">And we can list tasks for Brandon this way:</span></span>

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="7ab6c-291">Se tudo isso funcionar, estamos prontos para adicionar o OAuth ao servidor de API REST.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-291">If all this works, we're ready to add OAuth to the REST API server.</span></span>

<span data-ttu-id="7ab6c-292">Você tem um servidor de API REST com o MongoDB!</span><span class="sxs-lookup"><span data-stu-id="7ab6c-292">You have a REST API server with MongoDB!</span></span>

## <a name="step-18-add-authentication-to-our-rest-api-server"></a><span data-ttu-id="7ab6c-293">Etapa 18: adicionar autenticação ao nosso servidor de API REST</span><span class="sxs-lookup"><span data-stu-id="7ab6c-293">Step 18: Add authentication to our REST API server</span></span>
<span data-ttu-id="7ab6c-294">Agora que temos uma API REST em execução, vamos começar ativando-a com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-294">Now that we have a running REST API, let's start making it useful with Azure AD.</span></span>

<span data-ttu-id="7ab6c-295">Na linha de comando, altere os diretórios para a pasta **azuread**, se você ainda não estiver nela.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-295">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="7ab6c-296">Use o OIDCBearerStrategy que está incluído no passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="7ab6c-296">Use the OIDCBearerStrategy that is included with passport-azure-ad</span></span>
<span data-ttu-id="7ab6c-297">Até agora, criamos um servidor típico TODO do REST sem nenhum tipo de autorização.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-297">So far we have built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="7ab6c-298">Aqui é onde começamos a juntar as peças.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-298">This is where we start putting that together.</span></span>

1. <span data-ttu-id="7ab6c-299">Primeiro, precisamos indicar que queremos usar o Passport.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-299">First, we need to indicate that we want to use Passport.</span></span> <span data-ttu-id="7ab6c-300">Coloque isso logo após a configuração do servidor:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-300">Put this right after your other server configuration:</span></span>

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > <span data-ttu-id="7ab6c-301">Ao escrever APIs, recomendamos que você sempre vincule os dados a algo exclusivo do token que o usuário não possa falsificar.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-301">When you write APIs, we recommend that you always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="7ab6c-302">Quando esse servidor armazena itens TODO, ele faz isso com base na ID de objeto do usuário no token que colocamos no campo "proprietário" (chamado por meio de token.oid).</span><span class="sxs-lookup"><span data-stu-id="7ab6c-302">When this server stores TODO items, it stores them based on the object ID of the user in the token (called through token.oid), which we put in the “owner” field.</span></span> <span data-ttu-id="7ab6c-303">Isso garante que somente o usuário possa acessar seus TODOs.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-303">This ensures that only that user can access their TODOs.</span></span> <span data-ttu-id="7ab6c-304">Não há exposição na API do "proprietário”, portanto, um usuário externo pode solicitar os TODOs de outras pessoas, mesmo que estejam autenticados.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-304">There is no exposure in the API of “owner,” so an external user can request the TODOs of others even if they are authenticated.</span></span>                    

2. <span data-ttu-id="7ab6c-305">Em seguida, vamos usar a estratégia de portador que vem com o `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-305">Next let’s use the bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="7ab6c-306">Por enquanto, apenas olhe o código, e explicaremos o restante daqui a pouco.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-306">Look at the code for now and we'll explain the rest shortly.</span></span> <span data-ttu-id="7ab6c-307">Coloque isto depois do que você colou acima:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-307">Put this after what you pasted above:</span></span>

```Javascript
    /**
    /*
    /* Calling the OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides the need to manage users and info tokens
    /* with a FindorCreate() method that must be provided by the implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want to do something smarter.
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
            log.info('verifying the user');
            log.info(token, 'was the token retreived');
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

<span data-ttu-id="7ab6c-308">O Passport usa um padrão semelhante para todas as estratégias (Twitter, Facebook e assim por diante) que todos os gravadores de estratégia seguem.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-308">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="7ab6c-309">Observando a estratégia, você verá que passamos a ela uma função que tem um token e um done como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-309">Looking at the strategy, you see we pass it a function that has a token and a done as the parameters.</span></span> <span data-ttu-id="7ab6c-310">A estratégia de volta para nós depois faz seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-310">The strategy comes back to us after it does its work.</span></span> <span data-ttu-id="7ab6c-311">Depois disso, armazenamos o usuário e guardamos o token, para que não precisemos pedi-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-311">After it does, we store the user and stash the token so we won’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ab6c-312">O código anterior usa qualquer usuário que tente se autenticar em nosso servidor.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-312">The previous code takes any user that happens to authenticate to our server.</span></span> <span data-ttu-id="7ab6c-313">Isso é conhecido como registro automático.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-313">This is known as auto-registration.</span></span> <span data-ttu-id="7ab6c-314">Em servidores de produção, não convém permitir que qualquer pessoa entre sem primeiro passar por um processo de registro em que você decida.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-314">In production servers, you we recommend that you don't let anyone in without first having them go through a registration process that you decide on.</span></span> <span data-ttu-id="7ab6c-315">Esse geralmente é o padrão que você vê em aplicativos de consumidor que permitem que você se registre com o Facebook, mas depois pedem que preencha informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-315">This is usually the pattern you see in consumer apps, which allow you to register with Facebook but then ask you to fill out additional information.</span></span> <span data-ttu-id="7ab6c-316">Se esse não fosse um programa de linha de comando, poderíamos ter extraído o e-mail do objeto de token que é retornado e pedido que o usuário preenchesse informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-316">If this wasn’t a command-line program, we could have extracted the email from the token object that is returned and then asked the user to fill out additional information.</span></span> <span data-ttu-id="7ab6c-317">Como esse é um servidor de teste, basta adicioná-los ao banco de dados na memória.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-317">Because this is a test server, we simply add them to the in-memory database.</span></span>
>
>

### <a name="protect-some-endpoints"></a><span data-ttu-id="7ab6c-318">Proteger alguns pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="7ab6c-318">Protect some endpoints</span></span>
<span data-ttu-id="7ab6c-319">Proteja os pontos de extremidade ao especificar a chamada `passport.authenticate()` com o protocolo que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-319">You protect endpoints by specifying the `passport.authenticate()` call with the protocol that you want to use.</span></span>

<span data-ttu-id="7ab6c-320">Para que o nosso código de servidor faça algo mais interessante, vamos editar a rota.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-320">To make our server code do something more interesting, let’s edit the route.</span></span>

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

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a><span data-ttu-id="7ab6c-321">Etapa 19: executar o aplicativo de servidor novamente e certificar-se de que rejeitará você</span><span class="sxs-lookup"><span data-stu-id="7ab6c-321">Step 19: Run your server application again and ensure it rejects you</span></span>
<span data-ttu-id="7ab6c-322">Vamos usar `curl` novamente para ver se agora temos proteção OAuth2 para nossos pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-322">Let's use `curl` again to see if we now have OAuth2 protection against our endpoints.</span></span> <span data-ttu-id="7ab6c-323">Fazemos isso antes de executar qualquer um dos nossos SDKs de cliente para esse ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-323">We do this test before running any of our client SDKs against this endpoint.</span></span> <span data-ttu-id="7ab6c-324">Os cabeçalhos retornados devem ser suficientes para nos indicar que estamos no caminho certo.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-324">The headers that are returned should be enough to tell us if we're going down the right path.</span></span>

1. <span data-ttu-id="7ab6c-325">Primeiro, verifique se a instância do MongoDB está em execução:</span><span class="sxs-lookup"><span data-stu-id="7ab6c-325">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

2. <span data-ttu-id="7ab6c-326">Em seguida, vá até o diretório e inicie a ondulação.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-326">Then, change to the directory and start curling.</span></span>

      <span data-ttu-id="7ab6c-327">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="7ab6c-327">`$ cd azuread` `$ node server.js`</span></span>

3. <span data-ttu-id="7ab6c-328">Tente uma POSTAGEM básica.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-328">Try a basic POST.</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="7ab6c-329">Um 401 é a resposta que você está procurando.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-329">A 401 is the response you are looking for here.</span></span> <span data-ttu-id="7ab6c-330">Essa resposta indica que a camada do Passport está tentando redirecionar-se para o ponto de extremidade autorizado, que é exatamente o que você deseja.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-330">This response indicates that the Passport layer is trying to redirect to the authorized endpoint, which is exactly what you want.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ab6c-331">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7ab6c-331">Next steps</span></span>
<span data-ttu-id="7ab6c-332">Você já fez tudo o que podia com esse servidor sem usar um cliente compatível com o OAuth2.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-332">You've gone as far as you can with this server without using an OAuth2 compatible client.</span></span> <span data-ttu-id="7ab6c-333">Você precisará passar por um passo a passo adicional.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-333">You will need to go through an additional walkthrough.</span></span>

<span data-ttu-id="7ab6c-334">Agora, você aprendeu como implementar uma API REST usando o Restify e o OAuth2.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-334">You've now learned how to implement a REST API by using Restify and OAuth2.</span></span> <span data-ttu-id="7ab6c-335">Você também tem código mais do que suficiente para continuar desenvolvendo o seu serviço e aprender como compilar esse exemplo.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-335">You also have more than enough code to keep developing your service and learning how to build on this example.</span></span>

<span data-ttu-id="7ab6c-336">Se você estiver interessado nas próximas etapas de sua jornada ADAL, aqui estão alguns clientes ADAL suportados com os quais recomendamos que você continue trabalhando.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-336">If you are interested in the next steps in your ADAL journey, here are some supported ADAL clients we recommend that you  keep working with.</span></span>

<span data-ttu-id="7ab6c-337">Faça a clonagem para a sua máquina de desenvolvedor e configure conforme indicado no passo a passo.</span><span class="sxs-lookup"><span data-stu-id="7ab6c-337">Clone down to your developer machine and configure as described in the walkthrough.</span></span>

[<span data-ttu-id="7ab6c-338">ADAL para iOS</span><span class="sxs-lookup"><span data-stu-id="7ab6c-338">ADAL for iOS</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[<span data-ttu-id="7ab6c-339">ADAL para Android</span><span class="sxs-lookup"><span data-stu-id="7ab6c-339">ADAL for Android</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
