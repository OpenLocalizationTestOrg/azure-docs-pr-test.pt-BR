---
title: 'Azure AD B2C: proteger uma API Web usando o Node.js | Microsoft Docs'
description: "Como criar uma API Web do Node.js que aceita tokens de um locatário do B2C"
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
ms.openlocfilehash: 6480be75c314ede1b786e959a79c0385dd2edea8
ms.sourcegitcommit: 73f159cdbc122ffe42f3e1f7a3de05f77b6a4725
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="234d4-103">Azure AD B2C: proteger uma API Web usando o Node .js</span><span class="sxs-lookup"><span data-stu-id="234d4-103">Azure AD B2C: Secure a web API by using Node.js</span></span>
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

<span data-ttu-id="234d4-104">Com o Active Directory B2C do Azure (AD do Azure), você pode proteger uma API Web usando tokens de acesso do OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="234d4-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="234d4-105">Esses tokens permitem que os aplicativos cliente que usem o AD B2C do Azure se autentiquem na API.</span><span class="sxs-lookup"><span data-stu-id="234d4-105">These tokens allow your client apps that use Azure AD B2C to authenticate to the API.</span></span> <span data-ttu-id="234d4-106">Este artigo mostra como criar uma API de "lista de tarefas" que permite aos usuários adicionar e listar tarefas.</span><span class="sxs-lookup"><span data-stu-id="234d4-106">This article shows you how to create a "to-do list" API that allows users to add and list tasks.</span></span> <span data-ttu-id="234d4-107">A API Web é protegida usando o Azure AD B2C e permite que apenas usuários autenticados gerenciem sua lista de tarefas pendentes.</span><span class="sxs-lookup"><span data-stu-id="234d4-107">The web API is secured using Azure AD B2C and only allows authenticated users to manage their to-do list.</span></span>

> [!NOTE]
> <span data-ttu-id="234d4-108">Este exemplo foi escrito para que você se conecte a ele usando nosso [aplicativo de exemplo B2C para iOS](active-directory-b2c-devquickstarts-ios.md).</span><span class="sxs-lookup"><span data-stu-id="234d4-108">This sample was written to be connected to by using our [iOS B2C sample application](active-directory-b2c-devquickstarts-ios.md).</span></span> <span data-ttu-id="234d4-109">Primeiramente, explore este passo a passo e, depois, acompanhe usando esse exemplo.</span><span class="sxs-lookup"><span data-stu-id="234d4-109">Do the current walk-through first, and then follow along with that sample.</span></span>
>
>

<span data-ttu-id="234d4-110">**Passport** é middleware de autenticação para o Node.js.</span><span class="sxs-lookup"><span data-stu-id="234d4-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="234d4-111">Flexível e modular, o Passport pode ser instalado sem impedimento em qualquer aplicativo Web baseado em Express ou Restify.</span><span class="sxs-lookup"><span data-stu-id="234d4-111">Flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="234d4-112">Um conjunto abrangente de estratégias que dão suporte à autenticação usando um nome de usuário e uma senha, o Facebook, o Twitter e muito mais.</span><span class="sxs-lookup"><span data-stu-id="234d4-112">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="234d4-113">Desenvolvemos uma estratégia para o Azure AD (Active Directory do Azure).</span><span class="sxs-lookup"><span data-stu-id="234d4-113">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="234d4-114">Você instala esse módulo e, em seguida, adiciona o plug-in `passport-azure-ad` do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="234d4-114">You install this module and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="234d4-115">Para realizar este exemplo, você precisa:</span><span class="sxs-lookup"><span data-stu-id="234d4-115">To do this sample, you need to:</span></span>

1. <span data-ttu-id="234d4-116">Registrar um aplicativo com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="234d4-116">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="234d4-117">Configurar seu aplicativo para usar o plug-in `azure-ad-passport` do Passport.</span><span class="sxs-lookup"><span data-stu-id="234d4-117">Set up your application to use Passport's `azure-ad-passport` plug-in.</span></span>
3. <span data-ttu-id="234d4-118">Configurar um aplicativo cliente para chamar a API Web de "lista de tarefas pendentes".</span><span class="sxs-lookup"><span data-stu-id="234d4-118">Configure a client application to call the "to-do list" web API.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="234d4-119">Obter um diretório AD B2C do Azure</span><span class="sxs-lookup"><span data-stu-id="234d4-119">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="234d4-120">Antes de usar AD B2C do Azure, você deve criar um diretório ou locatário.</span><span class="sxs-lookup"><span data-stu-id="234d4-120">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="234d4-121">Um diretório é um contêiner para todos os usuários, aplicativos, grupos e muito mais.</span><span class="sxs-lookup"><span data-stu-id="234d4-121">A directory is a container for all users, apps, groups, and more.</span></span>  <span data-ttu-id="234d4-122">Se você ainda não tiver um, [crie um diretório B2C](active-directory-b2c-get-started.md) antes de prosseguir.</span><span class="sxs-lookup"><span data-stu-id="234d4-122">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="234d4-123">Criar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="234d4-123">Create an application</span></span>
<span data-ttu-id="234d4-124">Em seguida, você precisa criar um aplicativo no diretório B2C, que dá ao Azure AD algumas informações de que ele precisa para se comunicar de forma segura com o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="234d4-124">Next, you need to create an app in your B2C directory that gives Azure AD some information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="234d4-125">Nesse caso, o aplicativo cliente e a API Web são representados por uma única **ID de aplicativo**, pois eles abrangem um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="234d4-125">In this case, both the client app and web API are represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="234d4-126">Para criar um aplicativo, [siga estas instruções](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="234d4-126">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="234d4-127">É necessário que você:</span><span class="sxs-lookup"><span data-stu-id="234d4-127">Be sure to:</span></span>

* <span data-ttu-id="234d4-128">Incluir um **aplicativo Web/api Web** no aplicativo</span><span class="sxs-lookup"><span data-stu-id="234d4-128">Include a **web app/web api** in the application</span></span>
* <span data-ttu-id="234d4-129">Digite `http://localhost/TodoListService` como uma **URL de Resposta**.</span><span class="sxs-lookup"><span data-stu-id="234d4-129">Enter `http://localhost/TodoListService` as a **Reply URL**.</span></span> <span data-ttu-id="234d4-130">É a URL padrão deste exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="234d4-130">It is the default URL for this code sample.</span></span>
* <span data-ttu-id="234d4-131">Crie um **Segredo de aplicativo** para seu aplicativo e copie-o.</span><span class="sxs-lookup"><span data-stu-id="234d4-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="234d4-132">Você precisa destes dados mais tarde.</span><span class="sxs-lookup"><span data-stu-id="234d4-132">You need this data later.</span></span> <span data-ttu-id="234d4-133">Observe que esse valor precisa ser [seguido por caracteres de escape XML](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) antes de ser usado.</span><span class="sxs-lookup"><span data-stu-id="234d4-133">Note that this value needs to be [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
* <span data-ttu-id="234d4-134">Copie a **ID de aplicativo** atribuída ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="234d4-134">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="234d4-135">Você precisa destes dados mais tarde.</span><span class="sxs-lookup"><span data-stu-id="234d4-135">You need this data later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="234d4-136">Criar suas políticas</span><span class="sxs-lookup"><span data-stu-id="234d4-136">Create your policies</span></span>
<span data-ttu-id="234d4-137">No AD B2C do Azure, cada experiência do usuário é definida por uma [política](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="234d4-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="234d4-138">O aplicativo contém duas experiências de identidade: inscrever-se e entrar.</span><span class="sxs-lookup"><span data-stu-id="234d4-138">This app contains two identity experiences: sign up and sign in.</span></span> <span data-ttu-id="234d4-139">Você precisa criar uma política de cada tipo, conforme descrito no [artigo de referência de política](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="234d4-139">You need to create one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span>  <span data-ttu-id="234d4-140">Ao criar as três políticas, não deixe de:</span><span class="sxs-lookup"><span data-stu-id="234d4-140">When you create your three policies, be sure to:</span></span>

* <span data-ttu-id="234d4-141">Escolher o **Nome de exibição** e outros atributos de inscrição em sua política de inscrição.</span><span class="sxs-lookup"><span data-stu-id="234d4-141">Choose the **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="234d4-142">Escolha as declarações de aplicativo **Nome de exibição** e **ID do Objeto** em todas as políticas.</span><span class="sxs-lookup"><span data-stu-id="234d4-142">Choose the **Display name** and **Object ID** application claims in every policy.</span></span>  <span data-ttu-id="234d4-143">Você pode escolher outras declarações também.</span><span class="sxs-lookup"><span data-stu-id="234d4-143">You can choose other claims as well.</span></span>
* <span data-ttu-id="234d4-144">Copie o **Nome** de cada política após criá-la.</span><span class="sxs-lookup"><span data-stu-id="234d4-144">Copy down the **Name** of each policy after you create it.</span></span> <span data-ttu-id="234d4-145">Ele deve ter o prefixo `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="234d4-145">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="234d4-146">Mais tarde, você precisará desses nomes de política.</span><span class="sxs-lookup"><span data-stu-id="234d4-146">You need those policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="234d4-147">Depois de criar as três políticas, você estará pronto para compilar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="234d4-147">After you have created your three policies, you're ready to build your app.</span></span>

<span data-ttu-id="234d4-148">Para saber mais sobre o funcionamento das políticas no Azure AD B2C, comece com o [tutorial de introdução ao aplicativo Web do .NET](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="234d4-148">To learn about how policies work in Azure AD B2C, start with the [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="download-the-code"></a><span data-ttu-id="234d4-149">Baixar o código</span><span class="sxs-lookup"><span data-stu-id="234d4-149">Download the code</span></span>
<span data-ttu-id="234d4-150">O código para este tutorial é mantido [no GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="234d4-150">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span></span> <span data-ttu-id="234d4-151">Para compilar o exemplo à medida que avançar, [baixe um projeto de esqueleto como um arquivo .zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="234d4-151">To build the sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="234d4-152">Também é possível clonar o esqueleto:</span><span class="sxs-lookup"><span data-stu-id="234d4-152">You can also clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

<span data-ttu-id="234d4-153">O aplicativo completo também está [disponível como um arquivo .zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) ou na ramificação `complete` do mesmo repositório.</span><span class="sxs-lookup"><span data-stu-id="234d4-153">The completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) or on the `complete` branch of the same repository.</span></span>

## <a name="download-nodejs-for-your-platform"></a><span data-ttu-id="234d4-154">Baixar o Node.js para sua plataforma</span><span class="sxs-lookup"><span data-stu-id="234d4-154">Download Node.js for your platform</span></span>
<span data-ttu-id="234d4-155">Para usar este exemplo com êxito, você precisa de uma instalação do Node.js em funcionamento.</span><span class="sxs-lookup"><span data-stu-id="234d4-155">To successfully use this sample, you need a working installation of Node.js.</span></span>

<span data-ttu-id="234d4-156">Instale o Node.js de [nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="234d4-156">Install Node.js from [nodejs.org](http://nodejs.org).</span></span>

## <a name="install-mongodb-for-your-platform"></a><span data-ttu-id="234d4-157">Instalar o MongoDB para sua plataforma</span><span class="sxs-lookup"><span data-stu-id="234d4-157">Install MongoDB for your platform</span></span>
<span data-ttu-id="234d4-158">Para usar este exemplo com êxito, você deve ter uma instalação do MongoDB funcionando corretamente.</span><span class="sxs-lookup"><span data-stu-id="234d4-158">To successfully use this sample, you need a working installation of MongoDB.</span></span> <span data-ttu-id="234d4-159">Usamos o MongoDB para tornar a API REST persistente entre instâncias de servidor.</span><span class="sxs-lookup"><span data-stu-id="234d4-159">We use MongoDB to make your REST API persistent across server instances.</span></span>

<span data-ttu-id="234d4-160">Instale o MongoDB de [mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="234d4-160">Install MongoDB from [mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="234d4-161">Este passo a passo presume que você use os pontos de extremidade de servidor e de instalação padrão para MongoDB, que, no momento da redação deste artigo, são `mongodb://localhost`.</span><span class="sxs-lookup"><span data-stu-id="234d4-161">This walk-through assumes that you use the default installation and server endpoints for MongoDB, which at the time of this writing is `mongodb://localhost`.</span></span>
>
>

## <a name="install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="234d4-162">Instalar os módulos Restify na API Web</span><span class="sxs-lookup"><span data-stu-id="234d4-162">Install the Restify modules in your web API</span></span>
<span data-ttu-id="234d4-163">Usamos o Restify para criar a API REST.</span><span class="sxs-lookup"><span data-stu-id="234d4-163">We use Restify to build your REST API.</span></span> <span data-ttu-id="234d4-164">O Restify é uma estrutura de aplicativo do Node.js mínima e flexível, derivada do Express.</span><span class="sxs-lookup"><span data-stu-id="234d4-164">Restify is a minimal and flexible Node.js application framework derived from Express.</span></span> <span data-ttu-id="234d4-165">Tem um conjunto robusto de recursos para a criação de APIs REST sobre o Connect.</span><span class="sxs-lookup"><span data-stu-id="234d4-165">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="234d4-166">Instalar Restify</span><span class="sxs-lookup"><span data-stu-id="234d4-166">Install Restify</span></span>
<span data-ttu-id="234d4-167">Na linha de comando, altere o diretório para `azuread`.</span><span class="sxs-lookup"><span data-stu-id="234d4-167">From the command line, change your directory to `azuread`.</span></span> <span data-ttu-id="234d4-168">Se o diretório `azuread` não existir, crie-o.</span><span class="sxs-lookup"><span data-stu-id="234d4-168">If the `azuread` directory doesn't exist, create it.</span></span>

<span data-ttu-id="234d4-169">`cd azuread` ou `mkdir azuread;`</span><span class="sxs-lookup"><span data-stu-id="234d4-169">`cd azuread` or `mkdir azuread;`</span></span>

<span data-ttu-id="234d4-170">Digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="234d4-170">Enter the following command:</span></span>

`npm install restify`

<span data-ttu-id="234d4-171">Este comando instala o Restify.</span><span class="sxs-lookup"><span data-stu-id="234d4-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="234d4-172">Você obteve um erro?</span><span class="sxs-lookup"><span data-stu-id="234d4-172">Did you get an error?</span></span>
<span data-ttu-id="234d4-173">Em alguns sistemas operacionais, ao usar `npm`, você pode receber o erro `Error: EPERM, chmod '/usr/local/bin/..'` e uma solicitação para executar a conta como administrador.</span><span class="sxs-lookup"><span data-stu-id="234d4-173">In some operating systems, when you use `npm`, you may receive the error `Error: EPERM, chmod '/usr/local/bin/..'` and a request that you run the account as an administrator.</span></span> <span data-ttu-id="234d4-174">Se o problema ocorrer, use o comando `sudo` para executar `npm` com um nível de privilégio mais elevado.</span><span class="sxs-lookup"><span data-stu-id="234d4-174">If this problem occurs, use the `sudo` command to run `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-a-dtrace-error"></a><span data-ttu-id="234d4-175">Você recebeu um erro DTrace?</span><span class="sxs-lookup"><span data-stu-id="234d4-175">Did you get a DTrace error?</span></span>
<span data-ttu-id="234d4-176">Você pode ver algo como este texto ao instalar o Restify:</span><span class="sxs-lookup"><span data-stu-id="234d4-176">You may see something like this text when you install Restify:</span></span>

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

<span data-ttu-id="234d4-177">O Restify fornece um mecanismo poderoso para rastreamento de chamadas REST usando o DTrace.</span><span class="sxs-lookup"><span data-stu-id="234d4-177">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="234d4-178">No entanto, muitos sistemas operacionais não têm o DTrace disponível.</span><span class="sxs-lookup"><span data-stu-id="234d4-178">However, many operating systems do not have DTrace available.</span></span> <span data-ttu-id="234d4-179">Você pode ignorar com segurança esses erros.</span><span class="sxs-lookup"><span data-stu-id="234d4-179">You can safely ignore these errors.</span></span>

<span data-ttu-id="234d4-180">A saída do comando deve ser semelhante ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="234d4-180">The output of the command should appear similar to this text:</span></span>

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

## <a name="install-passport-in-your-web-api"></a><span data-ttu-id="234d4-181">Instalar o Passport.js na API Web</span><span class="sxs-lookup"><span data-stu-id="234d4-181">Install Passport in your web API</span></span>
<span data-ttu-id="234d4-182">Na linha de comando, altere o diretório para `azuread`, se ainda não estiver lá.</span><span class="sxs-lookup"><span data-stu-id="234d4-182">From the command line, change your directory to `azuread`, if it's not already there.</span></span>

<span data-ttu-id="234d4-183">Instale o Passport usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="234d4-183">Install Passport using the following command:</span></span>

`npm install passport`

<span data-ttu-id="234d4-184">A saída do comando deve ser semelhante ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="234d4-184">The output of the command should be similar to this text:</span></span>

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-to-your-web-api"></a><span data-ttu-id="234d4-185">Adicionar passport azuread à API Web</span><span class="sxs-lookup"><span data-stu-id="234d4-185">Add passport-azuread to your web API</span></span>
<span data-ttu-id="234d4-186">Em seguida, adicione a estratégia OAuth usando `passport-azuread`, um pacote de estratégias que conectam o Azure AD ao Passport.</span><span class="sxs-lookup"><span data-stu-id="234d4-186">Next, add the OAuth strategy by using `passport-azuread`, a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="234d4-187">Use essa estratégia para tokens de portador no exemplo de API REST.</span><span class="sxs-lookup"><span data-stu-id="234d4-187">Use this strategy for bearer tokens in the REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="234d4-188">Embora o OAuth2 forneça uma estrutura na qual qualquer tipo de token conhecido pode ser emitido, somente determinados tipos de token passaram a ser amplamente usados.</span><span class="sxs-lookup"><span data-stu-id="234d4-188">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types have gained widespread use.</span></span> <span data-ttu-id="234d4-189">Os tokens para proteger pontos de extremidade são tokens de portador.</span><span class="sxs-lookup"><span data-stu-id="234d4-189">The tokens for protecting endpoints are bearer tokens.</span></span> <span data-ttu-id="234d4-190">Estes tipos de tokens são mais amplamente emitidos em OAuth2.</span><span class="sxs-lookup"><span data-stu-id="234d4-190">These types of tokens are the most widely issued in OAuth2.</span></span> <span data-ttu-id="234d4-191">Muitas implementações presumem que os tokens de portador sejam o único tipo de token emitido.</span><span class="sxs-lookup"><span data-stu-id="234d4-191">Many implementations assume that bearer tokens are the only type of token issued.</span></span>
>
>

<span data-ttu-id="234d4-192">Na linha de comando, altere o diretório para `azuread`, se ainda não estiver lá.</span><span class="sxs-lookup"><span data-stu-id="234d4-192">From the command line, change your directory to `azuread`, if it's not already there.</span></span>

<span data-ttu-id="234d4-193">Instale o módulo `passport-azure-ad` do Passport usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="234d4-193">Install the Passport `passport-azure-ad` module using the following command:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="234d4-194">A saída do comando deve ser semelhante ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="234d4-194">The output of the command should be similar to this text:</span></span>

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

## <a name="add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="234d4-195">Adicionar os módulos do MongoDB à API Web</span><span class="sxs-lookup"><span data-stu-id="234d4-195">Add MongoDB modules to your web API</span></span>
<span data-ttu-id="234d4-196">Este exemplo usa o MongoDB como repositório de dados.</span><span class="sxs-lookup"><span data-stu-id="234d4-196">This sample uses MongoDB as your data store.</span></span> <span data-ttu-id="234d4-197">Para isso, instale o Mongoose, um plug-in amplamente utilizado para gerenciar modelos e esquemas.</span><span class="sxs-lookup"><span data-stu-id="234d4-197">For that install Mongoose, a widely used plug-in for managing models and schemas.</span></span>

* `npm install mongoose`

## <a name="install-additional-modules"></a><span data-ttu-id="234d4-198">Instalar módulos adicionais</span><span class="sxs-lookup"><span data-stu-id="234d4-198">Install additional modules</span></span>
<span data-ttu-id="234d4-199">Em seguida, instale os módulos necessários restantes.</span><span class="sxs-lookup"><span data-stu-id="234d4-199">Next, install the remaining required modules.</span></span>

<span data-ttu-id="234d4-200">Na linha de comando, altere o diretório para `azuread`, se ainda não estiver lá:</span><span class="sxs-lookup"><span data-stu-id="234d4-200">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="234d4-201">Instale os módulos no diretório `node_modules` :</span><span class="sxs-lookup"><span data-stu-id="234d4-201">Install the modules in your `node_modules` directory:</span></span>

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a><span data-ttu-id="234d4-202">Criar um arquivo server.js com suas dependências</span><span class="sxs-lookup"><span data-stu-id="234d4-202">Create a server.js file with your dependencies</span></span>
<span data-ttu-id="234d4-203">O arquivo `server.js` fornece a maior parte da funcionalidade para o servidor de API Web.</span><span class="sxs-lookup"><span data-stu-id="234d4-203">The `server.js` file provides the majority of the functionality for your Web API server.</span></span>

<span data-ttu-id="234d4-204">Na linha de comando, altere o diretório para `azuread`, se ainda não estiver lá:</span><span class="sxs-lookup"><span data-stu-id="234d4-204">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="234d4-205">Crie um arquivo `server.js` em um editor.</span><span class="sxs-lookup"><span data-stu-id="234d4-205">Create a `server.js` file in an editor.</span></span> <span data-ttu-id="234d4-206">Adicione as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="234d4-206">Add the following information:</span></span>

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

<span data-ttu-id="234d4-207">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="234d4-207">Save the file.</span></span> <span data-ttu-id="234d4-208">Você voltará a ele mais tarde.</span><span class="sxs-lookup"><span data-stu-id="234d4-208">You return to it later.</span></span>

## <a name="create-a-configjs-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="234d4-209">Criar um arquivo config.js para armazenar as configurações do Azure AD</span><span class="sxs-lookup"><span data-stu-id="234d4-209">Create a config.js file to store your Azure AD settings</span></span>
<span data-ttu-id="234d4-210">Esse arquivo de código passa os parâmetros de configuração do Portal do Azure AD para o arquivo `Passport.js` .</span><span class="sxs-lookup"><span data-stu-id="234d4-210">This code file passes the configuration parameters from your Azure AD Portal to the `Passport.js` file.</span></span> <span data-ttu-id="234d4-211">Você criou esses valores de configuração ao adicionar a API Web ao portal na primeira parte do passo a passo.</span><span class="sxs-lookup"><span data-stu-id="234d4-211">You created these configuration values when you added the web API to the portal in the first part of the walk-through.</span></span> <span data-ttu-id="234d4-212">Explicaremos o que deve ser inserido nos valores desses parâmetros depois que você copiar o código.</span><span class="sxs-lookup"><span data-stu-id="234d4-212">We explain what to put in the values of these parameters after you copy the code.</span></span>

<span data-ttu-id="234d4-213">Na linha de comando, altere o diretório para `azuread`, se ainda não estiver lá:</span><span class="sxs-lookup"><span data-stu-id="234d4-213">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="234d4-214">Crie um arquivo `config.js` em um editor.</span><span class="sxs-lookup"><span data-stu-id="234d4-214">Create a `config.js` file in an editor.</span></span> <span data-ttu-id="234d4-215">Adicione as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="234d4-215">Add the following information:</span></span>

```Javascript
// Don't commit this file to your public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in the portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // the Client ID of the application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add the B2C tenant name in the <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is the policy you'll want to validate against in B2C. Usually this is your Sign-in policy (as users sign in to this API)
passReqToCallback: false // This is a node.js construct that lets you pass the req all the way back to any upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a><span data-ttu-id="234d4-216">Valores necessários</span><span class="sxs-lookup"><span data-stu-id="234d4-216">Required values</span></span>
<span data-ttu-id="234d4-217">`clientID`: a ID do cliente do aplicativo de API da Web.</span><span class="sxs-lookup"><span data-stu-id="234d4-217">`clientID`: The client ID of your Web API application.</span></span>

<span data-ttu-id="234d4-218">`IdentityMetadata`: esse é o local onde `passport-azure-ad` procura os dados de configuração para o provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="234d4-218">`IdentityMetadata`: This is where `passport-azure-ad` looks for your configuration data for the identity provider.</span></span> <span data-ttu-id="234d4-219">Ele também procura as chaves para validar os tokens Web JSON.</span><span class="sxs-lookup"><span data-stu-id="234d4-219">It also looks for the keys to validate the JSON web tokens.</span></span>

<span data-ttu-id="234d4-220">`audience`: o URI (uniform resource identifier) do portal que identifica o aplicativo de chamada.</span><span class="sxs-lookup"><span data-stu-id="234d4-220">`audience`: The uniform resource identifier (URI) from the portal that identifies your calling application.</span></span>

<span data-ttu-id="234d4-221">`tenantName`: o nome do locatário (por exemplo, **contoso.onmicrosoft.com**).</span><span class="sxs-lookup"><span data-stu-id="234d4-221">`tenantName`: Your tenant name (for example, **contoso.onmicrosoft.com**).</span></span>

<span data-ttu-id="234d4-222">`policyName`: a política que você deseja que valide os tokens que chegam ao servidor.</span><span class="sxs-lookup"><span data-stu-id="234d4-222">`policyName`: The policy that you want to validate the tokens coming in to your server.</span></span> <span data-ttu-id="234d4-223">Essa política deve ser a mesma política que você usou no aplicativo cliente para entrar.</span><span class="sxs-lookup"><span data-stu-id="234d4-223">This policy should be the same policy that you use on the client application for sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="234d4-224">Por ora, use as mesmas políticas em instalações de cliente e de servidor.</span><span class="sxs-lookup"><span data-stu-id="234d4-224">For now, use the same policies across both client and server setup.</span></span> <span data-ttu-id="234d4-225">Se já tiver concluído um passo a passo e criado essas políticas, você não precisará fazer isso novamente.</span><span class="sxs-lookup"><span data-stu-id="234d4-225">If you have already completed a walk-through and created these policies, you don't need to do so again.</span></span> <span data-ttu-id="234d4-226">Como concluiu o passo a passo, você não deve precisar configurar novas políticas para um passo a passo de cliente no site.</span><span class="sxs-lookup"><span data-stu-id="234d4-226">Because you completed the walk-through, you shouldn't need to set up new policies for client walk-throughs on the site.</span></span>
>
>

## <a name="add-configuration-to-your-serverjs-file"></a><span data-ttu-id="234d4-227">Adicionar configuração ao arquivo server.js</span><span class="sxs-lookup"><span data-stu-id="234d4-227">Add configuration to your server.js file</span></span>
<span data-ttu-id="234d4-228">Para ler os valores do arquivo `config.js` criado, adicione o arquivo `.config` como um recurso necessário em seu aplicativo e, em seguida, defina as variáveis globais como aquelas no documento `config.js`.</span><span class="sxs-lookup"><span data-stu-id="234d4-228">To read the values from the `config.js` file you created, add the `.config` file as a required resource in your application, and then set the global variables to those in the `config.js` document.</span></span>

<span data-ttu-id="234d4-229">Na linha de comando, altere o diretório para `azuread`, se ainda não estiver lá:</span><span class="sxs-lookup"><span data-stu-id="234d4-229">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="234d4-230">Abra o arquivo `server.js` em um editor.</span><span class="sxs-lookup"><span data-stu-id="234d4-230">Open the `server.js` file in an editor.</span></span> <span data-ttu-id="234d4-231">Adicione as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="234d4-231">Add the following information:</span></span>

```Javascript
var config = require('./config');
```
<span data-ttu-id="234d4-232">Adicione uma nova seção a `server.js` que inclua o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="234d4-232">Add a new section to `server.js` that includes the following code:</span></span>

```Javascript
// We pass these options in to the ODICBearerStrategy.

var options = {
    // The URL of the metadata document for your app. We put the keys for token validation from the URL found in the jwks_uri tag of the in the metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

<span data-ttu-id="234d4-233">Em seguida, vamos adicionar alguns espaços reservados para os usuários que recebemos dos aplicativos de chamada.</span><span class="sxs-lookup"><span data-stu-id="234d4-233">Next, let's add some placeholders for the users we receive from our calling applications.</span></span>

```Javascript
// array to hold logged in users and the current logged in user (owner)
var users = [];
var owner = null;
```

<span data-ttu-id="234d4-234">Vamos prosseguir e criar nosso logger também.</span><span class="sxs-lookup"><span data-stu-id="234d4-234">Let's go ahead and create our logger too.</span></span>

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="234d4-235">Adicionar as informações de esquema e modelo do MongoDB usando Mongoose</span><span class="sxs-lookup"><span data-stu-id="234d4-235">Add the MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="234d4-236">A preparação anterior rende frutos quando você reune esses três arquivos em um serviço de API REST.</span><span class="sxs-lookup"><span data-stu-id="234d4-236">The earlier preparation pays off as you bring these three files together in a REST API service.</span></span>

<span data-ttu-id="234d4-237">Para este passo a passo, use o MongoDB para armazenar suas tarefas, como discutido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="234d4-237">For this walk-through, use MongoDB to store your tasks, as discussed earlier.</span></span>

<span data-ttu-id="234d4-238">No arquivo `config.js` , você chamou o banco de dados **tasklist**.</span><span class="sxs-lookup"><span data-stu-id="234d4-238">In the `config.js` file, you called your database **tasklist**.</span></span> <span data-ttu-id="234d4-239">Esse nome também foi o que você colocou no fim da URL de conexão `mongoose_auth_local` .</span><span class="sxs-lookup"><span data-stu-id="234d4-239">That name was also what you put at the end of the `mongoose_auth_local` connection URL.</span></span> <span data-ttu-id="234d4-240">Você não precisa criar esse banco de dados com antecedência no MongoDB.</span><span class="sxs-lookup"><span data-stu-id="234d4-240">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="234d4-241">Ele cria o banco de dados para você na primeira execução do aplicativo de servidor.</span><span class="sxs-lookup"><span data-stu-id="234d4-241">It creates the database for you on the first run of your server application.</span></span>

<span data-ttu-id="234d4-242">Após informar ao servidor qual banco de dados do MongoDB deve ser usado, você precisa escrever código adicional para criar o modelo e o esquema para suas tarefas de servidor.</span><span class="sxs-lookup"><span data-stu-id="234d4-242">After you tell the server which MongoDB database to use, you need to write some additional code to create the model and schema for your server tasks.</span></span>

### <a name="expand-the-model"></a><span data-ttu-id="234d4-243">Expandir o modelo</span><span class="sxs-lookup"><span data-stu-id="234d4-243">Expand the model</span></span>
<span data-ttu-id="234d4-244">Esse modelo de esquema é simples.</span><span class="sxs-lookup"><span data-stu-id="234d4-244">This schema model is simple.</span></span> <span data-ttu-id="234d4-245">Você pode expandi-lo conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="234d4-245">You can expand it as required.</span></span>

<span data-ttu-id="234d4-246">`owner`: quem está atribuído à tarefa.</span><span class="sxs-lookup"><span data-stu-id="234d4-246">`owner`: Who is assigned to the task.</span></span> <span data-ttu-id="234d4-247">Este objeto é uma **cadeia de caracteres**.</span><span class="sxs-lookup"><span data-stu-id="234d4-247">This object is a **string**.</span></span>  

<span data-ttu-id="234d4-248">`Text`: a própria tarefa.</span><span class="sxs-lookup"><span data-stu-id="234d4-248">`Text`: The task itself.</span></span> <span data-ttu-id="234d4-249">Este objeto é uma **cadeia de caracteres**.</span><span class="sxs-lookup"><span data-stu-id="234d4-249">This object is a **string**.</span></span>

<span data-ttu-id="234d4-250">`date`: a data em que a tarefa deverá ser concluída.</span><span class="sxs-lookup"><span data-stu-id="234d4-250">`date`: The date that the task is due.</span></span> <span data-ttu-id="234d4-251">Este objeto é um **datetime**.</span><span class="sxs-lookup"><span data-stu-id="234d4-251">This object is a **datetime**.</span></span>

<span data-ttu-id="234d4-252">`completed`: se a tarefa for concluída.</span><span class="sxs-lookup"><span data-stu-id="234d4-252">`completed`: If the task is complete.</span></span> <span data-ttu-id="234d4-253">Este objeto é um **Booliano**.</span><span class="sxs-lookup"><span data-stu-id="234d4-253">This object is a **Boolean**.</span></span>

### <a name="create-the-schema-in-the-code"></a><span data-ttu-id="234d4-254">Criar o esquema no código</span><span class="sxs-lookup"><span data-stu-id="234d4-254">Create the schema in the code</span></span>
<span data-ttu-id="234d4-255">Na linha de comando, altere o diretório para `azuread`, se ainda não estiver lá:</span><span class="sxs-lookup"><span data-stu-id="234d4-255">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="234d4-256">Abra o arquivo `server.js` em um editor.</span><span class="sxs-lookup"><span data-stu-id="234d4-256">Open the `server.js` file in an editor.</span></span> <span data-ttu-id="234d4-257">Adicione as seguintes informações abaixo da entrada de configuração:</span><span class="sxs-lookup"><span data-stu-id="234d4-257">Add the following information below the configuration entry:</span></span>

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect to MongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema to store our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use the schema to register a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
<span data-ttu-id="234d4-258">Primeiro você cria o esquema e, em seguida, cria um objeto de modelo que usa para armazenar os dados em todo o código ao definir suas **rotas**.</span><span class="sxs-lookup"><span data-stu-id="234d4-258">You first create the schema, and then you create a model object that you use to store your data throughout the code when you define your **routes**.</span></span>

## <a name="add-routes-for-your-rest-api-task-server"></a><span data-ttu-id="234d4-259">Adicionar rotas para o servidor de tarefa da API REST</span><span class="sxs-lookup"><span data-stu-id="234d4-259">Add routes for your REST API task server</span></span>
<span data-ttu-id="234d4-260">Agora que você tem um modelo de banco de dados com o qual trabalhar, adicione as rotas que usa para o servidor de API REST.</span><span class="sxs-lookup"><span data-stu-id="234d4-260">Now that you have a database model to work with, add the routes you use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="234d4-261">Sobre rotas no Restify</span><span class="sxs-lookup"><span data-stu-id="234d4-261">About routes in Restify</span></span>
<span data-ttu-id="234d4-262">As rotas funcionam no Restify da mesma forma como funcionam ao usar a pilha Express.</span><span class="sxs-lookup"><span data-stu-id="234d4-262">Routes work in Restify in the same way that they work when they use the Express stack.</span></span> <span data-ttu-id="234d4-263">Você define rotas usando o URI que espera que os aplicativos de cliente chamem.</span><span class="sxs-lookup"><span data-stu-id="234d4-263">You define routes by using the URI that you expect the client applications to call.</span></span>

<span data-ttu-id="234d4-264">Um padrão típico para uma rota do Restify é:</span><span class="sxs-lookup"><span data-stu-id="234d4-264">A typical pattern for a Restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep the server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

<span data-ttu-id="234d4-265">O Restify e o Express fornecem funcionalidade muito mais aprofundada, como a definição de tipos de aplicativos e o roteamento complexo entre diferentes pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="234d4-265">Restify and Express can provide much deeper functionality, such as defining application types and doing complex routing across different endpoints.</span></span> <span data-ttu-id="234d4-266">Para este tutorial, mantemos essas rotas simples.</span><span class="sxs-lookup"><span data-stu-id="234d4-266">For the purposes of this tutorial, we keep these routes simple.</span></span>

#### <a name="add-default-routes-to-your-server"></a><span data-ttu-id="234d4-267">Adicionar rotas padrão a seu servidor</span><span class="sxs-lookup"><span data-stu-id="234d4-267">Add default routes to your server</span></span>
<span data-ttu-id="234d4-268">Agora você adiciona rotas CRUD básicas de **create** e **list** para a API REST.</span><span class="sxs-lookup"><span data-stu-id="234d4-268">You now add the basic CRUD routes of **create** and **list** for our REST API.</span></span> <span data-ttu-id="234d4-269">Outras rotas podem ser encontradas na ramificação `complete` do exemplo.</span><span class="sxs-lookup"><span data-stu-id="234d4-269">Other routes can be found in the `complete` branch of the sample.</span></span>

<span data-ttu-id="234d4-270">Na linha de comando, altere o diretório para `azuread`, se ainda não estiver lá:</span><span class="sxs-lookup"><span data-stu-id="234d4-270">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="234d4-271">Abra o arquivo `server.js` em um editor.</span><span class="sxs-lookup"><span data-stu-id="234d4-271">Open the `server.js` file in an editor.</span></span> <span data-ttu-id="234d4-272">Abaixo das entradas de banco de dados que você criou acima, adicione as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="234d4-272">Below the database entries you made above add the following information:</span></span>

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you to set default headers
    // This headers comply with CORS and allow us to mongodbServer our response to any origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it to Mongodb
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
            req.log.warn(err, 'createTask: unable to save');
            next(err);
        } else {
            res.send(201, _task);

        }
    });

    return next();

}
```

```Javascript
/// Simple returns the list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you to set default headers
    // This headers comply with CORS and allow us to mongodbServer our response to any origin

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
            log.warn(err, "There is no tasks in the database. Add one!");
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


#### <a name="add-error-handling-for-the-routes"></a><span data-ttu-id="234d4-273">Adicionar tratamento de erro para as rotas</span><span class="sxs-lookup"><span data-stu-id="234d4-273">Add error handling for the routes</span></span>
<span data-ttu-id="234d4-274">Adicione tratamento de erros, para que possa comunicar os problemas encontrados ao cliente de forma que ele possa entender.</span><span class="sxs-lookup"><span data-stu-id="234d4-274">Add some error handling so that you can communicate any problems you encounter back to the client in a way that it can understand.</span></span>

<span data-ttu-id="234d4-275">Adicione os códigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="234d4-275">Add the following code:</span></span>

```Javascript
///--- Errors for communicating something interesting back to the client
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


## <a name="create-your-server"></a><span data-ttu-id="234d4-276">Criar seu servidor</span><span class="sxs-lookup"><span data-stu-id="234d4-276">Create your server</span></span>
<span data-ttu-id="234d4-277">Agora você definiu o banco de dados e incluiu as rotas.</span><span class="sxs-lookup"><span data-stu-id="234d4-277">You have now defined your database and put your routes in place.</span></span> <span data-ttu-id="234d4-278">A última coisa a fazer é adicionar a instância do servidor que gerencia suas chamadas.</span><span class="sxs-lookup"><span data-stu-id="234d4-278">The last thing for you to do is to add the server instance that manages your calls.</span></span>

<span data-ttu-id="234d4-279">O Restify e Express fornecem personalização aprofundada para um servidor de API REST, mas usamos a configuração mais básica aqui.</span><span class="sxs-lookup"><span data-stu-id="234d4-279">Restify and Express provide deep customization for a REST API server, but we use the most basic setup here.</span></span>

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

// Allow 5 requests/second by IP, and burst to 10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use the common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping to REST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-the-routes-to-the-server-without-authentication"></a><span data-ttu-id="234d4-280">Adicionar as rotas ao servidor (sem autenticação)</span><span class="sxs-lookup"><span data-stu-id="234d4-280">Add the routes to the server (without authentication)</span></span>
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
    consoleMessage += '\n Open your browser to %s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-to-your-rest-api-server"></a><span data-ttu-id="234d4-281">Adicionar autenticação a seu servidor de API REST</span><span class="sxs-lookup"><span data-stu-id="234d4-281">Add authentication to your REST API server</span></span>
<span data-ttu-id="234d4-282">Agora que tem um servidor de API REST em execução, você pode torná-lo útil no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="234d4-282">Now that you have a running REST API server, you can make it useful against Azure AD.</span></span>

<span data-ttu-id="234d4-283">Na linha de comando, altere o diretório para `azuread`, se ainda não estiver lá:</span><span class="sxs-lookup"><span data-stu-id="234d4-283">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="234d4-284">Use o OIDCBearerStrategy que está incluído no passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="234d4-284">Use the OIDCBearerStrategy that is included with passport-azure-ad</span></span>
> [!TIP]
> <span data-ttu-id="234d4-285">Ao escrever APIs, você deve sempre vincular os dados a algo exclusivo do token que o usuário não possa falsificar.</span><span class="sxs-lookup"><span data-stu-id="234d4-285">When you write APIs, you should always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="234d4-286">Quando o servidor armazena itens de ToDo, ele faz isso com base na **oid** do usuário no token (chamado por meio de token.oid) que é incluído no campo "proprietário".</span><span class="sxs-lookup"><span data-stu-id="234d4-286">When the server stores ToDo items, it does so based on the **oid** of the user in the token (called through token.oid), which goes in the “owner” field.</span></span> <span data-ttu-id="234d4-287">Esse valor garante que somente o usuário possa acessar seus próprios itens de Tarefas Pendentes.</span><span class="sxs-lookup"><span data-stu-id="234d4-287">This value ensures that only that user can access their own ToDo items.</span></span> <span data-ttu-id="234d4-288">Não há exposição na API do "proprietário". Portanto, um usuário externo pode solicitar os itens ToDo de outras pessoas, mesmo que estejam autenticados.</span><span class="sxs-lookup"><span data-stu-id="234d4-288">There is no exposure in the API of “owner,” so an external user can request others’ ToDo items even if they are authenticated.</span></span>
>
>

<span data-ttu-id="234d4-289">Em seguida, use a estratégia de portador que vem com o `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="234d4-289">Next, use the bearer strategy that comes with `passport-azure-ad`.</span></span>

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
        log.info('verifying the user');
        log.info(token, 'was the token retreived');
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

<span data-ttu-id="234d4-290">O Passport usa o mesmo padrão para todas as suas estratégias.</span><span class="sxs-lookup"><span data-stu-id="234d4-290">Passport uses the same pattern for all its strategies.</span></span> <span data-ttu-id="234d4-291">Você o passa como um `function()` que tem `token` e `done` como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="234d4-291">You pass it a `function()` that has `token` and `done` as parameters.</span></span> <span data-ttu-id="234d4-292">A estratégia volta para você após fazer seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="234d4-292">The strategy comes back to you after it has done all of its work.</span></span> <span data-ttu-id="234d4-293">Em seguida, você deve armazenar o usuário e salvar o token para que não precise pedi-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="234d4-293">You should then store the user and save the token so that you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="234d4-294">O código acima usa qualquer usuário que se autentique em seu servidor.</span><span class="sxs-lookup"><span data-stu-id="234d4-294">The code above takes any user who happens to authenticate to your server.</span></span> <span data-ttu-id="234d4-295">Este processo é conhecido como registro automático.</span><span class="sxs-lookup"><span data-stu-id="234d4-295">This process is known as autoregistration.</span></span> <span data-ttu-id="234d4-296">Em servidores de produção, não permitem que qualquer usuário acesse a API sem primeiro passar por um processo de registro.</span><span class="sxs-lookup"><span data-stu-id="234d4-296">In production servers, don't let in any users access the API without first having them go through a registration process.</span></span> <span data-ttu-id="234d4-297">Esse processo geralmente é o padrão em aplicativos de consumidor que lhe permitem registrar-se usando o Facebook, mas depois pedem que você preencha informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="234d4-297">This process is usually the pattern you see in consumer apps that allow you to register by using Facebook but then ask you to fill out additional information.</span></span> <span data-ttu-id="234d4-298">Se esse programa não fosse um programa de linha de comando, poderíamos ter extraído o email do objeto de token que é retornado e pedido que os usuários preenchessem informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="234d4-298">If this program wasn’t a command-line program, we could have extracted the email from the token object that is returned and then asked users to fill out additional information.</span></span> <span data-ttu-id="234d4-299">Como este é um exemplo, eles são adicionados a um banco de dados na memória.</span><span class="sxs-lookup"><span data-stu-id="234d4-299">Because this is a sample, we add them to an in-memory database.</span></span>
>
>

## <a name="run-your-server-application-to-verify-that-it-rejects-you"></a><span data-ttu-id="234d4-300">Executar o aplicativo de servidor e verificar se ele o rejeita</span><span class="sxs-lookup"><span data-stu-id="234d4-300">Run your server application to verify that it rejects you</span></span>
<span data-ttu-id="234d4-301">Você pode usar `curl` para ver se agora tem a proteção de OAuth2 para os pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="234d4-301">You can use `curl` to see if you now have OAuth2 protection against your endpoints.</span></span> <span data-ttu-id="234d4-302">Os cabeçalhos retornados devem ser suficientes para indicar que você está no caminho certo.</span><span class="sxs-lookup"><span data-stu-id="234d4-302">The headers returned should be enough to tell you that you are on the right path.</span></span>

<span data-ttu-id="234d4-303">Verifique se a instância do MongoDB está em execução.</span><span class="sxs-lookup"><span data-stu-id="234d4-303">Make sure that your MongoDB instance is running:</span></span>

    $sudo mongodb

<span data-ttu-id="234d4-304">Altere para o diretório e execute o servidor:</span><span class="sxs-lookup"><span data-stu-id="234d4-304">Change to the directory and run the server:</span></span>

    $ cd azuread
    $ node server.js

<span data-ttu-id="234d4-305">Em uma nova janela de terminal, execute `curl`</span><span class="sxs-lookup"><span data-stu-id="234d4-305">In a new terminal window, run `curl`</span></span>

<span data-ttu-id="234d4-306">Tente uma POSTAGEM básica:</span><span class="sxs-lookup"><span data-stu-id="234d4-306">Try a basic POST:</span></span>

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

<span data-ttu-id="234d4-307">Um erro 401 é a resposta desejada.</span><span class="sxs-lookup"><span data-stu-id="234d4-307">A 401 error is the response you want.</span></span> <span data-ttu-id="234d4-308">Isso indica que a camada do Passport está tentando se redirecionar para o ponto de extremidade de autorização.</span><span class="sxs-lookup"><span data-stu-id="234d4-308">It indicates that the Passport layer is trying to redirect to the authorize endpoint.</span></span>

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a><span data-ttu-id="234d4-309">Agora você tem um serviço de API REST que usa OAuth2</span><span class="sxs-lookup"><span data-stu-id="234d4-309">You now have a REST API service that uses OAuth2</span></span>
<span data-ttu-id="234d4-310">Você implementou uma API REST usando Restify e OAuth!</span><span class="sxs-lookup"><span data-stu-id="234d4-310">You have implemented a REST API by using Restify and OAuth!</span></span> <span data-ttu-id="234d4-311">Agora você tem código suficiente para continuar a desenvolver o serviço e ampliar este exemplo.</span><span class="sxs-lookup"><span data-stu-id="234d4-311">You now have sufficient code so that you can continue to develop your service and build on this example.</span></span> <span data-ttu-id="234d4-312">Você  fez tudo o que podia com esse servidor sem usar um cliente compatível com OAuth2.</span><span class="sxs-lookup"><span data-stu-id="234d4-312">You have gone as far as you can with this server without using an OAuth2-compatible client.</span></span> <span data-ttu-id="234d4-313">Para a próxima etapa, use um passo a passo adicional, como [Conectar-se a uma API da Web por meio do iOS com B2C](active-directory-b2c-devquickstarts-ios.md) .</span><span class="sxs-lookup"><span data-stu-id="234d4-313">For that next step use an additional walk-through like our [Connect to a web API by using iOS with B2C](active-directory-b2c-devquickstarts-ios.md) walkthrough.</span></span>

## <a name="next-steps"></a><span data-ttu-id="234d4-314">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="234d4-314">Next steps</span></span>
<span data-ttu-id="234d4-315">Agora você pode ir para tópicos mais avançados, como:</span><span class="sxs-lookup"><span data-stu-id="234d4-315">You can now move to more advanced topics, such as:</span></span>

[<span data-ttu-id="234d4-316">Conectar-se a uma API Web usando o iOS com o B2C</span><span class="sxs-lookup"><span data-stu-id="234d4-316">Connect to a web API by using iOS with B2C</span></span>](active-directory-b2c-devquickstarts-ios.md)
