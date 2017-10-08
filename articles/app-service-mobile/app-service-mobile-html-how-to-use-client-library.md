---
title: "aaaHow tooUse Olá SDK de JavaScript para aplicativos móveis do Azure"
description: "Como v tooUse para aplicativos móveis do Azure"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 53b78965-caa3-4b22-bb67-5bd5c19d03c4
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 3fcbb0c5bd6918a285bdafa1946ba0bd47bb21b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-javascript-client-library-for-azure-mobile-apps"></a><span data-ttu-id="bbca6-103">Como o tooUse hello biblioteca de cliente JavaScript para aplicativos móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="bbca6-103">How tooUse hello JavaScript client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="bbca6-104">Este guia ensina usando hello mais recente de cenários comuns de tooperform [SDK de JavaScript para aplicativos móveis do Azure].</span><span class="sxs-lookup"><span data-stu-id="bbca6-104">This guide teaches you tooperform common scenarios using hello latest [JavaScript SDK for Azure Mobile Apps].</span></span> <span data-ttu-id="bbca6-105">Se você for novo tooAzure os aplicativos móveis, primeiro conclua [início rápido do Azure Mobile aplicativos] toocreate um back-end e criar uma tabela.</span><span class="sxs-lookup"><span data-stu-id="bbca6-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend and create a table.</span></span> <span data-ttu-id="bbca6-106">Este guia, vamos nos concentrar em usar o back-end de saudação móvel em aplicativos Web HTML/JavaScript.</span><span class="sxs-lookup"><span data-stu-id="bbca6-106">In this guide, we focus on using hello mobile backend in HTML/JavaScript Web applications.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="bbca6-107">Plataformas com suporte</span><span class="sxs-lookup"><span data-stu-id="bbca6-107">Supported platforms</span></span>
<span data-ttu-id="bbca6-108">Podemos limite atual de toohello de suporte do navegador e versões de saudação da última principais navegadores: Microsoft Edge, Google Chrome, o Microsoft Internet Explorer e Mozilla Firefox.</span><span class="sxs-lookup"><span data-stu-id="bbca6-108">We limit browser support toohello current and last versions of hello major browsers:  Google Chrome, Microsoft Edge, Microsoft Internet Explorer, and Mozilla Firefox.</span></span>  <span data-ttu-id="bbca6-109">Esperamos Olá SDK toofunction com qualquer navegador moderno relativamente.</span><span class="sxs-lookup"><span data-stu-id="bbca6-109">We expect hello SDK toofunction with any relatively modern browser.</span></span>

<span data-ttu-id="bbca6-110">pacote de saudação é distribuído como um módulo de JavaScript Universal, para que ele suporta globais, AMD, e formatos de CommonJS.</span><span class="sxs-lookup"><span data-stu-id="bbca6-110">hello package is distributed as a Universal JavaScript Module, so it supports globals, AMD, and CommonJS formats.</span></span>

## <span data-ttu-id="bbca6-111"><a name="Setup"></a>Configuração e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bbca6-111"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="bbca6-112">Este guia pressupõe que você tenha criado um back-end com uma tabela.</span><span class="sxs-lookup"><span data-stu-id="bbca6-112">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="bbca6-113">Este guia presume que tabela Olá tenha Olá mesmo esquema de tabelas Olá esses tutoriais.</span><span class="sxs-lookup"><span data-stu-id="bbca6-113">This guide assumes that hello table has hello same schema as hello tables in those tutorials.</span></span>

<span data-ttu-id="bbca6-114">Instalar Olá SDK de JavaScript de aplicativos móveis do Azure pode ser feito por meio de saudação `npm` comando:</span><span class="sxs-lookup"><span data-stu-id="bbca6-114">Installing hello Azure Mobile Apps JavaScript SDK can be done via hello `npm` command:</span></span>

```
npm install azure-mobile-apps-client --save
```

<span data-ttu-id="bbca6-115">biblioteca de saudação também pode ser usada como um módulo ES2015, em ambientes de CommonJS como Browserify e Webpack e como uma biblioteca AMD.</span><span class="sxs-lookup"><span data-stu-id="bbca6-115">hello library can also be used as an ES2015 module, within CommonJS environments such as Browserify and Webpack and as an AMD library.</span></span>  <span data-ttu-id="bbca6-116">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="bbca6-116">For example:</span></span>

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

<span data-ttu-id="bbca6-117">Você também pode usar uma versão pré-criado do hello SDK baixando diretamente do nosso CDN:</span><span class="sxs-lookup"><span data-stu-id="bbca6-117">You can also use a pre-built version of hello SDK by downloading directly from our CDN:</span></span>

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="bbca6-118"><a name="auth"></a>Como autenticar usuários</span><span class="sxs-lookup"><span data-stu-id="bbca6-118"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="bbca6-119">O Serviço de Aplicativo do Azure oferece suporte à autenticação e autorização de usuários de aplicativos usando vários provedores de identidade externos: Facebook, Google, Conta da Microsoft e Twitter.</span><span class="sxs-lookup"><span data-stu-id="bbca6-119">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="bbca6-120">Você pode definir permissões de acesso a tabelas toorestrict para operações específicas de tooonly autenticado usuários.</span><span class="sxs-lookup"><span data-stu-id="bbca6-120">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="bbca6-121">Você também pode usar a identidade Olá usuários autenticados tooimplement de regras de autorização nos scripts de servidor.</span><span class="sxs-lookup"><span data-stu-id="bbca6-121">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="bbca6-122">Para obter mais informações, consulte Olá [Introdução à autenticação] tutorial.</span><span class="sxs-lookup"><span data-stu-id="bbca6-122">For more information, see hello [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="bbca6-123">Dois fluxos de autenticação são suportados: um server flow e um client flow.</span><span class="sxs-lookup"><span data-stu-id="bbca6-123">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="bbca6-124">fluxo do servidor de saudação fornece experiência de autenticação mais simples de Olá, como ele se baseia na interface de autenticação do provedor de saudação da web.</span><span class="sxs-lookup"><span data-stu-id="bbca6-124">hello server flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="bbca6-125">Olá fluxo cliente permite integração mais profunda com recursos específicos do dispositivo, como single-sign-on como ele se baseia em SDKs específicos de provedor.</span><span class="sxs-lookup"><span data-stu-id="bbca6-125">hello client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="bbca6-126"><a name="configure-external-redirect-urls"></a>Como configurar o Serviço de Aplicativo Móvel para URLs de redirecionamento externo.</span><span class="sxs-lookup"><span data-stu-id="bbca6-126"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="bbca6-127">Vários tipos de aplicativos JavaScript usam um toohandle de capacidade de loopback que OAuth UI flui.</span><span class="sxs-lookup"><span data-stu-id="bbca6-127">Several types of JavaScript applications use a loopback capability toohandle OAuth UI flows.</span></span>  <span data-ttu-id="bbca6-128">Esses recursos incluem:</span><span class="sxs-lookup"><span data-stu-id="bbca6-128">These capabilities include:</span></span>

* <span data-ttu-id="bbca6-129">Executar o serviço localmente</span><span class="sxs-lookup"><span data-stu-id="bbca6-129">Running your service locally</span></span>
* <span data-ttu-id="bbca6-130">Usando o Live recarregar com hello Framework Ionic</span><span class="sxs-lookup"><span data-stu-id="bbca6-130">Using Live Reload with hello Ionic Framework</span></span>
* <span data-ttu-id="bbca6-131">Redirecionando tooApp serviço para autenticação.</span><span class="sxs-lookup"><span data-stu-id="bbca6-131">Redirecting tooApp Service for authentication.</span></span>

<span data-ttu-id="bbca6-132">Em execução localmente pode causar problemas porque, por padrão, a autenticação é apenas do serviço de aplicativo configurado o acesso de tooallow do seu back-end do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="bbca6-132">Running locally can cause problems because, by default, App Service authentication is only configured tooallow access from your Mobile App backend.</span></span> <span data-ttu-id="bbca6-133">Use Olá seguindo as etapas toochange Olá autenticação de tooenable de configurações do serviço de aplicativo ao executar o servidor de saudação localmente:</span><span class="sxs-lookup"><span data-stu-id="bbca6-133">Use hello following steps toochange hello App Service settings tooenable authentication when running hello server locally:</span></span>

1. <span data-ttu-id="bbca6-134">Faça logon no toohello [portal do Azure]</span><span class="sxs-lookup"><span data-stu-id="bbca6-134">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="bbca6-135">Navegue back-end de aplicativo móvel tooyour.</span><span class="sxs-lookup"><span data-stu-id="bbca6-135">Navigate tooyour Mobile App backend.</span></span>
3. <span data-ttu-id="bbca6-136">Selecione **Gerenciador de recursos** em Olá **ferramentas de desenvolvimento** menu.</span><span class="sxs-lookup"><span data-stu-id="bbca6-136">Select **Resource explorer** in hello **DEVELOPMENT TOOLS** menu.</span></span>
4. <span data-ttu-id="bbca6-137">Clique em **vá** Gerenciador de recursos de saudação tooopen do seu back-end do aplicativo móvel em uma nova guia ou janela.</span><span class="sxs-lookup"><span data-stu-id="bbca6-137">Click **Go** tooopen hello resource explorer for your Mobile App backend in a new tab or window.</span></span>
5. <span data-ttu-id="bbca6-138">Expanda Olá **config** > **authsettings** nó para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bbca6-138">Expand hello **config** > **authsettings** node for your app.</span></span>
6. <span data-ttu-id="bbca6-139">Clique em Olá **editar** botão tooenable edição do recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="bbca6-139">Click hello **Edit** button tooenable editing of hello resource.</span></span>
7. <span data-ttu-id="bbca6-140">Localize Olá **allowedExternalRedirectUrls** elemento, que deve ser nulo.</span><span class="sxs-lookup"><span data-stu-id="bbca6-140">Find hello **allowedExternalRedirectUrls** element, which should be null.</span></span> <span data-ttu-id="bbca6-141">Adicione as URLs em uma matriz:</span><span class="sxs-lookup"><span data-stu-id="bbca6-141">Add your URLs in an array:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="bbca6-142">Substitua Olá URLs na matriz Olá Olá URLs do serviço, que neste exemplo é `http://localhost:3000` para o serviço de exemplo hello local Node. js.</span><span class="sxs-lookup"><span data-stu-id="bbca6-142">Replace hello URLs in hello array with hello URLs of your service, which in this example is `http://localhost:3000` for hello local Node.js sample service.</span></span> <span data-ttu-id="bbca6-143">Você também pode usar `http://localhost:4400` para serviço de ondulação hello ou outra URL, dependendo de como seu aplicativo está configurado.</span><span class="sxs-lookup"><span data-stu-id="bbca6-143">You could also use `http://localhost:4400` for hello Ripple service or some other URL, depending on how your app is configured.</span></span>
8. <span data-ttu-id="bbca6-144">Na parte superior de saudação da página de saudação, clique em **leitura/gravação**, em seguida, clique em **colocar** toosave suas atualizações.</span><span class="sxs-lookup"><span data-stu-id="bbca6-144">At hello top of hello page, click **Read/Write**, then click **PUT** toosave your updates.</span></span>

<span data-ttu-id="bbca6-145">Você também precisa tooadd Olá configurações de lista branca do mesmo loopback URLs toohello CORS:</span><span class="sxs-lookup"><span data-stu-id="bbca6-145">You also need tooadd hello same loopback URLs toohello CORS whitelist settings:</span></span>

1. <span data-ttu-id="bbca6-146">Navegue back toohello [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="bbca6-146">Navigate back toohello [Azure portal].</span></span>
2. <span data-ttu-id="bbca6-147">Navegue back-end de aplicativo móvel tooyour.</span><span class="sxs-lookup"><span data-stu-id="bbca6-147">Navigate tooyour Mobile App backend.</span></span>
3. <span data-ttu-id="bbca6-148">Clique em **CORS** em Olá **API** menu.</span><span class="sxs-lookup"><span data-stu-id="bbca6-148">Click **CORS** in hello **API** menu.</span></span>
4. <span data-ttu-id="bbca6-149">Insira cada URL no hello vazio **origens permitidas** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="bbca6-149">Enter each URL in hello empty **Allowed Origins** text box.</span></span>  <span data-ttu-id="bbca6-150">Uma nova caixa de texto é criada.</span><span class="sxs-lookup"><span data-stu-id="bbca6-150">A new text box is created.</span></span>
5. <span data-ttu-id="bbca6-151">Clique em **SALVAR**</span><span class="sxs-lookup"><span data-stu-id="bbca6-151">Click **SAVE**</span></span>

<span data-ttu-id="bbca6-152">Depois Olá back-end de atualizações, você será capaz de toouse Olá novas URLs de loopback em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bbca6-152">After hello backend updates, you will be able toouse hello new loopback URLs in your app.</span></span>

<!-- URLs. -->
[início rápido do Azure Mobile aplicativos]: app-service-mobile-cordova-get-started.md
[Introdução à autenticação]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[portal do Azure]: https://portal.azure.com/
[SDK de JavaScript para aplicativos móveis do Azure]: https://www.npmjs.com/package/azure-mobile-apps-client
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
